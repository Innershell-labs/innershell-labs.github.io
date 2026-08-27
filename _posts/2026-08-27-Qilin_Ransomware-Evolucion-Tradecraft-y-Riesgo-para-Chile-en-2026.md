---
layout: default
title: "Qilin Ransomware: evolución, tradecraft y riesgo para Chile en 2026"
lang : es
---

# Qilin no es solamente un ransomware que cifra al final

*Analizar Qilin únicamente como una familia de ransomware conduce a observar la fase más visible del incidente y, en muchos casos, la menos útil para prevenirlo. En 2026, la unidad de análisis adecuada es más amplia: una operación Ransomware-as-a-Service con un núcleo operativo, afiliados heterogéneos, múltiples rutas de acceso, tooling legítimo y malicioso, capacidad sobre Windows, Linux y VMware ESXi, doble extorsión y una evolución relevante en defensa evasiva.*

Su linaje público comienza en 2022 bajo el nombre Agenda. Con el tiempo, Qilin pasó a convertirse en la denominación predominante de la operación y del ransomware asociado. MITRE ATT&CK registra actualmente Qilin como S1242, mantiene Agenda como software relacionado y separa a Water Galura / GOLD FEATHER (G1050) como el grupo operador del servicio RaaS. Esta separación no es un detalle taxonómico: permite distinguir el código de cifrado, la infraestructura criminal, el equipo operador y los afiliados que efectivamente conducen las intrusiones.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_1.png' | relative_url }}"
    alt="Actores Qilin Ransomware"
    loading="lazy"
  >
  <figcaption>https://attack.mitre.org/software/S1242/</figcaption>
</figure>

El juicio central de esta investigación es de alta confianza: Qilin debe considerarse una de las amenazas/ransomware de mayor relevancia operacional en 2026, no por una técnica única ni por un encryptor excepcional, sino por la combinación de escala, diversidad de afiliados, explotación de acceso remoto, abuso de credenciales, progresión sobre Active Directory, deterioro de defensas, exfiltración, ataque a backups y virtualización, y capacidad de impacto multiplataforma (el ecosistema completo). Trend Micro documenta una expansión sostenida durante 2024-2025; Check Point lo mantuvo entre las operaciones con mayor volumen observable durante 2026; Cisco Talos añadió un elemento especialmente relevante al analizar un EDR killer utilizado en ataques Qilin con capacidad para interferir con más de 300 drivers de productos de seguridad.

> **El evento del ransomware no comienza cuando aparece la nota de rescate en el desktop de un usuario random de la empresa. Para Qilin, la fase decisiva suele estar mucho antes: acceso remoto o credenciales → identidad y privilegios → Active Directory → movimiento lateral → degradación de defensas → exfiltración → backups/virtualización → cifrado e impacto.**

Esta distinción también cambia la conversación para un CISO o la gerencia. La pregunta deja de ser si la organización puede detectar un binario Qilin o acumular millones de IoCs y pasa a ser si sus controles de identidad, acceso remoto, Tier-0, telemetría, backup y virtualización pueden interrumpir una cadena adversaria antes de que el actor llegue a una posición desde la cual el ransomware sea casi una formalidad operativa.

Para Chile, la conclusión es igualmente importante. Existe evidencia pública suficiente para afirmar con alta confianza que Qilin ya forma parte del espacio de amenaza real para organizaciones chilenas. Sin embargo, la transparencia pública no permite convertir automáticamente cada organización listada en un Data Leak Site en una víctima confirmada. Tambien hay que considerar la FALTA de transparencia de las empresas al esconder a los usuarios los compromisos reales donde se ven involucrados sus datos, y aquí existe la postura desde quien vela por la empresa donde “el negocio es la prioridad” y no revelaremos nada que afecte a la reputación, y la postura ética donde la empresa toma una postura madura donde sabe manejar incidentes en caso de haberlos, con transparencia y un plan de trabajo claro.

## 1. Antes de hablar de víctimas: cómo leer la evidencia

Una investigación de ransomware se degrada rápidamente cuando mezcla tres cosas distintas: lo que el actor criminal afirma, lo que un tercero reporta y lo que puede sostenerse con evidencia primaria o forense. En Qilin, esta diferencia es especialmente importante porque una parte considerable de la visibilidad pública proviene de Data Leak Sites y trackers que replican esos listings.

Los DLS son útiles para medir presión extorsiva observable, actividad relativa, temporalidad y posibles patrones sectoriales. No son un censo confiable de intrusiones. Una publicación puede ser auténtica, exagerada, duplicada, incompleta o incluso falsa; una organización comprometida puede pagar antes de ser publicada; un afiliado puede migrar entre programas RaaS; y distintos proveedores aplican reglas de deduplicación, captura y fechado diferentes. Por ello, sumar cifras de Trend Micro, Check Point, ReliaQuest, SOCRadar, Ransomfeed u otros trackers como si fueran incidentes confirmados produciría una precisión aparente, no inteligencia robusta. (Aunque quienes trabajamos en CTI, sabemos que la mayoría de claims chilenos de los últimos años son auténticos incidentes, no todos)

> **Un claim confirma que el actor o un tracker publicó una afirmación. No confirma por sí solo acceso, exfiltración, cifrado, volumen de datos ni impacto real, pero tampoco significa que sea falso, ojo ahí.**

La taxonomía utilizada en la investigación permite mantener esa separación y, más importante aún, conservar el nivel de confianza cuando la información se transforma en una decisión defensiva o ejecutiva.

| **Etiqueta** | **Uso en esta investigación** |
| --- | --- |
| CONFIRMADO | Respaldado por la organización afectada, una autoridad pública, evidencia forense directa o varias fuentes independientes fuertes. |
| CLAIMED | Publicación atribuida al DLS de Qilin o reproducida por un tracker. Confirma el claim, no la intrusión. |
| REPORTED | Atribución de un tercero con alguna evidencia o acceso a fuentes, pero sin confirmación pública primaria completa. |
| EVIDENCIA TÉCNICA | Comportamiento observado en malware analysis, incident response o telemetría de investigación. |
| INFERENCIA | Conclusión analítica derivada de hechos observados y separada explícitamente de ellos. |
| HIPÓTESIS | Explicación plausible cuya evidencia todavía es insuficiente para elevarla a inferencia robusta. |
| INSUFICIENTE / NO VERIFICABLE | La información pública no permite determinar razonablemente el hecho. |

La confianza tampoco es binaria. Una atribución puede ser sólida respecto de la existencia del incidente y débil respecto del actor; un tracker puede ofrecer alta confianza en que observó un listing y baja confianza en que el breach ocurrió como fue descrito. Esa granularidad es fundamental en el caso chileno, donde existen incidentes oficiales, atribuciones agregadas y múltiples claims nominales, pero no siempre coinciden en una misma fuente primaria.

Este punto no es una precaución académica. Una mala clasificación modifica el riesgo. Si un CISO interpreta un claim como una intrusión confirmada, puede sobrerreaccionar a un dato débil; si descarta todos los claims por no ser confirmados, puede ignorar una señal temprana de actividad relevante. La CTI que es útil no elimina la incertidumbre: la hace visible, trazable y utilizable.

## 2. Qilin, Agenda, RaaS, operadores y afiliados: separar la marca del intruso

