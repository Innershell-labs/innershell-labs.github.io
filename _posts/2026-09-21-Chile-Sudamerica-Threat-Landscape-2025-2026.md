---
layout: default
title: "Chile / Sudamerica Threat Landscape 2025–2026"
lang: es
---

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/1.png' | relative_url }}"
    alt="Imagen 1"
    loading="lazy"
  >
  <figcaption><a href="https://g5noticias.cl/2026/09/14/estudio-fue-realizado-en-17-paises-el-precio-de-volver-a-operar-tras-un-ataque-de-ransomware-en-chile-supera-el-millon-de-dolares/" target="_blank" rel="noopener noreferrer">https://g5noticias.cl/2026/09/14/estudio-fue-realizado-en-17-paises-el-precio-de-volver-a-operar-tras-un-ataque-de-ransomware-en-chile-supera-el-millon-de-dolares/</a></figcaption>
</figure>

## Executive Assessment

Entre 2025 y 2026 el ransomware en Sudamérica no disminuyó de forma estructural: cambió de forma. 2025 estuvo marcado por disrupciones, cierres de marcas históricas y una fragmentación sin precedentes del ecosistema Ransomware-as-a-Service. Los afiliados, sin embargo, no desaparecieron junto con las marcas. Se redistribuyeron, migraron hacia operaciones más estables o levantaron nuevos leak sites. Qilin fue uno de los grandes beneficiarios de ese proceso. En 2026 el mercado volvió a concentrarse parcialmente alrededor de operadores capaces de ofrecer infraestructura, negociación, tooling y reputación, al mismo tiempo que siguió creciendo el número total de grupos activos. [S01][S02][S03][S04][S05]

Para Sudamérica, el dato más consistente sigue siendo que Brasil concentra el mayor volumen observable de actividad ransomware y cibercrimen financiero, seguido a distancia por Argentina y Colombia. Chile no aparece como el país con mayor cantidad absoluta de víctimas públicas, pero 2026 muestra una aceleración clara de la visibilidad local: mayor densidad de claims, actores distintos operando contra organizaciones chilenas, incidentes confirmados por entidades afectadas, filtraciones corroboradas por terceros y un sistema nacional de reporte que está haciendo visible una porción que anteriormente permanecía fuera del espacio público. [S01][S06][S11][S16]

La tesis central de este reporte es que el evento ransomware comienza antes del ransomware. En la región, credenciales robadas por infostealers (como ENTEL en Chile reiteradas veces Telefonica), phishing, compromisos de identidad, accesos VPN, appliances expuestos, Initial Access Brokers y tooling legítimo de administración remota forman una economía de acceso que abastece a afiliados capaces de convertir una cuenta válida o una vulnerabilidad perimetral en control sobre Active Directory, backups, virtualización, datos y servicios críticos. Microsoft observó 5.606 dispositivos chilenos afectados por Lumma Stealer entre marzo y mayo de 2025 (y eso solo con Lumma, porque hay muchos mas en el ecosistema), CrowdStrike recuperó más de mil millones de credenciales relacionadas con usuarios y organizaciones LATAM en stealer logs y filtraciones, y ANCI reportó en 2026 casos de acceso no autorizado mediante credenciales válidas probablemente provenientes de filtraciones anteriores o infostealers. [S09][S10][S13]

Para una gerencia, la consecuencia es directa: el riesgo no debería modelarse como “probabilidad de que aparezca Qilin.exe”, sino como pérdida de capacidad de negocio ante un compromiso de identidad que alcanza los planos de control. Para un SOC, Red Team o equipo de Threat Intelligence, la unidad de análisis es la cadena completa: acceso inicial → identidad → privilegios → discovery → lateral movement → degradación de defensas → exfiltración → backup/virtualización → extorsión y/o cifrado. En sectores de baja tolerancia al downtime -manufactura, minería, alimentos, logística, salud, gobierno y servicios financieros- esa cadena puede producir impacto operacional mucho antes de que aparezca una nota de rescate.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/2.png' | relative_url }}"
    alt="Imagen 2"
    loading="lazy"
  >
  <figcaption><a href="https://www.infostealers.com/article/telefonica-breach-infostealer-malware-opens-door-for-social-engineering-tactics/" target="_blank" rel="noopener noreferrer">https://www.infostealers.com/article/telefonica-breach-infostealer-malware-opens-door-for-social-engineering-tactics/</a></figcaption>
</figure>

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/3.webp' | relative_url }}"
    alt="Imagen 3"
    loading="lazy"
  >
  <figcaption><a href="https://www.24horas.cl/actualidad/nacional/pdi-investiga-posible-espionaje-a-entel-movistar-telmex-hackeo" target="_blank" rel="noopener noreferrer">https://www.24horas.cl/actualidad/nacional/pdi-investiga-posible-espionaje-a-entel-movistar-telmex-hackeo</a></figcaption>
</figure>

### Key Intelligence Judgments

| **Juicio** | **Confianza** | **Fundamento** |
| --- | --- | --- |
| La presión ransomware sobre Sudamérica seguirá elevada durante los próximos 6–12 meses. | Alta | Volumen global históricamente alto, resiliencia del modelo de afiliados y continuidad de Qilin, The Gentlemen, Akira, LockBit 5.0 y otros operadores. |
| 2025 fue un año de fragmentación, 2026 combina reconcentración alrededor de marcas fuertes con expansión del número de grupos activos. | Alta | Q3 2025 llegó a 85 grupos activos, Q1 2026 bajó a 71 con top-10 en 71%, y Q2 volvió a 93 grupos. |
| Brasil seguirá siendo el principal centro sudamericano por volumen y diversidad de cibercrimen. | Alta | Lidera datasets de ransomware regionales y concentra además fraude financiero, banking malware e infraestructura criminal propia. |
| Chile muestra en 2026 mayor presión observable que en 2025, sin que eso implique ser el país más atacado de Sudamérica. | Alta | Mayor densidad de listings, incidentes públicos, filtraciones corroboradas y mejor institucionalidad de reporte. |
| Qilin es especialmente relevante para Chile, pero The Gentlemen y otros actores impiden reducir el riesgo a una sola marca. | Alta | Qilin aparece repetidamente en 2026, The Gentlemen muestra varios objetivos chilenos desde febrero y crece globalmente. |
| Identity + remote access seguirá siendo la superficie preventiva de mayor retorno. | Alta | Convergencia de incidentes públicos, infostealers, valid accounts, VPN, edge exploitation y tradecraft de los principales RaaS. |
| Infostealers y credenciales filtradas seguirán alimentando accesos corporativos. | Alta | Telemetría Microsoft, CrowdStrike y ANCI converge en el rol de credenciales válidas y stealer logs. |
| AD, backup, vCenter/ESXi y otros control planes seguirán concentrando el impacto. | Alta | Qilin, Akira y otros actores muestran targeting de virtualización, backups y administración privilegiada. |
| La evasión de EDR mediante BYOVD y EDR killers seguirá normalizándose. | Media-Alta | ESET documenta más de 100 EDR killers en uso, Qilin y otros grupos integran estas capacidades. |
| La IA reducirá el costo y tiempo de desarrollo y operación criminal, pero no reemplazará en el corto plazo al afiliado humano. | Media-Alta | The Gentlemen utilizó asistentes de código para acelerar su panel, la evidencia disponible muestra augmentation más que autonomía generalizada. |

> **LECTURA EJECUTIVA**  
> **El ransomware no es una “categoría de malware” aislada. Es una forma de monetización que se apoya en la misma superficie que sostiene fraude, robo de credenciales, espionaje, exfiltración y abuso de terceros. Si el control de identidad, remote access, Active Directory, backup y virtualización es débil, cambiar de EDR o comprar otra herramienta no corrige la clase de riesgo.**

## 1. Metodología: qué significa realmente una “víctima”

La primera dificultad de cualquier threat landscape es metodológica. Un Data Leak Site no es una base de datos forense y un tracker no es un CSIRT. Los actores criminales publican víctimas como mecanismo de presión, los trackers agregan esas publicaciones, los vendors mezclan fuentes propias con DLS, las organizaciones afectadas pueden confirmar el incidente, negarlo o simplemente no hablar (la mayoría en Chile y latam). Si esas categorías se mezclan, el análisis puede producir cifras aparentemente exactas que en realidad comparan cosas distintas.

Desde mi experiencia operativa en CTI, existe también un error inverso: tratar todo claim como si fuera ruido hasta que exista un comunicado corporativo. Esa posición tampoco refleja cómo funciona la inteligencia. **Una proporción importante de los listings de operaciones maduras termina correspondiendo a compromisos reales, aunque la víctima no publique detalles o confirme únicamente “un incidente de ciberseguridad”. Al mismo tiempo, existen duplicados, accesos parciales, materiales reciclados, falsas atribuciones y grupos que inflan su reputación. El valor analítico está precisamente en distinguir esos estados.**

| **Estado** | **Definición operativa** | **Qué permite afirmar** |
| --- | --- | --- |
| CONFIRMADO | La organización afectada, una autoridad, un CSIRT/CERT, evidencia forense directa o varias fuentes independientes robustas confirman el incidente. | Que el incidente ocurrió, la atribución al actor puede seguir teniendo un nivel de confianza distinto. |
| CORROBORADO | Existe claim y evidencia independiente consistente: interrupción visible, muestras de datos, documentos publicados, comunicaciones relacionadas o investigación periodística que inspeccionó el material. | Que existe evidencia real adicional al claim, no necesariamente confirma cifrado, vector inicial o alcance completo. |
| CLAIMED / REIVINDICADO | El actor publica a la organización en su DLS o un tracker reproduce ese listing. | Que el actor hizo la afirmación, no prueba por sí solo acceso, cifrado, volumen de datos o impacto. |
| DISPUTED / FALSO POSITIVO | Existe evidencia razonable de duplicación, material reciclado, error de identificación, acceso inexistente o negación respaldada por evidencia. | Que el listing no debe incorporarse como víctima sin advertencias o puede excluirse del dataset. |

