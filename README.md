# Sistema de Firma Electrónica EBG

Sistema interno de firma electrónica para EBG.

## Objetivo

Permitir la gestión y firma electrónica de documentos internos, reduciendo la impresión, firma manual y escaneo, y conservando trazabilidad y evidencia verificable.

## Arquitectura inicial

- Java + Spring Boot
- Monolito MVC con Thymeleaf
- Spring Security + JWT
- PostgreSQL
- JPA/Hibernate
- Migraciones de base de datos
- Almacenamiento de documentos fuera de la base de datos, con metadatos y referencias en PostgreSQL
- SHA-256 para integridad
- OTP independiente de JWT para autorizar cada firma
- Nginx + HTTPS en producción sobre VPS propio

## Alcance MVP

- Empleados EBG y roles múltiples
- Autenticación y autorización
- Gestión de documentos PDF
- Solicitudes de firma con múltiples firmantes y orden configurable
- OTP por firma
- Evidencia y trazabilidad completa
- Documento original y documento final preservados
- Código único de verificación y QR
- Portal de verificación e integridad por SHA-256
- Pruebas unitarias, integración, seguridad y flujo completo

## Documentación

La especificación del sistema está en `docs/`. Las decisiones de arquitectura deben respetarse y cualquier cambio debe quedar documentado.

## Regla de desarrollo

No considerar una funcionalidad terminada sin pruebas positivas, negativas y de seguridad cuando aplique. No almacenar contraseñas ni OTP en texto plano. No sobrescribir documentos originales ni evidencia de auditoría.
