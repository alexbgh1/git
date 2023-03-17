# ¿Qué es git?
Es un sistema de control de versiones, escencialmente para trabajar con muchas personas, permitiendo el trabajo "independiente" para posteriormente juntar el trabajo.

Se basa en un sistema de **"branches"** o **"ramas"**, donde existe una principal que llevará todos los cambios actualizados, se podrán crear distintas **ramas**, por ejemplo, para añadir características.

![git_branch](https://i.imgur.com/AMX6jQG.png])

## Instalación

La instalación oficial se encuentra en:
- [Git en Windows](https://git-scm.com/download/linux)
- [Git en Linux/Unix](https://git-scm.com/download/linux)


## ⚙️ Configuración global
#### Tags: git config, git init
La configuración global es la que prevalecerá en todos los repositorios, lo más recomendable es setear al menos un usuario y correo, aunque también se puede escoger un editor de código predeterminado, entre los más conocidos están 
- **Vim** "vim"  (_por defecto_)
- **VSCode** "code"
- **Nano** "nano"
- **Sublime Text** "subl"
~~~bash
$ git config --global user.name "<user_name>"
$ git config --global user.email "<email>"
$ git config --global core.editor "code"
~~~
> **ℹ️ Nota**<br>
> El simbolo ' $ ' es representativo para la terminal **Git Bash**, no es parte de los comandos como tal.


### Comprobar configuración
Puedes comprobar tu configuración utilizando el flag **--list**, de manera respectiva se presenta
- Revisar todas las configuraciones.
- Revisar todas las configuraciones globales.
- Revisar solo la configuración de email.
~~~bash
$ git config --list
$ git config --global --list
$ git config user.email
~~~

## 0️⃣1️⃣2️⃣3️⃣ Estados básicos de git
**0️⃣ Directorio raíz**
 
  **Inicializamos** nuestro proyecto con el archivo **.git**. Al crear archivos inicialmente estarán en modo "no trackeados".
  
  <sup>Principal comando asociado: **git init**</sup>

**1️⃣ Área transitoria**
  
  **Añadimos** los archivos que queremos subir

  <sup>Principal comando asociado: **git add**</sup>

**2️⃣ Repositorio Local**

  **Confirmamos** los archivos que serán subidos al entorno remoto

  <sup>Principal comando asociado: **git commit**</sup>

**3️⃣ Repositorio Remoto**

  **Subimos** los archivos al entorno remoto

  <sup>Principal comando asociado: **git push**</sup>


## 🏁 Inicializar git (local) 0️⃣
#### Tags: git config, git init, git status
Al inicializar git por defecto, nos creará un archivo local **.git**, con una rama inicial **"main"**.
~~~bash
$ git init
~~~
Podemos decirle que cree una carpeta y que la rama inicial reciba otro nombre, aunque por convención se suele mantener como **"main"**.
~~~bash
$ git init nuevo-proyecto --initial-branch=master
~~~

### Verificar el estado de los archivos
Podemos visualizar el estado de los archivos que está o no considerando git.
- En **rojo** se presentan los archivos no trackeados, es decir, los que no han sido considerados para la subida a la nube.
- En **verde** se presentan los archivos trackeados, es decir, los archivos que serán considerados para la subida a la nube.
~~~bash
$ git status
~~~
![git_status](https://i.imgur.com/veQc27j.png)

Podemos acortar el contenido utilizando el flag **-s**
~~~bash
$ git status -s
~~~
![git_status](https://i.imgur.com/8Kj8xnQ.png)


## ⬆️⬇️🗑️ Añadir, resetear o eliminar un archivo (local) 1️⃣
#### Tags: git add, git reset, git clean
Con git inicializado, bastará con añadir cualquier archivo a la carpeta en la que tengas el proyecto para que lo detecte con **"git status"**, nos dirá que los archivos "no han sido trackeados".

Para que git los detecte, deberemos añadir el contenido que queramos. Nuevamente podemos verificar el estado de los archivos con **"git status"**.

Esto corresponde a una etapa previa, de **"preparación"** en donde seleccionamos que archivos y carpetas queremos considerar antes de subirlas con un commit.

### ⬆️ Agregar archivos
- 📄📄 Añadir uno o varios documentos.
- 📂 Añadir una carpeta .
- 📂📂 Añadir todo.
~~~bash
$ git add texto1.txt texto2.txt
$ git add nueva_carpeta/
$ git add .
~~~

### ⬇️ Resetear
Indica archivos que no se incluirán para el commit.
- 📄📄 Resetear uno o varios documentos.
- 📂 Resetear una carpeta .
- 📂📂 Resetear todo.
~~~bash
$ git reset texto1.txt texto2.txt
$ git reset nueva_carpeta/
$ git reset .
~~~

### 🗑️ Eliminar
Si creamos algunos documentos, que no han sido trackeados y que queremos eliminar
- **-n** para ejecutar un dry-run. Esto hará que se ejecute el comando y te diga cuál sería el resultado de borrar los archivos, pero no los borrará.
- **-f** forzar el borrado de los archivos.
- **-d** para borrar también carpetas 📂 que no existían antes.
- **-i** para que te pregunte antes de borrar cada archivo.
Las siglas pueden combinarse según lo que quieras hacer según los flags mencionados.
~~~bash
$ git clean -n
$ git clean -nd
$ git clean -ni
$ git clean -nfi
~~~
> **Warning**<br>
> Esta acción no se puede deshacer. Por lo que es recomendable verificar qué se borrará con **-n** y preguntar si estás seguro con **-i**. O en caso de ser pocos archivos eliminarlo de forma manual.


## Commit 2️⃣
#### Tags: git commit, git log, git show, git reset, git reflog
Una vez evaluado los archivos que queremos subir (datos añadidos con **git add**) deberemos hacer un commit, que es equivalente a una confirmación de los archivos que subiremos. Guardará el **autor** y **fecha** del commit, además de un **hash** con información del commit.

Utilizaremos el flag **-m** (de message) para dar el motivo, podemos incluir más de un mensaje.

~~~bash
$ git commit -m "mi primer mensaje" -m "mi segundo mensaje"
~~~
<sub>Se recomienda utilizar comillas dobles.</sub>

### Visualizar los commits realizados
Para visualizar todos los commits realizados puedes utilizar **log**.
~~~bash
$ git log
~~~
![git_log](https://i.imgur.com/ZI9V7dX.png)

También podemos [filtrar los commits por autor](https://stackoverflow.com/questions/2845731/how-to-uncommit-my-last-commit-in-git) con el flag **--author**, ya sea para uno o varios autores
~~~bash
$ git log --author="alex"
$ git log --author="\(alex\)\|\(Jon\)"
~~~

En caso de querer más detalle existe **show**, en donde utilizaremos el **hash** para ver los cambios (información agregada o removida en ese commit).
Para el ejemplo, no existen inserciones o eliminación de datos, pero si se agregó un archivo .txt.
~~~bash
$ git show e4196bb496f4ff774638a618a4eef7e48e95cbb8
~~~
![git_show](https://i.imgur.com/toyIHW7.png)


### Hice un commit pero me equivoqué
- ¿Qué hacer si accidentalmente subí 2 commits que no debía y quiero volver atrás?

  1. **Ej:** Solo quiero eliminar el último commit sin perder los cambios.
  
      ~~~bash
      $ git reset --soft HEAD~1
      ~~~
      <sub>El **1** es opcional para decir cuántos commits queremos volver. Por defecto es 1.</sub>
  2. **Ej:** Quiero eliminar (todos) ambos commits sin perder los cambios
      ~~~bash
      $ git reset --soft HEAD^
      ~~~
  3. **Ej:** Quiero eliminar el último commit, y que además lo quite de archivos añadidos (**git add**)
      ~~~bash
      $ git reset --mixed HEAD~1
      ~~~
  4. **Ej:** Quiero deshacer por completo el último commit, eliminando los archivos que subí.
      ~~~bash
      $ git reset --hard HEAD~1
      ~~~
  5. **Podemos volver a un commit de esta manera** [fuente](https://stackoverflow.com/questions/5473/how-can-i-undo-git-reset-hard-head1)
      ~~~bash
      $ git reflog
      $ git reset --hard <hash_commit_al_que_quiero_volver>
      ~~~
     

- El último commit que hice tiene un comentario que no está bien, ¿Cómo lo cambio?
  ~~~bash
   git commit --amend -m "Este es mi nuevo mensaje"
  ~~~

### Restaurar un archivo dado el último commit en la nube
Puedes utilizar **restore** a partir de la versión 2.23. Restaura el archivo dado el último commit en el entorno remoto.
  - El **punto** considera restaurar todos los archivos.
  - El **asterisco** considera cualquier secuencia de caracteres, es decir, un documento cualquiera con terminación ".txt": 📄.txt

~~~bash
$ git restore archivo_especifico.txt
$ git restore .
$ git restore '*.txt'
~~~
o **checkout**
~~~bash
$ git checkout -- archivo_especifico.txt
$ git checkout .
$ git checkout -- '*.txt'
~~~
<sub>Los guines indican que se busca un archivo en específico. Ya que **git checkout** también es utilizado para cambiar entre branch/ramas.</sub>

# Ramas
Muchos comandos referente a visualizar, mezclar, crear o eliminar ramas nuevas. Una rama se establece como una especie de camino alternativo para nuestro trabajo actual, esto quiere decir, podemos crear estas ramas para crear nuevas "features" (características) y luego acoplarlas a nuestra rama main (principal), permitiendo así el trabajo en paralelo para un proyecto.

## 📝 Listar ramas
#### Tags: git branch 

   1. Listar ramas existentes
      ~~~bash
      $ git branch
      ~~~

   2. Listar ramas por fecha de creación
      ~~~bash
      $ git branch --sort=-committerdate
      ~~~

   3. Listar rama actual
      ~~~bash
      $ git branch --show-current
      ~~~

## Crear ramas
#### Tags: git branch, git switch, git checkout
Hay al menos 3 equivalencias para crear una rama y cambiarse a esta.

   1. Crear y moverse (por separado)
      ~~~bash
      $ git branch nueva-rama
      $ git switch nueva-rama
      ~~~
   2. Crear y moverse (a la vez)
      ~~~bash
      $ git switch -c nueva-rama
      ~~~   
   3. Crear y moverse (a la vez)
      ~~~bash
      $ git checkout -b nueva-rama
      ~~~

## Eliminar ramas
#### Tags: git branch
Cuando eliminamos una **rama** nos dirá la referencia.
**Ej:** "Deleted branch mi-rama (was 684fa35)."

   1. Eliminar una rama
      ~~~bash
      $ git branch --delete nueva-rama
      ~~~
   2. Eliminar una rama que no ha sido fusionada.
      ~~~bash
      $ git branch -D nueva-rama
      ~~~
   3. Para recuperarla
      ~~~
      $ git branch master2 <hash_branch_a_recuperar>
      ~~~

## Fusionar ramas
Si tenemos más de una rama y queremos fusionar nuestros avances deberemos utilizar uno de estos comandos según nuestra conveniencia.
#### Tags: git merge

   1. Merge.
      ~~~bash
      $ git merge <nueva-rama>
      ~~~
   2. Merge - fast forward. Hará un merge fast forward solo si es posible, se puede usar cuando el <feature> va por delante de la rama main.
      ~~~bash
      $ git switch main
      $ git merge --ff-only <feature>
      ~~~
   3. Merge - no fast forward. El caso de uso es equivalente a **crear una rama**, hacer un commit, volver al **main** y hacer otro commit.
      ~~~bash
      $ git switch main
      $ git switch -c feature
      $ git commit -m "commit 1 feature"
      $ git switch main
      $ git commit -m "commit 1 main"
      $ git merge feature --no-ff
      ~~~
   3. Merge - squash. Este tipo de fusión de cambios hace la fusión y junta todos los commits de la rama de origen en un solo commit que debe ser confirmado. Esto se conoce como squash.
      ~~~bash
      $ git switch - c feature
      $ git commit -m "commit 1"
      $ git commit -m "commit 2"
      $ git commit -m "commit 3"
      $ git switch main
      $ git merge feature --squash
      $ git commit -m "Merge feature"

   ~~~

