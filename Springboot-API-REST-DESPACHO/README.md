# Backend Despachos – Repo

Este repositorio contiene el backend de **Despachos** del proyecto DevOps P3.

El proyecto Spring Boot completo se encuentra en la carpeta `Springboot-API-REST-DESPACHO`.  
Dentro de esa carpeta se incluye:

- `pom.xml` y carpeta `src/`
- `application.properties` configurado con variables de entorno (`DB_ENDPOINT`, `DB_PORT`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`)
- `Dockerfile` para construir la imagen del servicio
- `README.md` con instrucciones de ejecución local y en Docker
- carpeta `.github/workflows` con el pipeline `deploy.yml`