El segundo eje es la confianza. Un caso puede tener alta confianza respecto de la existencia del listing y media respecto de la intrusión. Puede tener alta confianza respecto de una filtración y baja respecto del supuesto cifrado. En este documento, “alta confianza” significa que existen fuentes primarias o múltiples fuentes independientes consistentes, “media” significa evidencia fuerte pero incompleta, “baja” se reserva para claims o información secundaria sin corroboración suficiente.

También se separan métricas incompatibles. Recorded Future reporta víctimas públicamente conocidas en blogs de ransomware, Check Point mide DLS postings, ESET combina fuentes públicas como ransomware.live con telemetría propia, Kaspersky publica intentos bloqueados en endpoints, Microsoft reporta dispositivos afectados por familias concretas. Ninguna de esas métricas debe sumarse como si fueran “ataques”. Una detección no equivale a una víctima, una víctima en DLS no equivale a un cifrado confirmado, un incidente confirmado no necesariamente tiene atribución pública.

## 2. 2025: fragmentación, disrupción y redistribución de afiliados

2025 es el punto de partida porque explica la composición del mercado de 2026. Las disrupciones contra marcas grandes no eliminaron el ecosistema, alteraron su distribución. RansomHub dejó de operar en abril de 2025 y otras marcas relevantes redujeron o detuvieron publicaciones. En Q2, Check Point observó la desaparición o inactividad de RansomHub, BianLian, 8Base, Cactus, Hunters International y otras operaciones. El resultado no fue una caída estructural de la capacidad ofensiva, sino un mercado con más actores medianos y afiliados “huérfanos” buscando nueva infraestructura. [S02]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/4.png' | relative_url }}"
    alt="Imagen 4"
    loading="lazy"
  >
  <figcaption><a href="https://thehackernews.com/2025/04/ransomhub-went-dark-april-1-affiliates.html" target="_blank" rel="noopener noreferrer">https://thehackernews.com/2025/04/ransomhub-went-dark-april-1-affiliates.html</a></figcaption>
</figure>

Qilin aprovechó ese vacío. Check Point estimó que pasó de aproximadamente 35 víctimas mensuales en Q1 2025 a casi 70 en Q2. En Q3, el número de grupos activos alcanzó 85 -máximo observado en ese momento- y los diez principales representaron apenas 56% de las publicaciones. Qilin promedió alrededor de 75 víctimas mensuales y se transformó en el principal hub de RaaS del período. [S02][S03]

El dato más importante no es que una marca haya reemplazado a otra. Es la movilidad del afiliado. La infraestructura RaaS -paneles, encryptors, negociación, leak site, soporte- puede caer, pero los actores que obtienen accesos, roban credenciales, despliegan herramientas y realizan movimiento lateral conservan experiencia, contactos e inventario de accesos. La presión policial sobre administradores e infraestructura produce fricción y costos, pero no equivale automáticamente a sacar del mercado a los operadores de intrusión.

Recorded Future registró 452 incidentes/víctimas de ransomware en LAC (latam y caribe) durante 2025, poco más del 6% del total global de 7.346 publicaciones observadas. Los cinco países regionales con mayor volumen fueron Brasil (128), México (78), Argentina (63), Colombia (51) y Perú (27). Si se restringe la mirada a Sudamérica, Brasil fue claramente el principal mercado observable, seguido por Argentina, Colombia y Perú. [S01]

| **País / región** | **2025: métrica pública** | **Lectura** |
| --- | --- | --- |
| Brasil | 128 publicaciones en Recorded Future (130 en su evaluación de riesgo) | Mayor volumen regional, además concentra banking malware, fraude y ecosistemas criminales locales. |
| Argentina | 63 | Segundo mercado sudamericano del dataset 2025, exposición financiera, gubernamental y empresarial. |
| Colombia | 51 | Volumen alto y creciente interés en finanzas, gobierno y servicios. |
| Perú | 27 | Volumen menor que Brasil/Argentina/Colombia, pero actividad persistente y exposición corporativa. |
| Chile | No entra en top-5 regional de Recorded Future | Menor volumen absoluto en ese dataset, la falta de ranking no implica baja exposición ni ausencia de incidentes. |
| LAC total | 452 de 7.346 globales | Algo más de 6% de las publicaciones globales de 2025. |

Los sectores más afectados en LAC durante 2025 fueron manufactura (49), salud (36), gobierno (28), tecnología de la información (21) y educación (20). Qilin fue el grupo con mayor número de ataques/publicaciones regionales en el dataset de Recorded Future, con 54, le siguieron LockBit (29), SafePay (27), The Gentlemen (22) y Kazu (21). [S01]

> **JUICIO ANALÍTICO**  
> **2025 no fue el año en que el ransomware “se debilitó”. Fue el año en que la infraestructura criminal se volvió más fungible. La marca puede desaparecer, el afiliado, la credencial robada, el acceso vendido y el conocimiento operacional sobreviven.**

## 3. 2026: consolidación parcial a escala históricamente alta

Q1 2026 mostró el movimiento inverso. Check Point monitoreó más de 70 leak sites y registró 2.122 nuevas víctimas publicadas. Los diez principales grupos volvieron a concentrar 71% de los listings y Qilin lideró por tercer trimestre consecutivo con 338. The Gentlemen saltó a 166 desde 40 en Q4 2025, LockBit 5.0 alcanzó 163. La fragmentación de 2025 había producido demasiadas marcas pequeñas, el mercado comenzó a reconcentrarse alrededor de operadores capaces de atraer afiliados y sostener una infraestructura confiable. [S04]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/5.avif' | relative_url }}"
    alt="Imagen 5"
    loading="lazy"
  >
  <figcaption><a href="https://www.zerofox.com/intelligence/flash-report-qilin-claims-record-number-of-monthly-attacks-for-2026/" target="_blank" rel="noopener noreferrer">https://www.zerofox.com/intelligence/flash-report-qilin-claims-record-number-of-monthly-attacks-for-2026/</a></figcaption>
</figure>

Q2 2026 añadió una aparente contradicción que en realidad describe muy bien el ecosistema: el volumen se mantuvo estable en 2.139 publicaciones, pero el número de grupos activos subió hasta 93. Qilin mantuvo el primer lugar trimestral con 279, The Gentlemen llegó a 269 y lo superó durante junio. El ransomware se reconcentra por volumen y simultáneamente se fragmenta por número de marcas: existen hubs dominantes y una larga cola de grupos con vida corta. [S05]

ESET, utilizando datos de ransomware.live, contabilizó 4.699 registros durante H1 2026, 16,5% más que en H1 2025. Qilin (722), The Gentlemen (cerca de 550) y Akira (más de 300) representaron 33,5% del total, DragonForce se acercó a 300. Para Latinoamérica, Brasil superó las 100 víctimas en H1, Argentina llegó a 39 y Colombia a 33, México, utilizado aquí solo como comparador LAC, se acercó a 80. ESET reportó además que Qilin fue la familia con más detecciones en Chile, con un peak de 19 en enero. [S06]

Conviene detenerse en la palabra “confirmados” utilizada por algunos reportes. Cuando el dataset de origen es ransomware.live, el registro confirma que la víctima fue publicada o recolectada por el tracker, no necesariamente que la organización haya emitido un comunicado o que exista una imagen forense del cifrado. En este landscape se conserva esa diferencia para evitar convertir el volumen del DLS en un censo de intrusiones.

| **Dimensión** | **2025** | **2026 hasta septiembre** | **Lectura** |
| --- | --- | --- | --- |
| Estructura RaaS | Fragmentación récord, 85 grupos activos en Q3 | Reconcentración Q1, nueva expansión a 93 grupos en Q2 | Hubs dominantes + larga cola de marcas pequeñas. |
| Actor dominante | Qilin crece tras caída de RansomHub | Qilin sigue primero, The Gentlemen se acerca y lidera junio | Competencia por afiliados y access stockpiles. |
| Extorsión | Mayor peso de data theft y pressure tactics | Data theft, regulatory pressure y cifrado selectivo se normalizan | “Ransomware” describe solo parte de la operación. |
| Control defensivo | BYOVD/EDR kill en crecimiento | EDR killers más numerosos y especializados | El sensor defensivo es un objetivo activo. |
| Virtualización/backup | ESXi/Veeam ya relevantes | Control plane y recovery siguen en el centro del impacto | Aumenta blast radius por concentración de servicios. |
| Chile | Actividad sostenida pero menor volumen público | Mayor densidad de claims, incidentes y filtraciones corroboradas | Se eleva la presión observable, también mejora el reporting. |

## 4. Chile: por qué 2026 se siente distinto

Chile no pasó súbitamente a liderar Sudamérica por número absoluto de víctimas. La evidencia disponible no sostiene esa conclusión. Lo que sí cambió es la combinación de volumen visible, diversidad de actores, criticidad de algunas organizaciones afectadas y madurez institucional para reportar. Es decir, 2026 se siente distinto porque hay más actividad observable y porque una porción mayor de esa actividad está dejando trazas públicas.

