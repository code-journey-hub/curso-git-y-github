# Introducción a git

Git es la herramienta que más vamos a utilizar como desarrolladores y desarrolladoras. Se trata de un sistema de control de versiones, gracias al cual podremos:

1. Disponer de diferentes versiones de nuestros programas y aplicaciones.
1. Rescatar nuestro trabajo desde diferentes dispositivos.
1. Colaborar con otros desarrolladores y desarrolladoras.
1. En caso de error, rescatar una versión previa del proyecto, antes de que se rompiera.

Aunque esta herramienta es muy común en el sector de desarrollo de software, lo cierto es que también se puede utilizar en otros ámbitos. Por ejemplo, para coordinar la redacción de un proyecto u organizar ideas para escribir una novela.

## ¿Qué es git?

Git es un sistema de control de versiones gratuito de open source. Durante este curso vamos a aprender a utilizarlo desde la consola, ya que lo más común es que utilices tu CLI para gestionar el proyecto, pero también existen herramientas gráficas para interactuar con el sistema.

Necesitaré que [instales git](https://git-scm.com/) en tu ordenador en caso de no tenerlo instalado. Una forma de comprobar si tienes git instalado es abriendo la terminal y ejecutando el siguiente comando:

```
git --version
```

Si obtenemos una respuesta es porque git está instalado en nuestra máquina. En caso contrario, visita la página oficial de git y descarga e instala la última versión. Si has instalado git pero sigues recibiendo un error del tipo "No se reconoce git como un programa o comando" tendrás que comprobar que la instalación se haya realizado correctamente y git esté añadido a tu PATH. Puedes buscar información al respecto en Google, ya que es un error común.

Una vez hayas instalado git, podemos seguir con la clase. Ten en cuenta que si trabajas desde GitHub Codespaces, Gitpod u otro sistema similar, git vendrá instalado de antemano en tu máquina virtual.

## Configuración de git

Siempre que queramos utilizar un comando de git seguiremos la siguiente sintaxis:

```
git <instrucción>
```

Esta es nuestra forma de indicarle a la máquina que queremos utilizar una funcionalidad de git.

Lo primero que deberíamos hacer es [configurar nuestra instalación](https://git-scm.com/docs/git-config). Al menos, nuestro nombre e email:

```
git --global config user.name <nombre de usuario>
git --global config user.email <email de usuario>
```

Ten en cuenta que en cada proyecto puedes sobreescribir esta configuración global.

## Estructura y funcionamiento de un repositorio

Llamamos repositorio al conjunto de archivos que conforman nuestro proyecto. Un repositorio, además, funciona como un histórico de cambios. Gracias a ello podemos restaurar nuestros archivos a una versión anterior o alternativa.

Para crear un nuevo repositorio tenemos que ejecutar el comando:

```
git init
```

Sin embargo, lo más común es optar por una de estas alternativas:

```
git init --initial-branch=main
git init -b main
```

La segunda es una abreviatura de la primera. El objetivo de ambas es llamar `main` a la rama inicial (más adelante explicaremos qué son las ramas y cómo utilizarlas).

Al ejecutar el comando habremos inicializado el repositorio. El mejor modo de saber si estamos en un directorio que forma parte de un repositorio de git es lanzar el comando `git status`. Como verás, este comando es de gran utilidad a la hora de conocer el estado de nuestro repo, y de hecho lanzará un error cuando se ejecute fuera de un repo.

Otro modo de saber si el directorio en el que nos encontramos tiene un repositorio de git inicializado es lanzar el comando `ls -a`. Voy a centrarme en este para analizar la anatomía de un repositorio de git.

![Utilizando el comando `ls -a` para ver si existe un repositorio de git](/assets/imgs/2/repo.png)

Si te fijas en el outputde la consola, verás que encontramos una carpeta oculta, con el nombre `.git`. Este es el lugar desde el que se va a gestionar tu proyecto.

### La carpeta .git

Nunca debemos manipular manualmente la carpeta .git o sus contenidos, ya que es el propio programa el que se va a encargar de gestionarlos. De hecho, si eliminamos el directorio y lanzamos un `git status` comprobaremos que acabamos de eliminar el repo.

Sin embargo, me interesa analizar someramente su contenido antes de seguir, para que entiendas que toda la información relativa al repositorio está aquí dentro. Si inspeccionas los archivos de dentro del directorio `.git` verás ficheros como config o description que, obviamente, contienen la configuración del repositorio o su descripción. También encontrarás un archivo que define el HEAD, que te explicaré más adelante.

Por último, encontraremos directorios donde podemos almacenar diferentes tipos de objetos. Hay cuatro tipo de objetos en un repo: Blob (almacenamiento de archivos), Tree (almacenamiento de directorios), Commit, Annotated Tag (almacenamiento de anotaciones de texto). Ahora mismo solo nos interesa el commit, que explicaremos más adelante.

### ¿Dónde debo crear mi repositorio?

El repositorio admite directorios anidados. De modo que a la hora de lanzar `git init` debemos asegurarnos de estar en la raíz de nuestro proyecto. Es decir, en la carpeta más alta jerárquicamente.

No debemos iniciar repositorios dentro de otros repositorios salvo que sepamos lo que estamos haciendo. De modo que una buena idea puede ser lanzar `git status` antes de `git init` para asegurarnos de que no estamos ya dentro de un repo.

Ten en cuenta que muchos comandos de git utilizan rutas de archivos. De modo que es importante asegurarse también de que proporcionamos correctamente la ruta de los archivos con los que estemos trabajando.

## El flujo de trabajo con git

En esta sección aprenderemos acerca de los "tres árboles" de git para entender cómo utilizar el sistema. Los árboles hacen referencia al sistema de archivos, por su estructura ramificada.

#### Prácticas

1. Crea una carpeta y utiliza el comando `git status`. Debería quejarse de que no existe un repo (en caso contrario, busca el directorio `.git` y elimínalo).
1. Inicializa un repositorio de git con `git init -b main` y vuelve a lanzar `git status`.

### El árbol de trabajo

En primer lugar tenemos el árbol de trabajo (`working directory`). Se trata del conjunto de archivos sobre los que trabajamos directamente. Por ejemplo, si añado un archivo `index.html` a mi proyecto estoy incorporando un fichero al árbol de trabajo. Si añado unas líneas a mi archivo `styles.css` estoy editando el árbol de trabajo. En resumen, el árbol de trabajo no es más que el sitio donde estoy trabajando.

Los repositorios de git están configurados para hacer un seguimiento del árbol de trabajo, por lo que si hacemos cualquier cambio y lanzamos `git status` veremos un listado de nuestros cambios desde nuestro último `commit` (ahora entraremos a explicar qué es un `commit`, de momento entiéndelo como un _checkpoint_ o una fotografía del estado actual del repositorio).

Cuando estemos satisfechos con los cambios que hemos realizado, podremos añadirlos al staging area con el comando:

```
git add <ruta del archivo>
```

Normalmente nos ubicaremos en la raíz para utilizar esta versión del comando:

```
git add .
```

Como sabes, `.` es un alias para "esta carpeta", por lo que al lanzar este comando desde la raíz del proyecto le estamos diciendo al repo "eh, quiero que añadas todos los cambios al área de staging".

#### Prácticas

1. Haz algunos cambios en el árbol de trabajo. Por ejemplo, añade algunos archivos.
1. Luego, lanza de nuevo el comando `git status`. Verás que git detecta que se han hecho cambios en el repo, pero que no se han añadido al staging area.
1. Vete a la raíz del proyecto y lanza `git add .` para añadir todos los cambios al staging area. Esta operación nos permite marcar los cambios realizados como candidatos a guardarse en la nueva versión del repo.

### El staging area

En segundo lugar tenemos el área de ensayo (`staging area`). En este lugar podemos encontrar todos los cambios realizados desde el último `commit` (todavía no ha llegado el momento de explicarlo).

Las operaciones que realizaremos con estos cambios son, básicamente, dos: retirarlos del área de ensayo o confirmarlos para la siguiente versión.

Si queremos retirarlos del área de ensayo utilizaremos el siguiente comando:

```
git restore --staged <nombre-del-archivo>
```

Cuando estemos satisfechos con el estado del proyecto podremos crear una confirmación (`commit`). El commit guardará todos los cambios que haya en el staging area dentro del repositorio. Para ello utilizaremos el siguiente comando:

```
git commit -m "Mensaje descriptivo del motivo de confirmación"
```

Como ves, al hacer commit debemos incluir un mensaje. Esto nos permitirá entender mejor qué cambios ha introducido cada `commit` al repositorio.

#### Prácticas

1. Saca alguno de los archivos que hayas incluido en el staging area.
1. Ahora, confirma el resto de los archivos.
1. Vuelve a lanzar `git status` para ver el estado de tu repo.

### El repositorio

Por último tenemos el propio repositorio (`repository`). Como ves, el repositorio no es más que una colección de commits. Y cada commit es una instantánea que refleja el estado del repositorio en un momento dado.

Esta es precisamente la razón por la que git nos permite controlar versiones: el repositorio es un histórico de confirmaciones, y si en la última confirmación he metido un bug, puedo revertirla. O tal vez incorporé o eliminé una funcionalidad en algún momento que ahora debo retirar o recuperar. En ese caso no tengo más que buscar el momento en que lo hice para revertirlo.

Una forma de ver este histórico es mediante el comando `git log`. Personalmente, yo suelo utilizarlo con la opción `--oneline`, porque reduce el output y lo hace más fácil de seguir (rara vez necesitarás más detalles que los que te ofrezca esa línea).

#### Prácticas

1. Utiliza `git log` para analizar el histórico de tu repositorio.

## Viajes en el tiempo

El hecho de que un repositorio sea un histórico de commits implica que podemos viajar a un commit anterior en el tiempo si de pronto hemos introducido errores o hemos roto el proyecto sin querer. Por supuesto, que podamos hacerlo no significa que sea lo idóneo, ya que en ocasiones nos encontraremos con problemas para conciliar ambas versiones del código, especialmente hasta que nos hayamos familiarizado con git. Sin embargo, disponer de esta opción implica que es casi imposible que rompamos el proyecto sin querer.

### git checkout

Cada commit tiene un hash asociado, que podemos rescatar con `git log`. Con `checkout` podemos restaurar nuestro árbol de trabajo al estado que tenía en un momento determinado, indicando el commit que queremos restaurar:

```
git checkout <commit-hash>
```

En este momento (y si lanzamos `git status`) veremos un aviso como que estamos en "Detached HEAD". HEAD hace referencia al commit en el que nos encontramos, que normalmente será el último commit de una rama (más adelante hablaremos de ramas, de momento solo estamos trabajando con una única rama, que hemos llamado _main_).

Como hemos saltado a un momento anterior en el tiempo, pero sin eliminar todos nuestros cambios posteriores, el sistema indica que ahora mismo, HEAD no está en el último commit de la rama.

Para salir del estado "Detached HEAD" basta con que volvamos al último commit de la rama (con checkout) o que volvamos a la rama en sí (con checkout o switch). Como estos temas entran en materia propia de las ramas, los trataremos más adelante, pero te dejo por aquí los comandos que necesitarías para salir de este estado:

```
git checkout <commit-hash>
git switch main
```

¿Para qué sirve el estado "Detached HEAD"?

Básicamente porque me permite consultar cómo estaba el proyecto en un momento determinado. También me permite crear nuevas ramas para rescatar archivos o cambios perdidos, pero esto lo entenderemos mejor cuando sepamos utilizar ramas.

El comando `git checkout <hash> <file>` también nos permite recuperar archivos determinados en el estado que tenían en el commit indicado. Por ejemplo, si por error hemos eliminado la imagen ubicada en `assets/imgs/icon.ico`, podríamos restaurarla con el siguiente comando:

```
git checkout HEAD assets/imgs/icon.ico
```

#### Prácticas

1. Edita el contenido de un archivo y realiza el flujo `add` - `commit` varias veces para añadir varios commits a tu repo.
1. Visita las versiones anteriores de tus archivos con `git checkout` y vuelve a la última versión.
1. Ahora, elimina un archivo.
1. Recupéralo utilizando el comado checkout.

### git restore

El problema del comando checkout es que sirve para diferentes funcionalidades. Ya has visto que hemos tenido que hablar prematuramente de las ramas.

Para evitar la utilización de comandos que sirvan para finalidades muy diversas se introdujeron comandos como `restore` o `switch`. Con `git restore` podemos echar atrás los cambios que hayamos hecho en cualquier archivo desde nuestro último commit:

```
git restore <file-name>
```

Este comando también nos sirve para quitar del staging area archivos que hayamos añadido por error, como hemos visto anteriormente:

```
git restore --staged <file-name>
```

#### Prácticas

1. Haz cambios en, al menos, dos archivos diferentes.
1. Añade uno de ellos al staging area.
1. Ahora sácalo del staging area.
1. Devuelve los archivos a su estado original.

### git reset

`git reset` solicitará que indiquemos un commit objetivo, y restaurará el repo al estado de ese comit eliminando los posteriores:

```
git reset <commit-hash>
```

Ten en cuenta que `git reset` afectará al repo, pero no necesariamente a nuestro working directory. Para que los cambios se reseteen también en nuestro árbol de trabajo deberemos utilizar la opción `--hard`.

Se trata, por tanto, de una forma de echar atrás uno o varios commits, pero puede ser destructivo si no se utiliza con cuidado.

#### Prácticas

1. Edita el contenido de un archivo y realiza el flujo `add` - `commit` varias veces para añadir varios commits a tu repo.
1. Revisa tu historial con `git log --oneline`.
1. Elige uno de tus commits anteriores y devuelve el repo a su estado. Asegúrate de que también cambia el árbol de trabajo.
1. Vuelve a lanzar `git log --oneline`

### git revert

`git revert` cumple un objetivo similar a `git reset`, ya que indicaremos un commit que queremos revertir. Sin embargo, no eliminaremos los commits posteriores, como ocurre con git reset, sino que crearemos un nuevo commit que deshaga los cambios realizados desde el commit seleccionado.

Dado que respeta el historial previo, suele ser preferible a `git reset`, especialmente cuando estamos trabajando en equipo.

#### Prácticas

1. Edita el contenido de un archivo y realiza el flujo `add` - `commit` varias veces para añadir varios commits a tu repo.
1. Revisa tu historial con `git log --oneline`.
1. Elige uno de tus commits anteriores y devuelve el repo a su estado. Asegúrate de que también cambia el árbol de trabajo.
1. Vuelve a lanzar `git log --oneline`

## Ramas

Como hemos visto, un repositorio de git es un histórico de commits, que son representaciones de cómo era nuestro repositorio en el momento de ejecutar el comando `git commit -m 'nombre del commit`. También hemos visto que gracias a que vamos guardando estas "instantáneas", podemos "viajar atrás en el tiempo".

Esto se de debe a que todos los commits (salvo el inicial) guardan una referencia al commit anterior. De modo que si seguimos esta referencia podemos ir dando pasos atrás, hasta llegar al primer commit de nuestro repositorio. Además, cada commit tiene un hash que, como hemos visto, podemos consultar con `git log` y utilizar para viajar hasta él con `git checkout`.

Entender esta estructura nos lleva a los conceptos de HEAD y branch (rama). Una rama es una versión alternativa de nuestro proyecto. Por ejemplo, imagina que estás diseñando una interfaz y tienes que desarrollar una propuesta en esquema de color oscuro y otra en esquema de color claro, para que la dirección del proyecto elija la que más le guste. En este caso estamos hablando de dos versiones diferentes del proyecto, y git nos permite trabajar en ellas simultáneamente.

Para ello crearemos ramas, cosa que podemos hacer con el comando `git branch`. Lo cierto es que también podemos hacerlo con `git checkout`, que es como se ha hecho tradicionalmente, pero las últimas versiones de git incorporaron comandos como `restore` o `branch` para evitar el uso de comandos multiuso como `checkout`.

```
git branch <nombre-de-la-rama>
```

Con este comando podemos crear una rama para la versión oscura y otra rama para la versión clara de nuestro proyecto. Cada rama representará una versión del código, y los cambios que hagamos en una rama no afectarán a la otra.

Este es el modo en que se trabaja en la mayoría de estudios, proyectos y empresas. Cada característica que se va a añadir al proyecto se desarrolla en una rama, lo que permite que el resto de personas que estén utilizando el proyecto o trabajando en él lo hagan sin que les afecten los nuevos cambios.

Una vez creada la rama podemos cambiar a ella con el comando `switch`:

```
git branch version-clara
git switch version-clara
```

Este comando es equivalente al clásico

```
git checkout <nombre-de-la-rama>
```

También podemos hacer ambos pasos si al comando `branch` le pasamos la opción `create`:

```
git switch -c version-clara
```

Al crear una nueva rama, podremos trabajar una versión alternativa del código. En cuanto estemos satisfechos con nuestro trabajo y queramos hacerlo oficial, deberemos llevar todos los cambios que hemos hecho a la rama principal, habitualmente conocida como `main` o `master`. Para ello tendremos que seguir dos pasos:

1. En primer lugar, iremos a la rama de destino. En este ejemplo, `main`:

```
git switch main
```

2. En segundo lugar, indicaremos la rama cuyos cambios queremos hacer oficiales:

```
git merge version-clara
```

Esto permite a cada desarrollador o desarrolladora trabajar en una rama separada, o bien reservar ramas para cada característica del código, de modo que solo se unan cuando el trabajo haya terminado y sea estable.

Una vez terminado el trabajo en una rama conviene eliminarla:

```
git branch -D <nombre-de-la-rama>
```

Recuerda que en todo momento puedes utilizar el comando `branch` para ver en qué rama estás y qué ramas hay disponibles.

```
git branch
```

### HEAD

Anteriormente hemos hablado del concepto HEAD, y ahora ya sabes todo lo que necesitas para entenderlo. Conocemos HEAD como el lugar "en el que nos encontramos".

Por ejemplo, hemos hablado de las ramas y hemos dicho que podemos tener una rama dedicada a un tema oscuro y otra dedicada a un tema claro. Pero... ¿Cuál de los temas se mostrará en pantalla?

Pues bien, si mi HEAD está en la rama del tema oscuro, se mostrará el tema oscuro. Si está en la rama del tema claro, se mostrará el tema claro. Y si está en un commit hecho hace dos meses, se mostrará la versión del código que hubiera hace dos meses.

Así que puedes entender el HEAD como un puntero. Si entiendes cada commit como una especie de marcapáginas en un libro, el HEAD es la página que has elegido para que esté abierta. Del mismo modo que en un libro tienes que elegir qué página abres, en un repositorio tienes que elegir qué código forma parte de tu árbol de trabajo.

## Trabajo colaborativo (servidores locales)

Ahora sabes cómo mantener diferentes versiones de tu código. Puede que todavía no entiendas la utilidad, pero con el tiempo y la práctica verás que es muy conveniente contar con entornos aislados en los que hacer cambios, para que si algo se rompe no afecte al resto del proyecto. Y eso es una rama.

Además, disponer de varias versiones del código permite que cada desarrollador tenga una versión aislada. Lo cual facilita el trabajo en equipo. A la hora de desarrollar o mantener un proyecto, cada partícipe o equipo podrá trabajar en una funcionalidad, poniéndola en común una vez haya terminado.

Esto significa que todo el equipo estará compartiendo un repositorio. De modo que tendremos:

1. El repositorio local, donde estamos haciendo nuestros cambios.
1. El repositorio remoto, donde enviaremos nuestros cambios una vez sean definitivos, o desde donde traeremos los cambios de nuestros compañeros y compañeras.

La gestión del repositorio remoto se hace con la herramienta `remote`. Por ejemplo, si queremos ver a qué repositorios remotos está conectado nuestro repositorio local podemos lanzar:

```
git remote -v
```

Si nuestro repositorio local no está conectado con ningún repositorio remoto, podremos conectarlo utilizando:

```
git remote add <nombre-del-remoto> <direccion-del-repositorio>
```

Como ves, a la hora de crear una conexión debemos ponerle un nombre. Normalmente se llama origin al repositorio principal. Este nombre es libre, ya que funciona simplemente como una etiqueta, para que identifiquemos el remoto. También necesitamos una dirección donde ubicar el repositorio remoto, que puede radicar en nuestra propia máquina, en la red local o estar en un servicio remoto tipo github, gitlab o similar.

También podemos eliminar remotos con:

```
git remote rm <nombre-del-remoto>
```

O cambiarlos con:

```
git remote set-url <nombre-del-remoto> <direccion-del-nuevo-repositorio>
```

### Cómo trabajamos en equipo

Cuando trabajamos en equipo, cada integrante del equipo tendrá su repo local y los cambios se enviarán y recogerán del repo común. Para saber si ha habido cambios en el repo común desde que nos conectamos por última vez podemos utilizar:

```
git fetch
```

Ten en cuenta que si varias personas o equipos trabajamos en el mismo proyecto, es probable que mientras yo estoy desarrollando una funcionalidad otros compañeros y compañeras hayan terminado de desarrollar otras. En este caso habrán enviado sus cambios al repo común, y yo tendré que conectarme para actualizarme con esos cambios. `fetch` me indicará si ha habido cambios. En caso afirmativo, para descarlarlos utilizaré el siguiente comando:

```
git pull
```

`pull` es el comando que indica que queremos "traernos" cambios. En este caso, queremos traer los cambios que nuestros compañeros han hecho en el repo remoto al repo local.

Si lo que queremos hacer es subir cambios, lo haremos con el comando `push`. Lo que pasa es que si creamos una rama en local, que no existe en el remoto, y queremos guardar los cambios en el remoto, lo primero que tendremos que hacer es crear una rama homónima en el repo remoto.

Para ello vamos a ejecutar el comando:

```
git push <nombre-del-remoto> <nombre-de-la-rama>
```

Esto se puede volver molesto. Imagina que nuestro remoto se llama "origin" y la rama sobre la que estamos trabajando se llama "feature/dark-theme". Esto significa que cada vez que queramos guardar cambios en el repo remoto tendremos que ejecutar el siguiente comando:

```
git push origin feature/dark-theme
```

Pero, si siempre vamos a subir los cambios al mismo remoto y en la rama en la que estamos trabajando, ¿no sería mejor que el comando fuera simplemente `git push`?

En realidad podemos hacerlo. Siempre que antes establezcamos una conexión entre nuestra rama y la rama del remoto a la que queremos subir nuestros cambios. Para ello utilizamos el siguiente comando:

```
git push -u origin feature/dark-theme
```

-u es la abreviación de `--set-upstream-to`, y lo que indica es que, a partir de este momento, siempre que lancemos `git push` desde esa rama queremos que los cambios suban a la rama "feature/dark-theme" del repositorio "origin".

### Pull Request

Generalmente, cuando trabajamos en equipo no es buena idea tirar de `push` directamente. Esto se debe a que provocaremos cambios en el repo principal, lo que puede llevar a que:

1. Cometamos errores, introduciendo bugs, incorrecciones o código "sucio" en la versión oficial de nuestro proyecto.
1. Introduzcamos cambios de los que no son conscientes nuestros compañeros y compañeras.

Al trabajar en equipo suele ser mejor que todo el equipo participe en la revisión del código y su incorporación al proyecto oficial. De hecho, es probable que haya personas encargadas de revisar la corrección de nuestro código, y que este no pueda incorporarse a la versión oficial sin su visto bueno.

En estos casos utilizamos la herramienta conocida como `pull request`: no incorporamos nuestros cambios al repo oficial, sino que pedimos al repo oficial que incorpore nuestros cambios:

```
git request-pull <commit-inicial> <destino> <commit-final>
```

Si en lugar de empujar nuestros cambios solicitamos su incorporación, damos a nuestros compañeros y compañeras la oportunidad de revisar nuestro código antes de hacerlo público.

Los pull request también se pueden utilizar cuando trabajamos en solitario, ya que van a generar un informe con los cambios que hay entre los commits inicial y final, lo cual nos permite revisar el código que vamos a incorporar al proyecto. Sin embargo, lo cierto es que donde más peso tienen es en el desarrollo colaborativo. Y para entenderlo conviene que nos adentremos en el uso de herramientas como github.

## Próximos pasos

Como siempre, seguir aprendiendo, profundizando y mantenerte al día depende de ti. Busca en Internet para encontrar recursos y comunidades especializadas. En este caso, te recomiendo que utilices también estos recursos:

1. [Documentación oficial de git](https://git-scm.com/doc): aunque tiene un aspecto poco amigable si no estás familiarizado o familiarizada con los sitios de documentación, este es el sitio web oficial de git, y por tanto la fuente de verdad a la hora de encontrar referencias, explicaciones e información acerca de cómo utilizar el sistema de control de versiones. Incluye vídeos, tutoriales, libros y otros recursos avanzados.
1. [Colección de cursos de Microsoft](https://learn.microsoft.com/en-us/collections/7pgmtrozd4wp4p): git pertenece a Microsoft. Por ese motivo, el centro de formación de Microsoft incluye recursos de interés, con actividades y tests de evaluación. En su momento preparé esta selección para apoyar el curso.

### ¿Conoces alguna otra fuente de interés?

¡[Abre un issue](https://github.com/code-journey-hub/curso-git-y-github/issues/new) en nuestro repositorio e infórmanos para que podamos evaluar tus recursos y propuestas!
