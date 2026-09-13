# Especificación funcional — Sistema de Firma Electrónica EBG

## 1. Objetivo

Desarrollar un sistema interno de firma electrónica para EBG que permita gestionar y firmar documentos internos de forma digital, reduciendo impresión, firma manual y escaneo, y conservando evidencia verificable de cada actuación.

## 2. Alcance MVP

El sistema será para empleados de EBG y documentos internos. Debe funcionar en computador y móvil mediante interfaz web responsive.

Tipos iniciales: ACTA, AUTORIZACION, SOLICITUD, ENTREGA_EQUIPO, RECURSOS_HUMANOS y OTRO.

La fuente actual de empleados es la plataforma Integrates. La primera versión tendrá administración propia de empleados; la integración/sincronización con Integrates queda preparada para una fase posterior.

## 3. Roles

- ADMINISTRADOR: usuarios, roles, documentos, configuración y auditoría.
- SOLICITANTE: crea documentos y solicitudes de firma.
- FIRMANTE: revisa y firma documentos asignados.
- CONSULTA: consulta documentos autorizados.
- AUDITOR: consulta documentos, evidencias y trazabilidad sin modificarla.

Un empleado puede tener varios roles. Cargo y rol del sistema son conceptos independientes.

## 4. Flujo de firma

1. Solicitante crea el proceso.
2. Carga el PDF original.
3. Sistema calcula SHA-256 y conserva el original sin sobrescribirlo.
4. Selecciona uno o varios firmantes y define el orden.
5. Envía la solicitud.
6. El firmante recibe la notificación.
7. El firmante visualiza el documento.
8. Puede rechazar indicando motivo o continuar.
9. Para firmar debe autenticarse y validar un OTP específico para esa firma.
10. El sistema registra evidencia: usuario, fecha/hora, IP, agente/dispositivo, documento, solicitud, hash y método de autenticación.
11. Se procesa el siguiente firmante según el orden.
12. Cuando todos firman, el documento queda FINALIZADO/FIRMADO y se genera el documento final.
13. Se genera identificador único de verificación y QR.

## 5. Estados

BORRADOR, PENDIENTE_DE_FIRMA, EN_PROCESO, RECHAZADO, FIRMADO y CANCELADO.

Las transiciones válidas deben estar centralizadas en dominio/servicio y cubiertas por pruebas.

## 6. OTP

Cada firma requiere un OTP nuevo e independiente del JWT. Debe expirar, no poder reutilizarse y limitar intentos fallidos. El OTP no se almacena en texto plano.

El canal inicial de entrega podrá ser correo corporativo; debe quedar abstraído para permitir otro proveedor posteriormente.

## 7. Verificación

El documento final tendrá un código único, por ejemplo `SIGN-2026-000125`, y QR. La verificación por código o QR debe calcular/validar la integridad mediante SHA-256. Un hash que no coincida debe mostrar el documento como alterado/no íntegro.

La consulta pública debe minimizar datos personales; la consulta autenticada puede mostrar información adicional según permisos.

## 8. Requisitos funcionales

RF-001 Registrar empleados EBG.
RF-002 Actualizar empleados.
RF-003 Desactivar empleados sin borrar historial.
RF-004 Gestionar roles múltiples.
RF-005 Iniciar sesión.
RF-006 Generar JWT.
RF-007 Validar acceso.
RF-008 Autorizar por rol.
RF-009 Cerrar sesión/expirar sesión.
RF-010 Crear proceso de firma.
RF-011 Cargar PDF.
RF-012 Gestionar metadatos del documento.
RF-013 Calcular SHA-256.
RF-014 Preservar documento original.
RF-015 Crear solicitud de firma.
RF-016 Seleccionar múltiples firmantes.
RF-017 Definir orden.
RF-018 Enviar solicitud.
RF-019 Notificar firmante.
RF-020 Gestionar estados.
RF-021 Visualizar documento.
RF-022 Descargar documento si está autorizado y registrar auditoría.
RF-023 Continuar proceso después de revisar.
RF-024 Rechazar con motivo y evidencia.
RF-025 Solicitar OTP.
RF-026 Entregar OTP mediante proveedor abstraído.
RF-027 Validar OTP.
RF-028 Expirar OTP.
RF-029 Impedir reutilización.
RF-030 Limitar intentos.
RF-031 Ejecutar firma electrónica después de autenticación y OTP.
RF-032 Asociar inequívocamente la firma al usuario.
RF-033 Registrar fecha/hora exacta.
RF-034 Registrar contexto técnico.
RF-035 Generar evidencia de firma.
RF-036 Procesar firmantes secuencialmente.
RF-037 Registrar cada firma independientemente.
RF-038 Finalizar cuando todos completen.
RF-039 Generar documento final firmado.
RF-040 Asociar evidencias.
RF-041 Generar identificador único.
RF-042 Generar QR.
RF-043 Registrar eventos de auditoría.
RF-044 Registrar responsable.
RF-045 Registrar timestamp.
RF-046 Registrar información técnica.
RF-047 Consultar historial completo.
RF-048 Proteger la auditoría contra modificación normal.
RF-049 Verificar por código.
RF-050 Verificar por QR.
RF-051 Mostrar resultado de verificación.
RF-052 Verificar integridad por hash.
RF-053 Detectar alteraciones.
RF-054 Bandeja de pendientes.
RF-055 Consultar documentos firmados.
RF-056 Consultar documentos creados.
RF-057 Filtrar por estado, fecha, tipo, usuario e identificador respetando permisos.
RF-058 Administrar usuarios.
RF-059 Administrar roles.
RF-060 Administrar tipos de documento.
RF-061 Consultar auditoría según permisos.
RF-062 Preparar integración futura.
RF-063 Sincronizar empleados con Integrates en fase futura.
RF-064 Respaldar BD, originales, finales y evidencias.
RF-065 Recuperar desde respaldo.
