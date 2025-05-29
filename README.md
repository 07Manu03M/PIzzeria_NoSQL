# Actividad Pizzeria NoSQL

## CONSULTA
### Que es una base de datos NoSQL?

- Una base de datos NoSQL (Not Only SQL) es un tipo de base de datos que proporciona un mecanismo para el almacenamiento y recuperación de datos que no requiere un modelo tabular tradicional como las bases de datos relacionales (SQL). Las bases de datos NoSQL están diseñadas para manejar grandes volúmenes de datos distribuidos, no estructurados o semi-estructurados, y son especialmente útiles en aplicaciones modernas como big data, tiempo real, y escalabilidad horizontal en la nube.

### Que es MongoDB?

- MongoDB es una base de datos NoSQL de tipo documental diseñada para ser escalable, flexible y de alto rendimiento. Almacena los datos en un formato similar a JSON llamado BSON (Binary JSON), lo que permite una representación muy flexible y jerárquica de la información.

- 🔍 Características principales de MongoDB:
1. Modelo de documentos:

  - Los datos se almacenan en estructuras llamadas documentos, que son similares a objetos JSON.

  - Cada documento puede tener una estructura diferente (no necesita un esquema fijo).

2. Escalabilidad horizontal:

  - MongoDB permite distribuir datos entre múltiples servidores usando sharding, lo que facilita manejar grandes volúmenes de datos.

3. Consultas poderosas:

  - Soporta consultas complejas, agregaciones, filtros, índices, búsquedas de texto completo, entre otros.

4. Alta disponibilidad:

  - Utiliza réplicas para asegurar la redundancia de datos y tolerancia a fallos.

5. Flexible y rápido desarrollo:

  - Ideal para aplicaciones ágiles y modernas como apps web, móviles, IoT, big data, etc.

### ¿Qué diferencia hay entre una base de datos relacional (como MySQL) y una base de datos documental como MongoDB?

# Diferencias entre MySQL y MongoDB

A continuación se presentan las principales diferencias entre una base de datos relacional (como **MySQL**) y una base de datos documental (como **MongoDB**):

## 1. Modelo de datos

| Característica       | MySQL (Relacional)                        | MongoDB (Documental)                       |
|----------------------|-------------------------------------------|-------------------------------------------|
| Estructura           | Tablas con filas y columnas               | Documentos JSON/BSON en colecciones       |
| Esquema              | Fijo (tipos de datos y columnas definidos) | Flexible (los documentos pueden variar)   |
| Relaciones           | Claves foráneas y JOINs                   | Documentos embebidos o referencias        |

---

## 2. Consultas y relaciones

| Característica       | MySQL                                     | MongoDB                                   |
|----------------------|-------------------------------------------|-------------------------------------------|
| Lenguaje de consulta | SQL                                       | MongoDB Query Language (similar a JSON)   |
| Consultas            | Estructuradas con JOINs y subconsultas    | Consultas jerárquicas, embebidas          |
| Normalización        | Alta (varias tablas interrelacionadas)    | Baja (datos anidados en un documento)     |

---

## 3. Escalabilidad

| Característica       | MySQL                                     | MongoDB                                   |
|----------------------|-------------------------------------------|-------------------------------------------|
| Escalado             | Principalmente vertical                   | Horizontal (sharding)                     |
| Uso de clústeres     | Más complejo                              | Nativo y sencillo con réplicas y shards   |

---

## 4. Rendimiento y flexibilidad

| Característica       | MySQL                                     | MongoDB                                   |
|----------------------|-------------------------------------------|-------------------------------------------|
| Flexibilidad         | Baja: cambios de esquema costosos         | Alta: se adapta fácilmente a cambios      |
| Velocidad de desarrollo | Más lento por estructura rígida       | Rápido, ideal para desarrollo ágil        |

---

## 5. Casos de uso recomendados

- **MySQL**:
  - Sistemas financieros y bancarios
  - Aplicaciones que requieren integridad referencial estricta
  - Proyectos con estructuras de datos muy bien definidas

- **MongoDB**:
  - Aplicaciones web y móviles ágiles
  - Sistemas de gestión de contenido
  - Análisis de big data y aplicaciones con datos no estructurados

---

> 📝 **Conclusión:**  
MySQL es ideal para estructuras rígidas y relaciones complejas entre datos.  
MongoDB es mejor cuando se necesita flexibilidad, escalabilidad y rapidez en el desarrollo.


### Que son Documentos y Colecciones en MongoDB

# 📘 Documentos y Colecciones en MongoDB

MongoDB organiza los datos usando **documentos** y **colecciones**, que forman la base de su modelo de datos flexible y escalable.

---

## 📄 ¿Qué es un documento?

Un **documento** es la unidad básica de almacenamiento en MongoDB. Es similar a un objeto JSON, pero se guarda internamente como **BSON** (Binary JSON), lo que permite mayor compatibilidad de tipos de datos.

### 🔹 Características:
- Estructura tipo **clave-valor**.
- Puede contener datos anidados (subdocumentos y arrays).
- No requiere un esquema fijo.
- Cada documento tiene un campo `_id` único por defecto.

### ✅ Ejemplo de documento:
```json
{
  "_id": ObjectId("60f7e36e8d3e3a2b3c4f1e56"),
  "nombre": "Ana Gómez",
  "edad": 28,
  "email": "ana@example.com",
  "direccion": {
    "ciudad": "Madrid",
    "pais": "España"
  },
  "intereses": ["música", "cine", "deportes"]
}

