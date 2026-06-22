# Backend Despachos – Spring Boot API REST

Servicio backend desarrollado con **Spring Boot** que expone una API REST para la gestión de despachos.  
Complementa al backend de Ventas dentro del proyecto DevOps P3 y se conecta a una base de datos MySQL.

## Requisitos

- Java 17
- Maven
- Base de datos MySQL accesible desde el servicio

## Configuración de la aplicación

El archivo `src/main/resources/application.properties` está parametrizado con variables de entorno y define un puerto propio:

```properties
spring.application.name=Springboot-API-REST
server.port=8081

spring.datasource.url=jdbc:mysql://${DB_ENDPOINT}:${DB_PORT}/${DB_NAME}?useSSL=false&serverTimezone=UTC&createDatabaseIfNotExist=true
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
spring.jpa.hibernate.ddl-auto=update
```

Variables de entorno esperadas:

- `DB_ENDPOINT`
- `DB_PORT`
- `DB_NAME`
- `DB_USERNAME`
- `DB_PASSWORD`

El servicio escucha por defecto en el **puerto 8081**.

## Ejecución en entorno local

```bash
mvn spring-boot:run
```

La API queda disponible en `http://localhost:8081`.

## Swagger / documentación

La documentación de la API está disponible en:

- `http://localhost:8081/swagger-ui.html`
  (según la configuración de `springdoc.swagger-ui.path`).

## Imagen Docker

El proyecto incluye un `Dockerfile` para construir y ejecutar el servicio:

```bash
# Construir la imagen
docker build -t devops-p3-backend-despachos .

# Ejecutar el contenedor
docker run -d \
  -p 8081:8081 \
  -e DB_ENDPOINT=<host-db> \
  -e DB_PORT=3306 \
  -e DB_NAME=<nombre-db> \
  -e DB_USERNAME=<usuario> \
  -e DB_PASSWORD=<password> \
  devops-p3-backend-despachos
```

El servicio expone el puerto **8081** en el contenedor.

## Integración en CI/CD

El repositorio incluye un workflow `deploy.yml` en `.github/workflows` que:

- Se ejecuta al hacer push sobre la rama `deploy`.
- Construye la imagen Docker del backend de despachos.
- Publica la imagen en un registry (por ejemplo Amazon ECR).
- Deja preparado el paso de despliegue automático en AWS/EKS/EC2.