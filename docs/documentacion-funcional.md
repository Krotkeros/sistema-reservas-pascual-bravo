# Documentación Funcional

Esta sección describe la interacción de los usuarios con el sistema de reservas y las reglas de negocio que rigen el comportamiento de la aplicación.

## Reglas de Negocio del Sistema (RN)

### RN-01: Autenticación Institucional Obligatoria
* **Descripción:** Solo los usuarios con correo institucional activo (@pascualbravo.edu.co) pueden autenticarse, consultar disponibilidad y realizar reservas en la plataforma.

### RN-02: Control de Solapamientos de Horario
* **Descripción:** El sistema impide de forma estricta la creación o modificación de una reserva si el espacio seleccionado ya cuenta con una reserva activa en el mismo rango de fecha y hora.

### RN-03: Flujos de Aprobación Diferenciados
* **Espacios de Libre Reserva (Aulas, Canchas, Laboratorios):** Al registrar la solicitud, la reserva pasa automáticamente al estado `APROBADA`.
* **Espacios Críticos (Auditorios):** Al registrar la solicitud, la reserva queda en estado `PENDIENTE` y requiere la aprobación explícita en el sistema por parte de la Vicerrectoría Administrativa o Bienestar Universitario.

### RN-04: Tiempos Máximos de Cancelación
* **Aulas, Canchas y Laboratorios:** El usuario puede cancelar la reserva hasta **2 horas** antes de la hora de inicio programada.
* **Auditorios:** Debido al impacto logístico, la cancelación debe realizarse con un mínimo de **24 horas** de anticipación.

### RN-05: Inmutabilidad de Reservas Pasadas
* Ningún usuario ni administrador puede modificar o cancelar reservas cuya fecha y hora de finalización ya hayan pasado.

---

## Flujos Principales de Interacción

### Flujo Principal: Creación de Reserva (HU-05)
* **Actor:** Estudiante / Docente
* **Condición previa:** Usuario autenticado en el sistema (Token JWT válido).

```mermaid
sequenceDiagram
    actor Usuario
    participant Interfaz (React)
    participant Backend (Spring)
    participant BaseDatos (MongoDB)

    Usuario->>Interfaz: Selecciona espacio, fecha y hora
    Interfaz->>Backend: POST /api/v1/reservas (Datos + Token)
    Backend->>Backend: Valida Token JWT y verifica RN-01
    Backend->>BaseDatos: Consulta solapamientos de horario (RN-02)
    alt Existe solapamiento (RN-02)
        BaseDatos-->>Backend: Retorna conflicto de horario
        Backend-->>Interfaz: Error 409: Horario no disponible
        Interfaz-->>Usuario: Muestra alerta de conflicto
    else Horario disponible
        Backend->>Backend: Determina estado inicial (APROBADA o PENDIENTE segun RN-03)
        Backend->>BaseDatos: Guarda nueva reserva
        BaseDatos-->>Backend: Confirmacion de guardado
        Backend-->>Interfaz: 201 Created
        Interfaz-->>Usuario: Muestra mensaje de confirmación
    end