La continuidad Agenda → Qilin tiene alta confianza técnica, aunque distintas fuentes no fijan exactamente el mismo momento para el cambio de denominación. Trend Micro sitúa las primeras operaciones observadas de Agenda en julio de 2022, inicialmente con ransomware escrito en Go, y documenta variantes en Rust hacia finales de ese mismo año. Group-IB ubica la promoción formal del modelo RaaS en foros clandestinos a comienzos de 2023. MITRE utiliza hoy Qilin como entrada principal y Agenda como software relacionado. 

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_2.png' | relative_url }}"
    alt="Modelo Ransomware as a service"
    loading="lazy"
  >
  <figcaption>https://www.varonis.com/blog/ransomware-as-a-service</figcaption>
</figure>

***A partir de ese punto, conviene abandonar la idea de un único 'grupo Qilin' ejecutando una secuencia homogénea. Un RaaS desacopla la marca del ransomware respecto del actor que obtiene acceso y conduce la intrusión. La consecuencia práctica es que dos incidentes pueden terminar con Qilin y, aun así, presentar initial access, tooling, persistencia, exfiltración y tiempos operativos diferentes.***

| **Nivel** | **Aplicación a Qilin** |
| --- | --- |
| Ransomware family | El código de cifrado y sus variantes Go, Rust, Linux y ESXi. |
| RaaS operation | La infraestructura criminal que proporciona payload generation, negociación, soporte y publicación de datos. |
| Operator / core team | MITRE identifica a Water Galura / GOLD FEATHER como operadores del servicio Qilin RaaS. |
| Affiliate | Actor externo que obtiene acceso, conduce la intrusión y utiliza la plataforma o payload Qilin; su tradecraft puede diferir sustancialmente de otro afiliado. |
| Campaign / cluster | Conjunto de incidentes relacionados por infraestructura o TTPs; no implica necesariamente identidad con el core team. |

MITRE atribuye a Water Galura / GOLD FEATHER la generación de payloads, la negociación y la publicación de datos robados para afiliados, además del reclutamiento en foros rusófonos. Esa atribución es relevante para modelar la operación, pero no autoriza a atribuir automáticamente a Water Galura cada intrusión donde aparece Qilin.

La heterogeneidad de afiliados es uno de los elementos más importantes para detección. Arctic Wolf observó en 2026 intrusiones que compartían explotación inicial y deployment de Qilin, pero divergían después: algunas avanzaban hacia doble extorsión y otras aceleraban directamente al cifrado. El payload puede ser relativamente estable; el pre-ransomware tradecraft no lo es.

También existen relaciones públicas que requieren cuidado. Microsoft y Trend han asociado un uso limitado de Agenda/Qilin con Moonstone Sleet en 2025; esa asociación no demuestra que el actor norcoreano controle Qilin ni convierte la operación RaaS en una estructura estatal. Trend ha evaluado además migración de algunos afiliados tras la disrupción de RansomHub, mientras Check Point ha relacionado al fundador de The Gentlemen con experiencia previa como afiliado de Qilin. Estas relaciones son útiles para entender el mercado criminal, pero no deben confundirse con una identidad única detrás de todos los casos.

## 3. Evolución 2022-2026: de un ransomware configurable a una operación de impacto transversal

La evolución de Qilin no puede resumirse como una simple mejora del cifrador. El cambio más significativo ha sido la ampliación del sistema operativo criminal alrededor del payload: más plataformas, más rutas de acceso, mayor abuso de herramientas legítimas (LOTL para los que le saben ;) ), capacidad de atacar recuperación y virtualización, y una defensa evasiva que en 2026 ya incluye manipulación a nivel kernel.

| **Periodo** | **Evolución observada** | **Confianza** | **Lectura analítica** |
| --- | --- | --- | --- |
| Jul. 2022 | Primeras operaciones conocidas de Agenda con ransomware en Go altamente configurable. | Alta | Origen público del linaje. |
| Fin de 2022 | Aparición de implementación en Rust. | Alta | Mayor flexibilidad y evolución multiplataforma. |
| Feb. 2023 | Promoción formal del RaaS en foros clandestinos según Group-IB. | Alta | Maduración de familia a servicio criminal. |
| 2023-2024 | Expansión Windows/Linux/ESXi y crecimiento del soporte VMware. | Alta | La virtualización entra en el modelo de impacto. |
| 2024 | Variantes Rust incorporan propagación hacia vCenter/ESXi y uso de PsExec en determinadas versiones. | Alta | Mayor capacidad de fan-out y daño transversal. |
| 2024-2025 | Se observan loaders, RMM legítimo, BYOVD y mayor modularidad de defense evasion. | Alta | El ecosistema pre-ransomware gana protagonismo. |
| 2025 | Expansión DLS y migraciones/relaciones de afiliados en un ecosistema RaaS cambiante. | Media-Alta | Escala y flexibilidad operativa. |
| 2026 | Explotación de appliances remotos, intrusiones aceleradas y EDR killer especializado analizado por Talos. | Alta | Qilin combina acceso perimetral moderno con degradación de defensas y targeting de Tier-0/virtualización. |

La transición de Go a Rust es relevante para malware analysis, pero sería un error convertirla en la principal historia de evolución. El riesgo para una organización no creció solamente porque el código cambió de lenguaje. Creció porque el entorno operacional permitió a los afiliados moverse desde acceso remoto hacia identidad, Active Directory, backups y VMware, y porque el ransomware pasó a ser el componente final de una cadena capaz de producir simultáneamente pérdida de confidencialidad, disponibilidad y capacidad de recuperación.

El caso Synnovis muestra por qué esta distinción importa. NHS England confirmó que el incidente del 3 de junio de 2024 redujo de forma severa la capacidad de procesamiento de laboratorio, provocó más de 11.000 retrasos o cancelaciones y requirió meses para una restauración completa. Posteriormente, autoridades sanitarias indicaron que el incidente contribuyó a la muerte de un paciente; la atribución pública a Qilin fue reportada por Reuters. El ransomware dejó de ser un problema de archivos cifrados y se convirtió en un problema de continuidad clínica y seguridad humana.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_3.png' | relative_url }}"
    alt="Indicadores ataque synnovis/NHS"
    loading="lazy"
  >
  <figcaption>https://www.blackfog.com/qilin-ransomware-analysis-impact-and-defense-2025/</figcaption>
</figure>

> **IMPLICACIÓN DE RIESGO**
>
> **Cuando identidad, virtualización y recuperación comparten el mismo plano de confianza, un incidente con ransomware puede dejar de ser un evento de endpoint y convertirse en una interrupción simultánea de múltiples servicios críticos para la continuidad operativa con sus respectivas consecuencias.**

## 4. El centro de gravedad técnico: el ecosistema pre-ransomware

*La característica técnica más importante de Qilin en 2026 no es el encryptor. Es la capacidad de afiliados distintos para entrar por caminos diferentes y converger sobre los mismos objetivos operativos: identidad, Active Directory, administración remota, defensa, datos, backups y virtualización.*

Esta observación cambia la forma de hacer hunting. Una firma del binario puede ser útil para confirmar una fase tardía. No es suficiente para interrumpir el ataque. La estrategia con mayor retorno consiste en detectar y validar comportamientos que aparecen antes del impacto, incluso cuando la herramienta utilizada por el afiliado cambia. (Si el threat hunting en tu empresa se basa simplemente en algunas queries y listas de IoCs únicamente, espero que este sea el comienzo del cambio)

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_4.png' | relative_url }}"
    alt="Threat Hunting basado en comportamientos y patrones"
    loading="lazy"
  >
  <figcaption>https://www.vectra.ai/topics/threat-hunting</figcaption>
</figure>

### 4.1 Initial Access: remote access e identidad como superficie repetida

