# Kairós Tech

**Equipo académico de UTEC · Uruguay 🇺🇾**

Kairós Tech es un equipo de desarrollo de software formado en el marco de la **Licenciatura en Tecnologías de la Información de UTEC**.

Actualmente desarrollamos **Curupí**, una solución tecnológica orientada a complementar y modernizar procesos de gestión documental, comprobantes, trazabilidad y firma electrónica.

## 🌿 Curupí

Curupí surge como proyecto de grado con el objetivo de facilitar procesos administrativos mediante una aplicación móvil y una arquitectura de servicios desacoplados.

La plataforma trabaja sobre áreas como:

* 📄 Gestión de documentos y comprobantes.
* 📷 Digitalización y análisis de comprobantes.
* 🔎 Extracción de información mediante OCR.
* ✍️ Procesos de firma electrónica.
* 🔐 Identidad, autenticación y autorización.
* 🧾 Trazabilidad y auditoría de operaciones.
* 🤖 Asistencia basada en inteligencia artificial.
* 📱 Experiencia mobile para los distintos perfiles de usuario.

## 🏗️ Arquitectura

Curupí se desarrolla utilizando una arquitectura distribuida basada en microservicios y comunicación orientada a eventos.

```text
Mobile App
    │
    ▼
API Gateway
    │
    ├── Identity
    ├── Invoice Extractor
    ├── File Service
    ├── Signature Service
    ├── Audit Service
    └── otros servicios
              │
              ▼
            Kafka
```

El proyecto busca mantener una separación clara de responsabilidades entre servicios, contratos reproducibles y una infraestructura preparada para evolucionar progresivamente.

## 🛠️ Tecnologías

### Backend

* Python
* FastAPI
* Kafka
* PostgreSQL
* Redis
* Protobuf

### Mobile

* React Native
* Expo
* TypeScript

### Infraestructura

* Docker
* Docker Compose
* Traefik
* GitHub Actions
* Grafana
* Loki
* Tempo

### Procesamiento e IA

* OCR
* Modelos de visión
* Large Language Models
* Procesamiento automatizado de documentos

## 🔐 Ingeniería y seguridad

El desarrollo de Curupí contempla prácticas relacionadas con:

* CI/CD.
* Tests automatizados.
* Gestión segura de secretos.
* Contenedores reproducibles.
* Observabilidad.
* Autenticación y autorización.
* Auditoría.
* Versionado de dependencias y contratos.
* Separación de redes y servicios internos.

## 🎓 Contexto

Kairós Tech nace como equipo académico de la **Universidad Tecnológica del Uruguay (UTEC)**.

Curupí se encuentra actualmente en desarrollo y forma parte de nuestro proceso de formación, investigación y aplicación práctica de ingeniería de software.

---

<p align="center">
  <strong>Kairós Tech 🇺🇾</strong><br>
  Software engineering · Distributed systems · Mobile · AI
</p>
