# Arquitectura y modelo de datos

## Arquitectura

Monolito MVC desplegado inicialmente en VPS propio:

`Internet -> Nginx/HTTPS -> Spring Boot + Thymeleaf -> PostgreSQL + almacenamiento de documentos`

Tecnologías obligatorias del MVP:

- Java 21
- Spring Boot 3.x
- Spring Security
- JWT
- Thymeleaf
- Spring Data JPA/Hibernate
- PostgreSQL
- Flyway
- SHA-256

La separación frontend/backend no forma parte del MVP. Los endpoints internos necesarios pueden existir dentro del mismo monolito.

## Paquetes base

```text
com.ebg.firma
├── config
├── security
├── usuario
├── rol
├── documento
├── firma
├── otp
├── auditoria
├── verificacion
└── almacenamiento
```

Se permite subdividir paquetes cuando mejore cohesión, pero no romper el monolito.

## Persistencia

PostgreSQL relacional, con integridad referencial, PK/FK, UNIQUE, NOT NULL y CHECK. El modelo debe diseñarse y documentarse hasta 4NF, evitando dependencias multivaluadas innecesarias.

Entidades conceptuales mínimas:

- USUARIO
- CARGO
- ROL
- USUARIO_ROL
- DOCUMENTO
- TIPO_DOCUMENTO
- DOCUMENTO_VERSION
- SOLICITUD_FIRMA
- FIRMANTE_DOCUMENTO
- FIRMA
- OTP
- EVIDENCIA_FIRMA
- EVENTO_AUDITORIA
- IDENTIFICADOR_VERIFICACION

No almacenar el PDF como BLOB en PostgreSQL en el diseño inicial. Guardar metadatos, hash y referencia segura al almacenamiento de archivos.

Los originales nunca se sobrescriben. Las versiones/finales se manejan de forma explícita.

## UUID

Preferir UUID como identificadores internos de entidades, salvo que exista una razón técnica documentada para otra estrategia.

## Migraciones

Toda modificación del esquema debe hacerse mediante Flyway. No usar `ddl-auto=create` ni depender de cambios automáticos de Hibernate en producción.

## Seguridad de archivos

Los nombres y rutas físicas no deben ser controlados directamente por el usuario. Validar tipo/tamaño, generar nombres internos seguros, impedir path traversal y autorizar cada descarga mediante servicio.
