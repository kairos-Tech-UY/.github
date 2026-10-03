# Proceso de desarrollo y arquitectura de Curupí

Esta guía convierte los hallazgos de la auditoría transversal de los repositorios de Curupí en criterios de desarrollo verificables. Describe el proceso objetivo; no certifica por sí sola que todos los repositorios o ambientes ya cumplan esos criterios. El estado real debe comprobarse en cada workflow, configuración de rama y despliegue.

## Ciclo de cambio

1. **Definir alcance y ownership.** Identificar el servicio dueño del comportamiento, sus consumidores y los contratos o datos afectados.
2. **Registrar la decisión.** Para decisiones arquitectónicas relevantes, agregar un ADR con identificador, estado (`propuesto`, `aceptado`, `obsoleto`), contexto, decisión, alternativas y consecuencias. Los puntos abiertos de la auditoría deben permanecer `propuestos` hasta que el equipo los resuelva.
3. **Implementar en rama enfocada.** Usar nombres y commits convencionales según `CONTRIBUTING.md`. Mantener cambios pequeños y revisables.
4. **Validar localmente y en CI.** Ejecutar controles del repositorio y validar PRs contra su rama base. Tras el merge, ejecutar el workflow de integración en la rama destino y publicar imágenes/artefactos solo mediante los procesos autorizados.
5. **Revisar e integrar.** Requerir una aprobación independiente, checks exitosos y resolución de conversaciones. Usar squash merge con título Conventional Commit cuando esa sea la estrategia del repositorio.
6. **Publicar.** Release Please propone la versión y el changelog a partir de commits convencionales en la rama configurada. La integración del PR de release es el punto de publicación; no se asume despliegue a producción.

## Controles de ramas

Para cada rama base se recomienda protección que exija Pull Request, una aprobación independiente, checks de CI estables y exitosos, conversaciones resueltas, historial sin force-push y sin borrado accidental. Los administradores deben quedar sujetos a las reglas siempre que la plataforma y la política operativa lo permitan. Los checks requeridos solo se fijan luego de observar sus nombres exactos en ejecuciones exitosas del repositorio. Las excepciones deben ser temporales, justificadas y auditables.

## Criterios transversales de ingeniería

- El API Gateway es el único borde HTTP funcional para la aplicación móvil; los servicios internos se comunican mediante los contratos acordados. Healthchecks y métricas internas son interfaces operativas.
- Los mensajes Kafka deben tener identificadores de evento y correlación, timestamps, emisor, tipo y payload tipado. Los request/reply requieren timeout, correlación, idempotencia y errores normalizados. Los cambios Protobuf deben analizar compatibilidad con productores y consumidores.
- PostgreSQL es la fuente de verdad transaccional declarada y MongoDB se reserva para proyecciones de lectura. Los cambios deben tener dueño, migración compatible y comportamiento idempotente.
- MinIO almacena binarios; la metadata funcional pertenece a PostgreSQL. Los mecanismos temporales de compatibilidad deben tener plan y criterio de retiro.
- `kt-curupi-commons` contiene contratos e infraestructura reutilizable. Cada actualización debe documentar compatibilidad, versión y coordinación de adopción entre servicios.
- Secretos se obtienen desde el gestor definido por ambiente. No deben existir credenciales compartidas, claves por defecto ni secretos reales en archivos versionados, imágenes o logs.
- Integraciones institucionales y externas se encapsulan tras puertos/adaptadores. Los resultados obtenidos en sandbox no demuestran por sí solos disponibilidad ni aceptación productiva.

## ADR requeridos o recomendados por la auditoría

La auditoría identificó discrepancias que requieren decisión formal. Las recomendaciones siguientes no deben presentarse como decisiones aceptadas hasta contar con aprobación y evidencia de implementación:

| ADR | Tema | Recomendación a evaluar | Verificación necesaria |
|---|---|---|---|
| ADR-001 | Fuente de verdad de auditoría | PostgreSQL append-only como fuente canónica y MongoDB como proyección de lectura | Contrastar con persistencia desplegada y definir retención, consultas y migración |
| ADR-002 | Autoridad de esquema PostgreSQL | `kt-curupi-database-core` como dueño único de migraciones; infraestructura consume artefactos publicados | Inventariar migraciones activas y coordinar la transferencia sin duplicar aplicación |
| ADR-003 | Esquema de comprobantes | Consolidar `core.comprobantes` y `public.comprobantes` con migración compatible | Alinear Extractor, Invoices, ORM, consultas y datos existentes |
| ADR-004 | Metadata de archivos | `core.stored_files` como metadata canónica; retirar sidecar JSON tras migración | Verificar integridad, lecturas históricas, rollback y eliminación segura |

La auditoría también recomienda catálogo de eventos, pruebas de contrato y E2E, completar la validación GURI con build mobile actualizado, revisar endpoints obsoletos y verificar credenciales/defaults en ambientes compartidos. Cada acción debe registrarse con responsable, repositorio, evidencia y estado.

## Evidencia de cumplimiento

Por repositorio, conservar la configuración del workflow, ejecuciones de CI de PR y rama destino, configuración efectiva de protección, revisión registrada, changelog y release. Las capturas de dashboards son evidencia puntual del rango temporal mostrado: no bastan para afirmar disponibilidad, SLO, throughput o rendimiento sin intervalo, consulta, entorno y metodología documentados.
