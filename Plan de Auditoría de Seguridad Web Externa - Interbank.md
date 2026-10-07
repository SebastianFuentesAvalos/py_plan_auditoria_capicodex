# PLAN DE AUDITORÍA DE TECNOLOGÍAS DE LA INFORMACIÓN

## CARÁTULA DE LA UNIVERSIDAD

**[NOMBRE DE LA UNIVERSIDAD]**  
**[FACULTAD / ESCUELA PROFESIONAL]**  
**Curso:** [Nombre del curso]  
**Docente:** [Nombre del docente]  
**Estudiante(s):** [Nombres y apellidos]  
**Ciclo / Sección:** [Completar]  

## CARÁTULA DEL PLAN DE AUDITORÍA

### AUDITORÍA DE SEGURIDAD WEB EXTERNA BASADA EN OWASP A INTERBANK

### LIMA, LIMA, LIMA

### “SEGURIDAD DEL PORTAL WEB PÚBLICO Y CONTROLES DE PROTECCIÓN FRENTE A AMENAZAS EXTERNAS”

### LIMA, 7 DE OCTUBRE DE 2026

### “[DENOMINACIÓN OFICIAL DEL DECENIO]”
### “[DENOMINACIÓN OFICIAL DEL AÑO 2026]”

> **Naturaleza del documento:** Plan académico. Este documento no constituye autorización para ejecutar pruebas sobre sistemas reales. Toda actividad activa requerirá autorización previa, expresa y escrita del propietario del activo, así como reglas de compromiso aprobadas.

---

## ÍNDICE

| Denominación | N.° de sección |
|---|---:|
| I. Origen | I |
| II. Información de la entidad o dependencia | II |
| III. Denominación de la materia de control | III |
| IV. Alcance | IV |
| V. Objetivos | V |
| VI. Procedimientos de auditoría | VI |
| VII. Plazo de la auditoría y cronograma | VII |
| VIII. Criterios de auditoría | VIII |
| IX. Información administrativa | IX |
| IX.1 Comisión auditora | IX.1 |
| IX.2 Costos directos estimados | IX.2 |
| X. Documento a emitir | X |
| Anexos | A1-A6 |

---

## I. ORIGEN

La presente Auditoría de Tecnologías de la Información se origina en la necesidad de evaluar, dentro de un caso académico, la exposición externa y los controles de seguridad del portal web público de **Banco Internacional del Perú S.A.A. - Interbank**, accesible mediante `https://interbank.pe`.

El portal constituye un canal relevante de información y acceso a servicios financieros, formularios públicos, simuladores, campañas y enlaces hacia servicios autenticados. Debido al valor de los servicios ofrecidos y a la sensibilidad del sector financiero, una debilidad en la configuración, el desarrollo o la gestión de componentes web podría facilitar ataques contra la confidencialidad, integridad, disponibilidad o privacidad de la información.

El caso proporcionado identifica como asuntos preliminares de interés los encabezados HTTP de seguridad, las cookies, las bibliotecas de terceros, la protección de formularios y los mecanismos de redirección. Estos asuntos se consideran **hipótesis de auditoría pendientes de comprobación** y no hallazgos confirmados. La auditoría deberá obtener evidencia suficiente, pertinente, válida y reproducible antes de emitir una conclusión.

El plan adopta como marco principal el **OWASP Application Security Verification Standard (ASVS) 4.0.3**, complementado por OWASP Web Security Testing Guide y OWASP Top 10. Debido a que la auditoría planteada es externa y sin acceso inicial a código fuente, configuraciones internas o credenciales, se aplicarán requisitos ASVS Nivel 1 que sean verificables mediante caja negra. ASVS Nivel 2 se utilizará como referencia de madurez para los controles propios de una entidad financiera, únicamente cuando la organización proporcione la documentación, el acceso y la autorización necesarios.

### 1.1 Justificación

- Identificar debilidades externamente observables antes de que sean aprovechadas por terceros.
- Evaluar controles mínimos de protección en transporte, sesiones, entradas, respuestas HTTP y componentes del cliente.
- Determinar el nivel de exposición asociado a formularios, enlaces, subdominios y servicios públicos autorizados.
- Proporcionar recomendaciones priorizadas, verificables y alineadas con OWASP.
- Establecer una línea base para una futura auditoría híbrida o interna de mayor alcance.

### 1.2 Condición previa obligatoria

Antes de iniciar cualquier prueba activa deberá existir una carta de autorización firmada por Interbank o por el titular competente de los activos. El documento deberá establecer los activos incluidos, horarios, fuentes de prueba, límites técnicos, responsables, procedimiento de emergencia y tratamiento de la información. Si dicha autorización no existe, el trabajo se limitará al análisis documental, al diseño del plan y, cuando sea lícito, a observaciones pasivas no intrusivas.

---

## II. INFORMACIÓN DE LA ENTIDAD O DEPENDENCIA

