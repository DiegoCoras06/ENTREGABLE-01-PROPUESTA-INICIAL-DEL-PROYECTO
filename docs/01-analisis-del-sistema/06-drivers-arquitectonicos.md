# Drivers arquitectónicos

## Sistema de Gestión del Proceso de Admisión

| ID   | Driver arquitectónico                                                                                         | Origen                | ¿Por qué influye en la arquitectura?                                                         |
| ---- | ------------------------------------------------------------------------------------------------------------- | --------------------- | -------------------------------------------------------------------------------------------- |
| DA01 | El sistema debe soportar un incremento importante de postulantes durante los periodos de inscripción.         | AC03 - Escalabilidad  | Influye en la estrategia de escalamiento y en la distribución de la carga del sistema.       |
| DA02 | El sistema debe mantener tiempos de respuesta adecuados durante una alta concurrencia.                        | AC01 - Rendimiento    | Influye en el procesamiento de solicitudes, comunicación entre componentes y acceso a datos. |
| DA03 | El sistema debe proteger los datos personales y académicos de los postulantes.                                | AC04 - Seguridad      | Influye en la autenticación, autorización, protección de datos y control de acceso.          |
| DA04 | El sistema debe mantener la integridad de la información de las inscripciones.                                | AC06 - Integridad     | Influye en el diseño de la base de datos, validaciones y control de transacciones.           |
| DA05 | El sistema debe utilizar una API REST para la comunicación entre la aplicación web y el backend.              | RC03 - API REST       | Condiciona la forma en que se comunican la presentación y los servicios del sistema.         |
| DA06 | El sistema debe integrarse con servicios externos de validación de identidad y pagos.                         | RC05, RC06            | Condiciona la comunicación y los mecanismos de integración con sistemas externos.            |
| DA07 | El sistema debe permitir modificar y mantener sus módulos sin afectar innecesariamente otras funcionalidades. | AC05 - Mantenibilidad | Influye en la separación de responsabilidades y organización de los módulos.                 |
