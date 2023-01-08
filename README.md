# Instalación

La instalación oficial
- [Git en Windows](https://git-scm.com/download/linux)
- [Git en Linux/Unix](https://git-scm.com/download/linux)


## ⚙️ Configuración global
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

### ⚙️ Comprobar configuración
Puedes comprobar tu configuración utilizando el flag **--list**, de manera respectiva se presenta
- Revisar todas las configuraciones.
- Revisar todas las configuraciones globales.
- Revisar solo la configuración de email.
~~~bash
$ git config --list
$ git config --global --list
$ git config user.email
~~~

## 🏁 Inicilizar git (local)
Al inicializar git por defecto, nos creará un archivo local **.git**, con una rama inicial **"main"**.
~~~bash
$ git init
~~~
Podemos decirle que cree una carpeta y que la rama inicial reciba otro nombre, aunque por convención se suele mantener como **"main"**.
~~~bash
$ git init nuevo-proyecto --initial-branch=master
~~~
Puedes verificar los datos utilizando
~~~bash
$ git status
~~~

## Al añadir o modificar archivos (local)
Con git inicializado, bastará con añadir cualquier archivo a la carpeta en la que tengas el proyecto para que lo detecte con **"git status"**, nos dirá que los archivos "no han sido trackeados".

## ⬆️⬇️ Añadir o remover un archivo git
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
### ⬇️ Remover
En este caso remover no indica elimnar los archivos, sino, que no se incluirán para la "subida a la nube".
- 📄📄 Remover uno o varios documentos.
- 📂 Remover una carpeta .
- 📂📂 Remover todo.
~~~bash
$ git reset texto1.txt texto2.txt
$ git reset nueva_carpeta/
$ git reset .
~~~

## Restaurar dado el último commit
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
~~~

