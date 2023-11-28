# Introducción a la interfaz de línea de comandos (CLI)

La interfaz de línea de comandos (**Command Line Interface** o CLI por sus siglas) nos permite interactuar con nuestro sistema operativo. La habrás visto representada en decenas de películas y series como una pantalla negra con texto verde o blanco. Y, si llevas cierto tiempo trabajando con un ordenador, la recordarás de los tiempos de MS-DOS.

Actualmente, estamos acostumbrados a utilizar sistemas gráficos para interactuar con nuestras máquinas (**Graphic User Interface** o GUI, por sus siglas). Sin embargo, cuando utilizamos un servidor remoto no tenemos acceso a periféricos como una pantalla o un ratón. Este es uno de los motivos por los que, como desarrolladores, debemos aprender a utilizar la consola.
Pero no te asustes: no es necesario que aprendas a utilizar la terminal a fondo. Basta con que sepamos cómo funciona y cuáles son los comandos más recurrentes, y el resto del tiempo podremos apoyarnos en búsquedas en Google, Stack Overflow, ChatGPT o la fuente que elijamos.

De modo que en esta introducción vamos a hablar de los conceptos fundamentales que debemos dominar para trabajar con la consola y a aprender los comandos más utilizados. A lo largo del tema utilizaré indistintamente los términos “consola”, “terminal” o “CLI”, pese a las diferencias que puedan existir entre ellas.

## ¿Cómo seguir este tema?