La investigación encuentra soporte para varias rutas de acceso inicial. Group-IB documentó actividad asociada a infraestructura Fortinet/SSL-VPN y explotación de servicios públicos; en algunos casos existían indicios de password guessing o brute force, aunque la eliminación de logs impedía confirmar completamente el mecanismo. Sophos investigó una intrusión iniciada con credenciales comprometidas sobre una VPN sin MFA, con una permanencia aproximada de 18 días antes del ransomware. Trend ha descrito históricamente Initial Access Brokers, credenciales robadas y, en campañas más recientes, técnicas de social engineering.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_5.png' | relative_url }}"
    alt="Metodos acceso inicial QILIN"
    loading="lazy"
  >
  <figcaption>https://www.securin.io/articles/threat-actors-intelligence-report-qilin-ransomware</figcaption>
</figure>

En 2026 el perímetro remoto vuelve a aparecer con fuerza. Arctic Wolf observó múltiples intrusiones Qilin iniciadas mediante CVE-2026-0257 contra GlobalProtect; Unit 42 confirmó de forma independiente explotación activa de esa vulnerabilidad. Check Point relacionó otro caso post-exploitation con Qilin tras explotación de CVE-2026-50751 en Remote Access/Mobile Access.

Chile encaja en la misma clase de riesgo. El caso OIV/PSE de enero de 2026, reproducido desde una alerta del CSIRT Nacional, describió un acceso por fuerza bruta contra un firewall WatchGuard donde faltaban controles como MFA y mecanismos adecuados de bloqueo. La relevancia aquí no es WatchGuard como producto: la convergencia entre acceso remoto expuesto, autenticación débil y una ruta posterior hacia activos internos.

> **JUICIO TÉCNICO - ALTA CONFIANZA**
>
> **Remote access + identity es el principal punto de intersección entre el tradecraft global de Qilin y la evidencia pública chilena. Cambiar de fabricante de VPN sin corregir MFA, exposure management, lifecycle, lockout/risk-based authentication y segmentación no elimina la clase de riesgo.**

### 4.2 Credential Access: robar credenciales no siempre significa ejecutar Mimikatz

Qilin y sus afiliados han utilizado múltiples formas de acceso a credenciales. Group-IB observó módulos Mimikatz integrados para acceder a tokens y procesos privilegiados. Arctic Wolf documentó en 2026 dumping de LSASS mediante rundll32/comsvcs.dll y extracción de NTDS utilizando ntdsutil IFM. Trend añade acceso a credenciales almacenadas por Veeam en determinadas variantes o campañas.

El caso documentado por Sophos es particularmente valioso porque muestra una operación de identidad más sistémica. El actor modificó Group Policy y utilizó scripts depositados en SYSVOL para recolectar credenciales almacenadas en Google Chrome desde endpoints del dominio. La técnica transforma una capacidad administrativa legítima del dominio en un mecanismo de recolección distribuida. El problema ya no es solamente una workstation comprometida: es la conversión del plano de administración de AD en un multiplicador de acceso.

Este punto obliga a revisar la idea de Tier-0. Si GPO, SYSVOL, cuentas administrativas, backup credentials y vCenter comparten rutas de administración o identidades reutilizadas, la segmentación lógica declarada puede no existir operacionalmente.

### 4.3 Discovery: el atacante necesita comprender el sistema antes de destruirlo

Trend documenta nltest, whoami, net group, PowerShell/AD enumeration, WMI, process/network discovery y enumeración de ESXi. Arctic Wolf observó SoftPerfect Network Scanner y NetExec en intrusiones recientes. Son herramientas y comandos familiares para cualquier administrador o pentester, lo que reduce el valor de una detección basada únicamente en nombre de proceso.

La oportunidad está en el contexto: quién ejecuta la enumeración, desde qué segmento, después de qué autenticación, contra qué volumen de hosts y con qué relación temporal respecto de cambios de privilegios o accesos remotos. Un nltest desde una PAW autorizada durante mantenimiento no equivale a una ráfaga de descubrimiento AD desde una estación recién alcanzada desde VPN.

También es importante no inflar el perfil con comandos 'típicos de ransomware' si no existe observación específica. La investigación solo eleva a soporte Qilin aquellas técnicas para las cuales existe evidencia en las fuentes revisadas. Esa disciplina evita que el mapping ATT&CK se convierta en una checklist genérica sin valor analítico.

### 4.4 Lateral Movement y persistencia: herramientas legítimas, fan-out y administración remota

El movimiento lateral documentado incluye RDP con credenciales robadas, SMB/admin shares y PsExec. Las variantes Rust modernas pueden incorporar PsExec dentro del propio ransomware; otras campañas han mostrado Cobalt Strike, SSH/PuTTY y herramientas RMM. Arctic Wolf identificó además MeshAgent y una tarea \MeshUserTask en incidentes de 2026, junto con AnyDesk, LogMeIn y Ngrok en diferentes contextos. 

El valor defensivo no está en bloquear de forma indiscriminada toda herramienta dual-use. En organizaciones grandes, muchas son necesarias. El control debe distinguir uso autorizado de uso anómalo: nueva instalación o tenant RMM, ejecución desde hosts fuera de baseline, creación de servicios remotos, ADMIN$/C$ fan-out, nuevas sesiones este-oeste desde pools VPN o endpoints de usuario, y privilegios utilizados fuera del plano administrativo esperado.

La persistencia puede incluir Run/RunOnce, modificación de ImagePath de servicios, scheduled tasks, creación de cuentas administrativas y cambios de GPO. Cada una de estas técnicas tiene un significado distinto cuando aparece después de un acceso remoto anómalo o junto con credential dumping. La correlación entre fases es más robusta que una firma aislada.

### 4.5 Defense Evasion: cuando perder telemetría EDR puede ser la detección

Defense evasion es una de las áreas donde Qilin muestra una evolución técnica más clara. Las primeras capacidades de service/process termination y log clearing han sido complementadas por BYOVD y componentes especializados. Cisco Talos analizó msimg32.dll, un loader multi-stage asociado a ataques Qilin y probablemente ejecutado mediante DLL side-loading. La cadena utiliza técnicas para dificultar hooks y telemetría, interferir con ETW, manipular objetos kernel y cargar rwdrv.sys/hlpdrv.sys. Talos indica que el conjunto puede neutralizar callbacks y terminar procesos asociados con más de 300 drivers de productos EDR.

El detalle más importante para un SOC no es memorizar el nombre msimg32.dll. Es reconocer una nueva propiedad del incidente: el control defensivo puede convertirse en un objetivo activo. Si varios endpoints dejan de reportar de forma coordinada durante una secuencia de actividad privilegiada, tratar el evento como un simple problema de salud del agente puede eliminar precisamente la señal que el atacante está generando.

> **DETECCIÓN DE ALTO VALOR**
>
> **Un EDR heartbeat loss colectivo, acompañado por privileged execution o carga anómala de drivers, debe tratarse como una posible señal de ataque y correlacionarse con telemetría independiente: firewall, NDR, Windows Event Forwarding, SIEM, vCenter y plataforma de backup.**

Esto también limita una estrategia defensiva centrada exclusivamente en EDR. La investigación no sugiere que el EDR sea irrelevante; al contrario, muestra que es tan valioso que el adversario intenta neutralizarlo. Pero su capacidad debe complementarse con tamper protection, control de drivers vulnerables y fuentes de observabilidad que sobrevivan a la degradación del endpoint.

### 4.6 Exfiltration: doble extorsión sin una herramienta universal

No existe una herramienta única de exfiltración asociada a Qilin. Trend ha observado MEGAsync y WinSCP; Arctic Wolf ha documentado Rclone, MEGA, Proton Drive y FileZilla en diferentes incidentes 2026. El patrón relevante es funcional: una utilidad legítima o portable, ejecutada con frecuencia desde un servidor de alto valor, generando transferencias volumétricas hacia cloud o file-sharing antes del evento de cifrado.

