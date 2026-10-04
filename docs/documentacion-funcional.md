# Documentación Funcional

Esta sección describe cómo interactúan los usuarios con el sistema de reservas y las reglas de negocio aplicadas[cite: 20].

## Flujo Principal: Creación de Reserva (HU-05)

**Actor:** Estudiante / Docente

**Condición previa:** El usuario debe estar autenticado (Token JWT válido).

### Diagrama de Flujo (Comportamiento)

```mermaid

sequenceDiagram

    actor Usuario

    participant Interfaz (React)

    participant Backend (Spring)

    participant BaseDatos (MongoDB)

    Usuario->>Interfaz: Selecciona espacio, fecha y hora

    Interfaz->>Backend: POST /api/v1/reservas (Datos + Token)

    Backend->>Backend: Valida Token JWT

    Backend->>BaseDatos: Consulta solapamientos (Mismo espacio y horario)

    alt Hay solapamiento

        BaseDatos-->>Backend: Retorna reserva existente

        Backend-->>Interfaz: Error 409: Horario no disponible

        Interfaz-->>Usuario: Muestra alerta de conflicto

    else Horario disponible

        Backend->>BaseDatos: Guarda nueva reserva (Estado: APROBADA o PENDIENTE)

        BaseDatos-->>Backend: OK

        Backend-->>Interfaz: 201 Created

        Interfaz-->>Usuario: Muestra confirmación de éxito

    end