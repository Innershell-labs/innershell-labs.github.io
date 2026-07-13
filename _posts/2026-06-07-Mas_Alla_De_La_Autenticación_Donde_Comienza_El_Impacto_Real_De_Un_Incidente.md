---
layout: default
title: "Más allá de la autenticación: donde comienza el impacto real de un incidente"
lang : es
---

# Más allá de la autenticación: donde comienza el impacto real de un incidente

En seguridad ofensiva todavía es común tratar la autenticación como si fuera el principal límite o punto de inflexión de la seguridad de un activo o sistema.

Si el login resiste, el sistema parece razonablemente protegido.

Si las credenciales son robustas, existe MFA y el manejo de sesiones parece aceptable, muchas evaluaciones pasan rápidamente a buscar vulnerabilidades tradicionales: inyecciones, paneles expuestos, malas configuraciones, componentes desactualizados, headers ausentes, CVEs, scanners y hallazgos aislados.

Todo eso sigue siendo relevante.

Pero en incidentes reales, especialmente en entornos empresariales modernos, la pregunta más importante no siempre es si un atacante puede autenticarse.

La pregunta más importante suele ser qué puede hacer una identidad válida una vez que el sistema la acepta.

Ahí es donde la autorización se convierte en el verdadero límite del impacto.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/authentication-to-authorization-boundary.svg' | relative_url }}"
    alt="Path from valid identity to incident impact through authority and delegation"
    loading="lazy"
  >
  <figcaption>A valid identity is only the starting point. The real impact depends on how far its authority can propagate.</figcaption>
</figure>

## El incidente no termina con el acceso

Muchas evaluaciones de seguridad todavía tratan el acceso como el gran hito ofensivo:

- obtener credenciales
- evadir un login
- robar una sesión
- comprometer una cuenta
- alcanzar un panel interno

Desde la perspectiva de un atacante real, eso es solo el comienzo.

Una identidad válida no es el objetivo final.

Es un contexto de ejecución.

Una vez que el sistema acepta una identidad, las preguntas relevantes cambian:

- ¿Qué recursos puede alcanzar?
- ¿Qué acciones puede ejecutar?
- ¿Qué relaciones de confianza hereda?
- ¿Qué servicios actuarán en su nombre?
- ¿Qué límites de datos puede cruzar?
- ¿Qué flujos de negocio puede activar?
- ¿Qué controles limitan su radio de impacto?
- ¿Qué telemetría existe cuando esa identidad se comporta de forma anómala?

Ahí es donde muchos sistemas fallan, ya que muchas veces ni quienes diseñan el sistema, implementan servicios y tecnologías, desarrollan, defienden o evalúan ofensivamente consideran todos estos puntos.

Autentican correctamente al usuario, servicio o aplicación que realiza la solicitud, pero no limitan adecuadamente las consecuencias del acceso legítimo.

Nos descansamos demasiado en la autenticación.

## La autenticación responde identidad. La autorización define el radio de impacto

La autenticación responde:

¿Quién está haciendo la solicitud?

La autorización responde:

¿Qué puede hacer esta identidad, sobre qué recurso, bajo qué contexto, por qué camino y con qué efectos posteriores?

Esa última parte suele ignorarse.

En sistemas reales, la autorización no es un único check. Es una cadena de decisiones distribuidas entre componentes:

- API gateways
- servicios de aplicación
- workers en segundo plano
- APIs internas
- bases de datos
- colas de mensajes
- servicios cloud
- integraciones de terceros
- cuentas de servicio
- motores de políticas
- capas de caché

Un usuario puede ser autenticado en el perímetro del sistema, pero el impacto real de esa sesión se define mucho más adentro.

El error es asumir que la autenticación crea un contexto seguro.

No lo hace.

La autenticación crea un contexto de identidad.

La autorización debe decidir hasta dónde puede propagarse ese contexto y qué autoridad puede ejercer.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/authorization-blast-radius-clean.svg' | relative_url }}"
    alt="Authorization checkpoints across request, service, job, data, and download stages"
    loading="lazy"
  >
  <figcaption>Authorization should be checked across the full execution path, not only at the first request.</figcaption>
</figure>

## El problema de las pruebas ofensivas centradas en el login

Gran parte del aprendizaje ofensivo todavía condiciona a las personas a pensar en términos de puntos de entrada rotos.

1. Encuentra el login.

2. Pregunta a ChatGPT o Claude.

3. Prueba payloads comunes.

4. Busca SQL injection.

