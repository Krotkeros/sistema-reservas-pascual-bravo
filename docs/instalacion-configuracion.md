# # Guía de Instalación y Ejecución

Instrucciones claras para garantizar que cualquier miembro del equipo (o tercero) pueda levantar el entorno.

## Prerrequisitos

- Node.js (v18+)

- Java JDK (17+)

- Maven

- MongoDB (Instancia local en puerto 27017 o cluster Atlas)

## 1. Configuración del Backend (Spring Boot)

1. Abrir terminal en `/src/backend`.

2. Renombrar `src/main/resources/application-example.properties` a `application.properties`.

3. Configurar variables de entorno:

   ```properties

   [spring.data](http://spring.data).mongodb.uri=mongodb://localhost:27017/reservas_db

   jwt.secret=CLAVE_SUPER_SECRETA_2026

   ```

4. Compilar e instalar dependencias: `mvn clean install`

5. Ejecutar: `mvn spring-boot:run` *(El API quedará expuesta en* `http://localhost:8080`*[)*[cite](http://localhost:8080`)*[cite): 69]

## 2. Configuración del Frontend (React)

1. Abrir terminal en `/src/frontend`.

2. Instalar dependencias: `npm install`

3. Crear archivo `.env` en la raíz del frontend:

   ```env

   REACT_APP_API_URL=[http://localhost:8080/api/v1](http://localhost:8080/api/v1)

   ```

4. Levantar servidor de desarrollo: `npm start` *(La interfaz gráfica estará disponible en* `http://localhost:3000`*[)*[cite](http://localhost:3000`)*[cite): 69]