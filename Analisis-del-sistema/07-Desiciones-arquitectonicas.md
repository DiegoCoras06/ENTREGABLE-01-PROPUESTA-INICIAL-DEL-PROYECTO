
# 5. Decisiones Arquitectónicas (ADR)

## Sistema de Gestión del Proceso de Admisión

Las decisiones arquitectónicas se establecen a partir de los siete drivers arquitectónicos (DA01–DA07), considerando el estilo de microservicios Serverless en AWS, el enfoque Clean Architecture, la base de datos PostgreSQL, el uso de caché Redis y la comunicación segura mediante API REST.

| **IDENTIFICACIÓN** | **Decisión arquitectónica** | **Conductor relacionado** | **Justificación** | **Resultado** |
|---|---|---|---|---|
| **ADR-001** | **Arquitectura de microservicios Serverless** | DA01 - Escalabilidad<br>DA07 - Mantenibilidad | Organizar las funcionalidades en servicios independientes, permitiendo su escalamiento y mantenimiento sin afectar innecesariamente otros componentes. | Microservicios de **Usuarios, Postulantes, Inscripciones, Evaluación, Documentos, Pagos y Notificaciones**, implementados mediante AWS Lambda. |
| **ADR-002** | **Clean Architecture (Arquitectura Limpia)** | DA07 - Mantenibilidad | Separar las reglas de negocio de los detalles tecnológicos para reducir el acoplamiento y facilitar las pruebas y modificaciones. | Cada microservicio organizado en **Dominio, Aplicación, Interfaces e Infraestructura**. |
| **ADR-003** | **Estrategia de caché mediante Redis** | DA02 - Rendimiento | Reducir las consultas repetitivas a PostgreSQL y mejorar los tiempos de respuesta durante periodos de alta concurrencia. | **Amazon ElastiCache con Redis** para modalidades, programas de estudio y consultas frecuentes. |
| **ADR-004** | **Persistencia mediante PostgreSQL** | DA04 - Integridad | Garantizar la consistencia de la información mediante restricciones, validaciones y transacciones, manteniendo la propiedad de datos por microservicio. | **Amazon RDS PostgreSQL**, con separación lógica de datos por servicio. |
| **ADR-005** | **Comunicación mediante API REST** | DA05 - API REST<br>DA03 - Seguridad | Establecer una comunicación estandarizada y segura entre la aplicación web y los microservicios. | **Amazon API Gateway** con endpoints REST y comunicación HTTPS. |
| **ADR-006** | **Integración mediante interfaces y adaptadores** | DA06 - Integraciones<br>DA07 - Mantenibilidad | Desacoplar los casos de uso de los proveedores externos de validación de identidad y procesamiento de pagos. | **Contratos de integración y adaptadores** para servicios de identidad y pasarelas de pago. |
| **ADR-007** | **Seguridad mediante HTTPS y control de acceso** | DA03 - Seguridad | Proteger los datos personales y académicos mediante comunicaciones cifradas, autenticación y autorización. | **AWS Certificate Manager, HTTPS, autenticación y control de acceso basado en roles**. |
| **ADR-008** | **Comunicación asíncrona mediante eventos** | DA01 - Escalabilidad<br>DA02 - Rendimiento<br>DA07 - Mantenibilidad | Reducir el acoplamiento entre microservicios y permitir el procesamiento independiente de operaciones complementarias. | **Amazon EventBridge** para eventos de inscripción, pagos y notificaciones. |
| **ADR-009** | **Despliegue Serverless en AWS** | DA01 - Escalabilidad<br>DA07 - Mantenibilidad | Ejecutar y desplegar los microservicios sin administrar servidores de aplicaciones ni infraestructura de contenedores. | **AWS Lambda**, con despliegue independiente de funciones, sin Docker ni Kubernetes. |
| **ADR-010** | **Distribución web mediante dominio propio y CDN** | DA02 - Rendimiento<br>DA03 - Seguridad | Optimizar la distribución del portal web y proporcionar acceso seguro mediante un dominio propio. | **Amazon Route 53, CloudFront, Amazon S3 y certificados HTTPS**. |