5. Corre el scanner: Acunetix, Invicti, Nessus u otra herramienta similar.

6. Encuentra el CVE.

7. Explota la máquina.

8. Pasa al siguiente objetivo.

Ese es un enfoque preocupante que sigo viendo de forma masiva en LATAM.

Puede ser útil para aprender fundamentos o hacer revisiones genéricas, pero construye un modelo superficial de cómo fallan los sistemas reales.

Los laboratorios, máquinas vulnerables y entornos intencionalmente rotos suelen enseñar una visión lineal del compromiso:

```text
reconocimiento → explotación → shell → escalamiento de privilegios
```

Los sistemas empresariales reales rara vez son lineales.

Están compuestos por identidades, servicios, workflows, políticas, roles, límites de datos, procesos asíncronos, integraciones y supuestos implícitos de confianza.

Una plataforma SaaS, un flujo bancario, un entorno cloud o una API empresarial no son simplemente un conjunto de endpoints.

Son sistemas de autoridad delegada.

Si una revisión no modela esa autoridad, probablemente va a perder los riesgos más importantes.

## Las fallas de autorización no siempre son checks ausentes

Una idea común es pensar que las fallas de autorización ocurren solo cuando alguien olvidó agregar un control de acceso.

Eso ocurre, pero no es toda la historia.

En sistemas más maduros, el check puede existir y aun así estar equivocado.

El sistema puede estar validando:

- el recurso incorrecto
- el tenant incorrecto
- la acción incorrecta
- el rol incorrecto
- la audiencia incorrecta del token
- el momento incorrecto
- la identidad de servicio incorrecta
- la relación incorrecta dentro del grafo

Por eso muchas fallas de autorización no son simplemente ausencia de autorización.

Son decisiones de autorización tomadas con contexto incompleto o incorrecto.

Un servicio puede aplicar una política.

La política puede evaluarse correctamente.

La decisión puede seguir siendo insegura porque el contexto usado para decidir era incorrecto.

Esa es la parte que las pruebas automáticas suelen perder.

## Las credenciales válidas no son el threat model completo. La autoridad mal usada sí

En muchos incidentes, los atacantes no necesitan romper la autenticación.

Usan:

- credenciales filtradas
- sesiones válidas
- cookies robadas
- tokens OAuth
- refresh tokens
- API keys
- cuentas de servicio
- roles con privilegios excesivos
- integraciones de terceros comprometidas
- cuentas internas
- identidades de workloads cloud

Desde una perspectiva defensiva, esto cambia el threat model.

La pregunta no es solamente:

¿Puede entrar un atacante?

La mejor pregunta es:

Si un atacante obtiene una identidad válida, ¿cuánta autoridad puede ejercer antes de ser detenido?

Esa pregunta es mucho más difícil.

Obliga a revisar:

- principio de mínimo privilegio
- aislamiento entre tenants
- validación de ownership
- herencia de permisos
- diseño de scopes
- revocación de sesiones
- confianza entre servicios
- auditabilidad
- cobertura de detección
- reducción del radio de impacto

Esta es la diferencia entre probar autenticación y evaluar resiliencia.

## La superficie de autorización es más grande que la superficie de API

Las pruebas de seguridad suelen partir mapeando endpoints.

Eso es necesario, pero insuficiente.

La superficie de autorización incluye cada lugar donde la autoridad se crea, transforma, delega, cachea, asume o aplica.

Eso incluye:

- quién emitió el token
- quién lo valida
- quién confía en esa validación
- dónde se interpretan los scopes
- dónde se mapean los roles
- dónde se valida ownership
- dónde se aplican los límites de tenant
- dónde se usan cuentas de servicio
- dónde continúan ejecutándose jobs asíncronos
- dónde se cachean permisos
- dónde se resuelven relaciones entre recursos
- dónde se registran las decisiones de política

Un sistema puede tener una superficie de API pequeña y una superficie de autorización grande.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/authorization-surface-vs-api-surface.svg' | relative_url }}"
    alt="Authorization checkpoints across request, service, job, data, and download stages"
    loading="lazy"
  >
  <figcaption>large authorization surface examples.</figcaption>
</figure>

Esto es especialmente cierto en entornos distribuidos, donde una sola solicitud puede activar múltiples acciones internas.

Por ejemplo:

Un usuario solicita una exportación.

La API valida la solicitud.

Se encola un job.

Un worker lo procesa más tarde.

El worker lee datos desde storage.

Se genera un archivo.

Se crea una URL firmada.

Se envía una notificación.