Esto refuerza otra separación analítica: la detección de ransomware no debe comenzar con T1486. La exfiltración puede ser el momento en que el actor ya posee suficiente control para generar impacto regulatorio y reputacional, incluso si nunca cifra. Para sectores intensivos en datos -salud, finanzas, hospitality, servicios- la extorsión por publicación puede convertirse en el objetivo principal.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_6.png' | relative_url }}"
    alt="Algoritmos de encriptacion usados por actores de amenazas"
    loading="lazy"
  >
  <figcaption>https://www.picussecurity.com/resource/the-most-common-ransomware-ttp-mitre-attck-t1486-data-encrypted-for-impact</figcaption>
</figure>

### 4.7 Backups, Veeam y VMware/ESXi: atacar la capacidad de recuperarse

Qilin busca degradar la recuperación mediante eliminación de VSS/shadow copies, manipulación o eliminación de backups y targeting de Veeam. Group-IB documentó eliminación de tareas, cintas y backups; Trend registra daño a snapshots y discos VMware; MITRE mapea explícitamente Inhibit System Recovery (T1490).

La capacidad sobre VMware/ESXi no es teórica. MITRE registra ESXi como plataforma y Trend documenta variantes Linux/ESXi, propagación mediante vCenter, cambio de passwords, parada de máquinas virtuales y eliminación de discos o snapshots.

La implicación arquitectónica es severa. Muchas organizaciones consolidan decenas o cientos de servicios sobre un plano reducido de virtualización y backup. Si el mismo dominio, las mismas cuentas privilegiadas o las mismas rutas de administración alcanzan AD, Veeam y vCenter, el actor puede transformar un compromiso de identidad en una falla concentrada de recuperación. La eficiencia que hace atractiva la virtualización para operar también puede amplificar el blast radius cuando el plano de gestión es comprometido.

Para sectores chilenos con alta dependencia de VMware -industria, salud, minería, gobierno, logística- la pregunta defensiva no debería ser solamente si existen backups. Debe incluir si las identidades de backup y hypervisor están separadas, si existe acceso administrativo independiente, si los snapshots pueden ser destruidos desde el mismo trust plane y si la restauración completa fue realmente probada.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_7.jpg' | relative_url }}"
    alt="Preparacion de backups contra ransomware"
    loading="lazy"
  >
  <figcaption>https://mytekrescue.com/how-to-prevent-ransomware/</figcaption>
</figure>

### 4.8 El encryptor y la criptografía: importante, pero no la mejor superficie defensiva

Las implementaciones criptográficas varían entre builds. Group-IB analizó variantes con AES-256/CTR o ChaCha20 y protección asimétrica RSA-4096; Trend documenta otros builds con AES-256 y RSA-2048. Esta variación es coherente con generaciones configurables y refuerza que una estrategia basada exclusivamente en detalles criptográficos o firmas del payload es frágil.

Desde una perspectiva de Threat Engineering, la prioridad no es demostrar qué algoritmo usa cada muestra, salvo que el objetivo sea malware research o recuperación específica. Para reducción de riesgo, el valor está antes: impedir que el actor alcance credenciales, Tier-0, privilegios sobre backup o la capacidad de distribuir el payload a escala.

| **Fase** | **ATT&CK** | **Comportamiento Qilin observado** | **Oportunidad de detección** |
| --- | --- | --- | --- |
| Initial Access | T1133 / T1190 / T1078 | VPN, credenciales, appliances expuestos, explotación de servicios remotos | Auth anomalies, exploit telemetry, new device/ASN, pivot inmediato |
| Credential Access | T1003.001 / T1003.003 | LSASS, NTDS, Mimikatz, credenciales de navegador/backup | LSASS access, ntdsutil IFM, GPO/SYSVOL cambios |
| Discovery | T1018 / T1087 / T1069 | AD enumeration, host scanning, ESXi discovery | Ráfagas de consultas AD, scanners desde hosts inusuales |
| Lateral Movement | T1021.001 / T1021.002 / T1569.002 | RDP, SMB/admin shares, PsExec, RMM | East-west RDP, ADMIN$ fan-out, remote service creation |
| Defense Evasion | T1562.001 / T1574.002 / T1070.001 | EDR kill, BYOVD, DLL side-loading, log clearing | Driver loads, agent health loss, DLL path anomalies, log clear |
| Exfiltration | T1567.002 | MEGA, Rclone, Proton Drive, FileZilla, WinSCP | High-volume uploads desde servidores de valor |
| Impact | T1490 / T1486 / T1489 | Backup/snapshot destruction, service stop, encryption Windows/Linux/ESXi | Cambios backup/vCenter + mass file operations |

## 5. Qilin no tiene una cadena universal: el problema de detectar un RaaS

Una consecuencia directa del modelo RaaS es que no debe inferirse que cada intrusión Qilin despliega todos los componentes descritos. Buena parte del tooling pertenece al afiliado, no al core service. Esto explica por qué una campaña puede mostrar Cobalt Strike y otra no; por qué una intrusión utiliza Rclone y otra MEGA; o por qué dos casos con el mismo ransomware difieren en persistencia, tiempo de permanencia y orden de las fases.

El error defensivo sería construir una 'firma universal de Qilin' a partir de una muestra o un caso forense y asumir que el siguiente afiliado repetirá la secuencia. La estrategia más resistente combina detecciones por fase con correlación temporal y contextual: acceso remoto inusual + descubrimiento privilegiado + manipulación de GPO + pérdida de telemetría + fan-out administrativo + alteración de backups ofrece mucho más valor que esperar un hash.

El error analítico equivalente sería atribuir toda actividad observada al operador central. En un RaaS, el ransomware puede ser el elemento común mientras las decisiones tácticas -cómo entrar, qué herramientas usar, cuánto tiempo permanecer, qué datos robar y cuándo cifrar- pertenecen al afiliado. Por ello, 'Qilin' describe con alta confianza el ecosistema/payload en determinados casos, pero no siempre identifica al intrusion set responsable de cada paso.

## 6. Victimología global: volumen observable, diversidad sectorial e impacto

Los datasets públicos coinciden en que Qilin alcanzó una visibilidad muy alta durante 2025 y 2026, aunque sus cifras no son directamente comparables. Trend Micro contabilizó 1.377 organizaciones reclamadas entre octubre de 2022 y el 31 de enero de 2026 y casi 1.400 publicaciones durante 2025. Check Point registró 338 publicaciones durante Q1 2026 y 279 durante Q2, manteniendo a Qilin entre las operaciones más prolíficas de su dataset.

Estas cifras deben leerse como telemetría DLS, no como número de breaches confirmados. Aun así, su persistencia en datasets independientes, junto con el crecimiento de tooling y campañas observadas por equipos de incident response, sustenta la conclusión de que Qilin sigue siendo una operación de primer nivel en 2026.

Trend identifica manufacturing, healthcare y technology entre los sectores destacados, y su telemetría de intentos de ataque de 2025 sitúa especialmente alto a manufacturing, seguido por financial services, healthcare y government. Dragos, desde una perspectiva industrial, describe a Qilin como una de las operaciones persistentes contra organizaciones industriales y mantuvo su actividad como relevante durante Q1 2026.

La victimología tampoco se limita a grandes corporaciones. El modelo de afiliados y la explotación de superficies replicables favorecen organizaciones de diferentes tamaños. La oportunidad puede estar en una credencial válida, un appliance vulnerable, una VPN sin MFA o una relación de confianza; no necesariamente en la importancia pública de la marca.

