# # Guía de Instalación y Ejecución[cite: 69]

Instrucciones claras para garantizar que cualquier miembro del equipo (o tercero) pueda levantar el entorno[cite: 69].

## Prerrequisitos[cite: 69]

- Node.js (v18+)[cite: 69]

- Java JDK (17+)[cite: 69]

- Maven[cite: 69]

- MongoDB (Instancia local en puerto 27017 o cluster Atlas)[cite: 69]

## 1. Configuración del Backend (Spring Boot)[cite: 69]

1. Abrir terminal en `/src/backend`[cite: 69].

2. Renombrar `src/main/resources/application-example.properties` a `application.properties`[cite: 69].

3. Configurar variables de entorno[cite: 69]:

   ```properties

   [spring.data](http://spring.data).mongodb.uri=mongodb://localhost:27017/reservas_db

   jwt.secret=CLAVE_SUPER_SECRETA_2026

   ```[cite: 69]

4. Compilar e instalar dependencias: `mvn clean install`[cite: 69]

5. Ejecutar: `mvn spring-boot:run` *(El API quedará expuesta en* `http://localhost:8080`*[)*[cite](http://localhost:8080`)*[cite): 69]

## 2. Configuración del Frontend (React)[cite: 69]

1. Abrir terminal en `/src/frontend`[cite: 69].

2. Instalar dependencias: `npm install`[cite: 69]

3. Crear archivo `.env` en la raíz del frontend[cite: 69]:

   ```env

   REACT_APP_API_URL=[http://localhost:8080/api/v1](http://localhost:8080/api/v1)

   ```[cite: 69]

4. Levantar servidor de desarrollo: `npm start` *(La interfaz gráfica estará disponible en* `http://localhost:3000`*[)*[cite](http://localhost:3000`)*[cite): 69]