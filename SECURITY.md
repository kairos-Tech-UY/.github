# Política de seguridad

La seguridad es parte del desarrollo de los proyectos de Kairós Tech. Agradecemos los reportes responsables de vulnerabilidades que puedan afectar nuestros repositorios, servicios, infraestructura o datos.

## Reportar una vulnerabilidad

No publiques vulnerabilidades, credenciales, tokens, claves, datos sensibles ni detalles de explotación en un issue público, discusión o Pull Request.

Si el repositorio tiene habilitado **Private vulnerability reporting**, utilizá la opción **Security → Report a vulnerability** de GitHub.

Si esa opción no está disponible, contactá de forma privada a los maintainers de Kairós Tech por un canal acordado con el equipo antes de compartir detalles técnicos sensibles.

Incluí, cuando sea posible:

- Repositorio o componente afectado.
- Descripción del problema.
- Condiciones necesarias para reproducirlo.
- Impacto potencial.
- Evidencia mínima necesaria para verificarlo.
- Versión, commit o ambiente afectado.
- Medidas de mitigación conocidas, si existen.

No incluyas secretos reales ni datos personales innecesarios en el reporte.

## Alcance

Son especialmente relevantes los problemas relacionados con:

- Autenticación y autorización.
- Gestión de sesiones y tokens.
- Cifrado y manejo de claves.
- Exposición de secretos o credenciales.
- APIs y controles de acceso.
- Kafka y mensajería entre servicios.
- Procesamiento y almacenamiento de archivos.
- PostgreSQL, Redis y otros servicios de datos.
- Docker, Traefik, redes y configuración de infraestructura.
- CI/CD, GitHub Actions y cadena de suministro de dependencias.
- Dependencias compartidas como `kt-curupi-commons`.
- Exposición o modificación no autorizada de información.

## Investigación responsable

Para evitar impactos sobre los sistemas y datos:

- No realices pruebas destructivas.
- No provoques indisponibilidad deliberadamente.
- No accedas, modifiques o elimines datos que no sean necesarios para demostrar el problema.
- No intentes persistir acceso luego de confirmar una vulnerabilidad.
- No publiques detalles antes de que el equipo haya tenido oportunidad razonable de evaluar y corregir el problema.

## Respuesta

Los reportes serán revisados por el equipo de Kairós Tech. La prioridad y el tiempo de resolución dependerán del impacto, la explotabilidad y el componente afectado.

Cuando corresponda, el equipo coordinará de forma privada la validación, mitigación y eventual divulgación del problema.

## Secretos expuestos

Si detectás una credencial, token, clave privada u otro secreto expuesto, reportalo inmediatamente por un canal privado. No reutilices, pruebes ni difundas el secreto más allá de lo estrictamente necesario para identificar la exposición.