ANCI cerró 2025 con 3.258 instituciones inscritas en su portal de reporte y más de 400 reportes de incidentes. En la primera etapa se calificaron 915 Operadores de Importancia Vital, en julio de 2026 la segunda etapa elevó el total a 1.154 OIV. Eso cambia el entorno de observabilidad: incidentes que antes podían quedar confinados a la organización, proveedor o aseguradora ahora tienen deberes de reporte, coordinación y continuidad más explícitos. [S11][S12]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/6.png' | relative_url }}"
    alt="Imagen 6"
    loading="lazy"
  >
  <figcaption><a href="https://www.diariooficial.interior.gob.cl/publicaciones/2026/07/24/44507/01/2842835.pdf" target="_blank" rel="noopener noreferrer">https://www.diariooficial.interior.gob.cl/publicaciones/2026/07/24/44507/01/2842835.pdf</a></figcaption>
</figure>

En un seminario de AmCham realizado en 2026, se atribuyeron a ANCI datos según los cuales 161 de los 410 reportes recibidos en 2025 correspondieron a incidentes de efecto significativo y más de 60% de esos casos graves comenzaron con contraseñas robadas o vulnerabilidades expuestas. La misma presentación señaló que Qilin habría estado detrás de tres de cinco incidentes que costaron al Estado cerca de $850 millones en recuperación durante 2025. Al tratarse de una atribución agregada difundida por un tercero y no de incident reports públicos con identidades y artefactos, este documento la utiliza como señal de riesgo, no como base para identificar nominalmente a tres instituciones. [S27]

La consecuencia metodológica es importante: un crecimiento de incidentes visibles en Chile durante 2026 puede reflejar simultáneamente más actividad adversaria, mayor cobertura de leak sites, mejor seguimiento por parte de la comunidad CTI y una capacidad institucional superior para detectar y reportar. En lugar de elegir una sola explicación, el análisis debe conservar las cuatro.

## 5. Panorama chileno 2025–2026: una línea de tiempo seleccionada

Ransomware.live/ransomwatch mantiene a la fecha del corte decenas de registros históricos asociados a Chile y muestra una concentración especialmente visible durante 2026. El número bruto del tracker no debe interpretarse como incidentes confirmados: incluye claims, casos con prensa, posibles duplicados y registros históricos. La utilidad está en observar actores, secuencia temporal y sectores. [S16]

| **Fecha** | **Entidad / evento** | **Actor / estado** | **Lectura CTI** |
| --- | --- | --- | --- |
| Ene. 2025 | Garces Fruit | Akira – claimed | Sector agroexportador, continuidad con interés ransomware en producción y alimentos. |
| Feb.–Jun. 2025 | Emin, CMSG, Megacentro, Emotrans, Univ. de Chile, Petroquim | Akira, RansomHub, Hunters, NightSpire, Lynx – claimed | Diversidad de actores y sectores, no existe un único “ransomware de Chile”. |
| Sep.–Dic. 2025 | Nubox/SumaSaaS, Liceo Francés, OfficePro, Pangea, Clínica Dávila | AlphaLocker, The Gentlemen, Qilin, Devman – mezcla de claims | The Gentlemen aparece ya en 2025, Qilin gana presencia y Devman expone riesgo sanitario. |
| 28 Ene. 2026 | Entidad estratégica OIV/PSE no identificada | Qilin – reported/attributed | Alerta AIC26-00002: brute force contra WatchGuard, ausencia de MFA/lockout adecuados. [S14] |
| Ene.–Feb. 2026 | Valbifrut, INDH, Pucobre, Ducasse, Conectados, Graneles, ISESA y otros | Qilin / The Gentlemen / INC / LockBit – mostly claimed | Cluster inicial del año en agro, gobierno, minería, comercio y tecnología. |
| Mar.–Abr. 2026 | NOI Hotels, Corporación Colina, SAAM Towage, Frutícola Olmué | Qilin / The Gentlemen – claims, SAAM leak corroborado por prensa | Mayor visibilidad en hospitality, público/local, transporte y producción. |
| Jun. 2026 | Clínica Maitenes | Incidente confirmado por la clínica, Qilin claim separado | Afectó un sistema de respaldo, organización informó a ANCI y mantuvo continuidad. [S15] |
| Jul.–Ago. 2026 | Las Cenizas, CONTAC, AGUNSA, ESPAC, Layher, Difor, Incolur | The Gentlemen / Qilin – claimed | Sector productivo, minero, transporte, construcción y tecnología. |
| 30 Ago. 2026 | Hospital Clínico Universidad de Chile | DireWolf – claimed | Claim de alto impacto potencial en salud, sin confirmación independiente suficiente al corte. [S28] |
| 2–4 Sep. 2026 | Tanner | Qilin – claim + filtración corroborada por prensa | Qilin publica a Tanner, Interferencia accede a archivos internos filtrados y describe contenido específico. [S17] |
| 7 Sep. 2026 | S&A Chile | The Gentlemen – claimed | Proveedor/integrador TI: recordatorio del blast radius potencial en terceros y MSP. |

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/7.png' | relative_url }}"
    alt="Imagen 7"
    loading="lazy"
  >
  <figcaption><a href="https://socradar.io/free-tools/ransomware-intelligence/countries/chile" target="_blank" rel="noopener noreferrer">https://socradar.io/free-tools/ransomware-intelligence/countries/chile</a></figcaption>
</figure>

## 6. Tanner: cuando un claim deja de ser solamente un claim

Tanner es un caso especialmente útil para explicar por qué una taxonomía binaria “confirmado/no confirmado” puede quedarse corta. Qilin publicó a la financiera chilena a comienzos de septiembre de 2026. En ese momento, el hecho verificable era el listing: un actor conocido de ransomware/extorsión afirmaba haber comprometido a Tanner. Algunos trackers, correctamente, lo mantuvieron como un claim no verificado. Hoy en día cualquiera con un pequeño conocimiento en CTI y curiosidad puede llegar a los documentos filtrados de este caso.[S16]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/8.png' | relative_url }}"
    alt="Imagen 8"
    loading="lazy"
  >
  <figcaption><a href="https://www.ransomware.live/id/VGFubmVyQHFpbGlu" target="_blank" rel="noopener noreferrer">https://www.ransomware.live/id/VGFubmVyQHFpbGlu</a></figcaption>
</figure>

El 17 de septiembre, Interferencia publicó una investigación basada en archivos internos filtrados por Qilin a los que el medio tuvo acceso. El reportaje describe expedientes de cobranza, estudios de títulos, actas societarias, certificados de dominio y gravámenes, documentación legal interna y carpetas vinculadas a clientes y operaciones concretas. El medio no se limitó a repetir el claim del leak site: inspeccionó material, describió documentos y contrastó parte de su contenido con registros públicos y antecedentes judiciales. [S17]

Eso cambia el estado analítico. A partir de esa publicación, la existencia de una filtración de información interna deja de depender únicamente de la palabra del actor. Para este landscape, Tanner pasa a **CORROBORADO** en compromiso/exfiltración/publicación de información, con alta confianza de que Qilin operó la extorsión y publicó los datos. Lo que todavía no está demostrado públicamente es el vector de acceso, si hubo cifrado de sistemas productivos, el dwell time, el alcance exacto de la intrusión, el monto de la extorsión o el proceso de recuperación. Decir “no está confirmado” a secas sería demasiado pasivo, decir “sabemos exactamente cómo ocurrió el ransomware” sería excesivo. CTI útil vive entre esos extremos.

> **POR QUÉ TANNER IMPORTA**  
> **El caso demuestra que un DLS es el comienzo de la evaluación, no el final. Un claim puede evolucionar hacia corroboración cuando aparecen datos reales, evidencia operacional o investigación independiente. La disciplina consiste en actualizar el nivel de confianza sin rellenar los huecos técnicos que todavía no conocemos.**

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/9.png' | relative_url }}"
    alt="Imagen 9"
    loading="lazy"
  >
  <figcaption><a href="https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup" target="_blank" rel="noopener noreferrer">https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup</a></figcaption>
</figure>

Desde el punto de vista gerencial, el impacto tampoco se limita a “archivos robados”. Una institución financiera administra información legal, crediticia, patrimonial y relacional capaz de alimentar fraude, ingeniería social, extorsión secundaria y campañas dirigidas contra clientes o terceros. La publicación de documentos internos convierte un incidente técnico en riesgo reputacional, de privacidad, regulatorio y de negocio. El dato exfiltrado adquiere una segunda vida una vez que sale del perímetro: puede ser consultado, revendido, correlacionado y reutilizado por otros actores.

Desde el punto de vista técnico, Tanner también obliga a evitar una inferencia cómoda: que todo caso Qilin en Chile necesariamente siguió el mismo vector visto en el incidente OIV/PSE o en investigaciones globales. La marca ransomware no identifica al afiliado ni demuestra que se reutilizó una misma vulnerabilidad. Hasta que existan logs, artefactos, nota de rescate, telemetría EDR o disclosure técnico, el initial access debe mantenerse como un intelligence gap.

## 7. Otros casos chilenos que ayudan a entender el riesgo

### 7.1 Entidad OIV/PSE: acceso remoto, autenticación y una alerta nacional

La alerta AIC26-00002, reproducida públicamente desde el CSIRT Nacional, describió a fines de enero un incidente de efecto significativo en una entidad estratégica OIV/PSE (varios ya saben de quien hablamos) y señaló tempranamente a Qilin. El acceso habría comenzado mediante fuerza bruta contra un firewall WatchGuard en un entorno sin MFA ni mecanismos adecuados de bloqueo o restricciones regionales. [S14]

El dato más útil no es la marca del firewall. Es la clase de riesgo: un servicio remoto expuesto, autenticación insuficiente y una ruta posterior hacia activos internos. Cambiar de fabricante sin corregir MFA, lifecycle, lockout, risk-based authentication, management exposure y segmentación mantiene la misma superficie lógica.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/10.png' | relative_url }}"
    alt="Imagen 10"
    loading="lazy"
  >
  <figcaption><a href="https://x.com/ANCIChile/status/2016609735160496194" target="_blank" rel="noopener noreferrer">https://x.com/ANCIChile/status/2016609735160496194</a></figcaption>
