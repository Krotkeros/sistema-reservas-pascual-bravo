# Requisitos del Sistema y Control de Cambios

## Control de Cambios (Refinamiento Entrega 1)
- **Ajuste de Stakeholders:** Se retiró al equipo de desarrollo del nivel de stakeholders de negocio.
- **Alineación de Épicas:** Se eliminó la HU-01 (Configuración de GitHub) por ser una tarea técnica; las épicas ahora reflejan exclusivamente valor para el usuario.
- **Trazabilidad Incorporada:** Se agregaron identificadores únicos para conectar requerimientos con endpoints y pruebas, evitando documentación aislada.

## Requisitos Funcionales (RF)
| ID | Descripción | Ref. Épica / HU |
| :--- | :--- | :--- |
| **RF-01** | El sistema debe autenticar a los usuarios validando el dominio del correo institucional. | EP-01 / HU-03 |
| **RF-02** | El sistema debe impedir la creación de reservas si existe un solapamiento en fecha, hora y espacio. | EP-02 / HU-05 |
| **RF-03** | El sistema debe enviar los espacios críticos (Ej: Auditorios) a un estado "PENDIENTE" de aprobación por Vicerrectoría. | EP-02 / HU-05 |

## Requisitos No Funcionales (RNF) - Verificables
- **RNF-01 (Rendimiento):** El 95% de las consultas de disponibilidad en el calendario debe responder en menos de 2 segundos bajo una concurrencia de 200 usuarios.
- **RNF-02 (Seguridad):** Las contraseñas deben almacenarse utilizando algoritmos de hashing (Bcrypt) y las sesiones gestionarse mediante tokens JWT con expiración de 2 horas.

## Matriz de Trazabilidad
| Requisito | Historia de Usuario | Interfaz Técnica (API) | Caso de Prueba (Futuro) |
| :--- | :--- | :--- | :--- |
| RF-01 | HU-03: Inicio de sesión | POST /api/v1/auth/login | CP-01: Validar dominio de correo |
| RF-02 | HU-05: Crear reserva | POST /api/v1/reservas | CP-02: Registrar con solapamiento |