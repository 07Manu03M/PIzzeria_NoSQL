# Actividad Pizzeria NoSQL

# 1. CONSULTA
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
```{
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
```
# 2. 📁 Colecciones propuestas

Definimos las siguientes colecciones para representar los elementos principales del negocio:

| Colección      | Descripción                                                                 |
|----------------|-----------------------------------------------------------------------------|
| `clientes`     | Guarda los datos personales de los clientes (nombre, dirección, etc.).     |
| `productos`    | Contiene todos los tipos de productos: pizzas, panzarottis, bebidas, etc.  |
| `ingredientes` | Lista de ingredientes disponibles para personalizar productos.             |
| `combos`       | Agrupa varios productos con un precio especial.                            |
| `pedidos`      | Guarda los pedidos con los productos solicitados, el cliente y el total.   |

---

### 🧠 Decisiones de modelado

MongoDB permite estructurar los datos como documentos JSON, lo que nos permite optimizar la estructura para consultas rápidas y desarrollo ágil:

- **Productos en los pedidos**: Se copian directamente (no se usa referencia) para mantener los precios, tamaños y adiciones tal como estaban en el momento del pedido.
- **Cliente en los pedidos**: Se guarda una versión reducida del cliente dentro del pedido (nombre y teléfono) para facilitar consultas históricas y evitar inconsistencias si el cliente cambia sus datos después.
- **Combos**: Usan referencias a productos por ID, ya que los combos se arman a partir de productos existentes.
- **Ingredientes**: Se guardan como lista de strings en cada producto o pedido personalizado. No se referencian por ID para no complicar la estructura, ya que no requieren búsquedas complejas.

---

### 🔍 Estructura y tipo de datos utilizados

| Campo                     | Tipo de dato              | Ubicación                       |
|--------------------------|---------------------------|----------------------------------|
| `ingredientes`           | Lista de strings           | En productos y personalizaciones|
| `productos` en pedido    | Lista de objetos           | En pedidos                      |
| `cliente` en pedido      | Objeto incrustado          | En pedidos                      |
| `productos` en combo     | Lista de IDs (referencia)  | En combos                       |
| `tamaño`, `precio`, etc. | Strings / números simples  | En productos y pedidos          |



# 📁 3. Crear ejemplos de documentos JSON
clientes

productos (pizzas, panzarottis, bebidas, postres, adiciones)

combos

ingredientes

pedidos

## 🧾 Ejemplo de documentos y decisiones de modelado
## 📦 Colección: productos
Agrupamos todos los tipos de productos en una sola colección, diferenciándolos por tipo.

json
Copiar
Editar
```{
  "_id": "prod1",
  "nombre": "Pizza Hawaiana",
  "tipo": "pizza",
  "precio": 32000,
  "ingredientes": ["queso", "piña", "jamón"],
  "tamaño": "mediana",
  "personalizable": true
}
```
json
Copiar
Editar
```{
  "_id": "prod2",
  "nombre": "Coca-Cola 400ml",
  "tipo": "bebida",
  "precio": 5000,
  "personalizable": false
}
```
## 🧂 Colección: ingredientes
Lista de ingredientes disponibles (útil para validar las adiciones o personalizaciones).

json
Copiar
Editar
```{
  "_id": "ing1",
  "nombre": "Champiñones",
  "tipo": "vegetal"
}
```
## 🧾 Colección: combos
Los combos contienen productos (referenciados por ID) y un precio especial.

json
Copiar
Editar
```{
  "_id": "combo1",
  "nombre": "Combo Pareja",
  "productos": ["prod1", "prod2", "prod3"],
  "precio_combo": 45000
}
```
## 👤 Colección: clientes
json
Copiar
Editar

```{
  "_id": "cli1",
  "nombre": "Laura Gómez",
  "telefono": "3124567890",
  "direccion": "Cra 12 #45-78",
  "email": "laura@example.com"
}
```
## 📦 Colección: pedidos
Aquí se guarda el resumen completo del pedido. Incluye detalles embebidos como cliente y productos (para conservar el estado del pedido en el tiempo incluso si luego cambian los precios o ingredientes).

json
Copiar
Editar

```{
  "_id": "pedido1",
  "cliente": {
    "_id": "cli1",
    "nombre": "Laura Gómez",
    "telefono": "3124567890"
  },
  "tipo": "para llevar",
  "fecha": "2025-05-29T15:30:00Z",
  "productos": [
    {
      "_id": "prod1",
      "nombre": "Pizza Hawaiana",
      "tamaño": "grande",
      "precio": 38000,
      "adiciones": ["Champiñones", "Tocineta"]
    },
    {
      "_id": "prod2",
      "nombre": "Coca-Cola 400ml",
      "precio": 5000
    }
  ],
  "total": 43000,
  "estado": "En preparación"
}
```

# 💭 4. Reflexión grupal

### 🧠 ¿Qué fue lo más difícil de imaginar sin tablas?

Lo más difícil fue dejar de pensar en términos de relaciones estrictas como en MySQL. Estamos tan acostumbrados a usar claves foráneas, normalizar datos y evitar redundancia, que al principio nos costó aceptar que duplicar información (como los datos del cliente dentro del pedido) puede ser algo positivo en MongoDB. 

También fue un reto decidir cuándo incrustar datos y cuándo referenciar, ya que eso no siempre es obvio.

---

### ✅ ¿Qué nos gustó del enfoque con documentos?

Nos gustó la flexibilidad que ofrece MongoDB para modelar la información. El hecho de poder guardar toda la información de un pedido (cliente, productos, adiciones, etc.) en un solo documento facilita mucho la lectura y evita hacer varias "joins".

Además, como MongoDB usa JSON, nos pareció muy intuitivo, ya que se parece a cómo se manejan los datos en JavaScript, que es un lenguaje que ya dominamos.

---

### ❓ ¿Qué dudas nos surgieron?

Tuvimos dudas sobre:

- Cuándo es mejor incrustar datos y cuándo referenciarlos.
- Qué pasa si un producto cambia de precio, ¿cómo mantener la integridad del pedido anterior?
- Si hay límites de tamaño para los documentos y qué tan grande puede crecer un documento sin que afecte el rendimiento.
- Si existen buenas prácticas para modelar colecciones cuando los datos pueden cambiar con el tiempo (por ejemplo, si se actualiza un combo o se elimina un ingrediente).

