# Contribuir a Kairós Tech

Gracias por contribuir a los proyectos de Kairós Tech.

Este documento define pautas generales para los repositorios de la organización. Si un repositorio contiene instrucciones propias, esas instrucciones tienen prioridad.

## Flujo de trabajo

1. Trabajá desde la rama base definida por el repositorio (`dev` o `main`, según corresponda).
2. Creá una rama corta y enfocada para el cambio.
3. Implementá solamente los cambios necesarios para el alcance de la tarea.
4. Ejecutá los tests, linters y validaciones relevantes antes de abrir el Pull Request.
5. Abrí un Pull Request utilizando la plantilla de la organización.
6. Esperá la revisión y los checks de CI requeridos antes de mergear.

## Nombres de ramas

Preferimos nombres descriptivos y consistentes:

```text
feature/<descripcion>
fix/<descripcion>
refactor/<descripcion>
chore/<descripcion>
docs/<descripcion>
```

Ejemplos:

```text
feature/receipt-analysis
fix/kafka-timeout
chore/update-commons
```

## Pull Requests

Cada Pull Request debe:

- Tener un alcance claro y acotado.
- Explicar qué cambia y por qué.
- Incluir cómo se validó el cambio.
- Mantener los tests existentes funcionando.
- Agregar o actualizar tests cuando el comportamiento cambie.
- Documentar cambios de configuración, variables de entorno o pasos operativos.
- Identificar impactos sobre APIs, Kafka, Protobuf, base de datos, infraestructura o servicios consumidores.
- Evitar cambios no relacionados con el objetivo del PR.

No deben incluirse secretos, tokens, contraseñas, claves privadas, archivos `.env` reales ni datos sensibles en commits, issues, logs o Pull Requests.

## Compatibilidad entre servicios

Curupí utiliza múltiples servicios y contratos compartidos. Antes de modificar una interfaz entre componentes, verificá sus consumidores.

Prestá especial atención a cambios en:

- APIs y endpoints.
- Eventos y topics de Kafka.
- Contratos Protobuf.
- Esquemas de base de datos.
- `kt-curupi-commons`.
- Autenticación, autorización y cifrado.
- Configuración de Docker, redes, Traefik y despliegue.

Los cambios incompatibles deben documentar claramente el impacto, el orden de despliegue y cualquier migración necesaria.

## Tests y calidad

Ejecutá las herramientas definidas por cada repositorio. No desactives tests, linters, validaciones de seguridad o checks de CI únicamente para conseguir un pipeline verde.

Si una validación no puede ejecutarse localmente, indicalo en el Pull Request junto con el motivo.

## Commits

Preferimos commits pequeños y descriptivos. Ejemplos:

```text
feat: add receipt validation
fix: handle kafka response timeout
refactor: simplify auth middleware
chore: update commons dependency
```

No reescribas historia compartida ni hagas force-push sobre ramas protegidas salvo que exista una razón explícita y acordada por el equipo.

## Seguridad

Si encontrás una vulnerabilidad o un problema que pueda exponer credenciales, datos o infraestructura, no lo publiques en un issue abierto. Seguí las instrucciones de [SECURITY.md](SECURITY.md).
