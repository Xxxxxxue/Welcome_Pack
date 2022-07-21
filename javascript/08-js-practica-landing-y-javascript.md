# Práctica: Landing + Js

Lo primero sería seleccionar la API con la que vamos a traernos la información que vamos a manejar para después definir nuestra landing. Dentro de nuestra landing vamos a jugar con el DOM, por ello tendréis que renderizar una serie de elementos dentro del Html:

**Vista Principal → index.html**

1. Nuestra vista principal está compuesta por:
    1. Header → Enlaces a nuevas vistas.
    2. Content → Explicación de nuestra Landing.
    3. Footer → Redes sociales e info básica.
    

**Vista List → list.js**

1. Nuestra vista List está compuesta por:
    1. Header → Enlaces a nuestras vistas.
    2. Content → Listado de elementos.
    3. Footer → Redes sociales e info básica.

**Vista Detail → detail.js**

1. Nuestra vista Detail está compuesta por:
    1. Header → Enlaces a nuestras vistas.
    2. Content → Detalle del elemento.
    3. Footer → Redes sociales e info básica.

No hay navegación por lo tanto cuando clickemos en Ver listado se deberá manipular el DOM para mostrarlo → al igual cuando clickemos en un elemento del listado para ver el detalle.

### Funcionalidad

En todo proyecto que se precie tendrá que tener una documentación base que nos indique qué debe hacer cada una de nuestras vistas y cómo es la interacción del usuario con cada una de ellas. Por ello vamos a definir una funcionalidad mínima dentro de nuestro proyecto que nos ayude a completar esta aplicación.

![https://media.giphy.com/media/26tn33aiTi1jkl6H6/giphy.gif](https://media.giphy.com/media/26tn33aiTi1jkl6H6/giphy.gif)

**Header**:

1. Enlaza todas las páginas que hemos definido. → Home y List - para acceder a Detail se hará por otra vía. 
2. Cuando clickas en cada una de ellas te sustituye clases mostrando el contenido de dicha página.
3. En caso de clickar sobre la página en la que nos encontramos te mostrara un mensaje "Ya estamos aquí".
4. Si clickas sobre el logo de nuestra aplicación te llevará a la **Vista principal**.

**Footer**:

1. Estará enlazadas las redes sociales - usando iconos de las mismas.
2. Cuando clickas en cada icono te llevará a dicha red social.
3. Opcional - Mapa de ubicación.
4. Opcional - Listado de participantes.

**Vista principal/Controlador → index.js + index.html**

1. En la vista principal explicaremos en qué consiste la temática de la aplicación web.
2. Tendremos diversos eventos que modificarán la visual de dicha página:
    1. A los 2 segundos mostrará un mensaje de Bienvenida a nuestra web.
    2. Cuando hagan over por algún elemento este debe cambiar de color.
    3. Cuando hagan out por dicho elemento volverá a su estado.
    4. Cuando clicken un bloque que esté condensado deberá desplegarse más información.

**Vista List → list.js**

1. Recuperaremos nuestros elementos de un fichero info.js.
2. Pintaremos los elementos de manera dinámica - es decir - del info.js.
3. Se pintará tan solo el nombre y la imagen.
4. Cuando clickemos sobre un elemento de nuestra lista nos navegará a **Vista Detail**.
5. **Vista Detail** deberá ****recibir un objeto con los datos del elemento clickado.

**Vista Detail → detail.js**

1. Pintaremos los datos del objeto que hemos recibido desde Vista List.
2. En esta vista aparecerá nombre, imagen y despcripción.

Con esto tendríamos nuestra primera aplicación 100% funcional, recordad que podemos poner en práctica todo lo aprendido hasta ahora. Desde el uso de variables, objectos, condicionales, bucles, arrays y eventos en la parte de .js y no menos importante BEM, responsive design, arquitectura html del bloque anterior.

Chic@s es el momento que desplegueis vuestra mágia y veáis por fin lo que sería una aplicación. Ver que todas esa batalla con la sintaxis y programación funcional tenía su porqué. 

Además os recordamos que gracias a esto aprenderéis a trabajar mejor con Git, buenas prácticas y estructura de proyectos y código. Ya solamente nos queda decir **Happy Coding!** 

![https://media.giphy.com/media/tEaDT85En43i8/giphy.gif](https://media.giphy.com/media/tEaDT85En43i8/giphy.gif)