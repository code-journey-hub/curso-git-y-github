# Introducción a GitHub

GitHub es una plataforma ideada para almacenar repositorios remotos en la nube. Esto nos permite colaborar con desarrolladores y desarrolladoras de todo el mundo, pues como has aprendido en la sección dedicada a las ramas de git, cada persona que contribuye al proyecto puede tener una versión del código en la que está implementando una funcionalidad y todo el público puede acceder a otra u otras versiones oficiales.

Existen otras plataformas con el mismo objetivo, como BitBucket o GitLab. Y en el tema anterior vimos que, en realidad, basta con instalar git en una máquina para que se pueda utilizar como repositorio remoto. Sin embargo, nos vamos a centrar en GitHub porque es la más conocida y utilizada.

Además, GitHub tiene una vertiente de red social muy interesante para los desarrolladores y desarrolladoras. Puedes utilizar la plataforma para descubrir proyectos de interés o conocer a personas con quienes compartas inquietudes, para participar en proyectos de código abierto o para mostrar tus proyectos. De hecho, es una de las fuentes que muy probablemente consultará un reclutador antes de contratarte.

Pese a su nombre, git y GitHub son cosas diferentes. Como ya has visto, git es un sistema de control de versiones, y no depende en absoluto de GitHub. Podrías utilizarlo profesionalmente sin que existiera GitHub siquiera.

Por su parte, GitHub incluye una serie de prestaciones y funcionalidades en torno al control distribuido de versiones. No podría existir sin git, y hace referencia específicamente al conjunto de servicios de la compañía, actualmente propiedad de Microsoft.

## Qué es y cómo funciona GitHub

GitHub es una red social, que conecta a desarrolladores y desarrolladoras de todo el mundo. También es un servicio en la nube que nos permite sincronizar repositorios compartidos. Además, podemos explorar proyectos en su página web, así como clonarlos y adaptarlos a nuestras necesidades. Y también cuenta con servicios de ejecución de cógigo, despliegue, testeo, recomendación, planificación, revisón... se trata, por tanto, de una herramienta muy completa que conviene controlar como desarrollador.

## Creación de cuenta en GitHub