### 6.1 Synnovis: cuando disponibilidad, datos y seguridad física se cruzan

El incidente de Synnovis es una referencia útil para separar 'ransomware' de 'impacto por ransomware'. NHS England documentó una interrupción severa de servicios de laboratorio, más de 11.000 retrasos o cancelaciones y un proceso de recuperación prolongado. La atribución pública a Qilin fue reportada por Reuters y, posteriormente, autoridades sanitarias indicaron que el incidente contribuyó a la muerte de un paciente.

Para un CISO, este caso cambia la unidad de impacto. El activo crítico no es solamente el servidor cifrado: puede ser la capacidad de procesar una prueba, entregar un resultado, operar una cadena logística, producir alimento, administrar un puerto o sostener un proceso gubernamental. El riesgo técnico se materializa cuando los servicios dependen de identidades, virtualización, datos y recuperación que el atacante puede degradar en conjunto.

> **La severidad de ransomware debe modelarse como pérdida de capacidad de negocio, no como cantidad de endpoints cifrados ni un valor genérico.**

## 7. Chile: presencia demostrable, victimología nominal todavía incompleta

*El hallazgo más importante para Chile no es una lista de nombres. Es que existen señales públicas independientes -incidentes oficiales o cercanos a fuentes oficiales, atribuciones agregadas y claims nominales- que justifican tratar Qilin como una amenaza local operativamente relevante.*

La evidencia más sólida localizada incluye un incidente de efecto significativo reportado en enero de 2026 sobre una entidad estratégica OIV/PSE no identificada (o eso dicen algunas autoridades). La reproducción pública de la alerta AIC26-00002 vinculó tempranamente el incidente con Qilin y describió acceso mediante fuerza bruta contra un firewall WatchGuard sin MFA y sin mecanismos adecuados de lockout o restricciones. La entidad permanece “anónima”.

Existe además información pública atribuida a ANCI según la cual Qilin estuvo detrás de tres de cinco incidentes estatales particularmente costosos durante 2025. La señal es relevante, pero las identidades concretas y los detalles forenses no fueron publicados. Por eso, la conclusión correcta no es 'estas tres instituciones fueron víctimas confirmadas de Qilin', sino 'existe una atribución agregada suficientemente fuerte para elevar el riesgo Qilin en el sector público chileno'.

En paralelo, durante 2026 múltiples organizaciones chilenas aparecieron en trackers que reproducen claims del DLS de Qilin. La investigación registra Valbifrut, Ducasse Comercial, Conectados Chile, Graneles de Chile, NOI Hotels, Comercial Echave Turri, Clínica Maitenes, ATCOM Outsourcing, AGUNSA y Difor, entre otras. En estos casos, la evidencia pública demuestra que hubo un listing atribuido a Qilin; no demuestra por sí sola que la organización sufrió exactamente el acceso, exfiltración, cifrado o volumen de datos que el actor alega.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_8.png' | relative_url }}"
    alt="Ultimas victimas de QILIN en Chile"
    loading="lazy"
  >
  <figcaption>https://www.ransomware.live/country/CHL</figcaption>
</figure>

Esta distinción es especialmente importante al comunicar inteligencia. Etiquetar cada listing como 'víctima confirmada' aumenta artificialmente la certeza, contamina datasets históricos y puede producir conclusiones sectoriales incorrectas. En cambio, mantener estados como Claimed, Reported y Confirmed permite actualizar la evaluación cuando aparece nueva evidencia.

| **Fecha** | **Entidad** | **Sector** | **Estado CTI** | **Confianza** | **Limitación principal** |
| --- | --- | --- | --- | --- | --- |
| 2025 | Tres incidentes estatales no identificados | Gobierno | Reported / atribución agregada | Media-Alta | Declaración atribuida a ANCI; identidades no públicas. |
| 28-29 Ene. 2026 | Entidad estratégica OIV/PSE no identificada | Servicio esencial | Reported / attributed | Media-Alta | Alerta reproducida: WatchGuard, fuerza bruta, controles de autenticación insuficientes. |
| 28 Ene. 2026 | Valbifrut | Agroalimentos / exportación | Claimed | Media en listing; baja en breach | Tracker confirma listing, no intrusión. |
| 12 Feb. 2026 | Ducasse Comercial Ltda. | Industrial / comercial | Claimed | Media | Sin confirmación pública independiente localizada. |
| 12 Feb. 2026 | Conectados Chile S.A. | Tecnología / servicios | Claimed | Media | Listing DLS reproducido por tracker. |
| 19 Feb. 2026 | Graneles de Chile | Industria / alimentos | Claimed | Media | Claim, no confirmación de la organización. |
| 26 Mar. 2026 | NOI Hotels | Hospitality | Claimed | Media | Volumen/contenido de datos proviene de alegación del actor. |
| 2 Jun. 2026 | Clínica Maitenes | Salud | Claimed | Media en listing; baja en contenido | No se localizó confirmación pública independiente. |
| Jun. 2026 | ATCOM Outsourcing | Servicios / tecnología | Claimed / low-verification | Baja | Fuente pública secundaria de menor calidad. |
| 16 Ago. 2026 | AGUNSA | Transporte / logística / marítimo | Claimed | Media-Alta en claim; baja en breach | Listing reciente reproducido por múltiples trackers; sin confirmación independiente al corte. |
| 23 Ago. 2026 | Difor | Automotriz | Claimed | Alta | Listing DLS reproducido por tracker. |

Los incidentes del Instituto de Salud Pública y de la Subsecretaría de Prevención del Delito ilustran otra dificultad metodológica. Ambos fueron incidentes reales y coincidieron temporalmente con comunicaciones sobre Qilin, pero las fuentes revisadas no proporcionan una atribución pública suficientemente sólida para convertir esa coincidencia en un hecho. La investigación los mantiene como incidentes confirmados con atribución Qilin no verificada, en lugar de forzar una narrativa más atractiva pero menos rigurosa.

> **JUICIO SOBRE CHILE**
>
> **Alta confianza en que Qilin ya opera dentro del espacio de amenaza chileno. Confianza media en la victimología nominal pública. La ausencia de confirmación pública de cada organización no reduce la necesidad de actuar sobre el tradecraft que sí está demostrado.**

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_9.png' | relative_url }}"
    alt="Aviso de incidente por parte del ISP en Chile"
    loading="lazy"
  >
  <figcaption>https://www.latercera.com/nacional/noticia/instituto-de-salud-publica-sufre-incidente-de-ciberseguridad-en-sus-servidores/</figcaption>
</figure>

## 8. ¿Qué sectores chilenos deberían prestar más atención?

El riesgo sectorial no debe derivarse solamente de qué nombres aparecen en el DLS. Debe construirse como intersección entre tradecraft probado, exposición arquitectónica y consecuencia de negocio. Una organización puede no haber aparecido nunca en un leak site y, aun así, compartir exactamente las condiciones que Qilin ha explotado en otros entornos.

