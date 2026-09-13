# Reglas para Codex y plan de implementación

## Reglas obligatorias

1. Leer toda la documentación de `docs/` antes de implementar una funcionalidad.
2. No cambiar Java, Spring Boot, Thymeleaf, PostgreSQL, JWT ni la arquitectura monolítica sin una decisión arquitectónica documentada.
3. No inventar requisitos de negocio cuando falte una definición; documentar la decisión pendiente y usar una implementación segura y reversible.
4. Cada cambio funcional debe incluir pruebas.
5. No marcar una tarea como terminada si fallan pruebas o compilación.
6. No guardar secretos en el repositorio.
7. No almacenar contraseñas ni OTP en texto plano.
8. No sobrescribir documentos originales.
9. No permitir que un usuario descargue o consulte documentos sin autorización.
10. Toda acción sensible debe generar auditoría.
11. Todas las migraciones de BD deben usar Flyway.
12. Mantener separación por dominio y responsabilidades claras dentro del monolito.
13. Usar transacciones en operaciones que modifiquen el estado del proceso de firma.
14. Validar concurrencia para impedir doble firma o avance incorrecto del flujo.
15. No eliminar evidencia histórica por operaciones administrativas normales.
16. Revisar seguridad antes de considerar terminada cada fase.

## Fases

### Fase 1 — Fundación

Spring Boot, estructura de paquetes, Thymeleaf, configuración por entorno, PostgreSQL, Flyway, manejo global de errores, logging y base de seguridad.

Criterio: compila, arranca y ejecuta migraciones sobre PostgreSQL.

### Fase 2 — Usuarios, cargos y roles

CRUD de empleados, cargos, roles múltiples, activación/desactivación, login, JWT y autorización.

Criterio: un usuario activo puede autenticarse y acceder únicamente a funciones permitidas por sus roles.

### Fase 3 — Documentos

Tipos, carga de PDF, metadatos, almacenamiento seguro, SHA-256, versiones y preservación del original.

Criterio: se puede cargar un PDF autorizado, obtener su hash y recuperar el archivo sin exponer rutas físicas.

### Fase 4 — Solicitudes de firma

Creación de solicitudes, selección de firmantes, orden, estados, notificaciones y bandejas.

Criterio: una solicitud con varios firmantes solo permite actuar al firmante cuyo turno esté activo.

### Fase 5 — OTP y firma

OTP por firma, expiración, intentos, uso único, firma electrónica, evidencia y registro técnico.

Criterio: la firma solo se ejecuta con usuario autorizado + OTP válido y queda evidencia completa.

### Fase 6 — Auditoría

Eventos de trazabilidad, consulta por administradores/auditores y protección contra modificación normal.

Criterio: todas las acciones sensibles tienen trazabilidad consultable.

### Fase 7 — Documento final y verificación

Generación/consolidación del final, identificador único, QR, portal de verificación y comprobación SHA-256.

Criterio: un documento final puede verificarse por código y QR y una alteración es detectada.

### Fase 8 — Pruebas y endurecimiento

Unitarias, integración, seguridad, flujo completo, concurrencia, rendimiento básico, archivos, backup/restore y responsive.

Criterio: suite automatizada aprobada y escenarios críticos cubiertos.

### Fase 9 — VPS

Nginx, HTTPS, firewall, variables de entorno/secretos, PostgreSQL, almacenamiento, backups, logs, monitoreo y recuperación.

Criterio: despliegue reproducible y procedimiento de restauración probado.

## Definition of Done

Una tarea está terminada únicamente cuando:

- el código compila;
- las migraciones funcionan;
- las pruebas relevantes pasan;
- no existen secretos en Git;
- existe validación de autorización;
- las acciones sensibles están auditadas;
- la documentación se actualizó si cambió el comportamiento o arquitectura;
- se revisaron escenarios negativos y de seguridad;
- el cambio es coherente con la arquitectura del sistema.
