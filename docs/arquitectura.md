# Arquitectura del Sistema[cite: 66]

El sistema utiliza una arquitectura Cliente-Servidor basada en el **Modelo C4** (Nivel 2: Contenedores) para separar responsabilidades de presentación, lógica de negocio y persistencia[cite: 66].

## Diagrama de Contenedores (C4)[cite: 66]

```mermaid

C4Context

    title Diagrama de Contenedores - Sistema de Reservas

    Person(usuario, "Estudiante/Docente", "Busca y reserva espacios universitarios.")

    Person(admin, "Administrador", "Gestiona espacios y aprueba reservas.")

    System_Boundary(sistema, "Sistema de Reservas Pascual Bravo") {

        Container(spa, "Single Page App", "React", "Provee toda la interfaz de usuario interactiva y el calendario.")

        Container(api, "API Application", "Spring Boot / Java", "Provee endpoints REST, lógica de reservas, validación de solapamientos y seguridad JWT.")

        ContainerDb(db, "Base de Datos", "MongoDB", "Almacena usuarios, espacios y el historial de reservas.")

    }

    Rel(usuario, spa, "Usa", "HTTPS")

    Rel(admin, spa, "Usa", "HTTPS")

    Rel(spa, api, "Llama APIs REST", "JSON/HTTPS")

    Rel(api, db, "Lee y escribe", "MongoDB Driver")

```[cite: 66]

## Decisiones Técnicas (ADR)[cite: 66]

- **Frontend:** Se eligió **React** por su eficiencia al manejar cambios de estado complejos en tiempo real (necesario para el calendario interactivo)[cite: 66].

- **Backend:** Se seleccionó **Spring Boot** por su robustez en la gestión de seguridad (Spring Security) y su facilidad para construir APIs REST escalables[cite: 66].

- **Base de datos:** Se optó por **MongoDB** dada la flexibilidad requerida para almacenar diferentes tipos de espacios con atributos variables sin requerir esquemas rígidos[cite: 66].