- **Entidad:** Banco Internacional del Perú S.A.A. - Interbank.
- **Sector:** Banca y finanzas.
- **Nivel de gobierno:** No aplica; entidad privada regulada.
- **Ubicación principal referencial:** Lima, Perú.
- **Tamaño referencial:** Más de 6000 colaboradores a nivel nacional, según el caso académico.
- **Servicios digitales relacionados:** Portal institucional, acceso a banca por internet, formularios públicos, simuladores, contratación de productos, subdominios y campañas digitales.
- **Activo principal propuesto:** Portal web público `https://interbank.pe`.
- **Responsable del activo:** Por confirmar formalmente con la entidad.
- **Unidades de enlace esperadas:** Seguridad de la Información, Ciberseguridad, Tecnología, Desarrollo Web, Infraestructura, Riesgos y Cumplimiento.

### 2.1 Contexto tecnológico

El portal está expuesto a Internet y sirve como punto de acceso hacia servicios informativos y transaccionales. La superficie de ataque puede incluir páginas web, formularios, recursos JavaScript, cookies, APIs públicas, mecanismos de redirección y enlaces hacia otros dominios o subdominios. La inclusión de cualquiera de estos elementos en las pruebas dependerá de la confirmación de propiedad y de su incorporación expresa al alcance autorizado.

### 2.2 Partes interesadas

| Parte interesada | Interés o responsabilidad |
|---|---|
| Alta dirección | Conocer la exposición y aceptar o tratar los riesgos relevantes. |
| Seguridad de la Información | Coordinar el alcance, atender alertas y validar recomendaciones. |
| Desarrollo / Proveedor web | Corregir defectos de código, dependencias y configuración. |
| Infraestructura / Operaciones | Corregir TLS, encabezados, servidor, CDN, WAF y monitoreo. |
| Riesgos y Cumplimiento | Evaluar impacto normativo y riesgo residual. |
| Comisión auditora | Ejecutar procedimientos, custodiar evidencia y emitir el informe. |

---

## III. DENOMINACIÓN DE LA MATERIA DE CONTROL

**Seguridad del portal web público de Interbank y efectividad de los controles frente a amenazas externas, con énfasis en comunicaciones cifradas, configuración HTTP, gestión de cookies y sesiones, validación de entradas, componentes de terceros y mecanismos de redirección, conforme a OWASP ASVS 4.0.3.**

La materia de control comprende la evaluación del diseño observable y la operación externa de los controles de seguridad aplicables al portal web público. No comprende la certificación integral de toda la plataforma ni la declaración de cumplimiento total de ASVS, debido a las limitaciones propias de una auditoría de caja negra.

---

## IV. ALCANCE

### 4.1 Alcance organizacional

La auditoría se enfocará en los responsables del portal institucional y, de ser necesario, en las áreas de Seguridad de la Información, Desarrollo Web e Infraestructura que administren los controles incluidos en la materia de control.

### 4.2 Alcance técnico

**Activo principal propuesto:**

- `https://interbank.pe` y sus rutas públicas, siempre que la titularidad y autorización sean confirmadas.

**Elementos incluidos:**

- Exposición HTTP y HTTPS del activo autorizado.
- Configuración TLS, certificado y redirección segura de HTTP a HTTPS.
- Encabezados HTTP de seguridad y políticas del navegador.
- Cookies emitidas por el activo y atributos de protección aplicables.
- Formularios públicos, parámetros y validaciones observables.
- Controles contra inyección, XSS, clickjacking, CSRF y redirección abierta, mediante pruebas controladas y no destructivas.
- Configuración CORS y métodos HTTP expuestos.
- Manejo externo de errores y divulgación de información técnica.
- Recursos JavaScript y componentes de terceros detectables desde el cliente.
- Protección contra automatización de formularios, evaluada por sus controles efectivos y no únicamente por la presencia de CAPTCHA.
- APIs públicas descubiertas desde el propio portal, solo después de su incorporación expresa al alcance.

**Elementos de inclusión condicionada:**

- Subdominios institucionales.
- Banca por Internet y otros servicios autenticados.
- APIs no publicadas.
- Infraestructura de nube, CDN, WAF o proveedores.

Estos elementos solo serán probados si figuran individualmente en la autorización y se proporcionan, cuando corresponda, cuentas de prueba y datos ficticios.

### 4.3 Alcance temporal

- **Periodo objeto de revisión:** Configuración y comportamiento observable entre el 12 y el 27 de octubre de 2026.
- **Periodo de ejecución estimado:** Del 12 al 30 de octubre de 2026.
- **Duración:** 15 días hábiles.

Las fechas podrán ajustarse a la aprobación formal del alcance y a las ventanas autorizadas por la entidad.

### 4.4 Tipo y enfoque de auditoría