1. Navega hasta el repositorio que he creado para trabajar el tema: [Curso de git y github](https://github.com/code-journey-hub/curso-git-y-github).
1. Ahora abre un codespace, siguiendo la ruta Code > Codespaces > Abrir en Codespaces.
   ![como crear un codespace](/assets/imgs/codespaces-path.jpg)
1. Sigue las instrucciones que encontrarás a lo largo del curso, bajo los apartados "Prácticas".

## ¿Por qué utilizamos la consola?

Como ya hemos visto, la consola nos permite interactuar con nuestra máquina del mismo modo que una interfaz gráfica. Además, hay ocasiones en las que no disponemos de periféricos o interfaz gráfica en absoluto, por lo que la CLI se convierte en la única forma de trabajar.

Por otro lado, si te habitúas a trabajar en la consola habrá ciertas operaciones cotidianas que te acabarán resultando más rápidas desde la terminal que si tienes que utilizar una interfaz gráfica. Con el tiempo, la consola será tu forma de interacción por defecto con la máquina, lo que aumentará tu velocidad y productividad.

## ¿Cómo se utiliza la CLI?

La CLI consiste básicamente en un prompt, donde podemos insertar los comandos que queremos ejecutar. Además, algunos comandos admiten argumentos y opciones, que nos permitirán indicar cómo queremos que funcione la instrucción.

Por ejemplo, el comando para copiar un archivo es `cp`. Pero, además de decirle a la máquina que queremos copiar un archivo, tendremos que indicarle qué archivo es el que queremos copiar, y dónde queremos copiarlo. Esto son los argumentos que pasaríamos al comando `cp`.

Una vez escrito nuestro comando, argumentos y opciones, pulsaremos `enter` para que se ejecute.

La CLI no tiene mucho más misterio, aunque sí debemos saber:

1. Cómo navegar en nuestros archivos. Ten en cuenta que no tenemos una interfaz con el clásico explorador con iconos de carpetas y archivos.
1. Algunos atajos de teclado, que nos facilitarán el trabajo.
1. Ten en cuenta que algunas instrucciones no se cumplen instantáneamente. Por ejemplo, puedo renombrar un archivo instantáneamente, pero si abro un audio con un reproductor se estará reproduciendo hasta que lo cierre. Cuando tenemos un proceso abierto no podemos utilizar la terminal. En estos casos podemos cerrar el proceso y recuperar la terminal mediante la combinación de teclas `Ctrl+c`. Pronto veremos ejemplos.

### ¿Qué es la shell?

Al hablar de la CLI o investigar al respecto de su uso, es fácil que encuentres referencias a la shell. La shell es la interfaz que "traduce" los comandos que le pasamos a la CLI, haciendo de intermediaria con el propio sistema operativo. Las shells más conocidas son Windows Shell y Bash (utilizada por Linux y MacOS).

Ten en cuenta que dependiendo del sistema operativo que utilices, los comandos que necesitarás serán unos u otros. De modo que si estás utilizando Windows te recomiendo que [instales bash](https://hackernoon.com/how-to-install-bash-on-windows-10-lqb73yj3). A lo largo del curso voy a utilizar los comandos propios de Linux, porque la mayoría de servidores con los que interactuarás en tu vida profesional tendrán este sistema instalado. De hecho, siempre que trabajes con GitHub Codespaces (más adelante hablaremos de esta herramienta) estarás trabajando con Linux.

### ¿Cómo puedo averiguar qué comandos, opciones o argumentos puedo utilizar?

Para saber qué comandos, opciones o argumentos podemos utilizar, podemos:

1. Buscar en Google, Stack Overflow, ChatGPT o foros especializados.
1. Utilizar las herramientas especializadas de la terminal. En particular, los comandos `man` y `help`. `man` abre el manual del usuario, mientras que la opción `--help` nos ofrece un resumen de uso sobre el comando que estamos utilizando.

#### Prácticas

1. Abre una terminal en tu codespace y utiliza el comando `help` para ver los comandos que tienes disponibles. Puedes investigar sobre alguno de ellos.
1. Ahora utiliza el comando `man`. Verás que recibes un error. Si te fijas, el error te está diciendo que necesita que le indiques una página. Prueba a escribir `man cp`. En esta ocasión verás que se abren las instrucciones del comando cp (copia). En este ejemplo, man es el comando y cp es un argumento.
1. Sal del manual con `q`, como indica la línea inferior del mismo.
1. Ahora utiliza el comando `cp`. Recibirás un error, porque este comando necesita argumentos (qué archivo queremos copiar y dónde queremos copiarlo). Utiliza la opción help para ver cómo se utiliza este comando: `cp --help`.

## El sistema de archivos

Nuestra terminal siempre va a "ubicarse" en una ruta determinada. Puedes pensar en las rutas como el sistema que muestra cualquier explorador de archivos, así que conoces el modo en que se jerarquizan los archivos.

Por ejemplo, si quiero abrir una foto que está en mi carpeta personal utilizando la GUI, primero tendré que abrir el explorador de archivos, luego viajar hasta mi carpeta personal y por último hacer doble click sobre el icono de la foto.

Pues bien, el CLI no es muy diferente. Al utilizar esta interfaz, lo primero que encontramos es un cursor, que nos indica el lugar en el que nos ubicamos. En este ejemplo, nos encontramos en la ruta /workspaces/curso-git-y-github:

![Cursor de la terminal](/assets/imgs/cursor.png)

En este ejemplo verás que al principio del cursor nos está indicando, además, qué usuario está activo (agarzon48) y al final nos indica en qué rama del repositorio nos encontramos (main). No es necesario que entiendas esto todavía, profundizaremos más adelante.

#### Prácticas

1. Utiliza el comando `pwd` (print working directory) para imprimir por consola tu ruta actual.

### ¿Cómo moverse por el sistema de archivos?

Ya sabes que con el comando `pwd` puedes imprimir tu ubicación actual. Si quieres cambiar esta ubicación, utiliza el comando `cd` (change directory), seguido de la ruta a la que quieras moverte.

![Uso básico del comando cd](/assets/imgs/cd.png)

Si te fijas, al principio de la ruta de destino hemos utilizado una barra. Esta barra representa la raíz de nuestro sistema de archivos. Es decir, el directorio dentro del cual se encuentran el resto de directorios. Se trata de una ruta válida, y podemos visitarla:

![Para volver a la raíz podemos utilizar cd /](/assets/imgs/cd-2.png)

Si queremos volver a nuestra ubicación inicial, deberemos escribir la ruta que nos conduce a ella desde la raíz del proyecto:

![Volver a la ruta original](/assets/imgs/cd-3.png)

El problema de esta forma de navegación es que, si queremos acceder a una carpeta muy anidada, la ruta que tendremos que escribir es muy larga. Para estos casos podemos utilizar las _rutas relativas_. Por ejemplo, fíjate en mi estructura de archivos actual:

![Alt text](/assets/imgs/cd-4.png)

En este caso, si quisiera entrar a mi carpeta de imágenes tendría que utilizar el siguiente comando:

```
cd /workspaces/curso-git-y-github/assets/imgs
```

Sin embargo, al utilizar el comando `pwd` veo que estoy en la siguiente ruta:

```
/workspaces/curso-git-y-github
```

Como ves, ya he recorrido parte del camino. ¿Por qué tengo que escribir la ruta cada vez desde la raíz? Pues lo cierto es que no tengo por qué hacerlo.

Cuando escribo una ruta desde la raíz la llamo "ruta absoluta", porque da igual dónde me ubique yo en ese momento: la ruta siempre será la misma. Sin embargo, puedo utilizar rutas relativas a mi posición actual.

En el ejemplo de arriba, si quiero llegar a la carpeta de imágenes desde donde estoy tendría que acceder a `assets` y desde ahí a `imgs`. Pues bien, para crear una ruta relativa basta con obviar la barra inicial en nuestro argumento:

```
cd assets/imgs
```