| **Sector** | **Exposición estimada** | **Superficie crítica** | **Razonamiento** |
| --- | --- | --- | --- |
| Manufactura | Alta | Remote access, AD, file servers, IT/OT dependencies, virtualización | Actividad global sostenida y alta dependencia operacional. |
| Industria salmonera / alimentos / producción | Alta | VPN, plantas remotas, vendors, VMware, ERP, logística | Claims chilenos en agro/industrial + patrón global manufacturing; no se infiere campaña salmonera específica. |
| Salud | Muy alta en impacto | VPN, AD, sistemas clínicos, PII/PHI, virtualización | Synnovis demuestra impacto clínico; existe claim chileno de salud. |
| Gobierno / servicios esenciales | Alta | Legacy remote access, AD compartido, vendors, datos ciudadanos | Atribución agregada 2025 + incidente OIV/PSE 2026. |
| Transporte / logística | Alta | ERP/EDI, vendor VPN, port/logistics systems, VMware | AGUNSA claimed + elevada dependencia de continuidad. |
| Tecnología / MSP | Alta | RMM, cuentas privilegiadas, tooling multi-tenant, VPN | RMM observado en incidentes y potencial de gran blast radius. |
| Energía / minería | Media-Alta | Remote access, contractors, IT/OT bridge, VMware | Exposición industrial compatible; evidencia nominal Chile específica limitada. |
| Finanzas | Media-Alta | Identity, remote access, VDI, data stores, terceros | Financial services aparece en victimología global; evidencia chilena Qilin limitada. |

Para la industria productiva chilena, la concentración de riesgo suele estar en la dependencia entre TI corporativa y operación: VPN de proveedores, Active Directory, sistemas de archivos, ERP, plataformas de virtualización y servicios que sostienen producción o logística. Un atacante no necesita comprometer directamente un PLC para detener una planta si puede cifrar o eliminar la infraestructura de TI que coordina órdenes, calidad, despacho o trazabilidad.

En salud, la consecuencia puede ser aún más directa. La interrupción de sistemas clínicos, laboratorios, identidad o virtualización puede trasladarse a disponibilidad asistencial. En gobierno, la combinación de legacy remote access, múltiples proveedores y datos ciudadanos aumenta tanto la superficie como el costo regulatorio y reputacional. En tecnología/MSP, el riesgo se amplifica por RMM y tooling multi-tenant: una identidad o plataforma con autoridad transversal puede convertirse en un multiplicador de acceso.

La evaluación sectorial, por tanto, no es una predicción de quién será atacado. Es una forma de decidir dónde la misma técnica puede producir una consecuencia mayor.

## 9. Proyección 2026-2027 para Chile: qué es razonable esperar y qué no

La hipótesis más razonable no es una operación exclusivamente orientada a Chile. La evidencia es más consistente con afiliados globales que explotan superficies replicables -credenciales, remote access, appliances vulnerables, RMM y entornos Windows/VMware- y encuentran esas mismas condiciones en organizaciones chilenas.

La concentración de claims durante 2026 en agroindustria, tecnología, industria, hospitality, salud y logística es una señal de actividad sectorialmente diversa. No demuestra una campaña única ni un afiliado común. En un RaaS, asumir que varios listings cercanos temporalmente pertenecen al mismo intruder set sin infraestructura, artefactos o TTPs específicos sería una atribución excesiva.

Remote access probablemente seguirá siendo una superficie prioritaria. En aproximadamente un año, la investigación pública ha relacionado Qilin con infraestructura Fortinet/SSL VPN, WatchGuard en Chile, Palo Alto GlobalProtect y Check Point Remote Access/Mobile Access. Esa diversidad de fabricantes es, en sí misma, una señal: el riesgo no está en una marca concreta, sino en la clase de activo expuesto y en la capacidad del atacante de transformar acceso perimetral en identidad interna.

También es razonable esperar que la evolución ocurra tanto o más en tooling y access de afiliados que en el encryptor. El ecosistema RaaS permite adoptar rápidamente nuevas vulnerabilidades, loaders, RMM y técnicas de defense evasion sin esperar una nueva generación de ransomware. La evidencia 2026 sobre CVE-2026-0257 y el EDR killer refuerza esa lectura. 

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/QILIN_10.png' | relative_url }}"
    alt="Descripcion de CVE usado por operadores de QILIN Ransomware"
    loading="lazy"
  >
  <figcaption>https://arcticwolf.com/resources/blog/exploitation-of-cve-2026-0257-leads-to-qilin-ransomware/</figcaption>
</figure>

Las disrupciones de otros programas RaaS también pueden modificar el volumen de Qilin mediante migración de afiliados. Trend ha evaluado movimientos posteriores a RansomHub y existen precedentes públicos de actores que operaron como afiliados antes de formar nuevas marcas. La confianza aquí es media: la economía de afiliados es opaca y las identidades criminales se solapan, cambian alias o exageran relaciones. 

Un escenario MSP/RMM debe considerarse seriamente por su potencial de blast radius, pero la investigación no encontró evidencia suficiente para afirmar una campaña Qilin de supply chain contra Chile. La formulación correcta es de riesgo e hipótesis: Qilin ha utilizado RMM legítimo y las organizaciones con tooling multi-tenant o accesos de proveedor concentran una autoridad que merece controles JIT/PAM, restricciones de tenant y monitoreo de sesiones. No debe transformarse esa exposición en una campaña atribuida sin evidencia.

## 10. Key Intelligence Judgments

Los siguientes juicios sintetizan la investigación y mantienen explícitamente sus fundamentos. Su objetivo no es producir certeza absoluta, sino permitir decisiones proporcionales a la calidad de la evidencia.

| **Juicio** | **Confianza** | **Fundamento** |
| --- | --- | --- |
| Qilin seguirá siendo una amenaza ransomware de primer nivel durante 2026. | Alta | Dominio DLS, RaaS activo y mejoras técnicas; los rankings pueden cambiar entre grupos. |
| Chile ya forma parte del espacio operativo real de Qilin. | Alta | Incidente OIV/PSE 2026, atribución estatal 2025 y claims nominales; identidades oficiales siguen parcialmente ocultas. |
| Los listings DLS chilenos no deben denominarse víctimas confirmadas. | Alta | Varios trackers marcan explícitamente Claimed; nueva evidencia podría elevar casos concretos. |
| Identity + remote access es la ruta preventiva de mayor retorno para Chile. | Alta | Coincidencia entre Sophos, Group-IB, Arctic Wolf y evidencia chilena; no todos los afiliados usarán la misma ruta. |
| EDR por sí solo es insuficiente frente al tradecraft 2026. | Alta | EDR killer con manipulación kernel y targeting masivo de drivers; requiere privilegios previos del atacante. |
| Compromiso VMware/backup es un riesgo de concentración severo. | Alta | Targeting ESXi/vCenter/Veeam documentado; severidad depende de arquitectura y trust plane. |
| Industria, salud, gobierno, tecnología y logística merecen especial prioridad en Chile. | Media-Alta | Intersección entre victimología global, claims/evidencia Chile y dependencia operacional. |
| La evolución futura probablemente se verá primero en access/tooling de afiliados. | Media-Alta | Adopción rápida de vulnerabilidades, RMM y defense evasion; puede aparecer un nuevo payload. |

## 11. Detection Engineering: detectar la cadena, no esperar al ransomware

*La detección de mayor retorno frente a Qilin ocurre antes de T1486 (encriptación). El objetivo no es reconocer una muestra conocida, sino identificar cuándo una identidad, un host o un plano de administración comienza a comportarse como parte de una cadena adversaria.*

Una estrategia robusta debe combinar señales que, por separado, pueden ser legítimas: un login VPN exitoso, un nltest, una sesión RDP, una modificación de GPO, un PsExec, una transferencia a cloud. El contexto temporal y la relación entre identidades, segmentos y activos convierten esas señales en una hipótesis de ataque.

La investigación prioriza especialmente cinco familias de detección: identidad anómala en acceso remoto; cambios sobre GPO/SYSVOL y credential access en Domain Controllers; fan-out de PsExec/admin shares; degradación de EDR y carga de drivers; y actividad destructiva sobre backups/vCenter. A ellas deben sumarse exfiltración desde servidores de alto valor y uso anómalo de RMM (recursos cpu, red, cloud, etc).

