---
---
math: true
---

{% assign tp = site.data.trabajos.TP3 %}
{% capture fecha %}{{tp.entrega | date: "%e/%m"}}{% endcapture %}

Trabajo Práctico 3: Los 6 grados de Kevin Bacon
================
{:.no_toc}

El trabajo práctico número 3 tiene fecha de entrega para el día **{{fecha}}**.

## Contenido
{:.no_toc}

* Contenido
{:toc}


## Introducción

La conocida comunidad IMDB está realizando un balance de años anteriors. Son devotos de conocer qué películas son las más populares y a qué actores se les podría llamar más famosos.
Pero no solo quieren saber esto, ya que este año el CEO de la página escuchó sobre la idea de los “Seis grados de Kevin Bacon” y decidió que podía utilizar la enorme base de datos que maneja diariamente la página para corroborar la veracidad de esta idea.
Para esto, decidió sabiamente confiar en los alumnos de Algoritmos y Estructuras de Datos de la FIUBA, aprovechando su conocimiento para poder así resolver el misterio.

## ¿Seis grados de separación? ¿Seis grados de Kevin Bacon?

<p style="text-align: center;">
  <img src="{{ 'assets/tps/2017_2/tp3/logo_tp3.png' | relative_url }}" width="300">
</p>

"Seis grados de separación" es la idea que asegura que toda persona está a seis "pasos" o menos de cualquiera otra persona en el mundo, a partir de una cadena de conocidos. Por ejemplo, si Juan conoce a Facundo y Facundo conoce a Pedro, Juan está, entonces, a dos pasos de Pedro. Para más información de por qué esto se cumple se puede ver [este video](https://youtu.be/TcxZSmzPw8k).

La teoría de los "Seis grados de Kevin Bacon" lleva esta idea al cine, afirmando que el prolífico actor Kevin Bacon actuó en tantas peliculas y con tantos actores conocidos que está conectado a cualquier actor del mundo en una cadena de seis películas como máximo.

Por ejemplo, con la idea de conectar a Naomi Watts con Kevin Bacon:

* Naomi Watts actuó con Sean Penn en _**21 Gramos.**_
* Sean Penn actuó con **Kevin Bacon** en _**Río Místico.**_¹

Por lo tanto, **Naomi Watts tiene un Kevin Bacon Number (KBN) de 2**.

Es importante ver que **el Bacon Number de un actor es siempre el mismo**, sin importar el camino. Esto es tanto porque los actores colaboren juntos en más de una película (de Naomi Watts a Sean Penn se puede llegar por _**The Assassination of Richard Nixon**_), como por que se tome un camino distinto (por ejemplo, Naomi Watts trabajo con Jeffrey Donovan en _**J Edgar**_ quien a su vez trabajo con Kevin Bacon en _**Sleepers**_).

Cuando un actor esta completamente desconectado de KB, es decir, no tiene forma de llegar a él, se dice que tiene un 'Kevin Bacon Number of infinity'.


¹Tanto _**Río Místico**_ como _**21 Gramos**_ son fuertes recomendaciones de muy buenas películas.

## Datos Disponibles

Para poder trabajar, contamos con un set de datos obtenido desde IMDB, [`actors.csv`](https://drive.google.com/drive/folders/1hBZT2aE7haJT9s9COmqqACFYCDpGlrrF?usp=sharing) (**comma separated values**) con un total de 2.480.000 actores y actrices y 800.000 películas. Cada linea de este archivo tiene el formato de `apellido nombre, pelicula1, pelicula2, pelicula3, ...` Por ejemplo:

```
Bacon Kevin,A Few Good Men (1992),A Little Vicious (1991),Animal House (1978),Apollo 13 (1995/I),Balto (1995),Beauty Shop (2005),Beyond All Boundaries (2009),Black Mass (2015),Cavedweller (2004),Cop Car (2015),Crazy Stupid Love (2011),Criminal Law (1988),Death Sentence (2007),Digging to China (1997),Diner (1982),Elephant White (2011),End of the Line (1987),Enormous Changes at the Last Minute (1983),Flatliners (1990),Footloose (1984),Forty Deuce (1982),Friday the 13th (1980),Frost/Nixon (2008),He Said She Said (1991),Hero at Large (1980),Hollow Man (2000),Jayne Mansfields Car (2012),JFK (1991),Lemon Sky (1988),Loverboy (2005),Murder in the First (1995),My Dog Skip (2000),My One and Only (2009),Mystic River (2003),New York Skyride (1994),Only When I Laugh (1981),Patriots Day (2016),Picture Perfect (1997),Pyrates (1991),Queens Logic (1991),Quicksilver (1986),RIPD (2013),Rails & Ties (2007),Saving Angelo (2007),Shes Having a Baby (1988),Sleepers (1996),Starting Over (1979),Stir of Echoes (1999),Super (2010/I),Telling Lies in America (1997),The Air I Breathe (2007),The Air Up There (1994),The Big Green (2014),The Big Picture (1989),The Darkness (2016/I),The Making of Apollo 13 (1995),The River Wild (1994),The Woodsman (2004),These Vagabond Shoes (2009),Tough Day (2014),Trapped (2002/I),Tremors (1990),Where the Truth Lies (2005),White Water Summer (1987),Wild Things (1998),X-men First Class (2011)
```

Siendo que `actors.csv` es muy pesado, un archivo de prueba más ligero, `test.csv`, también es proporcionado para probar resultados localmente. Este contiene lineas del archivo original escogidas al azar, más la linea de Kevin Bacon.

## Consigna 

Dado este archivo parseado, se debe modelar la red de acotes con una estructura Grafo considerando únicamente los datos provistos. Esto implica determinar todas las características necesarias para el grafo. 
Se pide implementar un programa que cargue inicialmente el grafo recibiendo como parámetro la ruta del archivo parseado:
```
    $ ./kevinbaconeta actors.csv
```

Una vez cargada la red, se deberán realizar acciones sobre la misma a partir de comandos ingresados desde entrada estándar. 

### Implementación

El trabajo puede realizarse en lenguaje a elección, siendo aceptados Go, Python y C, y cualquier otro a ser coordinado con el corrector asignado.

El trabajo consiste de 3 partes:
1. El TDA Grafo, con sus primitivas completamente agnósticas sobre su uso para modelar la red de actores.  
1. Una biblioteca de funciones de grafos, que permitan hacer distintas operaciones sobre un grafo que modela una red de actores, sin importar cuál es la red específica.
1. El programa `kevinbaconeta` que utilice tanto el TDA como la biblioteca para poder implementar todo
lo requerido.

Es importante notar que las primeras dos partes deberían poder funcionar en cualquier contexto: El TDA Grafo para cualquier tipo de TP3 (o utilidad); la biblioteca de funciones debe funcionar para aplicar cualquiera de las funciones implementadas sobre cualquier grafo que tenga las características de las de este TP. La tercera parte es la que se encuentra enteramente acoplada al TP en particular. 

El programa a realizar debe recibir por parámetro y cargar en memoria el set de datos (`$ ./kevinbaconeta actors.csv`) y luego solicitar el ingreso de comandos por entrada estándar, del estilo `comando 'parametro'`. Notar que esto permite tener un archivo de instrucciones a ser ejecutadas (e.g. `./kevinbacon actors.csv < comandos.txt`).


A continuación se listarán los comandos junto a ejemplos de entrada y salidas para el caso de la red reducida. 
Recomendamos trabajar con este set de datos, puesto que el original cuenta con una enorme cantidad de datos, por lo que
puede demorar mucho tiempo cada una de las pruebas a realizar (especialmente los comandos con una complejidad mayor a lineal).

#### Camino hasta un actor

* Comando: `camino`.
* Parámetros: `actor1` y `actor2`.
* Utilidad: nos imprime una lista con los actores y películas con las que actuaron con otros actuales, de tal manera de llegar del `actor1` al `actor2` en la menor cantidad de pasos. 
* Complejidad: Este comando debe ejecutar en $$\mathcal{O}(A + P)$$, siendo $$A$$ la cantidad
de actores, y $$P$$ la cantidad de actuaciones compartidas en películas en toda la red.
* Ejemplo:

```
camino Watts Naomi, Bacon Kevin
>>> 'Watts Naomi' actuó con 'Penn Sean' en 'Mystic River (2003)'.
>>> 'Penn Sean' actuó con 'Bacon Kevin' en '21 Grams (2003)'.
```

Si no hay camino posible, imprimir `No se encontró conexión entre actores`.


#### Bacon Number

* Comando: `bacon_number`.
* Parámetro: actor o actriz. 
* Utilidad:  Imprime el Kevin Bacon Number del actor recibido. Para representar un KBN infinito (no hay conexión entre KB y el actor) el KBN esperado es -1, y de no existir el actor ingresado se debe imprimir un mensaje acorde. Tener en cuenta que el KBN de Kevin Bacon es 0.
* Complejidad: Este comando debe ejecutar en $$\mathcal{O}(A + P)$$.
* Ejemplo: 

```
bacon_number 'Watts Naomi'
>>> 'Watts Naomi' tiene un Kevin Bacon Number igual a 2
```

#### Bacon Number promedio
* Comando: `kbn_promedio`.
* Parámetros: Ninguno. 
* Utilidad: Imprime el Kevin Bacon Number promedio. En este numero no influyen la cantidad de actores con un KBN infinito, pero si lo hace el KBN de Kevin Bacon.
* Complejidad: Este comando debe ejecutar en $$\mathcal{O}(A (A + P))$$.
* Ejemplo (siendo $$N$$ el valor correcto, simplemente se muestra el formato esperado):

```
KBN_promedio
>>> El Kevin Bacon Number promedio es N
```


#### Similares a un actor
* Comando: `similares`.
* Parámetros: `actor` y `n`. 
* Utilidad: Encuentra a los `n` actores más similares al `actor` dado. Se imprimen de más similar a menos similar.  
Para la implementación de este comando, leer [el apunte sobre Pagerank Personalizado](/aed/material/apuntes/pagerank).
* Complejidad: Este comando debe ejecutar en $$\mathcal{O}(A + P)$$.
* Ejemplo:

```
similares 'Bacon Kevin', 3
>>> 'Buscemi Steve', 'Brocksmith Roy', 'Hollander Providence'
```


#### Núcleo de la red

* Comando: `nucleo`.
* Parámetros: `K`. 
* Utilidad: Encuentra el K-core de la red. El K-core de la red, son los vértices de un grafo que quedan luego de haber eliminado todos los vértices de grado menor a $$K$$ (notar que luego de eliminar un vértice, sus adyacentes podrían pasar a tener grado menor a $$K$$, y deben ser eliminados). Es importante notar que con $$K=1$$, estamos hablando de todos los vértices de la red. Este parámetro imprime el K-core de actores de la red, sin un orden específico, considerando que hayan actuado en películas al menos $$K$$ películas que hayan sido actuadas por al menos $$K$$ actores. 
* Complejidad: Este comando debe ejecutar en $$\mathcal{O}(A + P)$$.
* Ejemplo:

```
nucleo 8
>>> ....
```


## Trivia

Como última tarea, y con el proposito de darle un pequeño uso al programa realizado, dejamos está trivia (no obligatoría) para que puedan completar haciendo uso del progama:

  * ¿Hay algun actor argentino con un KBN infinito?
  * ¿Cuál es el actor argentino más central? ¿Hay alguno más central que Kevin Bacon?
  * ¿Cuál es el actor argentino más similar a KB?
  * ¿Hay algun actor 'mejor' que Kevin Bacon para realizar este trabajo? Es decir, ¿hay algun actor más central?
  * Finalmente, ¿es cierto que no hay nadie con un KBN mayor a 6 (obviando los que se encuentran a infinito)?

## Anexo: links y más

Para ver una implementación online de Six Degrees of Bacon, pueden entrar al [Oracle de Bacon](https://oracleofbacon.org/). En su sección "How it Works" pueden encontrar información útil sobre teoría de grafos.

También tengan en cuenta que con sólo escribir en Google, por ejemplo, `bacon number of Clint Eastwood` pueden rápidamente comprobar sus resultados.


## Entrega

Adicionalmente a los archivos propios del trabajo práctico debe agregarse un archivo `entrega.mk` que contenga la regla `kevinbaconeta` para generar el ejecutable de dicho programa (sea compilando o los comandos que fueren necesarios). Por ejemplo, teniendo un TP elaborado en Python, podría ser:

``` makefile
kevinbaconeta:
    cp kevin.py kevinbaconeta
    chmod +x kevinbaconeta
```

**Importante**: En caso de recibir un error `FileNotFoundError: [Errno 2] No such file or directory: './kevinbaconeta': './kevinbaconeta'`, tener en cuenta que para el caso de enviar código escrito en Python es necesario además indicar la ruta del intérprete. Esto puede hacerse agregando como primera línea del archivo principal (en el ejemplo, sería `kevin.py`) la línea: `#!/usr/bin/python3`.

Si el TP fuera realizado en Go, un posible ejemplo del archivo podría ser:

``` makefile
kevinbaconeta:
    cd mi_implementacion_tp3; go build -o ../kevinbaconeta
```

## Criterios de aprobación

El código entregado debe ser claro y legible y ajustarse a las especificaciones
de la consigna.

La entrega incluye, obligatoriamente, los siguientes archivos de código:

- el código del TDA Grafo programado, y cualquier otro TDA que fuere necesario.
- el código de la solución del TP.

La entrega se realiza en forma digital a través del [sistema de entregas]({{site.entregas}}),
con todos los archivos mencionados en un único archivo ZIP.