- Auditoría de seguridad web externa.
- Enfoque inicial de caja negra y sin credenciales.
- Pruebas manuales y automatizadas controladas.
- Muestreo dirigido por riesgo.
- Validación ASVS Nivel 1 para controles comprobables externamente.
- Contraste de madurez con ASVS Nivel 2 cuando se proporcione evidencia interna suficiente.

### 4.5 Exclusiones y actividades prohibidas

- Denegación de servicio, estrés, agotamiento de recursos o pruebas de volumen.
- Fuerza bruta, credential stuffing o bloqueo deliberado de cuentas.
- Ingeniería social, phishing o contacto no autorizado con trabajadores o clientes.
- Instalación de malware, persistencia o ejecución de código destructivo.
- Modificación, eliminación o extracción de datos reales.
- Operaciones financieras reales o pruebas con información de clientes.
- Acceso físico, redes internas, aplicaciones móviles y cajeros automáticos.
- Activos de terceros, aunque estén enlazados desde el portal, salvo autorización independiente.
- Elusión agresiva de WAF, explotación posterior o movimiento lateral.

### 4.6 Limitaciones

- La ausencia de código fuente, configuraciones, arquitectura y entrevistas impide verificar totalmente ASVS Nivel 2 o 3.
- Los resultados representarán el estado observable durante la ventana de auditoría.
- Un control no observable externamente se clasificará como “No verificable con el alcance actual”, no como incumplido.
- La ausencia de una vulnerabilidad en la muestra no garantiza su inexistencia en rutas no examinadas.
- Los servicios dinámicos, CDN y WAF pueden producir respuestas diferentes según ubicación, hora o reputación de la fuente.

### 4.7 Reglas de compromiso

1. Utilizar exclusivamente direcciones IP de origen comunicadas a la entidad.
2. Ejecutar las pruebas dentro de las ventanas aprobadas.
3. Mantener una tasa de solicitudes conservadora y acordada.
4. Usar cuentas, datos y archivos de prueba suministrados o aprobados.
5. Detener inmediatamente la prueba ante degradación, exposición de datos reales o comportamiento inesperado.
6. Comunicar hallazgos críticos por el canal de emergencia sin esperar el informe final.
7. Cifrar las evidencias y restringir su acceso a la comisión auditora.
8. No conservar datos personales innecesarios; enmascarar cualquier dato incidental.
9. Registrar fecha, hora, origen, destino, solicitud, respuesta y responsable de cada prueba relevante.

---

## V. OBJETIVOS

### 5.1 Objetivo general

Evaluar la seguridad externa del portal web público de Interbank y la efectividad de los controles observables para prevenir, detectar o reducir riesgos de ataques web, tomando como criterio principal OWASP ASVS 4.0.3 y considerando las limitaciones de una revisión externa sin acceso interno.

### 5.2 Objetivos específicos

1. **OE1.** Determinar y validar la superficie de ataque autorizada, la exposición de servicios web y la seguridad de las comunicaciones mediante HTTPS/TLS.
2. **OE2.** Evaluar la configuración de seguridad HTTP, los encabezados de respuesta, CORS, los métodos permitidos y la divulgación de información técnica.
3. **OE3.** Verificar la protección de cookies, sesiones y, cuando el alcance lo permita, los mecanismos de autenticación y control de acceso.
4. **OE4.** Evaluar la validación de entradas, codificación de salidas, redirecciones, formularios y controles contra automatización y ataques del lado del cliente.
5. **OE5.** Identificar componentes y recursos de terceros expuestos, y evaluar sus controles de integridad, actualización y reducción de superficie de ataque.
6. **OE6.** Clasificar los riesgos identificados, determinar su impacto potencial y formular recomendaciones priorizadas, verificables y asignables a responsables.

---

## VI. PROCEDIMIENTOS DE AUDITORÍA

### 6.1 Metodología general

La auditoría se desarrollará en cinco fases:

1. **Preparación:** autorización, alcance, reglas de compromiso y canales de comunicación.
2. **Levantamiento:** inventario autorizado, arquitectura disponible y reconocimiento pasivo.
3. **Evaluación:** pruebas manuales y automatizadas no destructivas.
4. **Análisis:** validación manual, eliminación de falsos positivos y valoración del riesgo.
5. **Comunicación:** informe, recomendaciones, reunión de cierre y plan de seguimiento.

Las herramientas automatizadas se emplearán como apoyo y sus resultados no se considerarán hallazgos hasta ser reproducidos y validados por un auditor.

### 6.2 Cuadro n.° 1 - Procedimientos

