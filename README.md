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

db.createCollection("peliculas")
db.createCollection("series")
db.createCollection("usuarios")
db.createCollection("listaReproduccion")
db.createCollection("valoraciones")

Inserciones

    insertOne() → Para un solo documento (ej: película Inception).

    insertMany() → Para múltiples documentos (películas, series, usuarios, listas de reproducción).

    Uso de _id personalizado para evitar ObjectId por defecto.

Consultas (find())

    Filtrar por duración:

db.peliculas.find({ duracion: { $gt: 120 } })

    Filtrar por país usando $in:

db.usuarios.find({ "país": { $in: ["Colombia", "México"] } })

    Filtros compuestos con $and.

    Búsqueda con regex e insensible a mayúsculas:

db.usuarios.find({ nombre: { $regex: /^C/, $options: "i" } })

Actualizaciones

    Eliminar campo valoracion de una película con $unset:

db.peliculas.updateOne({ _id: 2 }, { $unset: { valoracion: "" } })

Índices

    Crear índice por título:

db.peliculas.createIndex({ titulo: 1 })

Aggregations

    Filtrar valoraciones por tipo:

db.valoraciones.aggregate([{ $match: { tipo: "pelicula" } }])

    Ordenar películas por duración descendente:

db.peliculas.aggregate([{ $sort: { duracion: -1 } }])

📌 Notas

    Se usaron fechas en formato ISODate para listas de reproducción.

    Las colecciones están relacionadas de forma lógica a través de usuarioId y id de películas/series.

    Uso básico de índices para mejorar rendimiento en búsquedas.