</figure>

### 7.2 Clínica Maitenes: incidente confirmado, atribución separada

El 13 de junio de 2026 Clínica Maitenes confirmó públicamente que detectó un incidente de ciberseguridad que afectó uno de sus sistemas de respaldo, activó contención, informó a ANCI e inició investigación interna. La clínica señaló que la atención a pacientes no fue interrumpida. Por separado, Qilin había publicado a la organización el 2 de junio. [S15]

Aquí existen dos hechos sólidos y una relación que debe manejarse con cuidado: el incidente está confirmado, el listing de Qilin está confirmado, el comunicado de la clínica no atribuye públicamente el incidente a Qilin. Es un ejemplo perfecto de cómo separar “existencia del incidente” de “atribución”. También es un recordatorio de que backup no es solamente una medida de recuperación: es un objetivo directo y un plano privilegiado dentro del ataque.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/11.png' | relative_url }}"
    alt="Imagen 11"
    loading="lazy"
  >
  <figcaption><a href="https://www.ransomware.live/id/Q2xpbmljYSBNYWl0ZW5lc0BxaWxpbg" target="_blank" rel="noopener noreferrer">https://www.ransomware.live/id/Q2xpbmljYSBNYWl0ZW5lc0BxaWxpbg</a></figcaption>
</figure>

### 7.3 SAAM Towage: transporte, contratos y sensibilidad operacional

SAAM Towage fue publicada por Qilin en abril y, posteriormente, prensa chilena reportó haber accedido a miles de documentos privados filtrados, incluyendo contratos, nóminas, remuneraciones y protocolos operacionales. Aunque el disclosure técnico del incidente sigue siendo limitado, el caso vuelve a mostrar el valor de separar claim, corroboración de datos y detalles forenses. [S29]

En transporte y logística, la información robada no solo tiene valor por privacidad. Contratos, protocolos, proveedores, rutas y relaciones comerciales pueden convertirse en inteligencia útil para fraude, ingeniería social, presión reputacional o ataques posteriores. Para un actor de extorsión, el valor del dataset es parte del arma.

## 8. Los actores que están definiendo 2026

### 8.1 Qilin: el hub de afiliados que sobrevivió a la fragmentación

Qilin no debe entenderse como un grupo homogéneo que ejecuta exactamente la misma intrusión cada vez. MITRE lo registra como ransomware/RaaS con variantes Go y Rust para Windows, Linux y VMware ESXi, y separa a Water Galura / GOLD FEATHER como operador del servicio. Los afiliados son quienes pueden decidir cómo obtener acceso, qué tooling utilizar y cuánto tiempo permanecer. [S24]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/12.jpg' | relative_url }}"
    alt="Imagen 12"
    loading="lazy"
  >
  <figcaption><a href="https://es.vectra.ai/modern-attack/threat-actors/qilin" target="_blank" rel="noopener noreferrer">https://es.vectra.ai/modern-attack/threat-actors/qilin</a></figcaption>
</figure>

Su importancia regional se explica por tres factores: escala, capacidad de absorber afiliados desplazados y amplitud de impacto. Qilin puede aparecer detrás de organizaciones productivas, financieras, salud, logística y tecnología, y ha mantenido actividad sostenida aun cuando componentes concretos de su ecosistema han sido interrumpidos. En Chile, su recurrencia durante 2026 -Valbifrut, Ducasse, Conectados, Graneles, NOI, SAAM, Maitenes, AGUNSA, Difor, Tanner y otros listings- lo vuelve un intelligence requirement permanente, aunque cada caso deba validarse individualmente.

Técnicamente, el valor defensivo está en sus objetivos operativos recurrentes: valid accounts y remote access, Active Directory, credenciales, administración remota, exfiltración, degradación de EDR, backups y virtualización. MITRE documenta PowerShell, GPO, scheduled tasks, Mimikatz/token manipulation, discovery de hosts, SMB/SSH, service stop, recovery inhibition y ESXi. La firma del encryptor es una evidencia tardía. [S24]

### 8.2 The Gentlemen: del afiliado experimentado a actor de primer nivel

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/13.webp' | relative_url }}"
    alt="Imagen 13"
    loading="lazy"
  >
  <figcaption><a href="https://healthexec.com/topics/health-it/cybersecurity/gentlemen-ransomware-gang-takes-over-hospital-facebook-after-cyberattack" target="_blank" rel="noopener noreferrer">https://healthexec.com/topics/health-it/cybersecurity/gentlemen-ransomware-gang-takes-over-hospital-facebook-after-cyberattack</a></figcaption>
</figure>

The Gentlemen pasó de no tener publicaciones en agosto de 2025 a 166 víctimas en Q1 2026 y 269 en Q2. Check Point vincula su origen con un antiguo afiliado de Qilin y una reserva de accesos previamente comprometidos. Una filtración interna del propio grupo expuso un núcleo de aproximadamente nueve operadores, varios afiliados y procedimientos de acceso que incluían vulnerabilidades Fortinet/Cisco, NTLM relay y OWA/M365. [S04][S05][S25]

La filtración mostró además uso de asistentes de código para construir en aproximadamente tres días parte de su panel de administración ransomware. Esto es más relevante que las narrativas de “ransomware autónomo”: existe evidencia primaria de IA reduciendo el tiempo de desarrollo y permitiendo a actores experimentados producir tooling más rápido. El humano sigue seleccionando víctimas, accesos y objetivos, la IA comprime el costo de implementación.

En Chile, The Gentlemen aparece en registros asociados a INDH, Corporación Colina, Las Cenizas, CONTAC, ESPAC, Layher, Incolur y S&A Chile, entre otros. No todos están corroborados. La señal relevante es que el país ya forma parte de su distribución geográfica y que la operación se interesa por gobierno, minería, tecnología, construcción e integradores.

### 8.3 Akira: consistencia operacional y presión sobre industria

Akira continúa entre las operaciones de mayor volumen, especialmente en manufactura e industrial services. Dragos la mantuvo entre los actores más activos contra organizaciones industriales en Q1 y Q2 2026. Sus patrones públicos incluyen abuso de VPN (recordemos a fin de 2023 en Chile) y cuentas legacy, robo de credenciales, exfiltración mediante servicios legítimos y destrucción de backups antes del cifrado. [S07][S08]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/14.jpg' | relative_url }}"
    alt="Imagen 14"
    loading="lazy"
  >
  <figcaption><a href="https://www.trellix.com/blogs/research/akira-ransomware/" target="_blank" rel="noopener noreferrer">https://www.trellix.com/blogs/research/akira-ransomware/</a></figcaption>
</figure>

Para Sudamérica, Akira importa porque el modelo no requiere una campaña “regional”. La misma combinación de VPN, cuentas heredadas, virtualización, servidores de archivos y alta presión por downtime existe en agroindustria, manufactura, minería, logística y servicios. Chile ya mostró listings de Akira en 2025, y la lógica de acceso que utiliza sigue siendo aplicable aunque el actor dominante local en 2026 sea otro.

### 8.4 LockBit 5.0, DragonForce y la larga cola

LockBit 5.0 regresó en 2025 y alcanzó 163 publicaciones en Q1 2026. DragonForce, por su parte, busca funcionar como una infraestructura/cartel para otros operadores y ha promocionado servicios de análisis de datos robados para mejorar la extorsión. La lectura correcta no es que estas marcas vayan a dominar necesariamente Chile, sino que la barrera de entrada para un afiliado continúa reduciéndose: puede elegir entre múltiples plataformas, reutilizar tooling y migrar cuando un programa cae. [S03][S04][S06]

## 9. Sudamérica no tiene un único threat landscape

### 9.1 Brasil: volumen, banking malware y crimen financiero especializado

Brasil es el principal mercado sudamericano en prácticamente todos los datasets comparables. Recorded Future registró 128 publicaciones de ransomware en 2025, ESET observó más de 100 víctimas durante H1 2026. Pero ransomware es solo una parte de la historia. Brasil posee un ecosistema maduro de banking malware, fraude de pagos, troyanos móviles y grupos que desarrollan tooling adaptado a Pix, boletos, software bancario y hábitos locales. [S01][S06]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/15.png' | relative_url }}"
    alt="Imagen 15"
    loading="lazy"
  >
  <figcaption><a href="https://www.zscaler.com/blogs/security-research/clickfix-campaign-generated-ai-delivers-smartrat" target="_blank" rel="noopener noreferrer">https://www.zscaler.com/blogs/security-research/clickfix-campaign-generated-ai-delivers-smartrat</a></figcaption>
</figure>

En septiembre de 2026 Google Threat Intelligence Group/Mandiant publicó su análisis de BREEZE COMET, actor financiero que desde 2024 compromete organizaciones de servicios financieros, retail y e-commerce brasileñas para manipular sistemas de pagos y software bancario. Este tipo de operación recuerda que “mayor ransomware” no equivale automáticamente a “mayor riesgo financiero”: en banca, fraude transaccional y account takeover pueden ser amenazas más directas. [S18]

El CTIR brasileño ha publicado durante 2026 recomendaciones específicas sobre ClickFix, campañas de phishing, explotación de vulnerabilidades, compromiso de identidades y abuso de subdominios .gov.br para distribuir malware de robo de información y control remoto. Es una cadena de acceso que converge perfectamente con el modelo de ransomware: credencial → sesión → privilegio → movimiento lateral → monetización. [S19][S20]

### 9.2 Argentina: alta exposición regional y targets de alto valor