¿Dónde se aplicó la autorización?

¿Al momento de la solicitud?

¿Al momento de ejecutar el job?

¿Al acceder a los datos?

¿Al generar el archivo?

¿Al descargarlo?

Si la respuesta es “solo al comienzo”, el sistema puede estar dependiendo de autorización obsoleta.

## Los incidentes reales explotan cadenas de confianza, no solo bugs

Tratar vulnerabilidades de forma aislada es otro error frecuente.

Un permiso débil puede parecer medio.

Una credencial filtrada puede parecer contenida.

Una validación de tenant ausente puede parecer un problema de un endpoint.

Una cuenta de servicio permisiva puede parecer una decisión operacional conveniente.

Una detección ausente puede parecer solo una brecha de monitoreo.

Pero los atacantes no experimentan estos elementos como hallazgos separados.

Los experimentan como un camino.

Ejemplo:

1. Una cuenta válida es comprometida.
2. La cuenta tiene más acceso del esperado.
3. Una API valida autenticación, pero no ownership del recurso.
4. Un job de exportación se ejecuta con privilegios de servicio.
5. Los archivos generados quedan almacenados en una ubicación accesible mediante enlaces predecibles o de larga duración.
6. Los logs registran la ejecución del job, pero no preservan correctamente el contexto del usuario original.
7. La detección observa comportamiento normal de servicio, no abuso.

Ninguno de estos pasos requiere un exploit clásico.

El incidente emerge de la composición de comportamientos legítimos.

Por eso la autorización debe revisarse como una propiedad del sistema, no como una propiedad aislada de un endpoint.

## El control de acceso también es un problema de detección

La autorización suele discutirse como prevención.

Permitir o denegar.

Pero en incidentes reales, el control de acceso también es un problema de detección y respuesta.

Un sistema maduro no debería preguntar solo:

¿Esta solicitud debería permitirse?

También debería preguntar:

¿Este patrón de acceso es esperado para esta identidad?

Ejemplos:

- Un usuario accede repentinamente a cientos de registros.
- Una cuenta de servicio empieza a leer datos fuera de su dominio normal.
- Un refresh token se usa desde una nueva ubicación geográfica.
- Una cuenta de bajo privilegio activa workflows de alto impacto.
- Un usuario limitado a un tenant prueba repetidamente recursos vecinos.
- Un servicio interno llama a una ruta de API que normalmente nunca utiliza.
- Un token se usa contra una audiencia para la que no fue emitido.

Estos no siempre son fallos de autenticación.

Son señales de abuso de autorización.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/access-control-radius.png' | relative_url }}"
    alt="Access Control Detection Radius"
    loading="lazy"
  >
  <figcaption>access control as a detection and response problem</figcaption>
</figure>

Si un sistema no puede observar cómo se usa la autoridad, difícilmente puede detectar cuándo el acceso legítimo se vuelve malicioso.


Esa es una de las razones por las que seguridad ofensiva, CTI, detection engineering y gestión de riesgos no deberían operar como disciplinas aisladas.

## La pregunta de una revisión madura

Una revisión superficial pregunta:

¿Puedo evadir el login?

Una revisión mejor pregunta:

¿Puedo acceder a algo que no debería?

Una revisión madura pregunta:

¿Cómo este sistema crea, propaga, limita, observa y revoca autoridad?

Esa pregunta cambia todo.

Obliga a inspeccionar:

- fuentes de identidad
- claims de tokens
- duración de sesiones
- comportamiento de refresh tokens
- rutas de revocación
- ownership de recursos
- límites entre tenants
- mapeo de roles
- modelos de relación
- puntos de enforcement
- identidades de servicio
- límites de confianza
- workflows asíncronos
- trazabilidad y auditoría
- lógica de detección
- modos de falla



Aquí es donde las revisiones senior se diferencian de las pruebas basadas en herramientas.

El objetivo no es acumular hallazgos.

El objetivo es entender cómo falla el sistema bajo uso adversarial.

## Fallo de autenticación vs fallo de autorización en el análisis de incidentes

Al analizar un incidente, puede ser útil separar tres capas.



Primero: adquisición de identidad.

¿Cómo obtuvo el atacante una identidad válida?

Ejemplos:

- phishing
- credential stuffing
- infostealer logs
- API keys expuestas
- robo de sesión
- abuso de consentimiento OAuth
- cuenta de servicio comprometida

Segundo: expansión de autoridad.

¿Qué podía hacer esa identidad?

Ejemplos:

- acceder a registros sensibles
- enumerar tenants
- invocar workflows privilegiados
- asumir roles
- crear tokens
- exportar datos
- acceder a APIs internas
- activar procesos en segundo plano

Tercero: materialización del impacto.

¿Cómo permitió el sistema que esa autoridad se transformara en impacto de negocio?

Ejemplos:

- exfiltración de datos
- toma de cuentas
- transacciones fraudulentas
- escalamiento de privilegios
- persistencia
- interrupción operacional
- movimiento lateral
- evasión de controles

Muchos reportes se enfocan demasiado en la primera capa.

Pero la segunda y la tercera suelen explicar por qué el incidente llegó a ser grave.

El atacante puede haber entrado por autenticación.

Pero el daño fue definido por autorización.

## Por qué esto importa para Red Team y Security Engineering

Un Red Team que solo demuestra acceso no es suficiente.

Una función senior de seguridad debería poder responder:

- ¿Qué supuestos permitieron la ruta de ataque?
- ¿Qué permisos amplificaron el impacto?
- ¿Qué límite de confianza falló?
- ¿Qué decisión de autorización fue demasiado amplia?
- ¿Qué detección debería haberse activado?
- ¿Qué control habría reducido el radio de impacto?
- ¿Qué cambio arquitectónico evita recurrencia?

Ese es el valor de la seguridad ofensiva cuando madura más allá de la explotación.

Se convierte en una forma de probar el modelo de confianza de la organización.

## Escenario simulado

Imaginemos una plataforma SaaS multi-tenant utilizada por distintas empresas para gestionar reportes financieros.

La arquitectura es relativamente común:

- los usuarios acceden mediante SSO
- un API Gateway valida tokens
- un servicio de reportes gestiona solicitudes de exportación
- un worker genera archivos en segundo plano
- los archivos quedan disponibles mediante URLs firmadas
- una cuenta de servicio accede al storage para generar y publicar los reportes

El flujo parece razonable.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/simulated_scenario_saas_architecture.svg' | relative_url }}"
    alt="Multi-tenant SaaS export flow where context loss can expose another tenant's data"
    loading="lazy"
  >
  <figcaption>In asynchronous workflows, the original user context can weaken or disappear while service-level authority continues execution.</figcaption>
</figure>

Un usuario autenticado solicita la exportación de un reporte.

El API Gateway valida que el token sea válido.

El servicio de reportes confirma que el usuario pertenece a la organización.

Luego se crea un job asíncrono para generar el archivo.

El problema aparece en los detalles.

El job no conserva correctamente el contexto completo del usuario original.

El worker ejecuta la exportación usando una cuenta de servicio con permisos amplios.

La consulta que genera el reporte recibe un `organization_id` desde el payload del job.

El sistema valida que el usuario pertenece a una organización, pero no revalida que el reporte solicitado pertenece a esa misma organización al momento de generar el archivo.

Desde el punto de vista de autenticación, todo parece correcto.

El usuario inició sesión.

El token era válido.

El gateway funcionó.

El servicio creó un job legítimo.

El worker ejecutó una operación esperada.

Pero desde el punto de vista de autorización, el sistema falló en varios puntos:

- se validó identidad al inicio, pero no autoridad al momento de uso
- se perdió contexto del usuario original en el flujo asíncrono
- una cuenta de servicio amplificó el impacto
- el `organization_id` se trató como contexto confiable
- la URL firmada expuso el resultado sin volver a evaluar permisos
- los logs registraron actividad normal del worker, no abuso de acceso

Este escenario no depende de una inyección, una RCE o un bypass clásico de login.

Depende de una cadena de confianza mal modelada.

El atacante no rompió la autenticación.

Usó una identidad válida para activar un flujo legítimo, y el sistema permitió que esa autoridad se propagara más allá de lo que debía.

## Conclusión

La autenticación es esencial. Autenticación débil, credenciales filtradas, sesiones robadas y tokens comprometidos pueden iniciar incidentes reales.

Pero la autenticación rara vez cuenta la historia completa.

En sistemas modernos, el impacto real está determinado por la autorización: permisos, relaciones, contexto, delegación, confianza entre servicios, duración de sesiones, revocación, detección y radio de impacto.

Una identidad válida nunca debería tratarse como una identidad segura.

Debería tratarse como un contexto de ejecución limitado.

La pregunta no es solo si un atacante puede entrar.

La pregunta es qué permite hacer el sistema una vez que alguien está dentro.

La autenticación puede iniciar el incidente.

La autorización define el impacto.
