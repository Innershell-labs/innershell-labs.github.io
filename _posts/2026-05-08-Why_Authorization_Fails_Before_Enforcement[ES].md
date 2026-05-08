---
layout: default
title: "Por qué la autorización falla antes de la aplicación del control de acceso"
---

# Por qué la autorización falla antes de la aplicación del control de acceso

## Introducción

Durante los últimos años, y especialmente a través del trabajo práctico y de riesgos en seguridad ofensiva, me he encontrado dedicando menos tiempo a buscar vulnerabilidades técnicas aisladas, y más tiempo intentando entender cómo están realmente diseñados los sistemas y cómo esas decisiones de diseño pueden ser utilizadas en su contra.

Ha existido un cambio claro de madurez.

Los enfoques tradicionales de red team suelen centrarse en identificar debilidades específicas: una mala configuración, un punto de inyección, un servicio expuesto. Todo eso sigue siendo importante. Pero en los sistemas modernos, las fallas de seguridad de mayor impacto rara vez provienen de un único bug.

Provienen de cómo se comporta el sistema como un todo, no de bugs aislados.

Más específicamente, emergen de cómo se modela la identidad, cómo se toman las decisiones de autorización y cómo se distribuye la confianza entre componentes.

Entender estos aspectos se ha vuelto mucho más valioso que simplemente encontrar problemas técnicos de forma aislada, por eso es que ya por más de 5 años el Broken Access Control sigue siendo el grupo de vulns mas comunes y con impacto hasta hoy.

Porque una vez que entiendes el sistema, ya no estás solamente buscando vulnerabilidades.

Estás buscando formas de romper las suposiciones sobre las que fue construido, y aquí es donde se separan los ethical hackers/pentesters obsoletos de los modernos y efectivos.


La mayoría de las discusiones sobre fallas de autorización tienden a enfocarse en controles ausentes, endpoints expuestos o recursos protegidos incorrectamente.

Aunque esos problemas sí existen, rara vez son la causa raíz.

En los sistemas modernos, la autorización no falla en el enforcement.

Falla mucho antes: a nivel de diseño.

## Autenticación vs Autorización: Un contexto rápido

Antes de profundizar, es importante aclarar la diferencia:

- **Autenticación (AuthN)** responde: *¿quién eres?*  
- **Autorización (AuthZ)** responde: *¿qué tienes permitido hacer?*

Los sistemas modernos se apoyan en distintos enfoques para implementar estos conceptos:

### Modelos de autenticación

- **Autenticación basada en sesiones**  
  - Ventajas: fuerte control del lado del servidor, revocación sencilla  
  - Desventajas: requiere estado centralizado, más difícil de escalar y dependencia de un solo punto 
  
- **Autenticación basada en tokens, por ejemplo JWT**  
  - Ventajas: escalable, portable entre servicios  
  - Desventajas: introduce identidad obsoleta, revocación difícil, estado oculto  
  
- **Enfoques stateful vs stateless**  
  - Los sistemas stateless buscan eliminar el estado del lado del servidor  
  - En la práctica, lo reintroducen mediante:
    - tiempos de vida de los tokens  
    - flujos de refresh  
    - mecanismos de revocación  
    - cachés distribuidos  

### Modelos de autorización

- **RBAC (Role-Based accesos Control)**  
  - Ventajas: simple, ampliamente adoptado  
  - Desventajas: explosión de roles, falta de contexto, dificil de escalar  
  
- **ABAC (Attribute-Based accesos Control)**  
  - Ventajas: flexible, consciente del contexto  
  - Desventajas: evaluación compleja, difícil de razonar y auditar  
  
- **ReBAC (Relationship-Based accesos Control)**  
  - Ventajas: modela relaciones del mundo real, por ejemplo Google Zanzibar  
  - Desventajas: complejidad del grafo, desafíos de rendimiento y consistencia  
  
