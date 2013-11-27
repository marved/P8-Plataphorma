Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```

P8
------------

1) click en botón de juego.
Los botones de cada juego están definidos en index.html, en el template de la linea 81. Los eventos para cada botón están definidos en client.js, desde la linea 112 hasta la 130. Aquí se programa para que cuando se haga click en algún botón de un juego, busca  qué juego es y lo guarda en la variable game, y se inicia ese juego llamando a Session.Set.

2) se escribe mensaje chat sin estar autenticado.
En la linea 87 de client.js se identifica si al escribir un mensaje se está autenticado o no. En este caso, al no estar autenticado, se ejecuta a partir de la linea 100, y se muestra una frase de error declarada en el div de la linea 60 de index.html, con el id "login-error".

3) se escribe mensaje chat estando autenticado.
Igual que en la pregunta anterior, pero en este caso, al estar autenticado, se entra en el if de la linea 87. Va a buscar en la base de datos de los mensajes para incorporarlo al chat.

4) se termina la partida con mayor puntuación sin estar autenticado.
Para el juego AlienInvasion, al acabar la partida, en la linea 103 se llama a la función matchFinish, que está en la linea 47 de server.js. Y aquí, al no estar el usuario autenticado, no se va a modificar la tabla de puntuaciones.

5) se termina la partida con mayor puntuación estando autenticado.
Todo igual que en el punto anterior. Pero ahora, al estar autenticado el usuario, se guarda la puntuación conseguida. En la linea 157 de client.js se buscan de entre todas las puntuaciones guardadas, las 5 mejores y se muestran en la tabla de jugadores con mejor puntuación.

6) ¿qué sale en la consola cuando te autenticas(sign in)? y por qué.
Deps.autorun se ejecuta cuando se modifica una fuente de datos reactiva, en este caso al iniciar sesión con un usuario.
Primero aparece el valor de CurrentUser a null porque se ha inicializado así. Pero despues CurrentUser coge el valor de la id del usuario, y es lo que muestra la consola la segunda vez.

7) ¿qué sale en la consola cuando sales(sign out)? y por qué.
En este caso ocurre lo contrario, la primera vez CurrentUser tiene el valor de la id del usuario, porque es el último valor guardado, y la segunda vez tiene valor null, porque en ese momento ya no hay usuario.