Argentina fue el segundo país sudamericano del dataset 2025 de Recorded Future con 63 publicaciones y ESET contabilizó 39 víctimas en H1 2026. La economía digital, el sector financiero, salud, gobierno y empresas de servicios la mantienen dentro de la superficie de interés regional. Recorded Future también observó FamousSparrow/TAG-141 contra entidades de México, Argentina y Chile, ilustrando que el país comparte con la región tanto crimen financiero como actividad de espionaje. [S01][S06]

El registro de Qilin sobre el Ejército Argentino durante julio de 2026 debe manejarse como claim mientras no exista evidencia pública adicional suficiente. Aun así, el hecho de que actores RaaS incluyan organizaciones estatales y militares en sus leak sites demuestra que los límites tradicionales entre “objetivos criminales” y “objetivos de interés estratégico” no siempre se reflejan en la selección de afiliados.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/16.png' | relative_url }}"
    alt="Imagen 16"
    loading="lazy"
  >
  <figcaption><a href="https://www.dexpose.io/qilin-ransomware-group-targets-ejercito-argentino/" target="_blank" rel="noopener noreferrer">https://www.dexpose.io/qilin-ransomware-group-targets-ejercito-argentino/</a></figcaption>
</figure>

### 9.3 Colombia: ransomware con impacto estatal confirmado

Colombia acumuló 51 publicaciones en 2025 y 33 en H1 2026 según las fuentes regionales revisadas. A diferencia de muchos listings, el Ministerio de Justicia colombiano confirmó el 3 de agosto de 2026 que parte de su infraestructura tecnológica había sido comprometida por un virus tipo ransomware, afectando disponibilidad de servicios. COLCERT aseguró evidencia y logs, inició análisis forense y el Ministerio activó canales alternos, semanas después algunos sistemas seguían temporalmente indisponibles. [S21][S30]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/17.png' | relative_url }}"
    alt="Imagen 17"
    loading="lazy"
  >
  <figcaption><a href="https://www.vanguardia.com/colombia/2026/08/03/atencion-ministerio-de-justicia-confirma-ataque-cibernetico-con-ransomware/" target="_blank" rel="noopener noreferrer">https://www.vanguardia.com/colombia/2026/08/03/atencion-ministerio-de-justicia-confirma-ataque-cibernetico-con-ransomware/</a></figcaption>
</figure>

La relevancia gerencial de este caso está en el tiempo de recuperación: un incidente ransomware puede convertirse en suspensión de plazos, canales alternos, contingencia administrativa y necesidad de coordinación con equipos nacionales e internacionales. El impacto real se mide en capacidad de prestar servicio, no en cantidad de endpoints cifrados.

### 9.4 Perú, Ecuador, Bolivia, Paraguay y Uruguay: menor granularidad no significa ausencia de riesgo

Perú registró 27 publicaciones en 2025 en Recorded Future. Para 2026 existen numerosos listings en trackers, pero no hay una fuente H1 equivalente con la misma metodología para todos los países sudamericanos. Ecuador aparece en casos financieros de Qilin durante 2025 y mantiene una exposición significativa a fraude y malware, Bolivia, Paraguay y Uruguay tienen volúmenes menores y reporting desigual. [S01]

La ausencia de una cifra comparable es un intelligence gap, no una prueba de menor actividad. En países con menor mercado, un solo incidente en un operador de telecomunicaciones, gobierno, salud o energía puede tener una consecuencia nacional desproporcionada frente al volumen estadístico.

## 10. El panorama por sector: dónde la misma técnica produce consecuencias distintas

La victimología no debería utilizarse únicamente para preguntar “qué sector aparece más veces”. El riesgo sectorial se construye como la intersección de exposición, dependencia tecnológica y consecuencia operacional. Un ataque idéntico produce resultados distintos en una fábrica, un banco, un hospital o un ministerio.

| **Sector** | **Superficie recurrente** | **Consecuencia dominante** | **Lectura 2025–2026** |
| --- | --- | --- | --- |
| Banca / financiero | Identity, OWA/M365, VPN, VDI, APIs, endpoints privilegiados, terceros | Fraude, fuga de información, indisponibilidad, abuso secundario de datos | Ransomware compite con fraude financiero y account takeover, Tanner muestra valor extorsivo de datos internos. |
| Gobierno / servicios esenciales | Legacy remote access, AD, proveedores, portales, datos ciudadanos | Interrupción de trámites, crisis pública, exposición de datos, obligación de reporte | ANCI, INDH claims, OIV/PSE Chile y MinJusticia Colombia elevan prioridad. |
| Manufactura / productivo | VPN, plantas remotas, ERP, AD, VMware, file servers, IT/OT dependencies | Downtime de producción, logística y trazabilidad | Sector más afectado en LAC 2025, 65% del dataset industrial de Dragos Q2 2026 fue manufactura. |
| Minería / energía | Contractors, remote access, IT/OT bridge, engineering systems, virtualization | Interrupción operacional y riesgo de seguridad física indirecta | Alta consecuencia aun sin tocar PLC, Las Cenizas/Pucobre ilustran interés visible en Chile. |
| Salud | AD, sistemas clínicos, backups, PII/PHI, proveedores | Disponibilidad asistencial, privacidad, continuidad clínica | Clínica Maitenes y Hospital Clínico claims, globalmente salud sigue bajo presión. |
| Transporte / logística | ERP/EDI, puertos, vendor access, VMware, proveedores | Parálisis de cadena logística, contratos y operaciones | SAAM/AGUNSA y tendencia Dragos reflejan presión sobre continuidad. |
| Tecnología / MSP | RMM, tenants, credenciales privilegiadas, tooling multi-cliente | Blast radius transversal y downstream compromise | S&A Chile y CONTAC en listings, riesgo de autoridad multi-tenant. |
| Educación | Identidad amplia, endpoints heterogéneos, legacy, investigación | Interrupción académica y filtración de datos | Universidades aparecen repetidamente en trackers regionales. |

### 10.1 Sector productivo: no hace falta comprometer un PLC para detener una planta

Manufactura fue el sector con más víctimas en LAC durante 2025 en el dataset de Recorded Future. En el universo industrial de Dragos, Q1 2026 registró 1.020 incidentes/publicaciones y Q2 1.140, manufactura representó 633 y 747 respectivamente, aproximadamente 62–65% del total. Qilin, Akira y The Gentlemen estuvieron entre los actores de mayor volumen. [S01][S07][S08]

La lectura para Chile es evidente. Una salmonera, minera, procesadora de alimentos, empresa de logística o manufactura puede detenerse sin que el atacante ejecute una sola instrucción en un PLC. Si ERP, Active Directory, file servers, virtualización, sistemas de calidad, planificación, despacho o trazabilidad quedan indisponibles, la operación puede degradarse igual. El límite IT/OT no elimina la dependencia operacional entre ambos mundos.

### 10.2 Banca y finanzas: ransomware es una amenaza, pero no la única monetización

El sector financiero concentra datos sensibles y capacidad de pago, pero en Sudamérica el adversario no necesita cifrar para monetizar. BREEZE COMET en Brasil, Grandoreiro, Mispadu, Astaroth, Coyote y otras familias muestran un ecosistema orientado a credenciales, sesiones y fraude transaccional. Recorded Future documenta continuidad de troyanos bancarios en 2025 y evolución de variantes durante 2026. [S01][S18]

Tanner añade otra dimensión: información legal y financiera interna puede ser utilizada como palanca de extorsión aun cuando el público no tenga evidencia de cifrado. En un banco o financiera, confidentiality loss puede ser tan monetizable como availability loss.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/18.png' | relative_url }}"
    alt="Imagen 18"
    loading="lazy"
  >
  <figcaption><a href="https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil" target="_blank" rel="noopener noreferrer">https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil</a></figcaption>
</figure>

### 10.3 Gobierno: el impacto se mide en servicio público

El caso MinJusticia Colombia y el incidente OIV/PSE chileno muestran que el ransomware en gobierno no puede evaluarse con el mismo criterio que un endpoint corporativo. Suspensión de trámites, canales alternativos, plazos administrativos, comunicación pública y coordinación nacional son parte del impacto. La recuperación tecnológica se vuelve un problema de continuidad institucional.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/19.png' | relative_url }}"
    alt="Imagen 19"
    loading="lazy"
  >
  <figcaption><a href="https://therecord.media/china-hackers-latin-america-espionage" target="_blank" rel="noopener noreferrer">https://therecord.media/china-hackers-latin-america-espionage</a></figcaption>
</figure>

### 10.4 Salud: disponibilidad y confidencialidad se cruzan

Salud aparece entre los sectores regionales más atacados en 2025 y continúa en la lista de los grandes actores. Un hospital puede mantener atención clínica aun con un incidente, como informó Clínica Maitenes, pero el compromiso de backups, sistemas de laboratorio, identidad o historias clínicas puede generar impacto acumulativo y riesgo de privacidad. La prioridad no es solo “evitar cifrado”, es preservar la capacidad de operar con seguridad.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/20.png' | relative_url }}"
    alt="Imagen 20"
    loading="lazy"
  >
  <figcaption><a href="https://thehackernews.com/2026/07/china-nexus-jadeprox-uses-new-triback.html" target="_blank" rel="noopener noreferrer">https://thehackernews.com/2026/07/china-nexus-jadeprox-uses-new-triback.html</a></figcaption>
</figure>

## 11. Antes del ransomware: la economía del acceso

La pieza que conecta casi todo el landscape es la economía del acceso. Microsoft considera el credential theft una de las principales preocupaciones de Latinoamérica. Entre el 16 de marzo y el 16 de mayo de 2025 registró 21.137 dispositivos brasileños afectados por Lumma Stealer, 10.486 argentinos, 8.303 colombianos, 6.618 peruanos y 5.606 chilenos. [S09]

