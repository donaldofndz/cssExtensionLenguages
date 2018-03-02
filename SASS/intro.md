# SASS para principiantes

## Variables 

Uno de los principales atributos que tiene SASS es el uso de variables, casi cualquier dato puede ser almacenado en una variable y la finalidad de esto es poder reutilizar ciertos datos, las variables se declara del siguiente modo **$(nombreVariable):(valor)**

```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}	

```

el resultado tras compilar el codigo anterior es el siguiente 


```

body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

```


##Nesting en Sass

Sass tiene una funcionalidad que se llama Nesting, el nesting consiste en la forma en la que se anidan elementos, dicha funcionalidad nos permite tener un mejor manejo del CSS

```
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}

```

El codigo anterior se convertira en 

```

nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}

```


##Partial e Import en Sass

Al momento de escribir codigo en CSS es recurrente que estos sean extensos y la modularizacion del código un poco tediosas, para estos casos, Sass nos permite utilizar la funcionalidad de **Partials**, un partial es una pequeña parte de codigo reusable que puede ser invocada al codigo principal, sin que el codigo menos sea covertido en css

###Partials


Para hacer uso de un snippet hay que seguir los siguientes pasos 

1. Crear un archivo con la siguiente forma **\_partial.scss**
2. Ese archivo será llamaado por medio de @import


###Import

Supongoamos que tener dos archivos 

**\_basico.scss**

```
html,
body,
ul,
ol {
  margin:  0;
  padding: 0;
}

```

**style.scss** 

```
@import 'basico';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

El resultado de nuestro codigo sera el siguiente: 

```
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}

```

A pesar de que CSS tiene su propia funcion de import, crea un peticion htttp para ejecutarla, sin embargo cuando usamos el import de Sass se crea un archivo grande en vez de generar peticiones 




##Mixin 

Este concepto tiene que ver con crear una clase a la que le podemos modificar los atributos mediante el paso de valor, a continuación un ejemplo que dejará este concepto más claro.

```

@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

.box { @include border-radius(10px); }


```

El resultado sería 

```
.box {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}

```

Se pueden pasar varios atributos a la funcion con tal de que sean conosecutivos.

##Extend / Inheritance

Esta propiedad de Sass nos permite como dice, heredar atributos de un elementos CSS a otro, un ejemplo se muestra a continuación: 

```
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

// This CSS will print because %message-shared is extended.
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}


```


El resultado de nuestro CSS será el siguiente:

```
.message, .success, .error, .warning {
  border: 1px solid #cccccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}

```


Hay que notar que **%equal-heights** no se muestra porque nunca se usa en la funcion



##Operators 

Dentro de de SASS existe distintos tipos de operadores que nos permiten hacer matematicas con ellos, un ejemplo de esto son los siguientes

```
.container { width: 100%; }


article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}

```

El resultado tras compilar el codigo anterior será el siguiente 



```
.container { width: 100%; }


article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}


```


#SASS intermedio 

##Estructuras de control

Como en todo lenguaje de programacion SASS soporta estructuras de control básicas, con estas podemos hacer distintos tipos de operaciones 

### Ejemplo IF

```

if(true, 1px, 2px) => 1px
if(false, 1px, 2px) => 2px


```


Así como existe if, también existe la estructura de control que siempre la acompaña **if else** 

```

$type: monster;

p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}

```

En el caso anterior, la forma compilada de SASS será: 

```
p {
  color: green; }

```


#### Ejemplo FOR


La estructura de control for sirve para iterar sobre una serie de elementos, un ejemplo de esto es el siguiente 

```

/* Esta sintaxis mostrara 3 elementos */

@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

/* Esta sintaxis mostrara 2 elementos */

@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}

```

el resultado del primer codigo será el siguiente 

```
.item-1 {
  width: 2em; }
.item-2 {
  width: 4em; }
.item-3 {
  width: 6em; }

```


Dentro de las estructuras de control que tratan de iteraciones existen otras como 

### Ejemplo EACH 

EACH es una forma de iterar sobre un "arreglo", a pesar de que no existen como tal los arreglos, podemos simular uno y haacer uso de la estructura EACH

```

@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}

```


El resultado de estao será 

```

.puma-icon {
  background-image: url('/images/puma.png'); }
.sea-slug-icon {
  background-image: url('/images/sea-slug.png'); }
.egret-icon {
  background-image: url('/images/egret.png'); }
.salamander-icon {
  background-image: url('/images/salamander.png'); }


```


### Ejemplo While

Como ya conocemos while es una de las condicionales en buena parte de los lenguajes de programacion, su estructura en SASS es la siguiente

```
$i: 6;

@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}

```


Y el resultado sería este: 

```
.item-6 {
  width: 12em; }

.item-4 {
  width: 8em; }

.item-2 {
  width: 4em; }



```


Debido a la trivialidad no se explicará más a detalle 



##Funciones en SASS 

Aparte de hacer uso de distintas funciones dentro de SASS tambien podemos definir las nuestras y usarlas en cualquier punto de nuetro programa, un ejemplo a continuacion 

```

$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }


```

Invocamos la funcion dentro de **sidebar**, para poder hacer uso e la funcion **grid-width** a la cual le pasamos el argumento 5 y el resultado de la funcion será el siguiente 

```

#sidebar {
  width: 240px; }


```