| Objetivo | ID | Procedimiento | Evidencia esperada | Criterios principales | Responsable |
|---|---|---|---|---|---|
| OE1 | P01 | Obtener la autorización, confirmar titularidad y aprobar la lista exacta de dominios, rutas, APIs e IP autorizadas. | Carta de autorización, matriz de alcance y acta de inicio. | Reglas de compromiso; ASVS 1.1 como referencia documental. | JCA / SUP |
| OE1 | P02 | Elaborar el inventario de la superficie pública mediante fuentes autorizadas y reconocimiento pasivo. | Inventario fechado, capturas, resolución DNS y diagrama de superficie. | OWASP WSTG - Information Gathering. | A1 |
| OE1 | P03 | Verificar redirección HTTP a HTTPS, certificado, cadena de confianza, nombres, vigencia, versiones y cifrados TLS. | Resultados reproducibles por host y evidencia del certificado. | ASVS 9.1.1, 9.1.2, 9.1.3 y 9.2.1. | ESP / A1 |
| OE2 | P04 | Revisar encabezados de respuesta en una muestra de páginas, errores, formularios y APIs autorizadas. | Solicitudes y respuestas HTTP con fecha y URL. | ASVS 14.3.3 y 14.4.1-14.4.7. | A1 |
| OE2 | P05 | Verificar métodos HTTP permitidos, comportamiento de `Origin` y política CORS, sin generar operaciones destructivas. | Matriz método-ruta-respuesta y respuestas CORS. | ASVS 14.5.1-14.5.3. | A2 |
| OE2 | P06 | Evaluar el manejo de errores y la exposición de versiones, rutas, trazas, identificadores o información sensible. | Respuestas controladas y capturas enmascaradas. | ASVS 7.4.1; 14.3.2-14.3.3. | A2 |
| OE3 | P07 | Inventariar cookies por host, finalidad aparente y sensibilidad; verificar `Secure`, `HttpOnly`, `SameSite`, dominio, ruta, vigencia y prefijo aplicable. | Matriz de cookies y encabezados `Set-Cookie`. | ASVS 3.4.1-3.4.4. | A1 |
| OE3 | P08 | Si se proporcionan cuentas de prueba, verificar creación, renovación, cierre e invalidación de sesión sin afectar usuarios reales. | Flujos documentados con cuentas ficticias. | ASVS V3, requisitos aplicables al nivel autorizado. | A1 / A2 |
| OE3 | P09 | Si existe autorización autenticada, comprobar controles de acceso horizontal y vertical con objetos de prueba propios. | Casos de prueba, respuestas y trazabilidad de cuentas. | ASVS V4. | A1 / ESP |
| OE4 | P10 | Identificar entradas en URL, formularios, encabezados y cuerpos; verificar validación y codificación mediante cargas inocuas. | Matriz entrada-salida y evidencia reproducible. | ASVS 5.1, 5.2 y 5.3, según aplicabilidad. | A2 |
| OE4 | P11 | Evaluar XSS reflejado o basado en DOM, inyección HTML, parámetros manipulables y controles del navegador, sin persistir contenido. | Pruebas inocuas y análisis de contexto. | ASVS 5.3; 14.4.3. | A2 |
| OE4 | P12 | Verificar protección frente a clickjacking mediante CSP `frame-ancestors` y/o `X-Frame-Options`. | Encabezados y prueba local controlada de enmarcado. | ASVS 14.4.7. | A1 |
| OE4 | P13 | Identificar parámetros de redirección y comprobar que los destinos estén restringidos a una lista segura, sin dirigir a usuarios reales. | Flujo de redirección reproducible con dominio de prueba. | ASVS V5 y WSTG Client-side Testing. | A2 |
| OE4 | P14 | Revisar formularios públicos respecto de CSRF, límites de frecuencia, validación de servidor y controles efectivos contra automatización. | Solicitudes de prueba de baja frecuencia y comportamiento observado. | ASVS V3/V4/V5/V11, según función. | A1 / ESP |
| OE5 | P15 | Inventariar bibliotecas JavaScript, recursos CDN y componentes detectables; confirmar versión antes de asociar CVE. | Lista de componentes, fuente de versión, CVE y análisis de alcanzabilidad. | ASVS 14.2.1-14.2.6. | A2 |
| OE5 | P16 | Verificar integridad de subrecursos para activos externos y revisar la necesidad y confianza de terceros. | Etiquetas HTML, cabeceras y matriz de terceros. | ASVS 14.2.3-14.2.4. | A2 |
| OE6 | P17 | Validar manualmente cada resultado, descartar falsos positivos y documentar causa, condición, efecto y evidencia. | Papeles de trabajo revisados. | Normas de evidencia; matriz de riesgo del Anexo 1. | JCA / SUP |
| OE6 | P18 | Calificar impacto y probabilidad; utilizar CVSS 4.0 como apoyo técnico cuando corresponda y ajustar por contexto financiero. | Ficha de valoración y justificación. | Metodología del Anexo 1. | JCA / ESP |
| OE6 | P19 | Formular recomendaciones, responsables sugeridos, prioridad y criterio de cierre; emitir borrador para comentarios. | Borrador, hoja de comentarios y matriz de acciones. | ASVS 4.0.3 y buenas prácticas aplicables. | JCA |
| OE6 | P20 | Realizar reunión de cierre y emitir informe final. | Acta de cierre e informe aprobado. | Plan de auditoría. | SUP / JCA |