CrowdStrike observó en 2024 a 107 access brokers anunciando acceso a 428 entidades LATAM y recuperó más de mil millones de credenciales regionales asociadas con filtraciones y stealer logs. El precio promedio del acceso inicial cayó 60% frente a 2023. La lectura económica es simple: cuando la oferta de credenciales y accesos aumenta, el afiliado ransomware no necesita desarrollar cada etapa desde cero. Puede comprar o reutilizar una entrada ya conseguida. [S10]

ANCI añadió evidencia local en mayo de 2026. Investigando filtraciones, señaló que no había evidencia de ataques directos contra la infraestructura en varios casos, pero sí accesos no autorizados mediante credenciales válidas probablemente provenientes de filtraciones previas o malware infostealer. [S13]

> **CADENA DE MONETIZACIÓN**  
> **Infostealer / phishing / leak → credencial válida → broker o afiliado → VPN / IdP / OWA / remote access → Active Directory / cloud → exfiltración → backup / virtualización → extorsión y/o cifrado.**

Este modelo explica por qué la prevención de ransomware no puede ser un proyecto aislado del programa de identidad. MFA incompleto, cuentas de proveedor, sesiones persistentes, dispositivos no gestionados, service accounts, credenciales de navegador y rutas legacy pueden transformarse en el eslabón inicial de un incidente cuyo impacto final aparecerá días o semanas después bajo una marca de ransomware.

## 12. Del acceso al impacto: el patrón técnico que se repite

### 12.1 Initial Access: identidad, edge devices y social engineering

Los principales actores de 2025–2026 convergen en un conjunto limitado de clases de acceso: credenciales válidas, VPN y servicios remotos, appliances perimetrales vulnerables, phishing/social engineering, acceso adquirido a terceros, y RMM. El cambio no está en que estas técnicas sean nuevas, sino en la velocidad con que son operacionalizadas y en la disponibilidad de access stockpiles.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/21.webp' | relative_url }}"
    alt="Imagen 21"
    loading="lazy"
  >
  <figcaption><a href="https://cyberhoot.com/es/cybrary/initial-access-broker-iab/" target="_blank" rel="noopener noreferrer">https://cyberhoot.com/es/cybrary/initial-access-broker-iab/</a></figcaption>
</figure>

Brasil ofrece un buen indicador de evolución en social engineering. CTIR.Gov advirtió sobre ClickFix contra dominios .gov.br y campañas que combinan phishing, explotación de vulnerabilidades, compromiso de identidad y exfiltración. ESET observó que las detecciones de ClickFix más que se duplicaron entre H2 2025 y H1 2026, mientras el quishing alcanzó niveles récord en su telemetría. [S19][S20][S23]

### 12.2 Credential Access y Active Directory: convertir una cuenta en autoridad

Una credencial válida solo es valiosa si puede convertirse en alcance. En intrusiones modernas, el objetivo es identificar grupos, cuentas privilegiadas, Domain Controllers, GPO, rutas de administración, backups y sistemas de virtualización. Qilin ha sido documentado utilizando Mimikatz/token manipulation, PowerShell, GPO y discovery, The Gentlemen utiliza credenciales, relay y servicios corporativos, Akira roba credenciales antes de destruir backups. [S24][S25][S08]

El problema no es únicamente Domain Admin. Tier-0 debe entenderse como el conjunto de identidades y activos cuyo compromiso otorga control sistémico: Domain Controllers, GPO/SYSVOL, PKI, PAM, identidades de backup, vCenter y jump hosts privilegiados. Si comparten rutas de administración o credenciales reutilizadas, la segmentación dibujada en un diagrama puede no existir operacionalmente.

### 12.3 Discovery y lateral movement: LOLBins, administración legítima y contexto

RDP, SMB/admin shares, PsExec, PowerShell, WMI, scanners, RMM, SSH y herramientas comerciales aparecen repetidamente porque ya existen en los entornos corporativos. La oportunidad defensiva no está en declarar malicioso un proceso por nombre, sino en observar quién lo ejecuta, desde qué segmento, después de qué autenticación y contra qué volumen de hosts.

Una sesión RDP este-oeste desde una PAW autorizada durante mantenimiento no tiene el mismo significado que una ráfaga de RDP/SMB desde una workstation que acaba de autenticar desde VPN. La correlación temporal entre identity, endpoint y network telemetry sigue siendo superior a la detección de una herramienta aislada.

### 12.4 Defense Evasion: cuando el EDR se convierte en objetivo

ESET reporta más de 100 EDR killers observados in the wild y nuevos ejemplares de forma regular. Qilin ha utilizado BYOVD y componentes especializados para interferir con seguridad, otros RaaS adoptan la misma lógica. El control defensivo se transforma en un objetivo explícito. [S23]

Esto cambia una regla operacional para el SOC: la pérdida coordinada de heartbeat de agentes no debe tratarse únicamente como health issue. Si ocurre después de actividad privilegiada, driver loading anómalo, service stop o remote administration, puede ser una señal de ataque. La organización necesita telemetría independiente que sobreviva al endpoint: firewall, NDR, IdP, Windows Event Forwarding, SIEM, vCenter, Veeam y appliances.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/22.jpg' | relative_url }}"
    alt="Imagen 22"
    loading="lazy"
  >
  <figcaption><a href="https://blog.talosintelligence.com/qilin-edr-killer/" target="_blank" rel="noopener noreferrer">https://blog.talosintelligence.com/qilin-edr-killer/</a></figcaption>
</figure>

### 12.5 Exfiltration-first: el impacto puede existir sin cifrado

El movimiento desde encryption-first hacia data theft / pressure-first se consolidó en 2025 y continúa en 2026. Exfiltrar reduce parte de la complejidad operacional del cifrado y crea presión regulatoria, reputacional y comercial. Qilin incluso ha promocionado asistencia para identificar consecuencias regulatorias y aumentar la presión sobre víctimas. [S02]

Tanner representa la materialización local de este modelo: una vez publicados documentos internos, el daño ya no depende de si se cifró un servidor. El dataset puede generar titulares, fraude, spearphishing y exposición de relaciones comerciales. Availability y confidentiality son palancas distintas del mismo negocio de extorsión.

### 12.6 Backup, Veeam, vCenter y ESXi: atacar recovery para multiplicar presión

El paso más importante antes del cifrado suele ser reducir la capacidad de recuperar. Los actores buscan VSS, repositorios de backup, Veeam, hipervisores, snapshots y credenciales privilegiadas. Qilin soporta ESXi y ha sido observado propagándose hacia vCenter/ESXi, Akira mantiene patrones de destrucción de backup y acceso a hipervisores. [S24][S08]

La concentración tecnológica amplifica el riesgo. Decenas de servicios pueden depender de un mismo vCenter y una misma plataforma de backup. Si AD, backup y virtualización comparten el mismo trust plane, el actor puede convertir un compromiso de identidad en indisponibilidad transversal. La pregunta madura no es “¿tenemos backup?”, sino “¿puede el mismo administrador comprometido destruir el backup y apagar las VMs?”

## 13. El malware alrededor del ransomware: infostealers, banking trojans, loaders y RATs

Si este análisis regional se limitara a ransomware, perdería la mitad del problema. Los infostealers suministran credenciales, los loaders entregan payloads, los RATs mantienen acceso, los banking trojans monetizan cuentas directamente, y campañas de phishing o ClickFix crean nuevos dispositivos comprometidos que pueden terminar en stealer logs o manos de brokers.

Recorded Future observó durante 2025 actividad relevante de Grandoreiro, Crocodilus, Mispadu, Astaroth, SORVEPOTEL, Casbaneiro, BBTok, Coyote y otras familias bancarias. Varias campañas se apoyan en WhatsApp, PDF/LNK, PowerShell, infraestructura cloud comprometida o apps móviles. La frontera entre “malware bancario” y “acceso inicial corporativo” puede ser más por objetivo de monetización que por técnica. [S01]

Kaspersky registró más de 1,1 millones de intentos ransomware en Latinoamérica entre agosto de 2024 y junio de 2025. Chile apareció tercero con aproximadamente 43.000 detecciones, detrás de Brasil y México. Ese dato no contradice los menores volúmenes de DLS chilenos: mide intentos bloqueados en endpoints, no organizaciones victimizadas. [S26]

La diferencia entre esos datasets es analíticamente útil. Un país puede tener muchas detecciones de malware y menos publicaciones en leak sites, otro puede tener menos telemetría endpoint pero incidentes corporativos de alto impacto. El threat landscape debe conservar las unidades de medida en vez de forzar una sola tabla.

## 14. No todo es cibercrimen: APT y convergencia de tradecraft

Ransomware es principalmente una economía criminal, pero las organizaciones sudamericanas también son objetivo de espionaje, operaciones estatales y actores híbridos. CrowdStrike describe a adversarios China-nexus como los state-sponsored más activos en LATAM en su análisis regional. Recorded Future menciona a FamousSparrow/TAG-141 utilizando SparrowDoor contra entidades de México, Argentina y Chile, y actividad de Storm-2603 desplegando distintos ransomwares contra sectores como gobierno, energía, agricultura y telecomunicaciones en LAC/APAC. [S01][S10]

Desde Detection Engineering, la separación “APT sofisticado vs. criminal ransomware” es menos útil de lo que parece. Ambos pueden explotar Exchange o VPN, abusar cuentas válidas, utilizar PowerShell, Cobalt Strike o RMM, robar credenciales y exfiltrar a cloud. La motivación sigue siendo fundamental para atribución e intelligence requirements, pero muchas señales defensivas son compartidas.