Si no lo has hecho todavía, deberías crearte una cuenta en [GitHub](https://github.com/) para poder continuar con el curso. Hasta ahora podías trabajar con tu terminal, pero a partir de este momento vamos a centrarnos en github.

## Creación de repo en GitHub

Existen diferentes formas de crear un repositorio en GitHub. Una vez entremos en la interfaz de creación del repositorio tendremos que rellenar algunos datos básicos como el nombre o descripción, y marcar opciones como si queremos que sea un repo público o privado o si queremos incluir algunos archivos iniciales.

El hecho de que sea un repo privado implicará que no lo podrá consultar nadie salvo nosotros o las personas a las que autoricemos. Si es público, todo el mundo tendrá acceso, pero esto no significa que puedan hacer cambios en nuestro código sin nuestro permiso. Lo que sí podrán hacer es un `fork` (es como se llama a copiar un repositorio de otra persona en neustra cuenta de GitHub), editarlo y luego mandarnos un pull request, pidiendo que incorporemos sus cambios en nuestro repo.

Para crear un repo de GitHub podemos utilizar tanto la GUI de su página web como su [CLI](https://cli.github.com/).

```
gh repo create
```

## git clone

Si hemos creado nuestro repo desde la interfaz web de GitHub o queremos trabajar sobre un repositorio público o compartido, tenemos dos opciones:

1. Trabajar desde GitHub codespaces (luego hablaremos de esto).
1. Clonar el repositorio en nuestra máquina.

Para clonar un repositorio basta con que vayamos al directorio donde queremos hospedarlo y ejecutemos:

```
git clone <url-del-repo>
```

Esto creará una copia del repo en nuestra máquina, lo que nos permitirá trabajar en él. Cuando vayamos implementando funcionalidades iremos ejecutando el flujo de trabajo habitual `add` - `commit` y después haremos `push` para subir nuestros cambios al repo de GitHub. Esto permitirá que otras personas conectadas al mismo repo puedan bajarse nuestras actualizaciones con el comando `git pull` o comprobar que las hemos hecho con el comando `git fetch`.

## Flujos de trabajo en GitHub

Cada empresa o proyecto tiene un flujo de trabajo particular, que se adapta a sus necesidades, costumbres o gustos. Por tanto, existen muchos flujos de trabajo diferentes.

Algo que comparten todos los flujos de trabajo es que cuando implementamos cambios en el código tenemos que hacer `add` - `commit` - `push` para añadir los cambios de nuestro árbol de trabajo al área de ensayo, de ahí crear una confirmación y, por último, incorporar esta confirmación al repo común.

Lo que sí difiere de un sistema a otro es, por ejemplo, las ramas utilizadas. Aunque la filosofía DevOps ha hecho que enfoques [basados en troncos](https://www.atlassian.com/es/continuous-delivery/continuous-integration/trunk-based-development) ganen peso, lo cierto es que muchas empresas y proyectos siguen uilizando flujos basados en gitflow, que además creo que son más sencillos de entender al iniciarse en el uso de GitHub o herramientas similares.

Gitflow propone que haya una rama principal, que suele llamarse "main" o "master". Esta rama representará la versión oficial del proyecto.

Además de esta rama, existirá una rama "dev", "develop" o similar, donde el equipo irá haciendo sus aportaciones. Cada aportación se desarrollará en una rama "feature", y al terminarse se hará `merge` desde develop. Esto significa que cada rama "feature" va a desarrollar una prestación y todas ellas se van a juntar en "develop". Cuando haya suficientes cambios en "develop" como para sacar una nueva versión del proyecto, se hará un `merge` desde "main".

A estas ramas se juntan otras, como las "hotfix", cuyo objetivo es parchear _bugs_ de forma urgente sin pasar por todo el proceso burocrático de crear rama - incorporar a dev - incorporar a main.

Aunque de momento no es imprescindible que te acojas a uno de estos flujos, te recomiendo familiarizarte con el modelo [gitflow](https://www.atlassian.com/es/git/tutorials/comparing-workflows/gitflow-workflow) para empezar.

## GitHub codespaces

Los Codespaces de GitHub son máquinas virtuales que podemos utilizar para desarrollar nuestros proyectos online. Como ventajas, se trata de entornos aislados, que además mantienen una configuración homogénea, lo que permite que varios miembros del equipo colaboren en igualdad de condiciones aunque sus equipos y configuraciones sean diferentes.

A lo largo del curso los utilizaremos recurrentemente, pero debes saber que existen servicios alternativos como [gitpod](https://www.gitpod.io/).

Para abrir un codespace solo tenemos que ir a la página principal de un repo y hacer click en "Code". Conviene que te familiarices con las políticas de uso, y particularmente con las de precios, materia en la que no entro aquí porque probablemente cambien desde que escribo hasta que lees.

## GitHub projects

GitHub projects nos permite integrar los issues que se puedan abrir en cualquier repositorio en un tablero kanban o una tabla con diferentes funcionalidades, todas ellas encaminadas a planificar y evaluar la realización de un proyecto.

## Próximos pasos

Como siempre, seguir aprendiendo, profundizando y mantenerte al día depende de ti. Busca en Internet para encontrar recursos y comunidades especializadas. En este caso, te recomiendo que utilices también estos recursos:

1. [Colección de cursos de Microsoft](https://learn.microsoft.com/en-us/collections/7pgmtrozd4wp4p): git pertenece a Microsoft. Por ese motivo, el centro de formación de Microsoft incluye recursos de interés, con actividades y tests de evaluación. En su momento preparé esta selección para apoyar el curso.

### ¿Conoces alguna otra fuente de interés?

¡[Abre un issue](https://GitHub.com/code-journey-hub/curso-git-y-GitHub/issues/new) en nuestro repositorio e infórmanos para que podamos evaluar tus recursos y propuestas!