### 6.3 Tratamiento de evidencia

Cada papel de trabajo deberá contener:

- Identificador único.
- Objetivo y procedimiento asociado.
- Activo, URL o componente evaluado.
- Fecha, hora y zona horaria.
- Auditor responsable.
- Condición inicial y pasos de reproducción.
- Solicitud y respuesta relevantes, con secretos y datos personales enmascarados.
- Capturas o archivos de apoyo y su hash.
- Resultado: Conforme, No conforme, No aplicable o No verificable.
- Referencia ASVS y valoración del riesgo.
- Revisión del jefe de comisión.

### 6.4 Criterios de confirmación de hallazgos

Un resultado se considerará hallazgo cuando:

1. Sea reproducible dentro del alcance autorizado.
2. Exista evidencia suficiente y trazable.
3. Se identifique el criterio incumplido.
4. Se explique el riesgo realista y el activo afectado.
5. Se descarte razonablemente un falso positivo.

La ausencia visible de CAPTCHA, la falta de un encabezado aislado o una versión aparentemente antigua no serán calificadas automáticamente como vulnerabilidad; se evaluará el control compensatorio, la sensibilidad del activo y la posibilidad de abuso.

---

## VII. PLAZO DE LA AUDITORÍA Y CRONOGRAMA

### 7.1 Cronograma general

| Etapa | Fecha de inicio | Fecha de finalización | Días hábiles | Producto |
|---|---:|---:|---:|---|
| Planificación | 12/10/2026 | 14/10/2026 | 3 | Alcance, autorización, reglas de compromiso y programa de trabajo. |
| Ejecución | 15/10/2026 | 27/10/2026 | 9 | Papeles de trabajo, evidencias y matriz preliminar de resultados. |
| Elaboración y aprobación del informe | 28/10/2026 | 30/10/2026 | 3 | Borrador, comentarios, reunión de cierre e informe final. |
| **Total** | **12/10/2026** | **30/10/2026** | **15** | |

### 7.2 Hitos de control

- 12/10/2026: Acta de inicio y autorización confirmada.
- 14/10/2026: Alcance congelado y programa aprobado.
- 21/10/2026: Revisión intermedia de evidencias.
- 27/10/2026: Cierre de pruebas.
- 28/10/2026: Comunicación inmediata de cualquier riesgo crítico pendiente.
- 29/10/2026: Recepción de comentarios al borrador.
- 30/10/2026: Emisión del informe final.

Si la autorización no está disponible el 12/10/2026, las fechas de ejecución activa quedarán suspendidas y solo continuará el trabajo documental académico.

---

## VIII. CRITERIOS DE AUDITORÍA

### 8.1 Criterio principal

- **OWASP Application Security Verification Standard 4.0.3**, especialmente:
  - V3 Gestión de sesiones.
  - V4 Control de acceso, cuando exista alcance autenticado.
  - V5 Validación, desinfección y codificación.
  - V7 Manejo y registro de errores, en lo externamente observable.
  - V8 Protección de datos del lado del cliente.
  - V9 Comunicación.
  - V11 Lógica de negocio, según los flujos públicos autorizados.
  - V13 API y servicios web, cuando se incluyan APIs.
  - V14 Configuración, dependencias y encabezados HTTP.

### 8.2 Criterios complementarios

- OWASP Web Security Testing Guide, para técnicas y casos de prueba.
- OWASP Top 10, para comunicar categorías generales de riesgo.
- OWASP Cheat Sheet Series, como orientación de remediación.
- Políticas internas, estándares de desarrollo seguro, arquitectura y procedimientos de la entidad, si son proporcionados.
- Legislación peruana de protección de datos personales y disposiciones sectoriales aplicables, previa validación por el área legal o de cumplimiento.
- CVSS 4.0 como referencia para severidad técnica, complementada por el impacto de negocio.

### 8.3 Nivel ASVS adoptado

| Nivel | Uso en esta auditoría | Justificación |
|---|---|---|
| ASVS Nivel 1 | Base verificable de la revisión externa. | Es el nivel completamente comprobable mediante pruebas de penetración de caja negra. |
| ASVS Nivel 2 | Referencia objetivo y evaluación condicionada. | Es adecuado para aplicaciones que manejan datos sensibles, pero requiere evidencia interna adicional. |
| ASVS Nivel 3 | Fuera del alcance de certificación. | Exige análisis profundo de arquitectura, código y controles de alta garantía. |

El informe no afirmará que el portal “cumple ASVS Nivel 1 o 2” salvo que se evalúe la totalidad de los requisitos aplicables del nivel, se documenten las exclusiones y se disponga de evidencia suficiente.

### 8.4 Escala de conclusión por control

