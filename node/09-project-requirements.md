# Project Requeriments

Tras acabar las sesiones teóricas del módulo de Node.js vamos a aplicar todos los conocimientos adquiridos para crear nuestra primera API Rest totalmente funcional 🔥 

### Requisitos

- Tener preparado MongoDB para desarrollo en local, ya sea instalado o mediante Docker.
- Instalar Robo3T de forma que podamos comprobar el estado de nuestra base de datos en cualquier punto del desarrollo.
- Crear una carpeta en Postman en la que añadiremos las requests necesarias para probar completamente nuestra API.
- Crear una cuenta en MongoAtlas para subir nuestra base de datos en Cloud.
- Crear un proyecto en GitLab en formato público al que subiremos nuestro código.
- Crear una cuenta en Heroku, instalar Heroku CLI y crear nuestro proyecto preparado para subir el servidor.

### Objetivo

El objetivo final de nuestra API será simular el funcionamiento completo de un e-commerce (Amazon, Ebay o cualquier web tipo Shopify).

Para poder lograrlo, necesitaremos tener usuarios que consuman nuestra API. Estos usuarios podrán registrarse e iniciar sesión para añadir productos a su carrito de la compra y finalizar la compra de los productos.

Pasos a seguir:

- Crear una seed con al menos 20 productos que consten, al menos, de los campos `name`, `price`, `description`, `image`. Estos productos se guardarán a través del modelo `Product`.
- Crear una seed para generar al menos un usuario de tipo administrador, con una contraseña segura y un mail adecuado. Esta información se guardará en el modelo `User`.
- Terminar el modelo usuario con los campos básicos y añadir el proceso completo de autenticación, registro e inicio de sesión de usuarios.
- Crear rutas para poder recoger todos los productos de la API mediante paginación, limitando los resultados de cada búsqueda a 10 productos. (MongoDB y mongoose exponen formas de pedir elementos a partir de un índice dado y limitar la cantidad de elementos que devuelve una request).
- Crear una ruta para poder buscar productos por nombre y otra ruta para poder filtrar productos por precio.
- Añadir un nuevo endpoint que permita añadir un producto por `_id` al documento del usuario que tenga sesión iniciada, tal y como ocurriría cuando un usuario añade un producto al carrito de la compra. Esto lo haremos relacionando modelos mediante un campo `cart` en el modelo usuario que consistirá en un array de ObjectId con referencia a Product.
- Crear un endpoint para que el usuario cuya sesión está iniciada pueda ver su carrito de la compra con los productos cargados en el array (populate).

### Bonus

- Crear una cuenta en Cloudinary para subir imágenes e integrarlo en nuestro servidor como middleware.
- Añadir imágenes a los productos de nuestra base de datos en un campo llamado `**image**`.
- Por último, crear un nuevo endpoint para comprar todos los productos del carrito de la compra, a través del cual vaciaremos el carrito de la compra del usuario, y moveremos todo el array de productos a un nuevo modelo `Purchase` que tendrá como campos `userId`, `totalPrice` y `products` (array con la id de los productos que se han comprado) en el que almacenaremos las compras realizadas.