- **Sistemas basados en políticas**  
  - Ventajas: lógica centralizada, reglas expresivas  
  - Desventajas: requiere disciplina estricta y consistencia entre servicios  

Cada uno de estos modelos resuelve parte del problema.

Ninguno de ellos, por sí solo, garantiza una autorización segura.

## Dónde realmente se rompe la autorización

Las fallas de autorización suelen emerger desde suposiciones incorrectas sobre identidad, estado y confianza.

### Se asume que la identidad es correcta

Los sistemas suelen asumir que la identidad sigue siendo válida entre solicitudes:

- tokens que contienen claims desactualizados  
- sesiones que ya no reflejan los permisos actuales  
- roles embebidos sin revalidación  

#### Ejemplo: identidad obsoleta en autenticación basada en tokens

Consideremos un sistema que usa autenticación basada en JWT, donde los roles del usuario están embebidos directamente en el token:

```json
{
  "user_id": 123,
  "role": "admin",
  "exp": 1710000000
}
````

El sistema asume que el rol contenido en el token refleja correctamente los privilegios actuales del usuario.

Ahora consideremos la siguiente secuencia:

1. Un usuario se autentica y recibe un token válido con privilegios elevados (`role = admin`)
2. Un administrador revoca esos privilegios en el sistema backend
3. El token emitido previamente sigue siendo válido hasta su expiración
4. Los servicios downstream siguen confiando en el token sin revalidar el rol actual del usuario

Desde la perspectiva del sistema, los controles de autorización están funcionando como se espera.

Sin embargo, están operando sobre datos de identidad desactualizados.

El problema no es un control de autorización ausente, sino una suposición incorrecta:

que los claims de identidad siguen siendo válidos durante toda la vida del token

Esto convierte efectivamente la identidad en una fotografía en el tiempo, en lugar de una representación del estado actual del sistema.

En la práctica, la identidad es dinámica. Cualquier sistema que la trate como estática introduce una ventana donde las decisiones de autorización se toman con información obsoleta.

---

### Se asume que el estado es consistente

Los sistemas distribuidos rara vez tienen una única fuente de verdad en todo momento.

Sin embargo, muchos diseños asumen:

* propagación inmediata de permisos
* estado sincronizado entre servicios
* enforcement consistente en todas partes

En realidad:

* las cachés introducen retrasos
* los servicios operan con datos obsoletos
* la revocación no es inmediata

Esto crea ventanas de accesoo no intencionado.

Estas ventanas suelen ser pequeñas, pero en sistemas distribuidos incluso inconsistencias de corta duración pueden ser explotadas de forma confiable.

Consideremos una arquitectura distribuida compuesta por múltiples servicios:

```
Usuario → API Gateway → Servicio A → Servicio B
```

El Servicio A es responsable de validar el accesoo a un recurso, mientras que el Servicio B se encarga de recuperar los datos.

El sistema asume que los cambios de permisos se reflejan inmediatamente en todos los servicios.

Ahora consideremos la siguiente secuencia:

1. Un usuario tiene acceso a un recurso
2. El accesoo es revocado en el sistema primario de autorización
3. El Servicio A refleja el estado actualizado inmediatamente
4. El Servicio B sigue dependiendo de datos de autorización en caché
5. Una solicitud es enrutada directa o indirectamente hacia el Servicio B

Debido a que el Servicio B opera con estado obsoleto, el usuario todavía puede acceder al recurso.

El sistema se comporta de manera inconsistente dependiendo de qué componente procese la solicitud.

La suposición subyacente es:

> que todos los servicios comparten una visión consistente y actualizada del estado de autorización

#### Escenario de falla combinada: identidad obsoleta + estado inconsistente

En muchos sistemas reales, las inconsistencias de identidad y estado no ocurren de forma aislada.

Consideremos el siguiente escenario:

1. Un usuario se autentica y recibe un token que contiene privilegios elevados
2. Los permisos del usuario son revocados poco después
3. El token sigue siendo válido y es aceptado por múltiples servicios
4. Algunos servicios dependen de datos de autorización en caché
5. Las solicitudes son procesadas usando tanto identidad obsoleta como estado obsoleto

En ningún momento falta un control de autorización.

Cada componente aplica control de accesoo en base a la información que tiene.

Sin embargo, la información en sí ya no es correcta.

Esto lleva a un modo de falla sutil pero crítico:

> las decisiones de autorización son técnicamente correctas, pero semánticamente incorrectas

Este tipo de problema es particularmente difícil de detectar con enfoques tradicionales de testing, ya que no se manifiesta como un bypass simple, sino como un problema de timing y consistencia dentro del sistema.

---

### Los límites de confianza son implícitos

Un patrón común:

```
Usuario → API Gateway → Servicio A → Servicio B
```

La autorización se verifica una vez y luego se confía implícitamente aguas abajo.

Esto crea zonas de confianza ocultas donde:

* los servicios asumen que la validación previa es suficiente
* no se realizan controles adicionales
* las APIs internas se convierten en superficies de alto riesgo

Este patrón cambia efectivamente el modelo de seguridad desde la verificación explícita hacia la confianza implícita, aumentando significativamente la superficie de ataque dentro de los sistemas internos.

---

### La lógica de autorización está incompleta

Incluso cuando se define un modelo, como RBAC, ABAC o ReBAC, la implementación suele desviarse:

* enforcement parcial entre endpoints
* uso inconsistente de políticas
* falta de validación de propiedad
* herencia incorrecta de permisos

En este punto, el enforcement existe, pero no es confiable.

El sistema aplica autorización, pero no con la consistencia suficiente para garantizar un comportamiento correcto.

## Por qué el enforcement ya llega demasiado tarde

Para cuando se ejecuta un control de autorización:

* la identidad puede estar obsoleta
* los permisos pueden estar desactualizados
* las suposiciones de confianza pueden haber sido violadas

Los mecanismos de enforcement no pueden corregir suposiciones defectuosas.

Solo operan sobre el estado actual, y potencialmente incorrecto, del sistema.

## La pieza faltante: threat modeling y análisis de riesgo

Uno de los patrones más comunes en sistemas reales es este:

* se implementan mecanismos de autenticación y autorización
* los sistemas pasan a producción
* los problemas se descubren a través de incidentes o pruebas
* las correcciones se aplican incrementalmente

Sin modelar explícitamente cómo un atacante interactuaría con el sistema, estas suposiciones permanecen sin  
cuestionarse hasta que fallan en producción, que es lo que suele fallar en latinoamérica que es que actuamos de forma  
reactiva mas que proactiva (sino ver el reciente ataque a registro civil y la respuesta de entidades como la anci).

Lo que falta es **pensamiento de seguridad en el diseño**.

Específicamente:

* threat modeling
* análisis del comportamiento adversario
* identificación de límites de confianza
* análisis de propagación de identidad
* evaluación de garantías de consistencia

Sin esto, los sistemas se diseñan bajo suposiciones optimistas o ingenuas:

* la identidad siempre es válida
* los servicios siempre se comportan correctamente
* los permisos siempre están actualizados

Los atacantes operan bajo las suposiciones opuestas.

## En qué deberían enfocarse las revisiones de seguridad

En lugar de enfocarse solamente en endpoints y controles, las evaluaciones de seguridad deberían analizar:

* cómo se propaga la identidad entre servicios
* dónde se toman y aplican las decisiones de autorización
* cómo se definen los límites de confianza
* cómo se maneja la consistencia del estado
* cómo se propagan los cambios de permisos

Estos aspectos definen la postura real de seguridad del sistema.

## Conclusión

Las fallas de autorización rara vez son causadas por controles ausentes.

Son causadas por sistemas que toman decisiones correctas basadas en suposiciones incorrectas.

Entender esas suposiciones, y cómo se rompen, es lo que separa probar inputs de evaluar realmente la seguridad.
