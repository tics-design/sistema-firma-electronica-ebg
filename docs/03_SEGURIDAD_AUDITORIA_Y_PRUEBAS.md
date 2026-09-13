# Seguridad, auditoría y pruebas

## Seguridad

- Spring Security para autenticación/autorización.
- JWT para sesiones de acceso; JWT no constituye por sí mismo la firma electrónica.
- Contraseñas con algoritmo de hashing adaptativo seguro; nunca texto plano.
- JWT con expiración y validación de firma.
- HTTPS obligatorio en producción.
- Control de acceso por roles y permisos.
- OTP independiente del JWT para cada firma.
- OTP con expiración, máximo de intentos y bloqueo de reutilización.
- No registrar contraseñas, OTP en claro ni secretos en logs.
- Secretos por variables de entorno/gestor de secretos, nunca en Git.
- Protección contra acceso directo a archivos.
- Validación de cargas PDF, tamaño y contenido.
- Protección CSRF donde corresponda al flujo basado en cookies/sesión web.
- Auditoría de operaciones sensibles.

## Auditoría y evidencia

Registrar como mínimo:

`DOCUMENTO_CREADO`, `DOCUMENTO_CARGADO`, `DOCUMENTO_VISUALIZADO`, `DOCUMENTO_DESCARGADO`, `SOLICITUD_CREADA`, `SOLICITUD_ENVIADA`, `FIRMA_SOLICITADA`, `OTP_GENERADO`, `OTP_VALIDADO`, `OTP_INCORRECTO`, `FIRMA_REALIZADA`, `FIRMA_RECHAZADA`, `DOCUMENTO_RECHAZADO`, `DOCUMENTO_CANCELADO`, `DOCUMENTO_FINALIZADO`, `DOCUMENTO_VERIFICADO`.

Cuando aplique, registrar usuario, fecha/hora, IP, user-agent, documento, solicitud, acción, resultado y hash. La auditoría debe ser inmutable para usuarios normales y las operaciones administrativas sensibles deben quedar también auditadas.

## Pruebas obligatorias

### Unitarias

Servicios de usuarios, estados, permisos, hash, OTP, firma, verificación y reglas de negocio.

### Integración

Spring Boot + PostgreSQL real de pruebas. Repositorios, migraciones, transacciones y relaciones.

### Seguridad

Login válido/inválido, expiración JWT, roles, acceso denegado, OTP correcto/incorrecto/expirado/reutilizado, límite de intentos, archivos no autorizados y ataques básicos de path traversal.

### Flujo de firma

- Un firmante.
- Varios firmantes.
- Orden incorrecto.
- Firma fuera de turno.
- Rechazo.
- Cancelación.
- Documento ya finalizado.
- OTP incorrecto.
- OTP expirado.
- OTP reutilizado.
- Concurrencia sobre una misma solicitud.

### Integridad y verificación

Hash original/final, código válido/inválido, QR válido/inválido y documento alterado.

### No funcionales

Pruebas de concurrencia, rendimiento básico, carga de archivos, backup/restore y pruebas responsive en desktop/móvil.

Una funcionalidad no se considera terminada si no tiene cobertura de sus escenarios positivos, negativos y de seguridad aplicables.
