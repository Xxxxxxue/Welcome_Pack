# MongoDB | Parte II

## Después de esta sesión podrás:

1. Editar documentos de la base datos.
2. Eliminar documentos de nuestra base de datos.
3. Trabajar con arrays en MongoDB.
4. Relacionar documentos entre sí y recuperar los datos del documento asociado.

## Editando documentos de nuestra DB

Ya tenemos nuestra base de datos llena de nuestros estudiantes, y podremos por tanto empezar a trabajar con los datos para organizar y estudiar el funcionamiento de nuestros bootcamps, pero tenemos que solucionar primero una serie de casuísticas.

Si cuando estábamos creando el perfil de uno de los estudiantes que se ha matriculado en el bootcamp de `**Frontend Development**` nos olvidamos de introducir el nombre del bootcamp, ¿cómo hacemos para añadir el campo en dicho documento?

Vamos a crear este perfil:

```bash
db.students.insert({
  firstName: "Alejandro",
  lastName: "Martínez",
  age: 28
})
```

Y ahora podemos añadir un campo usando la propiedad `**.update**` de una colección, usando como primer parámetro la condición de búsqueda para seleccionar el documento que vamos a editar, y como segundo parámetro un `**{ $set: { NOMBRE_CAMPO: VALOR_CAMPO  } }`.** Vamos a añadir el valor a nuestro estudiante:

Si buscamos y actualizamos un usuario por su nombre o edad, podemos errar actualizando algún otro elemento que no sea el que buscamos debido a una coincidencia inesperada. Vamos a buscar el perfil que queremos actualizar primero filtrando por los que tienen la propiedad `**bootcamp**` como `**null**`:

```bash
db.students.find({ bootcamp: null }).pretty()
```

Ahora tendremos nuestro estudiante y utilizaremos su valor `**_id**` para filtrar en el `**update**`:

```bash
db.students.update(
 { _id: ObjectId("5eb68e74960f42aa2e41a6e6") },
 { $set: {
    bootcamp: "Frontend Development"
   }
 }
)
```

Si todo ha funcionado correctamente, podremos buscar el perfil de nuevo usando la `**_id**`:

```bash
> db.students.find({ _id: ObjectId("5eb68e74960f42aa2e41a6e6") }).pretty()

{
        "_id" : ObjectId("5eb68e74960f42aa2e41a6e6"),
        "firstName" : "Alejandro",
        "lastName" : "Martínez",
        "age" : 28,
        "bootcamp" : "Frontend Development"
}
```

**¡Lo hemos conseguido! Ahora sabemos añadir valor a los campos de nuestros documentos 🎉**

¡Pero tenemos un nuevo problema tras esta pequeña victoria! Una estudiante de nuestra escuela nos ha pedido cambiar de bootcamp. **Arwen** nos ha dejado su `**_id**` de alumna para poder cambiar su bootcamp de `**Frontend Development**` a `**Full Stack Web Development**`.

Ahora tan solo tenemos que repetir lo mismo que hizimos con el `**update**` de antes y lo tendremos solucionado:

```bash
db.students.update(
 { _id: ObjectId("5eb48d6d6b30476d4817fb1c") },
 { $set: {
    bootcamp: "Full Stack Web Development"
   }
 }
)
```

Si ahora buscamos el documento en nuestra base de datos, podremos comprobar que lo hemos editado sin problemas:

```bash
> db.students.find({ _id: ObjectId("5eb48d6d6b30476d4817fb1c") }).pretty()

{
        "_id" : ObjectId("5eb48d6d6b30476d4817fb1c"),
        "firstName" : "Arwen",
        "lastName" : "Undómiel",
        "age" : 46,
        "bootcamp" : "Full Stack Web Development"
}
```

**¡Ahora si que hemos aprendido a editar documentos en nuestra DB! 🛠**

## Eliminando documentos de nuestra base de datos

Ahora que nuestros alumnos han terminado el bootcamp, vamos a eliminar su perfil de usuario de nuestra base de datos para dar cabida a los nuevos alumnos del bootcamp que empieza el mes que viene.

Para ello, vamos a eliminar todos los documentos que correspondan con alumnos del bootcamp `**"Full Stack Web Development"**`  de la siguiente manera:

```bash
db.students.remove({ bootcamp: "Full Stack Web Development" })
```

Podremos ver el siguiente output:

```bash
WriteResult({ "nRemoved" : 5 })
```

Esto quiere decir que hemos eliminado cinco elementos de la base de datos, podemos buscar usando el comando `**.find**` para comprobar que no nos quedan alumnos:

```bash
db.students.find({ bootcamp: "Full Stack Web Development" })
```

**¡Con esto, podremos comprobar que hemos eliminado todos estos perfiles de alumnos!**

### Eliminando colecciones o bases de datos 🚨

Tenemos que tener mucho cuidado con estos comandos, pero tenemos que aprenderlos para conocer más aceca de MongoDB y sus funcionalidades.

Para eliminar una colección, tan solo tendremos que usar el comando **(¡no lo lances si no quieres borrarla!)**:

```bash
db.students.drop()
```

Con esto, habremos eliminado la colección de nuestra base de datos correspondiente a los estudiantes.

Si ahora queremos eliminar nuestra base de datos por alguna razón (imagina el caso en que hemos gestionado mal las colecciones y documentos), solo tendremos que lanzar el comando:

```bash
use upgrade_hub
db.dropDatabase()
```

¡Y habremos hecho un `**drop**` de nuestra base de datos!

## Trabajando con arrays en MongoDB

Ahora que tenemos todos los aspectos de los documentos de MongoDB controlados, nos queda un pequeño detalle sobre el que trabajar.

Ya que los documentos de MongoDB son BSON, la representación binaria de los archivos JSON, podemos generar documentos que contengan arrays, al igual que cualquier JSON con el que trabajemos.

Vamos a añadir a nuestros alumnos un array de conocimientos adquiridos dentro del bootcamp `**Full Stack Web Development**`. Para ello consideraremos un array dentro de una propiedad que llamaremos `**skills**` en el que introduciremos strings con el nombre de la tecnología. 

Por ejemplo, veamos el conocimiento de un alumno que está llegando a la recta final del bootcamp:

```json
"skills": ["HTML", "CSS", "JS", "PHP", "MySQL", "Angular"]
```

Vamos a insertar unos nuevos alumnos en el bootcamp `**Full Stack Web Development`** y buscarlos en nuestro mongo shell para obtener sus ids:

```bash
> db.students.find({ bootcamp: "Full Stack Web Development" })

{ "_id" : ObjectId("5eb6e7edbcb485c24c8442c9"), "firstName" : "Peter", "lastName" : "Parker", "age" : 23, "bootcamp" : "Full Stack Web Development" }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442ca"), "firstName" : "Bruce", "lastName" : "Banner", "age" : 38, "bootcamp" : "Full Stack Web Development" }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442cb"), "firstName" : "Tony", "lastName" : "Stark", "age" : 40, "bootcamp" : "Full Stack Web Development" }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442cc"), "firstName" : "Natasha", "lastName" : "Romanoff", "age" : 36, "bootcamp" : "Full Stack Web Development" }
```

Vamos a considerar que Natasha Romanoff ha aprendido las siguientes tecnologías:

```json
"skills": ["HTML", "CSS", "JS", "PHP"]
```

Ahora actualizaremos el campo `**skills**` con los conocimientos:

```bash
db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442cc")}, 
  { $set: { skills: ["HTML", "CSS", "JS", "PHP"] } }
)
```

Si buscamos el documento correspondiente a nuestra alumna:

```bash
> db.students.find({ _id: ObjectId("5eb6e7edbcb485c24c8442cc")}).pretty()

{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442cc"),
  "firstName" : "Natasha",
  "lastName" : "Romanoff",
  "age" : 36,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "HTML",
    "CSS",
    "JS",
    "PHP"
  ]
}
```

Como puedes observar, los arrays se guardan tal y como esperábamos. Pero, ¿y si ahora resulta que Natasha no ha aprendido PHP pero sí Angular? Habrá que hacer un `$pull` del array `skills` para sacar PHP y un `$push` para introducir Angular.

```bash
db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442cc") }, 
  { "$pull": { "skills": "PHP" } }
)
```

Y ahora tocará añadir Angular al array:

```bash
db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442cc") }, 
  { "$push": { "skills": "Angular" } }
)
```

**¡Y con esto podemos ver que nuestro documento se ha actualizado! 🎉**