| Resultado | Definición |
|---|---|
| Conforme | La evidencia demuestra que el control aplicable opera según el criterio. |
| No conforme | Existe evidencia reproducible de incumplimiento o inefectividad. |
| Parcialmente conforme | El control existe, pero su cobertura o efectividad es incompleta. |
| No aplicable | El requisito no corresponde al componente o función examinada; debe justificarse. |
| No verificable | El alcance o la evidencia disponible no permiten concluir. |

---

## IX. INFORMACIÓN ADMINISTRATIVA

### IX.1 Comisión auditora

**Cuadro n.° 2 - Comisión auditora**

| Cargo | Nombres y apellidos | Perfil requerido | Planificación | Ejecución | Informe | Total |
|---|---|---|---:|---:|---:|---:|
| Supervisor (SUP) | [Completar] | Auditor TI / seguridad con experiencia de supervisión. | 1 día | 2 días | 1 día | 4 días |
| Jefe de Comisión (JCA) | [Completar] | Auditor de sistemas o especialista en ciberseguridad. | 3 días | 8 días | 4 días | 15 días |
| Auditor 1 (A1) | [Completar] | Especialista en seguridad web y redes. | 3 días | 8 días | 4 días | 15 días |
| Auditor 2 (A2) | [Completar] | Analista de aplicaciones y pruebas web. | 2 días | 6 días | 2 días | 10 días |
| Experto (ESP) | [Completar] | Especialista TLS, arquitectura y riesgo. | 1 día | 3 días | 1 día | 5 días |

### 9.1.1 Responsabilidades

- **Supervisor:** aprobar el plan, resolver controversias, revisar calidad y aprobar el informe.
- **Jefe de Comisión:** dirigir el trabajo, coordinar con la entidad, revisar evidencia y consolidar resultados.
- **Auditores:** ejecutar procedimientos, custodiar evidencias y documentar papeles de trabajo.
- **Experto:** apoyar pruebas especializadas y validar la valoración técnica de riesgos complejos.

### IX.2 Costos directos estimados

Los siguientes importes son referenciales para fines académicos y asumen trabajo remoto, sin pasajes ni viáticos.

**Cuadro n.° 3 - Costo de horas-hombre y asignaciones**

| N.° | Miembro | Tarifa referencial por hora | Días | Horas | Costo H/H (S/) | Asignación (S/) | Pasajes / viáticos (S/) | Costo total (S/) |
|---:|---|---:|---:|---:|---:|---:|---:|---:|
| 1 | Supervisor | 120 | 4 | 32 | 3,840 | 0 | 0 | 3,840 |
| 2 | Jefe de Comisión | 100 | 15 | 120 | 12,000 | 0 | 0 | 12,000 |
| 3 | Auditor 1 | 80 | 15 | 120 | 9,600 | 0 | 0 | 9,600 |
| 4 | Auditor 2 | 80 | 10 | 80 | 6,400 | 0 | 0 | 6,400 |
| 5 | Experto | 130 | 5 | 40 | 5,200 | 0 | 0 | 5,200 |
|  | **Total** |  | **49 jornadas-persona** | **392** | **37,040** | **0** | **0** | **37,040** |

**Supuestos:** jornada de 8 horas; herramientas disponibles mediante licencias institucionales o alternativas autorizadas; infraestructura de prueba provista por la organización o la universidad.

---

## X. DOCUMENTO A EMITIR

Como resultado se emitirá un **Informe de Auditoría de Seguridad Web Externa**, compuesto por:

1. Resumen ejecutivo.
2. Antecedentes, objetivo, alcance y limitaciones.
3. Metodología y criterios aplicados.
4. Resumen de cobertura de procedimientos.
5. Hallazgos confirmados y priorizados.
6. Para cada hallazgo: condición, criterio, causa probable, efecto, evidencia, activos afectados, severidad y recomendación.
7. Observaciones no confirmadas o no verificables.
8. Conclusión general de auditoría.
9. Plan de acción propuesto con responsables y plazos.
10. Anexos técnicos y matriz de trazabilidad.

Los hallazgos críticos se comunicarán inmediatamente por el canal acordado. El informe técnico tendrá distribución restringida y no incorporará secretos, datos personales completos ni cargas que permitan explotación directa innecesaria.

La revalidación posterior a la remediación se considerará una actividad separada. Su objetivo será verificar el cierre de los hallazgos sin ampliar el alcance original.

---

**Lima**, **7 de octubre de 2026**

| Aprobación | Firma |
|---|---|
| **[Nombres y apellidos]** - Supervisor | ____________________ |
| **[Nombres y apellidos]** - Jefe de Comisión | ____________________ |
| **[Nombres y apellidos]** - Responsable académico / organizacional | ____________________ |

---

# ANEXOS

## Anexo 1: Matriz de riesgos de TI

### A1.1 Método de valoración

- **Probabilidad (P):** 1 Rara, 2 Improbable, 3 Posible, 4 Probable, 5 Casi segura.
- **Impacto (I):** 1 Insignificante, 2 Menor, 3 Moderado, 4 Mayor, 5 Crítico.
- **Puntaje:** `P x I`.
- **Nivel:** Bajo 1-4; Medio 5-9; Alto 10-16; Crítico 17-25.

