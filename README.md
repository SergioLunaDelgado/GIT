# GIT

## Ayuda

**`git --version` o `git -v`**
* Muestra la versión instalada de Git.

**`git help` o `git -h`**
* Muestra la ayuda general de Git y una lista de todos los comandos disponibles.

**Archivo `.gitkeep`**
* Hace que mantenga y agregue una carpeta vacia al stage. El archivo debe estar vacio, la idea es que no pese

**Archivo `.gitignore`**
* Ignora los archivos y carpetas que se agregaran al stage, como por ejemplo la carpeta de **node_modules**

> [!NOTE]
> Este alias es muy util para revisar la historia de los commit´s. Es la versión mejorada del **git log**. <br>
> `git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"`
>
> Deshacer el último commit <br>
> `git config --global alias.undo 'reset --soft HEAD~1'`
> 
> Rehacer el último commit <br>
> `git config --global alias.redo 'reset HEAD@{1}'`


## Configuración

**`git config --global user.name "Lorem Ipsum"`**
* Establece el nombre de usuario global para Git.

**`git config --global user.email "lorem@ipsum.com"`**
* Establece el correo global para Git.

**`git config --global -e`**
* En listar las configuraciones globales.

**`git config --global core.autocrlf true`**
* Configurar salto de linea (como mi SO es Windows tengo que escribir el valor de true, si fuera Linux/Mac escribo input).

**`git config --global core.editor "code --wait"`**
* Configura a vs code como IDE por defecto y el --wait espera a terminar la instruccion hasta que se cierre el archivo en vs code.

**`git config --global init.defaultBranch main`**
* Establecer rama principal como **main**.

**`git config --global pull.ff only`**
* Cuando hagamos un pull solamentre traer los fast forward.

**`git config --global pull.rebase true`**
* Si realizamos una modificación en una misma línea en un mismo archivo tanto en GitHub como de forma local creamos un conflicto.
* Con esta línea podemos resolver este conflicto dentro de nuestro editor de texto.
* En caso de existir un conflicto nosotros damos respuesta añadimos y realizamos un commit pero nos encontramos en un rebase interactivo así que para terminar usamos el *git rebase --continue*.
* Al final lo podemos hacer permanente con un push

## Repositorio local

**`git init`**
* Iniciar el repositorio local.

**`git status`**
Información de los commits y las ramas.

> [!NOTE]
> Status
> * M modificado
> * U creado
> * R renombrado
> * A agregando

**`git add README.md` o `git add /carpeta` o `git add .`**
* Agregar archivos, carpetas o todos las modificaciones al stage.

**`git reset README.md` o `git reset /carpeta` o `git reset .`**
* Inverso del **add**.

**`git commit -m "first commit"`**
* Salva los cambios de forma local que se encuentran en el stage.

**`git checkout -* .` o `git checkout -* README.md` o `git checkout ##### -* README.md`**
  * Reconstrulle el proyecto como lo teniammos al dar el ultimo commit.

**`git branch`**
* Mostrar en que rama estamos. 
* "**-a**" enlistamos las ramas en local y en repositorio, a pesar de ser borradas.
* "**-m main**" cambia el nombre de la rama.

**`git log`**
* Ver el historial de los commits.

**`git diff`**
* Compara los cambios con el ultimo commit.

## Modificaciones

**`git commit --amend -m "mensaje nuevo"`**
* Con este comando puedo reescribir titulo del ultimo commit.

**`git reset --soft HEAD~` o `git reset --soft #######`**
* Lo que hace este comando es retroceder la referencia HEAD al commit anterior al último commit actual.
* Si es necesaro agregar cosas al ultimo commit podemos usar este comando. Esto es como alternativa a crear otro commit.

**`git reset --mixed HEAD~` o `git reset --mixed #######`**
* Hace lo mismo que el "**--soft**" pero conserva los cambios en el directorio de trabajo.

> [!CAUTION]
> **`git reset --HARD #######`**
> * Esto regresa **todo** hasta el commit indicado. 
> * Usar el hash del commit al que se quiere hacer rollback. 
> * Ya sea hacia adelante o atras. 
> * En automático esto se convierte en el HEAD.

> [!NOTE]
> No es recomendable jugar con los cambios en el tiempo lo ideal es crear una nueva rama y trabajar desde ahí.

`git reflog`
* Muestra el historia de los commits a pesar de haberse eliminado. 
* El **log** solo muestra los activos y el **reflog** todo.

**`git mv README.md README2.md`**
* Reenombrar archivo.

**`git rm README.md`**
* Eliminar archivo.

## Ramas

**`git branch lorem`**
* Crear una nueva rama.
**-d** colocando esta bandera antes del nombre de la rama seleccionada podemos borrarla. **-f** podemos colocar la bandera para forzar la eliminación de la rama.

**`git checkout lorem`**
* Moverse a otra rama. 
**-b** antes de colocar el nombre podemos colocar la bandera para crear la rama y movernos a esa rama.

> [!CAUTION]
> **`git merge lorem`** <br> 
> Traer los nuevos cambios de a la rama en que nos posicionamos. Al hacer merge pueden pasar 3 cosas:
> * **Fast-Forward** = Git no tuvo problemas y unio todo de forma exitosa. Este es el mejor de los escenarios posibles.
> * **Automatica** = Hubo otros cambios en otros archivos pero al hacer merge no hubo problemas para juntar todo.
> * **Conflicto** = En dos ramas se modifico un mismo archivo en una misma línea. En el documento con el conflicto se coloca una sintaxis para decir de forma manual cual es el cambio que debe permanecer. Al final debemos dar commit con el nuevo cambio.