Eso refuerza un enfoque adversary-informed: diseñar controles alrededor de las funciones del ataque -obtener acceso, escalar, descubrir, moverse, persistir, extraer, degradar recovery- y no alrededor de una marca específica. El mismo control de MFA o segmentación puede interrumpir a un afiliado Qilin, un operador de fraude y un cluster de espionaje.

## 15. Detection Engineering: qué debería cambiar en una organización sudamericana

La detección de mayor retorno ocurre antes de T1486. Esperar al encryptor significa que el actor probablemente ya posee credenciales, discovery, acceso a servidores de valor y capacidad para distribuir tooling. Las siguientes familias de detección son más resistentes al cambio de marca ransomware.

| **Detección** | **Qué buscar** | **Telemetría** | **Prioridad** |
| --- | --- | --- | --- |
| Remote access + identity | Spray distribuido, valid login desde nuevo ASN/dispositivo/país, proveedor fuera de patrón, sesión legacy | VPN / IdP / firewall / UEBA | P0 |
| Tier-0 / AD | GPO/SYSVOL changes, admin logon fuera de PAW, LSASS/NTDS access, new admin accounts | DC audit / WEF / EDR / SIEM | P0 |
| Lateral movement | RDP este-oeste, ADMIN$/C$ fan-out, PsExec, remote service creation, unusual SSH | NDR / Windows / firewall / EDR | P0 |
| EDR impairment | Heartbeat loss colectivo, service stop, driver loads, DLL side-loading, BYOVD indicators | EDR health / kernel telemetry / SIEM / NDR | P0 |
| Exfiltration | Uploads excepcionales desde file/DC/backup server a cloud/file-sharing, new sync tools | Proxy / NetFlow / NDR / CASB | P1 |
| Backup / vCenter | Task/snapshot deletion, new admin, password changes, VM shutdown, repository tampering | Veeam / vCenter / hypervisor audit | P0 |
| RMM / tunnels | Nueva instalación/tenant, AnyDesk/ScreenConnect/Mesh/Ngrok fuera de baseline | EDR / inventory / network | P1 |
| Credential economy | Credenciales corporativas en stealer logs, password reuse, breached third-party identities | CTI / identity / exposure monitoring | P0 |

Una detección no debería vivir aislada. “Valid VPN login” puede ser legítimo. “Valid VPN login + domain discovery + RDP east-west + GPO modification + EDR heartbeat loss” es una hipótesis de intrusión. El valor está en el contexto temporal y en la relación entre identidades, hosts y control planes.

## 16. Para CISO y gerencia: del control declarado al control operable

El panorama 2025–2026 refuerza una idea incómoda: tener un control no es lo mismo que tener una capacidad. Una organización puede declarar MFA y mantener una VPN de proveedor sin MFA, puede tener EDR y no alertar cuando veinte agentes dejan de reportar, puede tener backups y permitir que las mismas credenciales de dominio administren Veeam, puede tener segmentación y permitir SMB/RDP desde pools de VPN hacia servidores críticos.

| **Control** | **Pregunta de validación** | **Por qué importa** |
| --- | --- | --- |
| MFA / remote access | ¿Todas las rutas VPN, proveedor, break-glass y legacy están cubiertas y sin bypass? | Los accesos remotos siguen apareciendo como vector repetido. |
| PAM / JIT | ¿Una identidad obtenida desde un endpoint ordinario puede progresar hacia Tier-0? | Reduce la transformación de credencial en autoridad. |
| Segmentación | ¿VPN/user VLAN alcanza DC, backup o hypervisor management? | Limita el blast radius del foothold inicial. |
| EDR resilience | ¿Service stop, driver manipulation o telemetry loss generan una respuesta independiente? | El EDR es un objetivo activo. |
| Backup | ¿La restauración completa fue probada y las identidades están separadas? | Backup presente no equivale a recovery probado. |
| VMware / ESXi | ¿vCenter tiene acceso aislado, MFA, logging y cuentas separadas donde sea viable? | Controla disponibilidad de muchos servicios simultáneamente. |
| Third-party access | ¿Vendors tienen JIT, expiración, session recording y scope mínimo? | Los terceros concentran rutas de confianza. |
| Incident reporting | ¿SOC, legal y liderazgo pueden escalar/reportar dentro de plazos reales? | En Chile, detección y reporte son parte de la capacidad operativa. |

Para organizaciones sujetas a la Ley 21.663, el incidente ya no es solamente un problema técnico interno. La capacidad de detectar, clasificar, escalar y reportar se vuelve parte de la postura de seguridad. Una organización que descubre el ransomware al momento del cifrado puede haber perdido horas o días decisivos para contención, preservación de evidencia y comunicación regulatoria.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/23.png' | relative_url }}"
    alt="Imagen 23"
    loading="lazy"
  >
  <figcaption><a href="https://innershell-labs.github.io/2026/07/22/A_Security_Control_Is_Not_Real_Until_It_Can_Be_Operated.html" target="_blank" rel="noopener noreferrer">https://innershell-labs.github.io/2026/07/22/A_Security_Control_Is_Not_Real_Until_It_Can_Be_Operated.html</a></figcaption>
</figure>

> **MÉTRICA EJECUTIVA**  
> **La severidad de ransomware debería modelarse como pérdida de capacidad de negocio: ¿qué servicio deja de prestarse?, ¿por cuánto tiempo?, ¿qué información salió?, ¿qué terceros quedan expuestos?, ¿qué obligaciones se activan? Contar endpoints cifrados es una métrica demasiado pequeña para un problema de resiliencia empresarial.**

## 17. Mirada a 2026–2027: qué es razonable esperar

No existe evidencia suficiente para pronosticar una campaña única “contra Chile” dirigida por un solo actor. La hipótesis más consistente es otra: afiliados globales buscan superficies replicables y encuentran en Sudamérica las mismas combinaciones de remote access, credenciales, appliances vulnerables, RMM, Active Directory, VMware y baja tolerancia al downtime que monetizan en otros mercados.

1. Qilin y The Gentlemen seguirán siendo relevantes, pero el liderazgo de marca puede cambiar rápidamente. La movilidad de afiliados es más estable que el nombre del RaaS.

1. El valor de identity compromise seguirá creciendo. Infostealers, phishing, token theft y access brokers reducen el costo de entrar sin necesidad de un exploit sofisticado.

1. Edge devices continuarán siendo una superficie prioritaria. El tiempo entre disclosure/exploitation seguirá reduciéndose y los appliances con lifecycle deficiente serán rutas atractivas.

1. EDR killers, BYOVD y defense evasion se normalizarán como componentes reutilizables. La independencia de telemetría será más importante que otra firma de malware.

1. ESXi, vCenter, Veeam y otros recovery/control planes seguirán bajo presión porque convierten privilegios en impacto concentrado.

1. La extorsión será cada vez menos dependiente del cifrado. Publicar datos, contactar clientes, explotar consecuencias regulatorias o realizar presión reputacional puede ser suficiente.

1. La IA acelerará tooling, análisis de datos robados, phishing y adaptación de scripts. El cambio inmediato será productividad del atacante, no autonomía total.

1. MSP, integradores y proveedores tecnológicos aumentarán su valor como objetivos por la autoridad transversal y el acceso downstream que concentran.

1. La visibilidad en Chile seguirá creciendo también por madurez institucional: más OIV, más reporting y más capacidad de correlacionar incidentes que antes quedaban aislados.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/24.jpg' | relative_url }}"
    alt="Imagen 24"
    loading="lazy"
  >
  <figcaption><a href="https://www.gartner.com/en/newsroom/press-releases/2026-06-02-gartner-identifies-four-critical-threats-requiring-urgent-improvements-from-cybersecurity-leaders" target="_blank" rel="noopener noreferrer">https://www.gartner.com/en/newsroom/press-releases/2026-06-02-gartner-identifies-four-critical-threats-requiring-urgent-improvements-from-cybersecurity-leaders</a></figcaption>
</figure>

## 18. Intelligence gaps: lo que todavía no sabemos

Un análisis recopilatorio serio debe terminar también con sus límites. El principal gap de Chile sigue siendo la falta de disclosures técnicos detallados de incidentes. Tenemos claims, comunicaciones corporativas breves y escasas, alertas regulatorias, filtraciones y periodismo de investigación, pero rara vez aparecen timelines completas con vector inicial, dwell time, artefactos, infraestructura, exfiltration path, afiliado, controles evadidos y root cause, por lo que no aprendemos de los incidentes nacionales de manera que compartamos ese conocimiento y medidas para prevenir ataques.

- No existe un denominador nacional público de VPN sin MFA, appliances legacy o cuentas de proveedor expuestas.

- No existe un dataset público unificado que permita distinguir de forma consistente victim-confirmed, corroborated, claimed y false positive para Chile.

- La mayoría de los casos Qilin chilenos no permiten identificar qué afiliado condujo la intrusión.

- No conocemos públicamente el vector de acceso de Tanner, SAAM Towage, AGUNSA, Difor y múltiples listings de 2026.

- Los trackers utilizan diferentes fechas: publicación, descubrimiento, estimación de ataque o backfill, compararlos sin normalización fabrica tendencias.

- Las cifras de endpoint detections, DLS victims, incident reports y financial losses no son intercambiables.

- La exposición de terceros y MSP en Chile todavía carece de mediciones públicas comparables.

- La relación entre stealer-log exposure y ransomware victimization regional es plausible y operativamente útil, pero no debe transformarse en causalidad individual sin evidencia.

La forma de elevar confianza es conocida: VPN/IdP logs, EDR process trees, audit de Domain Controllers, SYSVOL/GPO history, Veeam/vCenter logs, NetFlow/proxy para exfiltración, ransom notes, hashes, timestamps y comunicaciones de la organización. Mientras esas evidencias no estén disponibles, las hipótesis deben permanecer etiquetadas como hipótesis.

