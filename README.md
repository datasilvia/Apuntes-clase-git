# Apuntes de GIT, GITHUB y GITFLOW


# ¿Qué es GIT?

Es un sistema de control de versiones.

Sirve para llevar un historial de todos los cambios que se hacen en el proyecto, y tener así el control sobre la evolución del mismo.

También se utiliza para el control del desarrollo colaborativo, y el desarrollo en paralelo de funcionalidades.

Git aparece el 7 de abril de 2005.

Su creador es [Linus Torvalds](https://es.wikipedia.org/wiki/Linus_Torvalds)  (la misma persona que hizo Linux)
<center><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/01/LinuxCon_Europe_Linus_Torvalds_03_%28cropped%29.jpg/800px-LinuxCon_Europe_Linus_Torvalds_03_%28cropped%29.jpg" width="100"></center>


## Antes de hacer la instalacion de GIT:

#### ¿Cómo sé si lo tengo ya instalado?

Usando el comnado `git`

#### ¿Cómo puedo saber qué version tengo instalada?


Usando `git --version` o `git -v`

Para obtener ayuda: `git -h`

### Comandos básicos:


`ls` Lista directorios.

`ls -la` Lista directorios con los archivos ocultos.

`cd ..` Para volver al directorio madre.

`pwd` Para saber en qué ruta estoy.

`mkdir` Crea directorio nuevo.

`touch nombre.extension` Crea archivo nuevo.

`clear` o `cls` limpia la consola de comandos.

`code .` Abre el Visual Studio Code.


# Instalación de GIT

En Linux usaremos:

`$ apt-get install git`

Tenemos que configurar nuestro nombre y el email:

`git config --global user.name "nombre"`
 
`got config --global user.email "email"`

Creamos la carpeta donde estará el proyecto, y dentro de ella hacemos:

`git init `

De esta forma estamos constatando que en este proyecto va a haber un control de versiones.

Ahora esta carpeta es un **repositorio**.

Al escribir `git init` se ha creado la carpeta .git (está oculta, así que no aparecerá al hacer `ls`, hay que hacer un `ls -la` para que te aparezca)

`git status` Se usa para ver el estado del repositorio, si existen cambios pendientes de guardar.

<center><table>
    <tr>
     <th>Working Copy</th>
     <th>Staging Area</th>
     <th>Repositorio</th>
     </tr>
  <tr>
    <td>
     <ul>
      <li>Es la carpeta de nuestro proyecto.</li>
      <li>Podemos ver su interior con el explorador de archivos.</li>
      <li>También se le conoce como Working Tree o Unstaged Files.</li>
    </td>
    <td>
     <ul>
      <li>Lugar donde ponemos los cambios que posteriormente guardaremos.</li>
      <li>Solo podemos ver lo que hay en su interior usando algún comando de git.</li>
      <li>También se conoce como Index o Cache.</li>
      </ul>
    </td>
    <td>
     <ul>
      <li>Es el lugar donde se almacenan lo cambios.</li>
      <li>Solo podemos ver lo que hay en su interior usando algún comando de git.</li>
      <li>Repositorio.</li>
     </ul>
    </td>
    </tr>
</table></center>

`git add archivo` Para añadir los cambio hechos en un archivo. (Añadir los cambios al **staging area**).

`git commit -m "nombre del commit"` Para commitear los cambios. (Mover lo que hay en el staging area al **repositorio**).

Es buena practica que el nombre del commit sea descriptivo de los cambios que se han realizado.

`git log` Para  ver un listado de todos los commits que hemos ido haciendo en el proyecto.


### ¿Qué es un commit?

Es un **paquete** que contiene:

<ul>
<li>Uno o más hunks (Cambios en los archivos).</li>
<li>Un mensaje descriptivo de los cambios (lo que escribimos en el texto del commit).</li>
<li>Un hash SHA para identificar el commit (identificador único).</li>
<li>La fecha y hora de creación.</li>
<li>El nombre y e-mail de la autora</li>
</ul>

`git show iddelcommit` muestra el contenido del commit especificado.

`git show HEAD` muestra el contenido del commit al que apunta HEAD.

`git show main` muestra el contenido del commit al que apunta la rama main.


para ver el `git log` más bonito:

`git log --graph --pretty=oneline`

`git log --graph --decorate --all --oneline`


### Crear alias

Lo utilizamos para simplificar si hay algo que vamos a hacer muchas veces y es un comando muy largo. Es crearle un nombre, un alias, más corto y fácil.

`git config --global alias.tree"log --graph --decorate --all --oneline"`

Así cada vez que escribamos `git tree`  obtendremos el mismo resultado que escribiendo `git log --graph --decorate --all --oneline`


### ¿Qué es el archivo .gitignore?

Lo creamos en la raíz del proyecto, e incluímos ahí los ficheros y rutas que no queremos commitear.
`touch .gitignore`
Hay que añdir y commitear el .gitignore después de crearlo.

_______________________________________________________________________________

El comando `git diff` nos sirve para ver exactamente qué ha cambiado en lo que no está preparado.
Con `git diff --staged` vemos los cambios en lo que sí están preparados.

`git checkout` sirve para cambiar el foco.

Puedo poner `git checkout` al hash de un commit anterior, y lo que estoy haciendo es cambiar el HEAD (el foco) ahí.

Cuando usamos GIT todo queda registrado y guardado. A veces puede parecer que han desaparecido archivos que se crearon, pero están guardaditos en la carpeta .git
Lo que ha cambiado ha sido el puntero, el head, el foco.


#### Para borrar un commit.

`git reset --hard iddelcommitalquequieresir`. Si ahora haces un `git log` , ya no se ven los commits que "borraste".

Pero con `git reflog` sí se ve el historial completo.

AHora con `git checkout iddelcommitalquequieresvolver` te posicionas en el commit al que quieres volver, pero tienes que volver a hacer  `git reset --hard iddelcommitalquequieresvolver` para restaurar todo. 

Si haces un `git log` y miras el `git tree` ves que está como antes :)

