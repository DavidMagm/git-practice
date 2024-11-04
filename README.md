# PRACTICA CON GIT 

## Que es Git
Git es un sistema de control de versiones, si tu quieres realizar cambios en tu proyecto pues cada cambio corresponderia a una nueva version pues git es un entorno que contiene tres estados (**working directory**,**stagin**,**local repository**) y para poder mover nuestros archivos pues vamos a ver los comandos basicos

## Comandos Basicos
el primer comando es el *git init* que nos creara una carpeta **.git** en donde se alojaran todos nuestros cambios, ahora que git comienze a traquear nuestros archivos podemos moverlos al stagin con *git add [name_file]* para poder verificar que si esta en stagin enjecutamos *git status*, pero bien este archivo aun no ha pasado a nuestro repository local hasta que ejecutemos *git commit -m "message"* por cierto es una buena practica agregar un mesaje para recordar que estabamos pensando con esos cambios 

## Volver en el tiempo
mientras mas repitamos el proceso anterior podremos agregar mas cambios en el local repository y para poder ver la historia de todos nuestro commit usamos *git log* nos dara el ID que le asigna git a cada commit, quien lo escribio y cuando claro ese ID nos servira para poder volver a versiones atras. Lo podemos hacer con un *git checkout [ID_commit]* y si queromos volver a nuestra version mas actual ponemos *git checkout main* o master dependiendo el nombre que tenga tu rama principal de hecho para cambiar el nombre de una rama puede utilizar *git branch -m [old_name] [new_name]* 

### git reset 
Bien git reset tambien nos ayuda a volver en el tiempo pero a diferencia de **checkout** no nos permite volver es un viaje de solo ida y hay dos flags mas utilizada para este comando *git reset --hard [ID_commit]* y *git reset --soft [ID_commit]* el reset --hard nos devuelve al commit que le dimos y ademas borra todos los commit que habiamos hecho **LO BORRA TODO** y toca volver a escribir. Ahora el reset --soft es parecido pero no borra lo que tengas en el Stagin

### git rm 
Por lo general la personas confunden *git rm* y *git reset* es simple git rm no nos permite retorcerder a versiones anteriores sino que elimina un archivo *git rm [name_file]* lo elimina de git para que ahora git no lo pueda traquear *git rm --cached [name_file]* sirve para esto lo quita del stagin y del historial de los commit, ahoara si quisieras borrar esta archivo no solo de git tambien de tu disco duro usas *git rm --force [name_file]*   

## Git merge
ahora vamos a fucionar dos ramas para traer los cambios que he realizado en otra rama pero primero debemos ver que es una rama

### ramas en git 
cuando escribimos los commit van creando un registro que podemos ver *git log* todos estos commit se guardan en la rama master o main que es la rama principal, claro si queremos trabajar algo que no este en nuestra rama principal puede ser un bug o una funcionalidad para eso creamos otra rama con *git branch [name]* como en este caso con el footer donde vamos a cambiar el **footer** para despues hacer un merge desde el main para traerme lo del footer *git merge footer* recordando que estamos en la rama main se va a unir el ultimo commit del footer y del main
