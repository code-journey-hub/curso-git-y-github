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

Llamamos repositorio al conjunto de archivos que conforman nuestro proyecto. Para crear un nuevo repositorio tenemos que ejecutar el comando:

```
git init
```

Sin embargo, lo más común es optar por una de estas alternativas:

```
git init --initial-branch=main
git init -b main
```

La segunda es una abreviatura de la primera. El objetivo de ambas es llamar `main` a la rama inicial (más adelante explicaremos qué son las ramas y cómo utilizarlas).

Al ejecutar el comando habremos inicializado el repositorio. Un modo de saber si el directorio en el que nos encontramos tiene un repositorio de git inicializado es lanzar el comando `ls -a`.

![Utilizando el comando `ls -a` para ver si existe un repositorio de git](/assets/imgs/2/repo.png)

## Próximos pasos

Como siempre, seguir aprendiendo, profundizando y mantenerte al día depende de ti. Busca en Internet para encontrar recursos y comunidades especializadas. En este caso, te recomiendo que utilices también estos recursos:

1. [Documentación oficial de git](https://git-scm.com/doc): aunque tiene un aspecto poco amigable si no estás familiarizado o familiarizada con los sitios de documentación, este es el sitio web oficial de git, y por tanto la fuente de verdad a la hora de encontrar referencias, explicaciones e información acerca de cómo utilizar el sistema de control de versiones. Incluye vídeos, tutoriales, libros y otros recursos avanzados.
1. [Colección de cursos de Microsoft](https://learn.microsoft.com/en-us/collections/7pgmtrozd4wp4p): git pertenece a Microsoft. Por ese motivo, el centro de formación de Microsoft incluye recursos de interés, con actividades y tests de evaluación. En su momento preparé esta selección para apoyar el curso.

### ¿Conoces alguna otra fuente de interés?

¡[Abre un issue](https://github.com/code-journey-hub/curso-git-y-github/issues/new) en nuestro repositorio e infórmanos para que podamos evaluar tus recursos y propuestas!