| **Detección** | **Qué buscar** | **Telemetría** | **Prioridad** | **Valor** |
| --- | --- | --- | --- | --- |
| Acceso remoto + identidad | Spray distribuido, éxito desde nuevo ASN/dispositivo/país, login de proveedor fuera de patrón | VPN / IdP / firewall | P0 | Detecta antes del pivot interno. |
| AD / GPO / SYSVOL | Cambios GPO, scripts nuevos en SYSVOL, logons administrativos anómalos, LSASS/NTDS | DC audit / Windows events / EDR | P0 | Qilin ha usado el dominio como mecanismo de recolección y deployment. |
| Lateral movement | RDP este-oeste desde VPN/user network, ADMIN$/C$ fan-out, remote service creation | Windows / NDR / firewall | P0 | Permite cortar propagación antes del cifrado masivo. |
| EDR impairment / BYOVD | Agent heartbeat loss colectivo, service stop, driver load anómalo, DLL side-loading | EDR health + kernel + SIEM + NDR | P0 | La pérdida de visibilidad puede ser el evento de seguridad. |
| Exfiltration | Upload volumétrico desde file/DC/backup server a cloud/file-sharing no baselineado | Proxy / NetFlow / NDR / CASB | P1 | Corta doble extorsión antes de encryption. |
| Backup / vCenter | Cambios de tareas, snapshots, passwords, shutdown de VMs, acceso administrativo nuevo | Veeam / vCenter / hypervisor audit | P0 | Protege recovery y limita concentración de impacto. |
| RMM / túneles | Nueva instalación/tenant, scheduled tasks, Ngrok o herramientas remotas en servidores | EDR / software inventory / network | P1 | Distingue administración autorizada de persistencia adversaria. |

Un principio especialmente importante es la independencia de telemetría. Si el endpoint es un objetivo activo, la organización necesita fuentes que sobrevivan al compromiso del endpoint: firewalls, NDR, IdP, Windows Event Forwarding, SIEM, vCenter, Veeam y registros de appliances. El control de detección no puede depender exclusivamente del mismo sensor que el adversario intenta apagar.

También debe evitarse la sobreingeniería de firmas Qilin. Un hash, una ruta como C:\PerfLogs\win.exe o un driver concreto pueden ser excelentes indicadores contextuales para una campaña observada. No deben convertirse en la única cobertura. **El afiliado puede cambiar filename o tooling manteniendo la misma función adversaria.**

La unidad de hunting útil es la hipótesis. Por ejemplo: 'una identidad obtenida desde remote access progresa rápidamente hacia Tier-0'; 'un actor está transformando GPO/SYSVOL en mecanismo de distribución'; 'la visibilidad de endpoint está siendo degradada antes de fan-out'; 'un servidor de alto valor comienza a transferir datos fuera de su baseline'. Estas hipótesis sobreviven mejor a cambios de malware que una lista de IOCs.

## 12. Control validation: qué debería probar una organización antes del próximo incidente

Qilin también es un buen caso para separar control deployment de control validation (lo profundizo en las entradas de blog anteriores). Tener MFA, EDR, segmentación y backups no demuestra que esos controles cambien el resultado de la cadena observada. **La pregunta madura es qué evidencia existe de que cada control funciona frente al escenario que pretende reducir.**

| **Control** | **Qué validar frente al tradecraft Qilin** | **Prioridad** |
| --- | --- | --- |
| MFA en remote access | Cobertura real de todas las VPNs, cuentas de proveedores, break-glass y rutas legacy; ausencia de bypass. | Crítica |
| VPN hardening | Firmware, servicios expuestos, protocolos obsoletos, config drift y emergency patch SLA. | Crítica |
| Identity analytics | Spray distribuido, new ASN/device, privilege escalation, service-account misuse. | Crítica |
| PAM / JIT | Cuentas Tier-0 no utilizables desde endpoints o pools VPN ordinarios. | Crítica |
| Protección de DC | GPO, SYSVOL, LSASS, NTDS, interactive logon y admin-share monitoring. | Crítica |
| Segmentación | VPN/user VLAN no alcanza libremente DC, backup ni hypervisor management. | Crítica |
| EDR resilience | Reacción a service stop, driver manipulation y pérdida de telemetría. | Crítica |
| Vulnerable-driver controls | Blocklist/WDAC/App Control equivalente según entorno. | Alta |
| Backups | Inmutabilidad, identidad separada, offline copy y restore drills completos. | Crítica |
| VMware / ESXi | MFA/jump host, cuentas separadas cuando sea viable, logging y snapshots protegidos. | Crítica |
| Central logging | VPN/DC/EDR/backup/vCenter conservan evidencia aunque endpoints sean comprometidos. | Crítica |
| Exfiltration monitoring | Transferencias excepcionales desde servidores de valor hacia cloud. | Alta |
| Third-party access | Expiración/JIT, tenant restrictions y trazabilidad de vendor/RMM. | Alta |
| IR / ransomware playbook | Contención simultánea de identity, VPN, DC, backup y ESXi. | Crítica |

### 12.1 Para Red Team y Security Validation

La emulación no necesita desplegar ransomware real para validar las propiedades relevantes. Un ejercicio controlado puede comprobar si una cuenta comprometida desde VPN puede alcanzar segmentos administrativos; si GPO/SYSVOL posee alertas y control de cambios; si credential dumping en un DC genera respuesta; si PsExec o admin-share fan-out es detectable; si una degradación de EDR dispara una escalación; y si las identidades de backup o vCenter están realmente separadas del dominio ordinario.

La salida de valor no es 'se logró Domain Admin'. Es identificar qué control debía interrumpir la cadena, si el control fue observado, por qué falló y cómo se demostrará que el camino permanece cerrado después de la remediación. En Qilin, esto es especialmente importante porque el payload puede cambiar mientras los objetivos operativos -identidad, recovery, virtualización- permanecen.

### 12.2 Para SOC y Blue Team

El SOC debería construir playbooks que correlacionen identity, endpoint y control-plane telemetry. Una alerta sobre carga de driver no debería evaluarse sin conocer si el host perdió heartbeat EDR, si hubo login privilegiado reciente o si existe actividad de PsExec. Del mismo modo, un login VPN válido no debería cerrarse automáticamente como benigno si en los minutos siguientes la identidad ejecuta discovery de dominio y accede a servidores de administración.

La ausencia de telemetría debe tener semántica de seguridad. Un agente que deja de reportar puede ser un problema operacional; veinte agentes que dejan de reportar después de actividad privilegiada pueden ser una fase de ataque. Esa diferencia exige health telemetry centralizada y rutas de escalación explícitas.

### 12.3 Para Infraestructura e IT

La prioridad es reducir blast radius. Domain Controllers, Veeam y vCenter no deberían ser administrables desde los mismos segmentos y con las mismas identidades que los endpoints ordinarios. Las cuentas de backup/hypervisor deben separarse cuando sea viable; el acceso desde VPN hacia RDP/SMB y planos administrativos debe limitarse a rutas justificadas; los appliances sin soporte deben salir del perímetro; y los restore drills deben validar recuperación de servicios completos, no solamente la existencia de copias.

Un control de backup que no puede restaurar bajo presión no es una capacidad de recuperación probada. Del mismo modo, un hypervisor que depende del mismo dominio comprometido para toda administración puede convertir un control de eficiencia operacional en un punto de concentración de riesgo.

