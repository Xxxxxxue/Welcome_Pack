# Metodología BEM en 5 minutos

### Metodología CSS: Block Element Modifier (BEM)

BEM constituye la metodología que usaremos para **nombrar y clasificar selectores CSS de manera estricta, transparente e informativa**. Este método se basa en nombrar las clases en un modo muy específico, ayudándonos a distinguir de manera simple de qué objeto hablamos y si tiene o no aplicado algún tipo de modificador en su estilo, ya sea por interacción del usuario, o por tipología del objeto. Cuando utilicemos la metodología BEM, deberemos tener en cuenta que solamente usaremos nombres de clases, nunca IDs, para fomentar así la reutilización de código.

Como su nombre indica, BEM distingue claramente **3 conceptos: el Bloque, el Elemento y el Modificador.**

> BEM es una metodología que usaremos para nombrar y clasificar selectores CSS de manera estricta, transparente e informativa
> 

### **El Bloque**

Representa la entidad independiente, es decir, el **objeto al que aplicar el estilo.** Un bloque puede componerse de otros bloques. Un buscador simple es un bloque simple, mientras que la cabecera de una web es un bloque compuesto.

Para ejemplificarlo pensaremos en la **cabecera de una web**: pondremos la clase de nuestro bloque como:

```css
.main-header
```

### **El Elemento**

Figura como una **pieza concreta, de un Bloque cualquiera, que cumple una función**. Evidentemente, un bloque puede estar compuesto de varios elementos. Las clases con las que identificamos cada elemento las escribiremos después del nombre del bloque, y las separaremos con dos guiones bajos:

```css
bloque__element
```

La idea de la doble barra sirve para ayudarnos a **navegar y manipular nuestro código CSS**. Para nuestro ejemplo, tendremos los siguientes elementos:

```css
.main-header__brand.main-header__primary-nav.main-header__recursive-nav.main-header__lang-chooser
```

La nomenclatura de las clases que usemos va completamente a gusto del desarrollador. En el ejemplo, `main-header__primary-nav` podría ser `main-header__primaryNav`. Lo más importante es que nos decidamos por una manera y **sea esa la que usemos en todo el proyecto**.

### **El Modificador**

Son las entidades que usaremos para definir la apariencia o comportamiento de un Bloque o Elemento concreto. Su uso es opcional, pero nos será muy **útil para separar claramente el objeto de su estilo gráfico**.

Los Modificadores los representaremos con doble guión, por ejemplo:

```css
bloque—modificador_bloquebloque__elemento—modificador_elemento
```

Si usamos el selector de idiomas del ejemplo, un modificador claro sería si aparece desplegado o no:

```css
main-header__lang-choosermain-header__lang-chooser—isOpen
```

Te darás cuenta que si la idea de todo esto es **generar código reutilizable**, nos encontramos ante una pequeña inconsistencia: tendremos que repetir el código. Para solucionar esto, usaremos [SASS](http://sass-lang.com/guide) y su propiedad @extend. De esta manera tendremos un único código.

```css
main-header__lang-chooser{position: relative;//estilo de nuestro elemento...}

main-header__lang-chooser—isOpen{@extends main-header__lang-chooser;position: block;}
```

### **En Conclusión**

Hemos visto cómo funciona BEM y, sobre todo, cómo nos puede ayudar a **estructurar nuestro código CSS: a mantenerlo limpio, reusable y mucho más semántico**. Habrá quien piense que los nombres de las clases se alargan demasiado, pero en el fondo dotamos a nuestro HTML y CSS de legibilidad, dado que especificamos en cada clase su uso y su porqué.

> BEM requiere de una planificación previa, donde el diseñador y el desarrollador trabajen en conjunto, **identificando todos los Bloques de diseño, sus Elementos, y si tienen o no Modificadores**.
>