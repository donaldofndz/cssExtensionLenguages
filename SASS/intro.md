# Sass para principiantes

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






















/**/