```bash
> db.students.find({ _id: ObjectId("5eb6e7edbcb485c24c8442cc")}).pretty()

{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442cc"),
  "firstName" : "Natasha",
  "lastName" : "Romanoff",
  "age" : 36,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "HTML",
    "CSS",
    "JS",
    "Angular"
  ]
}
```

### Buscando documentos por el contenido de un array

Vamos a actualizar el resto de nuestros alumnos con diferentes tecnologías:

```bash
db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442c9")}, 
  { $set: { skills: ["HTML"] } }
)

db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442ca")}, 
  { $set: { skills: ["HTML", "CSS", "JS", "PHP", "MySQL", "Angular"] } }
)

db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442cb")}, 
  { $set: { skills: ["JS", "PHP"] } }
)
```

Ahora que están todos actualizados, vamos a filtrar por conocimiento. Para filtrar y añadir una condición sobre los elementos que contiene un array utilizaremos el comando `**$in**`. Filtremos todos los alumnos que han conseguido aprender `**Angular`:**

```bash
db.students.find({ $and: [ 
  { bootcamp: "Full Stack Web Development" },
  { skills: { $in: ["Angular"] } } 
] }).pretty()
```

Y obtendremos el siguiente resultado de nuestra query:

```bash
{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442ca"),
  "firstName" : "Bruce",
  "lastName" : "Banner",
  "age" : 38,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "HTML",
    "CSS",
    "JS",
    "PHP",
    "MySQL",
    "Angular"
  ]
}
{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442cc"),
  "firstName" : "Natasha",
  "lastName" : "Romanoff",
  "age" : 36,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "HTML",
    "CSS",
    "JS",
    "Angular"
  ]
}
```

Ahora vamos a filtrar todos los alumnos que **NO hayan aprendido CSS**:

```bash
db.students.find({ $and: [ 
  { bootcamp: "Full Stack Web Development" },
  { skills: { $not: { $in: ["CSS"] } } }
] }).pretty()
```

Y ahora encontraremos los siguientes alumnos:

```bash
{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442c9"),
  "firstName" : "Peter",
  "lastName" : "Parker",
  "age" : 23,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "HTML"
  ]
}
{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442cb"),
  "firstName" : "Tony",
  "lastName" : "Stark",
  "age" : 40,
  "bootcamp" : "Full Stack Web Development",
  "skills" : [
    "JS",
    "PHP"
  ]
}
```

**¡Ya somos un@s expert@s manejando arrays! 💃 Solo nos queda relacionar documentos entre si para terminar de aprender MongoDB 🚀**

## Relacionando documentos en MongoDB

Hasta el momento hemos añadido un string que representa el bootcamp en el que estudia cada alumno de Minsait. Este patrón es algo repetido y que podríamos automatizar.

También hay que tener en cuenta que hay distintos grupos y horarios dentro de nuestros cursos, por lo que podemos crear una colección `**bootcamps`** en la que crearemos cursos con el siguiente esquema:

```json
{
  "name": "Full Stack Web Development",
  "group": 2,
  "format": "Part Time"
}
```

Este ejemplo nos servirá para crear distintos bootcamps, vamos a crear un archivo `bootcamps.json` con el siguiente contenido:

```json
[
  {
    "name": "Full Stack Web Development",
    "group": 1,
    "format": "Full Time"
  },
  {
    "name": "Full Stack Web Development",
    "group": 2,
    "format": "Full Time"
  },
  {
    "name": "Full Stack Web Development",
    "group": 1,
    "format": "Part Time"
  },
  {
    "name": "Full Stack Web Development",
    "group": 2,
    "format": "Part Time"
  },
  {
    "name": "Frontend development",
    "group": 1,
    "format": "Part Time"
  }
]
```

Y lo importaremos de nuevo desde MongoDB usando el comando que ya vimos anteriormente:

```bash
mongoimport --db upgrade_hub --collection bootcamps --file ~/Documents/upgrade/node/bootcamps.json --jsonArray                ─╯
```

Ahora que tenemos los bootcamps insertados en una nueva colección, vamos a conseguir sus ids para actualizar nuestros alumnos:

```bash
> db.bootcamps.find()

{ "_id" : ObjectId("5eb6ef657a5c086758381203"), "name" : "Frontend development", "group" : 1, "format" : "Part Time" }
{ "_id" : ObjectId("5eb6ef657a5c086758381204"), "name" : "Full Stack Web Development", "group" : 1, "format" : "Full Time" }
{ "_id" : ObjectId("5eb6ef657a5c086758381205"), "name" : "Full Stack Web Development", "group" : 2, "format" : "Part Time" }
{ "_id" : ObjectId("5eb6ef657a5c086758381206"), "name" : "Full Stack Web Development", "group" : 1, "format" : "Part Time" }
{ "_id" : ObjectId("5eb6ef657a5c086758381207"), "name" : "Full Stack Web Development", "group" : 2, "format" : "Full Time" } 
```

Vamos a buscar a nuestros alumnos y a hacer que los dos primeros alumnos pertenezan al grupo 1 Full Time de Full Stack, y los otros dos al grupo 2 Part Time:

```bash
{ "_id" : ObjectId("5eb6ef657a5c086758381204"), "name" : "Full Stack Web Development", "group" : 1, "format" : "Full Time" }
{ "_id" : ObjectId("5eb6ef657a5c086758381205"), "name" : "Full Stack Web Development", "group" : 2, "format" : "Part Time" }
```

```bash
> db.students.find({ bootcamp: "Full Stack Web Development" })

{ "_id" : ObjectId("5eb6e7edbcb485c24c8442c9"), "firstName" : "Peter", "lastName" : "Parker", "age" : 23, "bootcamp" : "Full Stack Web Development", "skills" : [ "HTML" ] }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442ca"), "firstName" : "Bruce", "lastName" : "Banner", "age" : 38, "bootcamp" : "Full Stack Web Development", "skills" : [ "HTML", "CSS", "JS", "PHP", "MySQL", "Angular" ] }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442cb"), "firstName" : "Tony", "lastName" : "Stark", "age" : 40, "bootcamp" : "Full Stack Web Development", "skills" : [ "JS", "PHP" ] }
{ "_id" : ObjectId("5eb6e7edbcb485c24c8442cc"), "firstName" : "Natasha", "lastName" : "Romanoff", "age" : 36, "bootcamp" : "Full Stack Web Development", "skills" : [ "HTML", "CSS", "JS", "Angular" ] }
```

Y vamos a actualizarlos con lo dicho:

```bash
db.students.update(
  { _id: ObjectId("5eb6e7edbcb485c24c8442c9") }, 
  { $set: { bootcamp: ObjectId("5eb6ef657a5c086758381204") } }
)
```

Si buscamos nuestro estudiante en la DB veremos que para el campo bootcamp aparece ahora:

```bash
"bootcamp" : ObjectId("5eb6ef657a5c086758381204"),
```

Si queremos que este campo se convierta en el bootcamp correspondiente, realizaremos un `**aggregate**` con `**$lookup**` .

En vez de utilizar `**find**` podemos utilizar `**aggregate**` que nos permite dar una serie de instrucciones en orden en nuestra query.

- Como primer argumento utilizaremos una serie de valores para filtrar utilizando `**$match**` y completando el resto como hacemos con `**find**`.
- El segundo argumento es un `**$lookup**` donde usando los campos haremos referencia a la colección correspondiente.
- Por último, utilizaremos `**{ "$unwind": "$NOMBRE_CAMPO" }**` para que el array que devuelve `**$lookup**` se convierta en una copia del documento que referenciemos con la id.

```bash
db.students.aggregate([
  {
    $match: {
      _id: ObjectId("5eb6e7edbcb485c24c8442c9"),
    }
  },
  { "$lookup": {
    from: "bootcamps",
    localField: "bootcamp", 
    foreignField: "_id", 
    as: "bootcamp"
  } },
  { "$unwind": "$bootcamp" }
]).pretty()
```

Y con esta query podremos obtener nuestro documento de estudiante con la información del bootcamp agregada:

```bash
{
  "_id" : ObjectId("5eb6e7edbcb485c24c8442c9"),
  "firstName" : "Peter",
  "lastName" : "Parker",
  "age" : 23,
  "bootcamp" : {
    "_id" : ObjectId("5eb6ef657a5c086758381204"),
    "name" : "Full Stack Web Development",
    "group" : 1,
    "format" : "Full Time"
  },
  "skills" : [
    "HTML"
  ]
}
```

**¡Ahora si que conocemos MongoDB en profundidad! 🚀 En las próximas sesiones aprenderemos a utilizarlo en conjuntos con Node.js para conseguir la persistencia de datos en nuestros servidores.**