La valoración inicial es una hipótesis de planificación. El nivel final se determinará únicamente después de validar cada condición y considerar controles compensatorios.

| ID | Riesgo de auditoría | Causa posible | Impacto potencial | P | I | Nivel preliminar | Controles a verificar |
|---|---|---|---|---:|---:|---|---|
| R01 | Intercepción o degradación de comunicaciones. | Configuración TLS débil o redirección insegura. | Exposición o alteración de comunicaciones. | 3 | 5 | Alto (15) | TLS moderno, certificado confiable, HSTS y redirección segura. |
| R02 | Ejecución de contenido no confiable en el navegador. | Validación o codificación insuficiente; CSP débil. | XSS, robo de sesión o suplantación de contenido. | 3 | 5 | Alto (15) | Validación, codificación contextual y CSP. |
| R03 | Exposición o abuso de sesiones. | Cookies sensibles sin atributos adecuados. | Secuestro o uso indebido de sesión. | 3 | 5 | Alto (15) | `Secure`, `HttpOnly`, `SameSite`, alcance y expiración. |
| R04 | Clickjacking. | Ausencia o mala configuración de `frame-ancestors` / `X-Frame-Options`. | Acciones inducidas o engaño al usuario. | 3 | 3 | Medio (9) | Política anti-framing y prueba controlada. |
| R05 | Redirección hacia sitios maliciosos. | Parámetro de destino no restringido. | Phishing y pérdida de confianza. | 3 | 4 | Alto (12) | Lista permitida, rutas relativas y validación de destinos. |
| R06 | Abuso automatizado de formularios. | Falta de límites y detección de automatización. | Spam, fraude, consumo de recursos o enumeración. | 3 | 4 | Alto (12) | Rate limiting, detección de bots, validación de servidor y monitoreo. |
| R07 | Explotación de componente vulnerable. | Dependencia desactualizada o no inventariada. | Compromiso del cliente o de la aplicación. | 3 | 5 | Alto (15) | Inventario, versión confirmada, CVE, SRI y proceso de actualización. |
| R08 | Acceso desde orígenes no confiables. | Configuración CORS permisiva. | Lectura o envío indebido de información. | 3 | 4 | Alto (12) | Lista de orígenes, credenciales y rechazo de `null`. |
| R09 | Divulgación de información técnica. | Errores detallados o banners de versión. | Facilitación de ataques posteriores. | 3 | 2 | Medio (6) | Manejo genérico de errores y minimización de banners. |
| R10 | Afectación del servicio durante la auditoría. | Pruebas excesivas o alcance ambiguo. | Interrupción operativa y reputacional. | 2 | 5 | Alto (10) | Autorización, límites de tasa, monitoreo y criterio de suspensión. |

## Anexo 2: Mapeo del proceso de auditoría

```text
Necesidad académica
        |
        v
Autorización y reglas de compromiso ---- No autorizada ----> Solo análisis documental
        |
        | Autorizada
        v
Inventario y reconocimiento pasivo
        |
        v
Pruebas controladas y no destructivas
        |
        v
Validación manual y descarte de falsos positivos
        |
        v
Valoración de riesgo y comunicación urgente
        |
        v
Informe, plan de acción y cierre
        |
        v
Revalidación posterior, si se contrata y autoriza
```

## Anexo 3: Lista de normativa y referencias aplicables

| Referencia | Aplicación en el plan |
|---|---|
| OWASP ASVS 4.0.3 | Criterios de verificación y trazabilidad de controles. |
| OWASP Web Security Testing Guide | Diseño de procedimientos de pruebas web. |
| OWASP Top 10 | Comunicación de categorías generales de riesgo. |
| OWASP Cheat Sheet Series | Orientación técnica para recomendaciones. |
| CVSS 4.0 | Apoyo para la valoración técnica de vulnerabilidades. |
| Políticas internas de Interbank | Criterio organizacional, si son entregadas y autorizadas. |
| Normativa peruana aplicable | Validación de obligaciones de privacidad, seguridad y sector financiero por Legal/Cumplimiento. |

## Anexo 4: Instrumentos de recolección de evidencia

### A4.1 Lista de comprobación mínima

| Control | Conforme | No conforme | N/A | No verificable | Evidencia |
|---|:---:|:---:|:---:|:---:|---|
| Inventario y alcance formalmente aprobados |  |  |  |  |  |
| Uso obligatorio de HTTPS |  |  |  |  |  |
| TLS y cifrados aceptables |  |  |  |  |  |
| Certificado válido y confiable |  |  |  |  |  |
| HSTS correctamente aplicado |  |  |  |  |  |
| CSP apropiada al contenido |  |  |  |  |  |
| Protección contra framing |  |  |  |  |  |
| `X-Content-Type-Options: nosniff` |  |  |  |  |  |
| `Referrer-Policy` apropiada |  |  |  |  |  |
| Cookies sensibles con atributos adecuados |  |  |  |  |  |
| CORS restringido |  |  |  |  |  |
| Métodos HTTP limitados |  |  |  |  |  |
| Errores sin información sensible |  |  |  |  |  |
| Validación y codificación de entradas/salidas |  |  |  |  |  |
| Redirecciones restringidas |  |  |  |  |  |
| Controles efectivos contra automatización |  |  |  |  |  |
| Componentes identificados y actualizados |  |  |  |  |  |
| Recursos externos con SRI cuando corresponda |  |  |  |  |  |

