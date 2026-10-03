# Contribuir a Kairós Tech

Este documento define el flujo común para los repositorios de Kairós Tech. Las instrucciones específicas de cada repositorio pueden ampliar estos requisitos, pero no deben reducir los controles de revisión, CI y seguridad aquí establecidos.

## Flujo de trabajo

1. Partí de la rama base indicada por el repositorio (`dev` o `main`) y actualizala.
2. Creá una rama corta y enfocada. Usá los prefijos `feat/`, `fix/`, `docs/`, `refactor/`, `test/`, `build/`, `ci/` o `chore/`.
3. Realizá un cambio acotado y registrá commits con Conventional Commits.
4. Ejecutá las pruebas, linters y validaciones pertinentes.
5. Abrí un Pull Request con la plantilla del repositorio. El título debe seguir Conventional Commits, porque se usa para generar versiones y notas de publicación.
6. Esperá al menos una aprobación independiente y todos los checks obligatorios de CI.
7. Integrá mediante el método permitido por el repositorio. No integres cambios con checks fallidos ni uses bypass salvo el procedimiento de emergencia documentado.

## Ramas y commits

Nombres de rama descriptivos en minúsculas y con guiones, por ejemplo:

```text
feat/receipt-analysis
fix/kafka-timeout
ci/release-please
```

Formato de commit y título de PR:

```text
<tipo>(<alcance opcional>): <descripción breve en imperativo>
```

Tipos comunes: `feat`, `fix`, `docs`, `refactor`, `test`, `build`, `ci`, `chore` y `perf`. Indicá cambios incompatibles con `!` (por ejemplo, `feat(api)!: ...`) y explicá `BREAKING CHANGE:` en el cuerpo cuando corresponda. Usá inglés para identificadores técnicos si el repositorio ya lo hace; mantené el mensaje concreto y sin punto final.

Ejemplos:

```text
feat(invoices): add receipt validation
fix(kafka): handle response timeout
 docs(adr): document schema ownership
```

Eliminá el espacio inicial del tercer ejemplo al escribirlo: el formato correcto es `docs(adr): document schema ownership`.

## Pull Requests y revisión

Cada PR debe explicar el problema, el cambio y su validación; indicar riesgos, migraciones, compatibilidad y orden de despliegue. Los cambios de APIs, eventos, Protobuf, esquemas, secretos o infraestructura deben identificar a sus consumidores y solicitar revisión de sus responsables. Se requiere una aprobación de una persona distinta de quien abrió el PR. La aprobación no reemplaza CI.

No mezcles refactors amplios con cambios funcionales sin justificación. No incluyas secretos, credenciales, tokens, claves privadas, `.env` reales ni datos sensibles en commits, incidencias, logs o PRs.

## CI, integración y publicación

Los workflows deben validar PRs hacia la rama base y volver a ejecutar las validaciones pertinentes luego de integrar en esa rama. Cada repositorio define checks adecuados a su tecnología: formato y análisis estático, pruebas unitarias e integración, validación de contratos, construcción de artefactos e inspecciones de seguridad cuando correspondan. Los nombres de jobs deben ser únicos y estables para poder protegerlos como checks requeridos.

Release Please debe ejecutarse al integrar commits convencionales en la rama estable configurada para el repositorio. Debe abrir o actualizar un PR de release, generar changelog y versión a partir de los commits, y publicar la versión solo al integrar dicho PR. No se debe crear un release manual paralelo salvo procedimiento documentado. Antes de adoptarlo, confirmar el tipo de proyecto, el nombre y esquema de tags, la rama de publicación y la estrategia para paquetes internos.

## Compatibilidad entre servicios

Antes de modificar interfaces, verificá los consumidores y documentá la secuencia de despliegue. Prestá atención a APIs, topics Kafka, mensajes Protobuf, esquemas PostgreSQL, `kt-curupi-commons`, autenticación, cifrado y configuración de infraestructura. Los contratos compartidos deben evolucionar de forma compatible cuando sea posible; los cambios incompatibles requieren estrategia de migración y compatibilidad explícitas.

Las decisiones que afecten límites de servicio, fuentes de verdad, contratos o migraciones se registran como ADR con contexto, decisión, alternativas y consecuencias. La guía de [proceso de desarrollo y arquitectura](DEVELOPMENT_PROCESS.md) describe el formato y los puntos abiertos detectados en la auditoría técnica.

## Calidad y seguridad

Usá las herramientas definidas por cada repositorio. No desactives pruebas, linters, validaciones de seguridad ni checks requeridos para obtener un pipeline verde. Si una validación no puede ejecutarse localmente, indicalo en el PR y apoyate en CI. Los secretos deben provenir del gestor aprobado por ambiente; los valores de desarrollo nunca deben ser válidos en ambientes compartidos.

Si encontrás una vulnerabilidad, seguí [SECURITY.md](SECURITY.md) y no la publiques en un issue abierto.
