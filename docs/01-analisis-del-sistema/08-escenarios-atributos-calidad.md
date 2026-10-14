# 08. Escenarios de Atributos de Calidad

## Sistema Integral de Gestión del Proceso de Admisión – UNSCH

Los escenarios de calidad describen cómo debe responder el sistema ante situaciones específicas, considerando los atributos de calidad, drivers arquitectónicos y decisiones arquitectónicas establecidas.

| ID | Atributo de calidad | Escenario de calidad | Respuesta esperada | Medida de respuesta |
|---|---|---|---|---|
| EC01 | Rendimiento | Múltiples postulantes realizan inscripciones y consultas simultáneamente. | El sistema procesa las solicitudes utilizando AWS Lambda, PostgreSQL y Redis. | El 95% de las solicitudes habituales responde en menos de 3 segundos, sin incluir demoras externas. |
| EC02 | Disponibilidad | Los postulantes acceden al sistema durante periodos críticos de inscripción y publicación de resultados. | La infraestructura mantiene operativa la plataforma y detecta interrupciones. | Disponibilidad objetivo del 99.9% durante los periodos críticos establecidos. |
| EC03 | Escalabilidad | Aumenta significativamente la cantidad de postulantes concurrentes. | AWS Lambda incrementa las instancias de ejecución y se controla el acceso a PostgreSQL. | El sistema soporta la carga objetivo definida mediante pruebas sin superar los tiempos de respuesta establecidos. |
| EC04 | Seguridad | Un usuario intenta acceder a información o funcionalidades sin autorización. | El sistema verifica la autenticación y los permisos antes de permitir el acceso. | El 100% de los intentos no autorizados evaluados en las pruebas debe ser rechazado. |
| EC05 | Mantenibilidad | Se requiere modificar una funcionalidad de inscripción o pagos. | La arquitectura modular y Clean Architecture permiten realizar cambios sin afectar otros módulos. | Las pruebas automatizadas de los módulos relacionados deben ejecutarse satisfactoriamente. |
| EC06 | Integridad | Dos solicitudes intentan registrar simultáneamente la misma inscripción o confirmar un pago duplicado. | PostgreSQL aplica restricciones, transacciones e idempotencia para mantener la consistencia. | No se generan registros duplicados ni transacciones inconsistentes. |
| EC07 | Usabilidad | Un postulante realiza su inscripción desde una computadora o dispositivo móvil. | El sistema presenta formularios claros, validaciones y mensajes de orientación. | Al menos el 90% de los usuarios participantes completa las tareas principales sin asistencia durante las pruebas de usabilidad. |
| EC08 | Interoperabilidad | El sistema necesita comunicarse con RENIEC, la pasarela de pagos u OpenRouter API. | Los adaptadores de infraestructura gestionan las solicitudes mediante interfaces seguras. | Las integraciones responden correctamente en las pruebas y gestionan los errores sin comprometer las operaciones. |
| EC09 | Confiabilidad | La pasarela de pagos o un servicio externo presenta una interrupción temporal. | El sistema conserva el estado de la operación y aplica reintentos controlados cuando corresponde. | No se pierden operaciones confirmadas ni se duplican transacciones. |
| EC10 | Auditabilidad | Un usuario autorizado modifica un expediente, pago o resultado. | El sistema registra la operación, el usuario responsable, la fecha y los cambios relevantes. | El 100% de las operaciones críticas definidas debe contar con registros de auditoría. |
| EC11 | Privacidad | Un postulante consulta información personal mediante el chatbot inteligente. | El backend verifica la identidad y proporciona a OpenRouter únicamente la información necesaria. | No se expone información personal de otros postulantes ni credenciales de servicios externos. |
| EC12 | Recuperabilidad | Ocurre una falla en la base de datos o una pérdida accidental de información. | El sistema utiliza los mecanismos de respaldo y restauración de Amazon RDS. | La restauración cumple los objetivos de recuperación definidos y validados mediante pruebas. |
| EC13 | Accesibilidad | Un postulante con necesidades de accesibilidad utiliza los formularios de inscripción. | La interfaz permite navegación mediante teclado, etiquetas accesibles y mensajes comprensibles. | Cumplimiento de los criterios aplicables de WCAG 2.2 nivel AA, verificado mediante pruebas. |
| EC14 | Observabilidad | Se produce un error en AWS Lambda, PostgreSQL o una integración externa. | Amazon CloudWatch registra errores, métricas y genera alertas configuradas. | Los errores críticos se registran y generan alertas dentro de los 5 minutos posteriores a su detección. |
| EC15 | Modularidad | Se incorpora una nueva funcionalidad o se modifica un módulo existente. | El monolito modular mantiene responsabilidades separadas y dependencias controladas. | Los cambios respetan los contratos internos y no generan dependencias prohibidas entre módulos. |

## Escenarios de Calidad Prioritarios

| Prioridad | Escenario | Justificación |
|---|---|---|
| Alta | EC01 - Rendimiento | Evitar lentitud durante inscripciones y consultas masivas. |
| Alta | EC02 - Disponibilidad | Mantener operativo el sistema durante las etapas críticas. |
| Alta | EC03 - Escalabilidad | Soportar incrementos de postulantes concurrentes. |
| Alta | EC04 - Seguridad | Proteger la información personal y académica. |
| Alta | EC06 - Integridad | Evitar inconsistencias en inscripciones, pagos y resultados. |
| Alta | EC09 - Confiabilidad | Garantizar operaciones seguras ante fallas externas. |
| Alta | EC11 - Privacidad | Proteger los datos utilizados por el chatbot con OpenRouter API. |
| Media | EC05 - Mantenibilidad | Facilitar modificaciones mediante Clean Architecture. |
| Media | EC07 - Usabilidad | Simplificar la inscripción de los postulantes. |
| Media | EC08 - Interoperabilidad | Garantizar la comunicación con servicios externos. |
| Media | EC10 - Auditabilidad | Mantener la trazabilidad de operaciones críticas. |
| Media | EC12 - Recuperabilidad | Permitir la restauración de información ante fallas. |
| Media | EC13 - Accesibilidad | Facilitar el acceso a todos los postulantes. |
| Media | EC14 - Observabilidad | Detectar errores y supervisar la infraestructura. |
| Media | EC15 - Modularidad | Mantener una estructura organizada y desacoplada. |

## Consideraciones Arquitectónicas

Los escenarios de calidad serán evaluados considerando las siguientes decisiones arquitectónicas:

- Arquitectura: Monolito Modular por Capas.
- Enfoque: Clean Architecture.
- Backend: AWS Lambda.
- Comunicación: API REST mediante HTTPS.
- Base de datos: Amazon RDS PostgreSQL.
- Caché: Redis mediante Amazon ElastiCache.
- Almacenamiento: Amazon S3.
- Inteligencia artificial: OpenRouter API.
- Seguridad: Autenticación, autorización, cifrado y AWS Secrets Manager.
- Monitoreo: Amazon CloudWatch.
- Escalabilidad: AWS Lambda y control de conexiones mediante RDS Proxy.
- Integraciones: RENIEC, pasarela de pagos y servicios de notificaciones.

## Resumen

- Total de escenarios de calidad: 15.
- Escenarios de prioridad alta: 7.
- Escenarios de prioridad media: 8.
- Arquitectura seleccionada: Monolito Modular por Capas.
- Enfoque arquitectónico: Clean Architecture.
- Infraestructura: Amazon Web Services (AWS).

**Nota:** Las medidas de respuesta representan objetivos propuestos para el proyecto y deberán validarse mediante pruebas de rendimiento, seguridad, usabilidad, integración y recuperación.