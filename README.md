# 📚 StreamHub – Base de datos en MongoDB

Este proyecto simula la base de datos de una plataforma de streaming (**StreamHub**) usando **MongoDB**. Contiene colecciones para películas, series, usuarios, listas de reproducción y valoraciones.  

## 📂 Colecciones creadas
```js
db.createCollection("peliculas");
db.createCollection("series");
db.createCollection("usuarios");
db.createCollection("listaReproduccion");
db.createCollection("valoraciones");
```

## 🛠 Operaciones realizadas

Insertamos documentos con `insertOne()` para un solo registro y `insertMany()` para varios. En algunos casos usamos `_id` manual para evitar el `ObjectId` automático. Ejemplo:
```js
db.peliculas.insertOne({ _id: 1, titulo: "Inception", duracion: 148, añoLanzamiento: 2010, genero: ["Ciencia ficción", "Acción"], reparto: ["Leonardo Di Caprio", "Cillian Murphy", "Joseph Gordon-Levitt", "Tom Hardy", "Elliot Page"] });
```

### Consultas (`find()`)
Películas con duración mayor a 120 minutos:
```js
db.peliculas.find({ duracion: { $gt: 120 } }).pretty();
```
Series con menos de 70 episodios:
```js
db.series.find({ episodiosTotales: { $lt: 70 } }).pretty();
```
Películas lanzadas en 2010:
```js
db.peliculas.find({ añoLanzamiento: { $eq: 2010 } });
```
Usuarios de Colombia o México:
```js
db.usuarios.find({ "país": { $in: ["Colombia", "México"] } });
```
Usuarios de Colombia que prefieran "Drama":
```js
db.usuarios.find({ $and: [ { "país": "Colombia" }, { "géneros preferidos": "Drama" } ] });
```
Usuarios cuyo nombre comience con "C" (sin importar mayúsculas/minúsculas):
```js
db.usuarios.find({ nombre: { $regex: /^C/, $options: "i" } });
```

### Actualizaciones
Eliminar campo `valoracion` de la película con `_id` 2:
```js
db.peliculas.updateOne({ _id: 2 }, { $unset: { valoracion: "" } });
```

### Índices
Crear índice por título:
```js
db.peliculas.createIndex({ titulo: 1 });
```
Buscar usando el índice:
```js
db.peliculas.find({ titulo: "Inception" });
```

### Aggregations
Filtrar valoraciones de películas:
```js
db.valoraciones.aggregate([{ $match: { tipo: "pelicula" } }]);
```
Ordenar películas por duración descendente:
```js
db.peliculas.aggregate([{ $sort: { duracion: -1 } }]);
```

## 📌 Notas
- Fechas en listas de reproducción están en formato `ISODate`.
- Las relaciones entre colecciones se manejan por `usuarioId` y `id` de película/serie.
- Uso de índices para optimizar búsquedas.
