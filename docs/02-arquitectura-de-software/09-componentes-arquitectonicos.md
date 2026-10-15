flowchart TB
    P["👤 Postulante<br/>Realiza inscripción y consultas"]
    AD["👤 Personal de Admisión<br/>Gestiona procesos"]
    ADM["👤 Administrador<br/>Configura y supervisa"]

    WEB["Aplicación Web<br/>Interfaz para postulantes y personal UNSCH"]
    EDGE["Amazon CloudFront + S3<br/>Distribución web mediante HTTPS"]
    API["Amazon API Gateway<br/>API REST · HTTPS · JSON"]

    subgraph BACKEND["API Admisión UNSCH · AWS Lambda · Monolito Modular"]
        direction TB
        REST["Controladores REST<br/>Validación · Autenticación · Autorización"]

        subgraph MODULOS["Módulos de negocio · Clean Architecture"]
            direction TB
            M01["Convocatorias<br/>Periodos y cronogramas"]
            M02["Usuarios<br/>Registro y validación DNI"]
            M03["Inscripción Ordinaria<br/>Registro de postulaciones"]
            M04["Inscripción Exonerados<br/>Modalidades especiales"]

            M05["Pagos<br/>Órdenes y confirmaciones"]
            M06["Expedientes<br/>Documentos y evaluación"]
            M07["Exámenes<br/>Programación"]
            M08["Sedes y Aulas<br/>Asignación de ambientes"]

            M09["Resultados<br/>Calificaciones y publicación"]
            M10["Chatbot IA<br/>Orientación y seguimiento"]
            M11["Notificaciones<br/>Correos y avisos"]
            M12["Reportes<br/>Estadísticas"]

            M13["Seguridad<br/>Roles y permisos"]
            M14["Configuración<br/>Parámetros e integraciones"]
        end

        ADAPT["Infraestructura y adaptadores<br/>Repositorios · Integraciones · Persistencia"]
    end

    REDIS["Caché Redis<br/>Amazon ElastiCache"]
    RENIEC["RENIEC<br/>Validación de identidad"]
    PAYMENT["Pasarela de pagos<br/>Procesamiento seguro"]
    OPENROUTER["OpenRouter API<br/>Inteligencia artificial"]
    EMAIL["Servicio de correo / SMS<br/>Notificaciones"]

    DB[("Amazon RDS PostgreSQL<br/>Datos de admisión")]
    S3[("Amazon S3<br/>Documentos y fichas PDF")]
    SQS["Amazon SQS<br/>Procesamiento asíncrono"]
    CLOUD["Amazon CloudWatch<br/>Logs y monitoreo"]

    P --> WEB
    AD --> WEB
    ADM --> WEB
    WEB --> EDGE
    EDGE -->|"HTTPS"| API
    API -->|"Invoca AWS Lambda"| REST

    REST --> M01
    REST --> M02
    REST --> M03
    REST --> M04
    REST --> M05
    REST --> M06
    REST --> M07
    REST --> M08
    REST --> M09
    REST --> M10
    REST --> M11
    REST --> M12
    REST --> M13
    REST --> M14

    M01 --> ADAPT
    M02 --> ADAPT
    M03 --> ADAPT
    M04 --> ADAPT
    M05 --> ADAPT
    M06 --> ADAPT
    M07 --> ADAPT
    M08 --> ADAPT
    M09 --> ADAPT
    M10 --> ADAPT
    M11 --> ADAPT
    M12 --> ADAPT
    M13 --> ADAPT
    M14 --> ADAPT

    ADAPT -->|"SQL"| DB
    ADAPT -->|"Caché"| REDIS
    ADAPT -->|"Archivos"| S3
    ADAPT -->|"Mensajes"| SQS
    ADAPT -->|"HTTPS REST"| RENIEC
    ADAPT -->|"HTTPS REST"| PAYMENT
    ADAPT -->|"HTTPS REST"| OPENROUTER
    ADAPT -->|"HTTPS"| EMAIL
    BACKEND -.-> CLOUD

    classDef actor fill:#244478,color:#fff,stroke:#244478
    classDef container fill:#3d6cba,color:#fff,stroke:#28539b
    classDef component fill:#9fc1ed,color:#102b50,stroke:#6a95cc
    classDef external fill:#929292,color:#fff,stroke:#777
    classDef database fill:#3d6cba,color:#fff,stroke:#28539b

    class P,AD,ADM actor
    class WEB,EDGE,API,REST container
    class M01,M02,M03,M04,M05,M06,M07,M08,M09,M10,M11,M12,M13,M14,ADAPT component
    class RENIEC,PAYMENT,OPENROUTER,EMAIL external
    class DB,S3,REDIS,SQS,CLOUD database

    style BACKEND fill:#ffffff,stroke:#777,stroke-width:1.5px,stroke-dasharray:6 4
    style MODULOS fill:#f8fbff,stroke:#aaa,stroke-dasharray:4 3