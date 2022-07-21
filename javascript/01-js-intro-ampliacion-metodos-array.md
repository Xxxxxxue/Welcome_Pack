# Javascript | Métodos del array

## Métodos que modifican el array

Los métodos que presentamos a continuación modifican el array inicial, que en nuestro caso va a ser este:

```jsx
var moderatIII = new Array();
            moderatIII[0] = "Eating hooks";
            moderatIII[1] = "Running";
            moderatIII[2] = "Finder";
            moderatIII[3] = "Ghostmother";
            moderatIII[4] = "Reminder";
            moderatIII[5] = "Intruder";
            moderatIII[6] = "Animal trails";    

console.log(moderatIII);
```

### `POP`

Poco más que decir. `pop()` no admite parámetros. Elimina el último elemento del array.

```jsx
moderatIII.pop();

console.log(moderatIII);
```

### `PUSH`

Entre los paréntesis se pueden añadir tantos valores como se quiera añadir a  el array, separados por comas (`,`). Añade un elemento al array en última posición.

```jsx
moderatIII.push('Ethereal');

console.log(moderatIII);
```

### `REVERSE`

`reverse()` tampoco admite parámetros. Invierte el orden del array.

```jsx
moderatIII.reverse();

console.log(moderatIII);
```

### `SHIFT`

`shift()` funciona como `pop()`, pero extrayendo del array el primer elemento.

Como se ve, todos los índices de la matriz se actualizan.

```jsx
moderatIII.shift();
```

### `SORT`

`sort()` ordena los elementos del array, tal y como ordena los nombres de archivo un ordenador, es decir:

- Los valores como los de esta matriz se ordenan por orden alfabético.
- Si la matriz consiste en una serie de números, estos se ordenan según las cifras más a la izquierda, de menor a mayor. Así, por ejemplo, una matriz que consista en `200,35,40,1`, no se ordenará según el valor de las cifras —`1,35,40,200`—, sino que `sort()` devolverá `1,200,35,40`.

```jsx
moderatIII.short();

console.log(moderatIII);
```

### `SPLICE`

`splice()` es un método especial, cuyo comportamiento depende de los parámetros que se le asignen:

- El primer parámetro es un número que representa el índice desde el que tiene que empezar a modificar la matriz.
- El segundo es otro númer que indica el número de elementos que debe eliminar o sustituir, contando el inicial (por ello un valor de `0` no modifica nada en absoluto).
- Tras estos dos parámetros, se puede incluir una lista de elementos separados por comas:
    - Si no se incluye ningún elemento, `splice()` simplemente elimina tantos elementos como se han indicado en el segundo parámetro, tomando como índice inicial el primer parámetro.
    - Si se incluyen menos elementos que el valor del segundo parámetro, rellena los «huecos» disponibles hasta quedarse sin valores, y elimina los que faltan.
    - Si se incluyen más elementos que el valor del segundo parámetro, primero elimina los indicados, y luego inserta todos los elementos proporcionados entre el anterior y el posterior a la sección eliminada. Sin embargo, en este caso `splice()` no devuelve la parte del array seccionada como en los anteriores, sino la nueva longitud.

vamos a comprobarlo:

```jsx
moderatIII.splice(2,2);

console.log(moderatIII);

moderatIII.splice(2,2,'Ethereal');

console.log(moderatIII);

moderatIII.splice(2,2,'Ethereal','Ethereal Remix vol.1','Ethereal Remix vol.2');

console.log(moderatIII);
```

### `UNSHIFT`

Como parámetros se puede proporcionar a `unshift()` una serie de elementos separados por comas, que se añaden al principio de la matriz. Los índices se actualizan en consecuencia, y el método devuelve la nueva longitud.

```jsx
moderatIII.unshift('Reminder Remix vol.1','Reminder Remix vol.2')
```

## Métodos que no modifican la matriz

Estos métodos devuelven una representación del array, pero no lo modifican.

Vamos a emplear los dos arrays siguientes:

```jsx

    var moderatII = new Array();
        titanes[0] = "The Mark";
        titanes[1] = "Bad Kingdom";
        titanes[2] = "Versions";
        titanes[3] = "Milk";
        titanes[4] = "Gita";
        titanes[5] = "Damage Done";
        
    var moderat = new Array();
        titanides[0] = "Rusty nails";
        titanides[1] = "Seanmonkey";
        titanides[2] = "Nasty silence";
        titanides[3] = "Berlin";
            
```

### `CONCAT`

En este caso he concatenado la segunda matriz a la primera, pero se pueden encadenar una serie de elementos separados por comas, o incluso varias matrices.

```jsx
moderatII.concat(moderat);

console.log(moderatII);

console.log(moderat);
```

Como se puede ver, sin embargo, la matriz `moderat` no ha sido alterada.

### `JOIN`

Empleado sin un parámetro, `join()` devuelve una mera cadena en la que los valores del array están separados por comas. Sin embargo, se puede especificar una cadena que sirva como separador:

```jsx
moderatII.join('-');

console.log(moderatII);
```

### `SLICE`

`slice()` extraé una copia de una sección especificada de una matriz, aunque a diferencia de `splice()` no la modifica.

Para este método el primer parámetro es obligatorio y el segundo opcional:

- Definidos ambos naturales, el primero es el índice desde el que debe comenzarse la copia (se incluye ese elemento en la misma), y el segundo el índice en el que debe detenerse (y este elemento que no se incluye).
- Definido sólo uno, cuenta como el índice desde el que comenzar la copia, que abarcará los elementos hasta el final de la matriz.

```jsx
moderatII.slice(2,4);

console.log(moderatII);

moderatIII.slice(3);

console.log(moderatIII);
```

### `TOSTRING`

Este método es similar a `join()`, sólo que no admite parámetros, y que el resultado es un objeto String, con sus propias propiedades y métodos.

```jsx
moderatII.toString()

console.log(moderatII);
```

## Localizar un valor en un array

Por último, recojo dos métodos muy útiles para localizar valores en un array.

```jsx

    var modeSelector = ["Who", "Fentanyl", "Tom", "Dy"]
            
```

### `INDEXOF`

Devuelve el índice del primer elemento que coincide con el parámetro proporcionado.

```jsx
modeSelector.indexOf('Who');
```

Si no se da coincidencia, devuelve -1:

```jsx
modeSelector.indexOf('Pastis');
```

### `LASTINDEXOF`

Devuelve el índice del último elemento que coincide con el parámetro proporcionado.

```jsx
modeSelector.lastIndexOf('Who');
```

Si no se da coincidencia, también devuelve -1:

```jsx
modeSelector.lastIndexOf('Pastis');
```

En realidad estos dos métodos son un poco limitados, pero son útiles precisamente cuando se está comprobando la **no existencia** de un elemento en un Array.