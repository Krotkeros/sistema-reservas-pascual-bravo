# Modelo de Datos[cite: 63]

Estructura de documentos en **MongoDB**. Se priorizó la referenciación (ObjectId) sobre la incrustación masiva para mantener las colecciones normalizadas y facilitar reportes[cite: 63].

### Colección: `users`[cite: 63]

```json

{

  "_id": "ObjectId",

  "correo_institucional": "[santiago.garces@pascualbravo.edu.co](mailto:santiago.garces@pascualbravo.edu.co)",

  "nombre": "Santiago Garcés",

  "rol": "ESTUDIANTE", 

  "password_hash": "$2a$10$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjQGM..."

}

```[cite: 63]

### Colección: `espacios`[cite: 63]

```json

{

  "_id": "ObjectId",

  "nombre": "Auditorio Bloque 4",

  "tipo": "AUDITORIO",

  "departamento": "Vicerrectoría",

  "capacidad": 120,

  "requiere_aprobacion": true,

  "activo": true

}

```[cite: 63]

### Colección: `reservas`[cite: 63]

```json

{

  "_id": "ObjectId",

  "espacio_id": "ObjectId (Ref: espacios)",

  "usuario_id": "ObjectId (Ref: users)",

  "fecha_inicio": "2026-10-15T14:00:00Z",

  "fecha_fin": "2026-10-15T16:00:00Z",

  "estado": "PENDIENTE"

}

```[cite: 63]