Por tanto, vemos que el `git reset --hard` funciona en las dos direcciones.


## Tags

Son etiquetas que sirven para etiquetar commits.

Son muy útiles para guardar la referencia de puntos importantes en el proyecto, como por ejemplo las versiones.

`git tag V.01.0`  crea un tag con nombre V.01.0

`git tag --delete V.01.0`  elimina el tal con nombre V.01.0

`git tag` lista los tags

`git checkout tags/V.01.0`  te lleva al tag con nombre V.01.0

Los tags hay que pushearlos al remoto de manera independiente, usando el comando: 

`git push --tags`

## Ramas

Sirven para trabajar en alguna funcionalidad concreta.

Cuando hay varias personas de un equipo trabajando en el mismo proyecto, es habitual que estén trabajando en ramas distintas.

En GitFlow las ramas que se suelen usar son:

Main

Develop

Feature

`git branch` lista las ramas de nuestro proyecto.

`git branch styled` crea una rama llamada "styled".

`git switch styled` te cambia a la rama styled.

`git switch main` te lleva de vuelta a la rama main.

`git checkout -b title` crea la rama title y te lleva a ella.

`git merge styled` te une (mergea) la rama styled con la rama en la que te encuentras en este momento.

`git branch -d title` elimina la rama titled.


### Diferencia entre switch y checkout

`switch` solo te cambia de rama

`checkout` hace mas cosas


## Conflictos

Suceden cuando en varias ramas se modifican las mismas líneas de código y tratas de hacer merge.

En el archivo que suceda el conflicto te informa de 2 posibilidades de resolución.

Borras la que no quieres, y haces un `git add archivo` y `git commit -m "resolución del conflicto"`



`git stash` te guarda algo en Work In Progress (WIP) pero aún no es commit.

`git stash list` lista tus stash

`git stash pop` para volver a tu stash y seguir trabajando ahí. Luego tendrás que hacer un add y un commit.

`git stash drop`  para elimiar el estado de WIP.


Antes de hacer un merge, para ver si tenemos conflictos, podemos usar `git diff rama` para ver las diferencias entre la rama en la que estás y la que nombras en el comando.

Con `diff` ves diferencias entre archivos, y también entre ramas.

`git branch -d rama` elimina la rama.


# GITHUB

Es una plataforma que utiliza git.

Nos facilita que nuestro código esté en un servidor remoto, y que más personas puedan trabajar en él desde distintos lugares.


# GITFLOW

Es un modelo para organizar el flujo de trabajo en git.

Es el más estandarizado actualmente, pero no es el único.

Facilita la colaboración entre equipos.

Al usar ramas independientes, contribuye a la paralelización del desarrollo.

Ayuda a mantener el historial del desarrollo del proyecto limpio y organizado.

Mejora la trazabilidad del código y la capacidad de revertir cambios.

Proporciona un flujo de trabajo claro y predecible para el equipo de desarrollo.