**`git tag lorem` o `git tag -a v1.0.0 ###### -m "Lorem Ipsum`**
* Un tag es un mensaje o etiqueta que se le coloca a los commits. 
* Es una manera para destacar un commit
* **git tag** en un listado muestra todos los tags. 
* **-d** si agrego la bandera antes del nombre borra el tag. 
* **-a** si agrego la bandera antes del nombre es una version anotada.

## Stash

> [!CAUTION]
> **`git stash`**
> * Todo el código que hemos trabajado y que aun no hacemos commit lo podemos mover provisionalmente a otra área llamada stash. 
> * WIP = Work In Progress. 
> * **list** podemos ver todos los stach agregando al final. 
> * **pop** para regresar los cambios podemos y borra el stash. 
> * **clear** borra el stash solamente. 
> * **apply "stash@{#}"** si tenemos varios stash y queremos volver a uno en especifico podemos agregar al final por un numero del stash, esto funciona como un hash. 
> * **drop "stash@{1}"** si queremos borrar un stash en especifico
> * **save "text para el stash"** por defecto el nombre es stash@{#} pero podemos especificar un nombre.

## Rebase

**`git rebase main`**
* Los commits hechos en una rama los pasa arriaba a la rama principal. 
* Con esto es más sencillo hacer un merge ya que sera un fast forward.

> [!CAUTION]
> **`git rebase -i HEAD~#`**
> * Con esto podemos unificar commits.
> * Podemos indicar el número de commits anteriores al head.
> * En la siguiente pantalla en lugar de seleccionar el pick (P) debemos seleccionar el squash (s) para unirlo. Si queremos renombrar un commit anterior es con el Reword (r), el amend aparte de renombrar te permite hacer mas correcciones. Una opción mas delicada es usar un edit (e) para separar los commits y nos redirecciona en un rebase interactivo (en medio de un proceso, nos encontramos en el limbo), para empezar a trabajar usamos un **git reset HEAD~** modificamos y para salirnos al final del rebase colocamos un **--continue**.

## Repositorio remoto

**`git remote add origin https...`**
* Añadir un origen remoto, el origin es el nombre del repositorio remoto.

**`git remote -v` **
* En listas conexiones remotas.

**`git push -u origin main` **
* Subir el codigo a un repositorio remoto.

**`git push --tag`**
* Pasar nuestras estiquetas de local al repositorio. 
* En GitHub podemos ver estas entiquetas en una nueva pestaña y poder descargar el código y no el historial. 
* Especificar = commit -> tag -> release (te crea un link)

> [!NOTE]
> Existe un truco si desde otra rama creo un tag para hacer push y convertirla como un release tag se mantiene el código. Si por accidente / error alguien borra la rama el release tag se mantiene como un respaldo

**`git pull`**
* Traer todos los datos del repositorio remoto al local.

**`git clone https...`**
* El código en el repositorio remoto lo podemos añadir a nuestra computadora. 
* La liga se consigue desde GitHub.
* Si nos incluye el historial.

> [!CAUTION]
> **`git remote add upstream https...`**
> * Añadir una nueva ruta remota, (Upstream) el nombre que le damos a la conección.
> * Ya con esto puedo hacer un pull + rama para traer los nuevos cambios del repositorio original.
> * Es posible crear conflictos.
> * Estoy dentro del rebase y para salir es con un --continue.

**`git push --set-upstream origin nombre-rama`**
* Enviar una nueva rama al repositio. 
* Ya despues no es necesario agreguar la bandera al hacer push ya que git sabe a que rama del repositorio corresponde

**`git remote prune origin`**
* Limpiar las ramas que ya no existen en el repositorio

## Comentarios

# Github

## Issues

* Los Issues es una sección dentro de GitHub donde se usa para postear preguntar, sugerir o mostrar erroes dentro del código.
* Dentro de un issue podemos especificar a que colaborador debe estar asignado
* Podemos crear templates para que los usuarios que necesiten postear algo tengan una forma base. En el template se puede configurar para aceptar labels.
* Un label es una manera de agregar una categoría a los issues.
* `git commit -m "Fixed #1: first commit`. Si el mensaje del commit usamos la palabra fixed más un número de cambio, de forma automática busca el número del Issue y lo cierra.

## Milestone

* Un Milestone es un agrupador de Issues, como si fuera un todolist donde se autocompleta las tareas o los issues cerrados.

## Wikis

* Los wikis es una forma de expandir los README.md cuando se necesita tener mas ordenado la documentación. Esto crea un link.
* Se pueden crear muchas paginas para los Wikis y como es formato Markdown podemos marcar un enlace. 
* Los repositiorios privados tiene un costo tener los wikis
GitHub tiene una sección de project que funciona como un KANBAN

# Consola

**`ls`**
* Ver todos los archivos que se encuentren en el directorio segun nos ubiquemos
* **-a** ver archivos ocultos 

**`pwd`**
* Nos muestra la ruta de donde nos ubiquemos

**`cd carpeta`**
* Avanzamos un nivel hacia otra carpeta.

**`cd ..`**
* Retroceder un nivel.

**`mkdir carpeta`**
* Crear una carpeta.

**`touch README.md`**
* Crea un archivo. Puede ser cualquier achivo de cualquier extension.

**`rm README.md`**
* Borra un archivo que le indiquemos.

**`mv README.md README2.md`**
* Renombrar archivo.

**`cat README.d`**
* Ver el contenido del archivo.

**`code .`**
* Abre la carpea donde nos encontremos en vs code.
