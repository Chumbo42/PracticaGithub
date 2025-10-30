
# Git Práctica guiada


Comenzamos creando y entrando a nuestro proyecto con: 
 ```sh
	mkdir prueba-git
	cd prueba-git
 ```

Creamos los archivos **texto.txt** y **script.sh** con el editor _nano_, teniendo el primer archivo:

>    uno <br>
>    dos <br>
>    tres <br>

Y el archivo script.sh llevará dentro:

 ```sh
    echo Listado completo
    ls -l
 ```


 Modificaremos los permisos del archivo para poder ejecutarlo, para lo cual usaremos


 ```sh
    chmod a+x script.sh
    ./script.sh
 ```

 Y con esto acabamos las preparaciones.


 
## 1. Inicialización

Para empezar a utiizar la herramienta git debemos inicializar nuestro directorio. Para ello utilizaremos el siguiente comando:

```sh
   git init
```

Esto creará el directorio .git con el historial de versiones.

Para ver el estado de nuestro repositorio usaremos el comando

```sh
   git status
```

Actualmete nuestra rama lleva el nombre por defecto _master_, por lo que lo primero que haremos será renombrarla.

Para ello utilizaremos el comando 

```sh
   git branch -m main
```

Este comado funcioa similar al mv linux, lo que realmete estamos haciendo es _mover_ la rama, pero al no cambiarla de directorio, lo único que se vé afectado es el nombre. 


## 2. Añadir archivos

Para añadir un archivo al repositorio utalizaremos el siguiente comando

```sh
   git add [archivo]
```

En nuestro caso, el archivo será **script.sh** 


Para que se confirme esta acción y se sincronice con equipos remotos debemos hacer un commit. Podremos, además, añadir un mensaje con el modificador -m

```sh
   git commit -m "Confirmacion inicial"
```

Además. podremos usar el modificador -F para añadirlos desde un archivo

```sh
   git commit -F mensaje.txt
```

Después de esto, añadiremos también el archivo _texto.txt_

```sh
   git add texto.txt
   git commit -m "Añadido archivo texto.txt"
   git status 
```

El status nos dirá que todo está correcto 

```
   On branch main
   nothing to commit, working tree clean
```


## 3. Modificando archivos

Después de modificar un arhivo se nos informará en _git status_ de que no se han agregado los camios al commit 

```
      On branch main
      Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   texto.txt

      no changes added to commit (use "git add" and/or "git commit -a")

```

Para añadir este archivo en el proximo commit deberemos hacer _-git add_. Después de este comando podremos modificar otra vez el archivo y, mientras no lo añadamos de nuevo, el comando _-git commit_ añadirá la versión de la que se haya hecho el comando _add_.

## 4. Información 

Una vez tenemos un proyecto establecido, siempre y cuando no queramos añadir nuevos archivos, podremos incluir el comando add en el commit co la orden

```sh
   git commit -a -m "mensaje"
```

Para ver esta versión usaremos el comado git show


```sh
   $ git show


      Author: Hornet <hornet@pharloom.com>
      Date:   Mon Oct 6 13:20:21 2025 +0200

      Archivo modificado

      diff --git a/texto.txt b/texto.txt
      index c829819..23c83ff 100644
      --- a/texto.txt
      +++ b/texto.txt
      @@ -1,4 +1,5 @@
      uno
      dos
      tres
      -
      +cuatro
      +cinco      
```

Para ver un histório de versiones, podemos usar el comando 



```sh
   $ git log

      commit 26ef37f88646071d47e888cd40a22d2261d03ec8 (HEAD -> main)
      Author: Hornet <hornet@pharloom.com>
      Date:   Mon Oct 6 13:20:21 2025 +0200

         Archivo modificado

      commit 9a5c9d4a21df209071fa92784e645e82e88b48d6
      Author: Hornet <hornet@pharloom.com>
      Date:   Mon Sep 29 12:56:55 2025 +0200

         Añadido archivo texto.txt

      commit 2510563216322241b2fd3fb5a517130dbf6e21eb
      Author: Hornet <hornet@pharloom.com>
      Date:   Mon Sep 29 12:45:21 2025 +0200

         Confirmacion inicial
```

## 5. Visualizar diferencias

Si se ha modificado un archivo pero no tenemos claro donde, se puede comprobar qué ha sido añadido y que ha sido eliminado mediante el comando 


```sh
   $ git diff
```

Este comando nos devolverá una previsualizacion de los archivos modificados mostrando con un + las lineas añadidas y con un - las eliminadas

## 6. Ignorar archivos

A medida que nuestro proyecto amenta, hay archivos que no querremos actualizar todas las veces ya que no se modifican. Para ello, fodemos usar un archivo llamando .gitignore, que añade filtros a los archivos que se actualizan en el repositorio

Podemos usar el * como "cualquier cosa", es decir, si ignoramos los archivos *.class, no añadiremos ingún archivo on ningún nombre, mientras sea .class [\*.class]

Si queremos actualizar un archivo que cumpe alguna ondicion para ser ignorado, podemos usar el signo ! seguido del nombre del archivo para que la herramienta no lo ignore [\!archivo.txt]


## 7. Tags y gestión de versiones

Si queremos ver el log, por ejemplo, de una versión anterior, necesitaremos usar su identificador

Git añade un identificador a las versiones, pero no es fácil de recordar.

Nosotros mismos podemos añadir un identficador a la versió actual podremos usar el siguiente comando

```sh
   git tag [nombre] {nombreAnterior}
```

Esto cambiará el nombre o identificador de una versión, y si omitimos el segundo parámetro, se cambiará el nombre de la verión actual

Tener identificadores claros ayudará a la gestion del proyecto y a combrobar versiones anteriores. Lo más común es usar números (1.0, 2.3, 0.7), aunque hay gente que para versiones importantes escoge 

Además, podemos usarlo para hacer más fácil nuestra búsqueda con

```sh
   git show [tag]
   git checkout [tag]
```


Para volver a la versión más reciente con checkout se usa:

```sh
   git checkout [master]
```

## 8 Ramas

Las ramas son versiones paralelas a la principal que nos ayudan a introducir ideas sin interferir en la linea de trabajo original. Al acabar, se puede abandonar si no es útil por el momento o eliminar si no lo va a ser, y sobre todo, se puede mezclar con la rama principal si la idea funciona


Para crear una rama usaremos el comando:

```sh
   git branch [nombre]
```


Si usamos **$git branch** sin un nombre, veremos una lista de las ramas activas en nuestro proyeto


El comando para cambiar de ramas es:

```sh
   git switch [rama]
```

Una vez se haya completado el trabajo experimetal en la rama, se puede anexionar a la rama principal (o otra) mediante el comando **$git merge [rama]**


## 9 Eliminar y quitar de seguimiento

Para eliminar archivos de nuestro directorio git usamos el comando **$git rm [archivo]**, después del cual se debe realizar un commit


Para eliminar archivos del seguimiento, una vez borrados se debe ejecutar **$ git reset HEAD *.class**


## 10 Repositorios remotos (Github)

Github es una herramenta oline de repositorios git. para clonar repositoriosen la red a nuestro dispositivo no necesitamos una cuenta, simplemete modemos usar el comando **$git clone [repo]** 


Si queremos enviar datos a un repositorio remoto usaremos el comando **$git push**

En caso de querer sincronizar un directorio local con uno existente en la red se pude utilizar el comando **$git remote add origin [url]**

Por último, se "descargan" los archivos en remoto con **$git pull origin main --allow-unrelated-histories**
