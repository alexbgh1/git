# Instalación

La instalación oficial
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
- En rojo se presentan los archivos no trackeados, es decir, los que no han sido considerados para la subida a la nube.
- En verde se presentan los archivos trackeados, es decir, los archivos que serán considerados para la subida a la nube.
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

Esto corresponde a una etapa previa, de **"preparación"** en donde seleccionamos que archivos y carpetas queremos considerar antes de subirlas a la nube.

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
Indica archivos que no se incluirán para la "subida a la nube".
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
#### Tags: git commit, git log, git show, git reset
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
¿Qué hacer si accidentalmente subí 2 commits que no debía y quiero volver atrás, sin perder los cambios?

  1. **Ej:** Solo quiero eliminar el último commit.
  
      ~~~bash
      $ git reset HEAD~1
      ~~~
      <sub>El **1** es opcional para decir cuántos commits queremos volver. Por defecto es 1.</sub>
  2. **Ej:** Quiero eliminar (todos) ambos commits.
      ~~~bash
      $ git reset HEAD^
      ~~~

## Restaurar un archivo dado el último commit "ya en la nube"
Puedes utilizar **restore** a partir de la versión 2.23.
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
<sub>Los guines indican que se busca un archivo en específico. Ya que **git checkout** también es utilizado para cambiar entre branch/ramas.</sub>
~~~