## 19. Conclusión: el ransomware es el resultado visible de un mercado de acceso mucho mayor

La principal diferencia entre 2025 y 2026 no es que haya aparecido una técnica mágica nueva. Es que el ecosistema criminal se volvió más eficiente reorganizando capacidades existentes. En 2025, la caída de grandes marcas produjo fragmentación, en 2026, operadores como Qilin y The Gentlemen demostraron que los afiliados, las credenciales, los accesos y el conocimiento operacional pueden reagruparse con rapidez. La marca cambia más rápido que la función.

Sudamérica reproduce esa dinámica con características propias. Brasil domina por escala y por la profundidad de su ecosistema de fraude financiero, Argentina y Colombia sostienen volúmenes relevantes, Perú mantiene exposición persistente, Chile muestra durante 2026 una presión mucho más visible y diversa de la que sugería mirar únicamente los rankings regionales de 2025.

El caso Tanner resume bien el problema. Un listing comenzó como claim. Días después, comprobaciones múltiples en el mundo CTI y una investigación periodística accedió a documentos internos y describió material específico, elevando el caso a una filtración corroborada. Lo que todavía no sabemos -vector, cifrado, dwell time, recovery- debe permanecer como gap. Esa combinación de firmeza y cautela es más útil que los dos extremos habituales: creer todo lo que publica un criminal o descartar todo hasta que la víctima publique un post-mortem que probablemente nunca llegará.

Para un CISO, el mensaje es menos atractivo pero más accionable: el ransomware no se resuelve comprando “anti-ransomware”. Se reduce evitando que una identidad comprometida se transforme en autoridad sobre Active Directory, backups, virtualización, datos y terceros. Para un SOC, la detección no debe esperar el encryptor. Para Red Team, el objetivo no es demostrar que puede lanzar ransomware, sino validar qué control debería haber interrumpido la cadena. Para CTI, el trabajo no es acumular IoCs: es conectar actores, accesos, TTPs, sectores, evidencia y niveles de confianza con decisiones defensivas.

> **JUICIO FINAL**  
> **Chile no necesita esperar a que cada claim sea confirmado públicamente para actuar, pero tampoco necesita inflar cada listing hasta convertirlo en un breach probado. La inteligencia madura funciona en ese espacio: evidencia suficiente para tomar decisiones antes de tener certeza total, y disciplina suficiente para saber exactamente qué parte todavía no conocemos.**

En 2026, conocer el nombre de Qilin, The Gentlemen o Akira es útil. Entender el sistema que los hace posibles es mucho más importante.

## Fuentes y referencias clave

Las fuentes se seleccionaron priorizando organismos oficiales, equipos de threat intelligence reconocidos, reportes técnicos y medios que aportan corroboración directa. Los trackers de leak sites se utilizan como telemetría de claims, no como confirmación automática de incidentes.

**[S01] Recorded Future / Insikt Group – Panorama del cibercrimen en América Latina y el Caribe (2025).** https://www.recordedfuture.com/research/latin-america-and-the-caribbean-cybercrime-landscape-es

**[S02] Check Point Research – The State of Ransomware Q2 2025.** [https://research.checkpoint.com/2025/the-state-of-ransomware-q2-2025/](https://research.checkpoint.com/2025/the-state-of-ransomware-q2-2025/)

**[S03] Check Point Research – The State of Ransomware Q3 2025.** [https://research.checkpoint.com/2025/the-state-of-ransomware-q3-2025/](https://research.checkpoint.com/2025/the-state-of-ransomware-q3-2025/)

**[S04] Check Point Research – The State of Ransomware Q1 2026.** [https://research.checkpoint.com/2026/the-state-of-ransomware-q1-2026/](https://research.checkpoint.com/2026/the-state-of-ransomware-q1-2026/)

**[S05] Check Point Research – The State of Ransomware Q2 2026.** [https://research.checkpoint.com/2026/the-state-of-ransomware-q2-2026/](https://research.checkpoint.com/2026/the-state-of-ransomware-q2-2026/)

**[S06] ESET / WeLiveSecurity – Ransomware en el primer semestre de 2026.** [https://www.welivesecurity.com/es/ransomware/primer-semestre-2026-ataques-sectores-mas-afectados/](https://www.welivesecurity.com/es/ransomware/primer-semestre-2026-ataques-sectores-mas-afectados/)

**[S07] Dragos – Industrial Ransomware Analysis Q1 2026.** [https://www.dragos.com/dragos-industrial-ransomware-analysis-q1-2026](https://www.dragos.com/dragos-industrial-ransomware-analysis-q1-2026)

**[S08] Dragos – Industrial Ransomware Analysis Q2 2026.** [https://www.dragos.com/blog/dragos-industrial-ransomware-analysis-q2-2026](https://www.dragos.com/blog/dragos-industrial-ransomware-analysis-q2-2026)

**[S09] Microsoft – Digital Defense Report 2025.** [https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/security/Microsoft-Digital-Defense-Report-2025.pdf](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/security/Microsoft-Digital-Defense-Report-2025.pdf)

**[S10] CrowdStrike – 2025 LATAM Threat Landscape Report / Deep Dive.** [https://www.crowdstrike.com/en-us/blog/2025-latam-threat-landscape-report-deep-dive/](https://www.crowdstrike.com/en-us/blog/2025-latam-threat-landscape-report-deep-dive/)

**[S11] ANCI – Primer Balance Anual 2025.** https://anci.gob.cl/noticias/anci-primer-balance/

**[S12] ANCI – Primer proceso de calificación de Operadores de Importancia Vital, julio 2026.** https://anci.gob.cl/noticias/anci-finaliza-el-primer-proceso-de-calificacion-de-operadores-de-importancia-vital/

**[S13] ANCI – Actualización: filtraciones por robo de credenciales, mayo 2026.** https://anci.gob.cl/noticias/actualizacion-anci-filtraciones-por-robo-de-credenciales/

**[S14] Reproducción pública de alerta CSIRT Nacional AIC26-00002 sobre Qilin / OIV-PSE.** https://blog.nivel4.com/anci/csirt-nacional-alerta-sobre-incidente-de-efecto-significativo-en-entidad-estrategica-e-identifica-a-ransomware-qilin-como-autor

**[S15] Clínica Maitenes – Información sobre incidente de ciberseguridad, 13 junio 2026.** https://clinicamaitenes.cl/comunicados/

**[S16] Ransomware.live / Ransomwatch – mapa y registros de Chile.** https://ransomwatch.mousqueton.io/map/CL

**[S17] Interferencia – Hackeo a Tanner expone gestiones vinculadas a clientes y operaciones, 17 septiembre 2026.** https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup

**[S18] Google Threat Intelligence Group / Mandiant – BREEZE COMET Targets Brazil, septiembre 2026.** [https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil](https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil)

**[S19] CTIR.Gov Brasil – Recomendação 03/2026, ClickFix.** [https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-03-2026](https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-03-2026)

**[S20] CTIR.Gov Brasil – Recomendação 04/2026, phishing, vulnerabilidades e identidades.** https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-04-2026

**[S21] Ministerio de Justicia de Colombia – Actualización sobre ataque ransomware, 3 agosto 2026.** https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/Actualizacion-sobre-el-ataque-cibernetico.aspx

**[S22] COLCERT – Boletines y reportes de inteligencia 2026.** https://colcert.gov.co/800/w3-propertyvalue-412601.html

**[S23] ESET Threat Report H1 2026.** [https://www.welivesecurity.com/en/eset-research/eset-threat-report-h1-2026/](https://www.welivesecurity.com/en/eset-research/eset-threat-report-h1-2026/)

**[S24] MITRE ATT&CK – Qilin / Agenda, S1242.** [https://attack.mitre.org/software/S1242/](https://attack.mitre.org/software/S1242/)

**[S25] Check Point Research – análisis interno de The Gentlemen (referencia y threat report).** [https://research.checkpoint.com/2026/18th-may-threat-intelligence-report/](https://research.checkpoint.com/2026/18th-may-threat-intelligence-report/)

**[S26] Kaspersky – Ataques de ransomware superan 1,1 millones de intentos en América Latina, octubre 2025.** https://latam.kaspersky.com/about/press-releases/ataques-de-ransomware-superan-11-millones-de-intentos-en-america-latina

**[S27] AmCham Chile – Seminario ANCI e implementación Ley Marco de Ciberseguridad, 2026.** https://amchamchile.cl/noticia/seminario-de-amcham-chile-reune-a-la-anci-y-a-la-industria-en-plena-implementacion-de-la-ley-marco-de-ciberseguridad/

**[S28] GalaxyWarden – Hospital Clínico Universidad de Chile listed by DireWolf, agosto 2026 (claim tracker).** [https://www.galaxywarden.com/blog/breach/hospital-clnico-universidad-de-chile-direwolf-2026-08](https://www.galaxywarden.com/blog/breach/hospital-clnico-universidad-de-chile-direwolf-2026-08)

**[S29] Interferencia – filtración de documentos de SAAM Towage por Qilin, mayo 2026.** [https://interferencia.cl/secciones/empresas](https://interferencia.cl/secciones/empresas)

**[S30] Ministerio de Justicia de Colombia – Plan de recuperación tecnológica, agosto 2026.** [https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/MinJusticia-activa-plan-de-recuperacion-tecnologica-luego-de-vulneracion-cibernetica-garantizando-servicios-esenciales.aspx](https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/MinJusticia-activa-plan-de-recuperacion-tecnologica-luego-de-vulneracion-cibernetica-garantizando-servicios-esenciales.aspx)
