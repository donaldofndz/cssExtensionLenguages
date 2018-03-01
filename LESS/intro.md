# Intro para usar LESS 

Se puede utilziar LESS de distintos modos 

* Agregar la libreria y LESS se compilará desde el navegador (muy lento)
* Compilar con **NodeJS** y subirlo a produccion cada que sea necesario


Pero en este tutorial lo haremos del modo tradicional con **NodeJS**
Para instalar el compilador de less tenemos que tener instalado **NodeJS** y sus librerias

```

	npm install -g less


```


Con esta instalacion podremos compilar archivos *.less* en archivo *.css* y este archivo estará listo
para poder agregarse a nuestro archivo HTML

```

	lessc style.less > style.css

```


Al ser un compilador en caso de que hayan errores de programación se mostrara un error en el finder 


## Uno de los principales beneficios de usar Less es la habilidad de crear variables (VARIABLES)

Pueden almacenar cualquier tipo de valor, dimensiones, nombres, entre otras cosas

**Ejemplo LESS 1**


```
	@background-color: #ffffff;
	@text-color: #1A237E;

	p{
	  background-color: @background-color;
	  color: @text-color;
	  padding: 15px;
	}

	ul{
	  background-color: @background-color;
	}

	li{
	  color: @text-color;
	}

```


##LESS nos permite aplicar estilos de una clase anterior a otra (MIXIN)

Un elemento puede recibir todos los atributos de otro elemeto (some cain of inherents)

```
#circle{
  background-color: #4CAF50;
  border-radius: 100%;
}

#small-circle{
  width: 50px;
  height: 50px;
  #circle 				/* < ---- Este elemento hace referencia a los atributos de arriba */
}

#big-circle{
  width: 100px;
  height: 100px;
  #circle
}

```


Otra forma de hacerlo, para poder distinguir de mejor forma a los elementos que se heradan es la siguiente: 

```
#circle(){
  background-color: #4CAF50;
  border-radius: 100%;
}

#small-circle{
  width: 50px;
  height: 50px;
  #circle
}

#big-circle{
  width: 100px;
  height: 100px;
  #circle
}


```

La desventaja de la forma anterior es que no se creara ninguna clase para el **ID: CIRCLE**

### Otras habilidades del MIXIN es que se pueden crear funciones con variables internas, como a continuacion


```
#circle(@size: 25px){
  background-color: #4CAF50;
  border-radius: 100%;

  width: @size
  heiht: @size
}

#small-circle{
  #circle
}

#big-circle{
  #circle(100px)
}


```


## Nesting y Scope en LESS


Esta propiedad nos permite crear elementos anidados dentro de nuestro CSS, por ejemplo un <ul> (unorder list) que contenga <li> (list Items)

```

ul{
  background-color: #03A9F4;
  padding: 10px;
  list-style: none;

  li{
    background-color: #fff;
    border-radius: 3px;
    margin: 10px 0;
  }
}


```


al igual que en la mayor parte de los lenguajes de programacion que utilizamos existe un scope y herada a sus hijos, pero no a sus padre un ejemplo de esto es lo siguiente: 

```
@text-color: #000000;

ul{
  @text-color: #fff;
  background-color: #03A9F4;
  padding: 10px;
  list-style: none;

  li{
    color: @text-color;
    border-radius: 3px;
    margin: 10px 0;
  }
}


```

## Operaciones con elementos de LESS

Con los operadores de LESS podemos hacer operaciones matematica básicas, suponiendo que quisieramos tener dos divs, uno con el doble de largo que otro y colores diferentes, lo que deberiamos hacer es lo siguiente

```

@div-width: 100px;
@color: #03A9F4;

div{
  height: 50px;
  display: inline-block;
}

#left{
  width: @div-width;
  background-color: @color - 100;
}

#right{
  width: @div-width * 2;
  background-color: @color;
}



```



## Functions en lESS 

LESS tiene sus propias funciones para realizar cierto tipo de acciones, a continuación podemos ver algunas de las cosas de las que LESS es capaz 


```
@var: #004590;

div{
  height: 50px;
  width: 50px;
  background-color: @var;

  &:hover{
    background-color: fadeout(@var, 50%)
  }
}


```