### A4.2 Formato de hallazgo

| Campo | Contenido requerido |
|---|---|
| Código y título | Identificador único y descripción breve. |
| Activo afectado | Host, ruta, componente o función. |
| Condición | Hecho comprobado. |
| Criterio | ASVS, política o requisito aplicable. |
| Causa | Razón probable, validada con el responsable cuando sea posible. |
| Efecto / riesgo | Escenario realista de amenaza e impacto. |
| Evidencia | Pasos, solicitud/respuesta y capturas enmascaradas. |
| Severidad | Probabilidad, impacto, puntaje y justificación. |
| Recomendación | Acción concreta y criterio de cierre. |
| Responsable / plazo | Propietario sugerido y fecha objetivo. |

## Anexo 5: Matriz de trazabilidad de objetivos, procedimientos y evidencias

| Objetivo | Procedimientos | Evidencias principales | Fuente | Responsable |
|---|---|---|---|---|
| OE1 | P01-P03 | Autorización, inventario, DNS, TLS y certificados. | Entidad y observación externa autorizada. | JCA / A1 / ESP |
| OE2 | P04-P06 | Respuestas HTTP, CORS, métodos y errores. | Portal y APIs autorizadas. | A1 / A2 |
| OE3 | P07-P09 | Matriz de cookies y flujos de sesión/acceso. | Navegador, proxy y cuentas de prueba. | A1 / A2 / ESP |
| OE4 | P10-P14 | Matriz de entradas, formularios, redirecciones y controles del cliente. | Portal público y datos ficticios. | A1 / A2 / ESP |
| OE5 | P15-P16 | Inventario de componentes, CVE confirmados, CDN y SRI. | Recursos del cliente y documentación entregada. | A2 |
| OE6 | P17-P20 | Papeles revisados, matriz de riesgos, informe y acta de cierre. | Comisión auditora y responsables de la entidad. | JCA / SUP |

## Anexo 6: Cronograma detallado por actividad y responsable

| Fecha | Actividad | Responsable | Producto / indicador |
|---|---|---|---|
| 12/10/2026 | Reunión de inicio, autorización y canales de emergencia. | SUP / JCA | Acta firmada y 100 % de contactos confirmados. |
| 13/10/2026 | Confirmación de activos, exclusiones y ventanas. | JCA / A1 | Matriz de alcance aprobada. |
| 14/10/2026 | Preparación de casos, datos ficticios y control de evidencia. | Equipo | Programa de trabajo aprobado. |
| 15/10/2026 | Inventario y reconocimiento pasivo. | A1 | Inventario inicial completo. |
| 16/10/2026 | Evaluación TLS y certificados. | ESP / A1 | Matriz TLS por host. |
| 19/10/2026 | Encabezados HTTP y configuración del navegador. | A1 | Muestra de respuestas evaluada. |
| 20/10/2026 | Cookies, CORS y métodos HTTP. | A1 / A2 | Matrices de cookies y CORS. |
| 21/10/2026 | Revisión intermedia y validación de seguridad operacional. | JCA / SUP | Acta de avance y ajustes aprobados. |
| 22/10/2026 | Formularios, entradas, salidas y redirecciones. | A2 | Casos de prueba ejecutados. |
| 23/10/2026 | Controles del cliente, clickjacking y automatización. | A1 / ESP | Evidencias reproducibles. |
| 26/10/2026 | Componentes, terceros, versiones y SRI. | A2 | Inventario y análisis de alcanzabilidad. |
| 27/10/2026 | Reprueba, descarte de falsos positivos y cierre de pruebas. | Equipo | 100 % de resultados revisados. |
| 28/10/2026 | Valoración de riesgos y elaboración del borrador. | JCA / ESP | Borrador y matriz de acciones. |
| 29/10/2026 | Control de calidad y recepción de comentarios. | SUP / JCA | Comentarios resueltos. |
| 30/10/2026 | Reunión de cierre y emisión del informe final. | SUP / JCA | Informe final y acta de cierre. |

---

## Referencias documentales utilizadas para elaborar el plan

1. Caso académico “Auditoría de Seguridad Web Externa basada en OWASP”.
2. Esquema académico “Plan de Auditoría de Tecnologías de la Información”.
3. OWASP Application Security Verification Standard 4.0.3, edición en español.

