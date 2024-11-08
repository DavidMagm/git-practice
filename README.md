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

## **Llaves publicas**
imaginemos que Pablo le quiere mandar un mesaje a Juan y el mensaje es *secreto* si se lo envia por internet es sencillo que alguien lo intercepte y lo abra asi que le pondemos poner un password al mensaje pero como mandamos ese password si lo mandamos por internet tambien lo pueden interceptar entoces utilizamos un ***cifrado simetrico de un solo camino***

### Llaves
para hacer el ***cifrado simetrico de un solo camino*** se necesitan dos llaves un publica y otra privada, estas dos llaves estan vinculadas matematicamente, al estar vinculadas lo que Pablo cifre con su llave publica lo puede abrir con su llave privada. Entonces el proceso de envio del mensaje se da asi Pablo le envia por internet su llave publica a Juan, este va a clonar la llave que le enviaron y mediante un proceso matematico de la llave publica va a convertir el mensaje *secreto* en un mensaje cifrado, y Juan le envia el mensaje a Pablo ahoro lo unico que debe hacer Pablo es copiar el mensaje cifrado y utilizar su llave privada para desencriptarlo con esto pueden Pablo y Juan mandar mensajes secretos por medios abiertos sin que un hacker pueda atrapar los mensajes

Todo esto para hablar el SSH por cierto la instalacion de ssh TODOS la buscan en google para configurarla en su entorno local
## Github
bueno pero pqra que sirve toda esta configuracion de llaves SSH para concetarte de manera remota de git a github (si ya creaste tu llave y pegaste la lleve publica en las configuraciones de git) creas tu repositorio y con la ruta de ssh que se encuetra en la pestaña clonar repositorio vas a tu proyecto y pones *git remote add origin [url_clone_repository]* con *git remote -v* podes ver si ya se configura la ruta que seleccionaste para mandar los cambios de mi repositorio local a mi repositorio de github pongo *git push origin main* es importante poner el nombre main o de la rama que quieras ya que en tu entorno local puedes tener muchas ramas claro antes de dar el push es buena practica traer lo que se encuentra en tu repositorio en github con *git pull origin main* 

## Git Tags 
No han notado que en muchos proyectos de codigo abierto encuentran v0.1, v.1.1 pues esto son las diferentes versiones del mismo todas estas referencias se hacen con tags, haces un *git log --all* y tomas el commit que quieres para que sea tu primera version con *git tag -a v0.1 -m "la primera version" [ID_COMMIT]* (la a es de add y en ves de v0.1 puedes ponerle el nombre que quieras como patito, lo que pasa es que las versiones pues siguen una nomenclatura estandar) para despues hacer *git push origin --tags* y aparecera en la esquina de nombre ramas al otro lado estaran los tags en Github 

Pero ahora como los quitamos sencillo *git tag -d [NAME_TAG]* si no te acuerdas del nombre del tag con *git tag* te apareceran todos los tags y vuelves a enviar *git push origin --tags*, pero cuando revises tu github se seguira viendo en tag que quisiste borrar porque github guarda esa referencia para borrar esa referencia ejecutas *git push origin :refs/tags/[NAME_TAG]*

Ahora hay un comando muy util para vizualizar de manera grafica el flujo de los commit *git log --all --graph --decorate --oneline* te dara este resultado

<image src="https://i.imgur.com/uT3ITgW.jpg" alt ="captura de la consola">

pero existe una manera de hacer git de forma visual con *gitk* 

<image src="https://i.imgur.com/a/HMp8S0R.jpg" alt ="captura-gitk">

Pero porque usamos la console entoces teniendo esto porque los desarrolladores profesionales la utilizan ya que los programadores se mueven con la consola no te preocupes es por tu bien 

## Fusion de ramas
cuando hacemos el *git push origin main* solo enviamos esa rama pero github no se entera que tenemos mas ramas como dev, header, footer a no ser que nosotros queramos enviarlas nos pasamos a la rama que queremos enviar con *git checkout [NAME_BRANCH]* y le haces el git push 

En los ultimos commit que envie emule con si trabajaran dos diferentes personas en el proyecto uno en la rama header y el otro en dev, despues lo que hice es pasarme a mi rama main y darle *git merge header* para agregar sus cambios y de pues lo mosmo con dev, recordemos que en main debe estar lo que queremos que vaya a produccion por lo tanto el trabajo de hacer un code review debe hacerse por parte de los manager, lider del proyecto o el encargado en cuestion 

## Pull Request
Vamos a hablar de los pull request en un entorno de desarrollo profesional el hacer *merge* tranquilamente a main, no se hace como estamos viendo aqui como te deje el la rama main se coloca todo lo que va a produccion que es el servidor donde vive la aplicacion en la que los clientes lo pueden ver, pero como provamos que todo lo que estamos haciendo salga bien para eso tenemos un entorno que es lo mas parecido al proyecto en el cual estamos trabajano (una app o sitio web de prueba) que normalmanete llaman **staging develop** o servidores de desarrollo son ramas que estan justo antes que la rama main y **staging develop** apunta a nuestro servidor de pruebas

Y el flujo de trabajo es sencillo ustedes crean una rama para el feature que estan desarrollando en nuestro caso podria ser header o footer y manda esa rama (le hacen un merge) a la rama **staging develop**, pero antes de hacer el merge se debe pasar por un lugar intermedio y ese lugar es el PULL REQUEST, el pull request permite que otros miembros del equipo revisen el codigo que escribiste y si les gusta pues le merge se ejecuta de forma automatica

Hay que recordar que un PULL REQUEST no es una caracteristica de git sino de github, ademas que el pull request permite a personas que no son colaboradores del proyecto aportar en una rama siempre y cuando el proyecto sea publico, por cierto todo este proceso lo realizan los lideres de equipos o un grupo de personas con el nombre de **DevOps** 

## .gitignore y archivos binarios
En este repositorio he estado haciendo una mala practica que es subir archivos binarios, los archivos binarios no son igulaes a los archivos de texto plano como el index.html o el README.md de este proyecto pero las imagenes que estan en la carpeta assects si, y estas imagenes deberian ir en algo llamado un **content delivery network** 

Y aqui vamos hacer esto de manera secilla lo primero es creando un archivo *.gitignore* y es muy importante el punto despues vamos a ir a *imgur.com* para subir las imagenes ahi y la url que nos de de cada imagen las ponemos en el *src* la url de iniciar con una **i** y despues ponerle la extencion de .jpg algo asi *src="http://[i].imgurURL.jpg"*