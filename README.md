
📚 StreamHub – Base de datos en MongoDB

Este proyecto simula la base de datos de una plataforma de streaming (StreamHub) usando MongoDB. Contiene colecciones para películas, series, usuarios, listas de reproducción y valoraciones.
📂 Colecciones creadas

    peliculas

    series

    usuarios

    listaReproduccion

    valoraciones

🛠 Operaciones realizadas
Creación de colecciones

db.createCollection("peliculas");
db.createCollection("series");
db.createCollection("usuarios");
db.createCollection("listaReproduccion");
db.createCollection("valoraciones");

Inserciones

    insertOne() → Para un solo documento (ejemplo: película Inception).

    insertMany() → Para múltiples documentos (películas, series, usuarios, listas de reproducción).

    Uso de _id personalizado para evitar ObjectId por defecto.

Ejemplo:

db.peliculas.insertOne({
  _id: 1,
  titulo: "Inception",
  duracion: 148,
  añoLanzamiento: 2010,
  genero: ["Ciencia ficción", "Acción"],
  reparto: ["Leonardo Di Caprio", "Cillian Murphy", "Joseph Gordon-Levitt", "Tom Hardy", "Elliot Page"]
});

Consultas (find())

Filtrar por duración:

db.peliculas.find({ duracion: { $gt: 120 } }).pretty();

Filtrar por país usando $in:

db.usuarios.find({ "país": { $in: ["Colombia", "México"] } });

Filtros compuestos con $and:

db.usuarios.find({
  $and: [
    { "país": "Colombia" },
    { "géneros preferidos": "Drama" }
  ]
});

Búsqueda por regex (ignora mayúsculas):

db.usuarios.find({ nombre: { $regex: /^C/, $options: "i" } });

Actualizaciones

Eliminar campo valoracion de una película:

db.peliculas.updateOne({ _id: 2 }, { $unset: { valoracion: "" } });

Índices

Crear índice por título:

db.peliculas.createIndex({ titulo: 1 });

Aggregations

Filtrar valoraciones por tipo:

db.valoraciones.aggregate([
  { $match: { tipo: "pelicula" } }
]);

Ordenar películas por duración descendente:

db.peliculas.aggregate([
  { $sort: { duracion: -1 } }
]);

📌 Notas

    Se usaron fechas en formato ISODate para listas de reproducción.

    Las colecciones están relacionadas de forma lógica a través de usuarioId y id de películas/series.

    Uso básico de índices para mejorar rendimiento en búsquedas.