### 12.4 Para Risk, GRC y liderazgo

Qilin debería modelarse como un escenario combinado de business interruption + confidentiality breach + third-party risk + regulatory incident. Reducirlo a la categoría 'malware' oculta la interacción entre pérdida de datos, indisponibilidad, crisis ejecutiva y obligaciones regulatorias.

Para sujetos obligados bajo la Ley 21.663, la detección y escalación también forman parte del control. La investigación recuerda que los incidentes con potencial impacto significativo exigen una alerta temprana al CSIRT Nacional en un máximo de tres horas desde que se toma conocimiento, seguida por actualizaciones en los plazos reglamentarios. SOC detection latency, executive escalation y regulatory reporting forman una misma cadena operacional.

La métrica de negocio debe ir más allá de 'porcentaje de backups exitosos'. Debe existir una comprensión de Maximum Tolerable Downtime y Recovery Time para servicios dependientes de AD, virtualización y backup. El impacto de Synnovis muestra por qué una organización necesita traducir pérdida de infraestructura en pérdida de servicio.

## 13. Escenarios de riesgo prioritarios para Chile

Una forma útil de operacionalizar la investigación es convertir tradecraft en escenarios. Estos escenarios no predicen un incidente específico; permiten revisar si arquitectura y controles actuales son capaces de interrumpir rutas plausibles respaldadas por evidencia.

| **Escenario** | **Supuesto** | **Impacto** | **Probabilidad / impacto** | **Controles clave** |
| --- | --- | --- | --- | --- |
| Credenciales filtradas → VPN → AD | MFA ausente/débil y credenciales válidas | Cifrado + robo de datos | Alta / Alto | MFA, identity analytics, VPN segmentation |
| Credential spraying de baja frecuencia | Lockout centrado en IP, intentos distribuidos | Foothold difícil de detectar | Media-Alta / Alto | Detección por usuario/ASN, MFA |
| Exploit de appliance VPN | Vulnerabilidad crítica sin parche inmediato | Pivot interno acelerado | Media-Alta / Muy alto | Exposure mgmt, emergency patching, management isolation |
| AD/GPO compromise | Admin creds accesibles; tiering débil | Compromiso enterprise-wide | Media-Alta / Muy alto | Tier-0 isolation, PAWs, GPO/SYSVOL audit |
| EDR kill + fan-out | SYSTEM/local admin alcanzado | Pérdida de visibilidad + cifrado masivo | Media-Alta / Muy alto | Driver blocking, tamper protection, independent telemetry |
| VMware/backup compromise | vCenter/Veeam en mismo trust plane | Recovery prolongado y múltiples servicios caídos | Media-Alta / Crítico | Identidades separadas, immutable/offline backup, isolated management |
| MSP/RMM abuse | RMM autorizado con autoridad extensa | Blast radius multi-entidad | Media / Muy alto | RMM allowlisting, tenant restrictions, JIT, session recording |
| Exfiltration-first | Acceso sostenido a datos antes de cifrado | Regulatorio/reputacional + extorsión | Alta / Alto-Muy alto | Egress analytics, DLP, data classification |
| Interrupción industrial | Servicios TI sostienen producción/logística | Producción o logística detenida | Media-Alta / Crítico | BCP, IT/OT segmentation, clean-room recovery |

## 14. Lo que todavía no sabemos

Una investigación CTI madura debe terminar también con sus límites. La mayor brecha para Chile es la transparencia de atribución. Existe una señal fuerte de participación de Qilin en incidentes estatales y entidades OIV/PSE, pero las organizaciones afectadas permanecen anónimas o no están vinculadas públicamente de forma inequívoca. Sin incident reports, notas de rescate, hashes, VPN telemetry, EDR timelines o declaraciones directas, esos casos no pueden transformarse responsablemente en una lista nominal de 'confirmed', aunque en el lado oscuro veamos que varios si son confirmados.

Tampoco es posible determinar públicamente qué afiliado o cluster estuvo detrás de Valbifrut, Ducasse, Conectados, Graneles, NOI, Clínica Maitenes o AGUNSA. Un DLS común no implica un intrusion set común. Precisamente, el modelo RaaS desacopla la marca del ransomware respecto del operador de la intrusión.

La relación Moonstone Sleet-Qilin requiere la misma prudencia. La evidencia pública sustenta uso o asociación limitada, no que Qilin sea controlado por un actor norcoreano ni que sus afiliados habituales sean state-sponsored.

Las cifras de 2025-2026 tampoco pueden compararse estrictamente entre vendors. Para un programa de Intelligence Engineering, cada dataset debería conservar source_dataset, collection_date, listing_date, status y reglas de deduplicación. Colapsar todos los trackers en un contador único elimina contexto y puede fabricar tendencias.

Finalmente, falta un denominador local sobre exposición: prevalencia de VPN sin MFA, appliances legacy, Veeam/vCenter accesibles desde AD, concentración de RMM, credenciales de infostealers o control de drivers vulnerables en organizaciones chilenas. Sin esos datos no es posible calcular una probabilidad nacional cuantitativa seria. Sí es posible, en cambio, identificar las superficies de mayor retorno defensivo.

## 15. Conclusión: Chile no necesita esperar una víctima confirmada para actuar

*La lectura más útil de Qilin en 2026 no es la de un malware específico, sino la de un sistema criminal distribuido que convierte accesos distintos en una cadena recurrente hacia identidad, control administrativo, datos y capacidad de recuperación.*

Qilin ha evolucionado desde el linaje Agenda observado en 2022 hacia una operación RaaS con soporte Windows/Linux/ESXi, afiliados heterogéneos, doble extorsión y una defensa evasiva notablemente más sofisticada. Pero su fortaleza operacional no está solamente en el código. Está en la capacidad de explotar credenciales, appliances, Active Directory, herramientas legítimas, RMM, backups y virtualización como partes de un mismo sistema de ataque.

Para Chile, la evidencia disponible permite afirmar con alta confianza que la amenaza es real y relevante. Existe un incidente estratégico atribuido tempranamente, información agregada sobre incidentes estatales y una secuencia creciente de claims nominales en sectores diversos. Lo que no existe públicamente es evidencia suficiente para llamar 'víctima confirmada' a cada organización publicada en el DLS. Mantener esa diferencia no debilita el análisis; lo hace más útil.

La implicación defensiva es directa: el objetivo no debería ser detectar 'Qilin.exe'. Debe ser romper la cadena antes de que el ransomware llegue. Remote access, identity, Tier-0, GPO/SYSVOL, lateral movement, EDR resilience, exfiltration, backup y VMware son los puntos donde una organización todavía puede cambiar el resultado.

También es una lección de arquitectura. Un EDR puede ser neutralizado; un backup puede existir y aun así compartir el mismo trust plane; un vCenter puede concentrar la disponibilidad de decenas de servicios; una VPN puede estar parchada y seguir siendo riesgosa si la identidad está débil; un DLS puede ser útil y, al mismo tiempo, insuficiente para confirmar victimología.

> **Qilin debe tratarse en Chile como un escenario de identity compromise y control-plane compromise que termina en ransomware. La fase de cifrado es el impacto visible; la capacidad de prevenirlo se decide mucho antes.**

La pregunta para un CISO no es si Qilin aparecerá con el mismo hash, la misma herramienta o el mismo afiliado. Es si, cuando un actor encuentre una credencial válida, un appliance vulnerable o una integración remota, la arquitectura actual podrá impedir que ese acceso se transforme en autoridad sobre Active Directory, backups, virtualización y datos.

Ahí está la diferencia entre conocer una familia de ransomware y entender la amenaza como sistema.
