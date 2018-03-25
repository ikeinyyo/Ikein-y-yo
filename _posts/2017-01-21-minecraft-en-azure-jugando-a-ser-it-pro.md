---
layout: post
current: post
cover: assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/mapcrafter.jpg
navigation: True
title: "Minecraft en Azure: jugando a ser IT Pro"
date: 2017-01-21 20:00:00
tags: tech minecraft
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hoy quiero explicaros como he montado un server de Minecraft en Azure. Jugando un poco a los IT Pros he montado en una máquina virtual un servidor de Minecraft (de hecho, dos), un servidor FTP, un servidor de Team Speack y un servidor web. A continuación lo veremos todo en detalle.

## Primero, la Máquina Virtual
Bueno, lo primero que necesitamos es tener una máquina virtual. En este caso yo he elegido una máquina virtual con Linux porque es más barata.

![Listado de precios](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/prices.jpg)

En mi caso he cogido una de tipo A2 con 2 núcleos y 3,5GB de RAM con Ubuntu 14.04. Es más que suficiente para todo lo que tengo montado.

## Servidor de Minecraft
El problema de no haber elegido una máquina con Windows Server es que no tenemos disponible de primeras el escritorio remoto. Eso lo haría más sencillo todo. Pero aun así montar todo esto no tiene ninguna complejidad. En mi caso lo voy a hacer todo conectando por SSH a la máquina virtual con [PuTTY](http://www.putty.org/).

**Nota:** Pese a que todos los amantes de Minecraft, como yo, desearíamos que no estuviese hecho en Java, no es así. Por tanto necesitamos tener Java instalado. Os dejo [aquí](http://www.ubuntu-guia.com/2012/04/instalar-oracle-java-7-en-ubuntu-1204.html) un enlace de como instalar tanto OpenJDK como Oracle Java en Ubuntu.

Lo primero que debemos de hacer es descargar el servidor de Minecraft desde la página web.
Basta con ejecutar el comando wget con el link de descarga de la versión 1.8.1 de Minecraft server.

`wget https://s3.amazonaws.com/Minecraft.Download/versions/1.8.1/minecraft_server.1.8.1.jar`

Y ahora simplemente basta con ejecutar el siguiente comando:

`java -Xmx2048M -Xms2048M -jar minecraft_server.1.8.1.jar nogui`

**Nota:** con los parámetros -Xmx y -Xms indicamos la memoria máxima y mínima. En mi caso le asigno 2GB (2048M). Por otro lado el parámetro nogui evita que se cargue la GUI del servidor.

**¡Importante!** Cuando iniciemos el server con el comando anterior nos dará un fallo diciendo que tenemos que aceptar los términos y condiciones de [EULA](https://account.mojang.com/documents/minecraft_eula). Para ello únicamente tenemos que modificar el fichero eula.txt, que se habrá generado en la carpeta del servidor, cambiando el flag `eula=false` por `eula=true`.

![Servidor funcionando](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/serverRun.jpg)

Ya tenemos nuestros servidor de Minecraft funcionando. Sólo nos quedan dos cositas por hacer: editar la configuración y [abrir los puertos](https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-windows-endpoints-in-resource-manager).

Para configurar el servidor tenemos que editar un fichero llamado server.properties que se nos genera en el directorio al iniciar el servidor. [Aquí](http://minecraft.gamepedia.com/Server.properties) podéis ver todas las opciones de configuración. Una de las cosas que podemos configurar es el puerto en el que está escuchando el servidor. Por tanto tenemos que acordarnos de abrir ese puerto en nuestra máquina virtual de Azure.

Yo en mi máquina virtual he lanzado en otra carpeta otro servidor de Minecraft con otro mapa en creativo. Simplemente le he cambiado en la configuración el puerto. Así se pueden tener varios servidores (lo que aguate tu máquina) activos.

## Screen: Mantener los servidores activos

Una vez que iniciamos el server no podemos cerrar PuTTY, porque se cerraría la consola de la máquina virtual. Para solucionar esto se puede intentar colocar el servidor de Minecraft como un servicio. En mi caso he optado por utilizar Screen que me genera consolar virtuales.
En el caso de la máquina virtual de Azure, Screen ya está instalado. Simplemente utilizamos el parámetro `-S` para crear consolas virtuales y `-x` para reconectarnos a ellas.

De este modo yo creo una consola virtual:

`screen -S “minecraft”`

Una vez la creo ya puedo lanzar el server y cerrar PuTTY, que el servidor seguirá corriendo en la consola virtual. Cuando vuelva a conectarme a la máquina virtual simplemente necesito ejecutar el siguiente comando para conectarme a la consola virtual:

`screen –x “minecraft”`

Como veis es mucho más cómo que ejecutar programas como servicios. Usaremos está técnica más adelante para el servidor web ya que se pueden crear diferentes consolas virtuales. Podemos listarlas con el comando:

`screen –list`

![Screen](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/screen.jpg)

**Nota:** Es una solución muy sencilla para mantener procesos lanzados. El problema es que si necesitas reiniciar la máquina virtual necesitas volver a lanzarlos. En cambio si los pones como servicios puedes hacer que se arranquen al inicio.

## Servidor FTP

Por último para dar por cerrada una primera versión del server, necesitaba un servidor FTP. ¿Por qué? Bueno, básicamente porque quería poder descargarme el mundo de Minecraft y poder tener copias de seguridad en local.

Esto fue lo que más problema me dio. Problemas de permisos, credenciales, etc. Por fin conseguí hacerlo funcionar. [Aquí](http://www.codechewing.com/library/configure-ftp-azure-linux-ubuntu-vm/) os dejo el tutorial que seguí para hacerlo.
Con todo esto ya hemos montado nuestro servidor de Minecraft con un servidor FTP para descargarnos el mapa. Con este servidor estuve jugando con un amigo durante mucho tiempo. Pero nos faltaba algo… nos faltaba dar un paso más. Necesitábamos poder hablar entre nosotros…

## TeamSpeack
Aprovechando la máquina virtual en Azure decidí montar un servidor de TeamSpeack. [Aquí](http://blog.bobbyallen.me/2014/01/11/setting-up-teamspeak-3-on-ubuntu-server-12-04-lts/) os dejo como instalarlo en Ubuntu.

Como podéis ver en el link anterior, al final acabamos lanzando el TeamSpeack como un servicio. En este caso, si reiniciáramos la máquina virtual no tendríamos que lanzar de nuevo el servidor de TeamSpeack.

`sudo service teamspeak3 start`

Tened cuidado y ponerle contraseña. Porque a nosotros se nos conectó un tan David (“deivit”, porque hablaba en inglés).

## Todo listo!
Ya tenemos un servidor de Minecraft en Azure, con su servidor FTP para descargar las copias de seguridad, un servidor de TeamSpeack para poder hablar con tus amigos… Aquí ya di por cerrada una segunda versión del servidor.

## MapCrafter

Poco después busqué un programa capaz de renderizar el mundo de Minecraft en una imagen. Pero encontré algo mucho mejor: [MapCrafter](http://mapcrafter.org/). Este programa renderiza el mapa en pequeñas imágenes a diferentes resoluciones y crea una web al estilo Bing Maps o Google Maps. Es una web muy sencilla, con un archivo HTML, su Javascript y todos los recursos que se genera. Es decir, basta con abrir el index.html para poder disfrutarla.

![MapCrafter](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/mapcrafter.jpg)

Simplemente creando un fichero de configuración y ejecutando el siguiente comando generamos la web en el directorio de salida.

`mapcrafter -c map.conf`

Esto me dio una idea: montar un servidor http en la máquina virtual para tener publicado el mapa.

## Http Server
Existen muchas formas de crear un servidor web. Yo decidí hacerlo en Node.js. En Node es [muy sencillo](http://community.logicalbricks.com/node/181) hacer un servidor, pero que [muy sencillo](http://blog.kevinchisholm.com/javascript/node-js/making-a-simple-http-server-with-node-js-part-i/), sencillísimo. Pero yo he encontrado la forma más sencilla de todas: [http-server](https://www.npmjs.com/package/http-server). Basta con tener instalado node y npm.

Instalamos http-server:

`npm install http-server -g`

Y ahora ejecutamos en el directorio que queramos http-server:

![Http Server](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/httpserver.jpg)

Ya tenemos un servidor HTTP en el directorio donde lo ejecutemos. En mi caso lo tengo escuchando en el puerto 8080. Únicamente tengo que abrir en Azure un puerto para la web y listo. Yo he abierto el puerto 80 público.
En este caso, igual que hago con el servidor de Minecraft, lo ejecuto en otra screen diferente. Tal y como hemos visto antes tengo dos consolas virtuales ejecutándose.

![Http Server Screen](/assets/images/posts/minecraft-en-azure-jugando-a-ser-it-pro/screen.jpg)

## ¿Qué nos depara el futuro?
Quedan muchas cosas por mejorar. De momento el renderizado del mapa lo hago yo a mano conectándome por SSH. Paro el servidor de Minecraft, renderizo el mundo y vuelvo a arrancarlo. Como una primera solución he creado un script que primero renderiza el mapa y luego ejecuta el servidor. De este modo está un poco más automatizado: paro el servidor de Minecraft, ejecuto el script y me olvido.

Pero me gustaría automatizar esto de tal forma que cada día a las 5 de la mañana se actualizara el mapa. También me gustaría poder hacer copias de seguridad periódicamente.

Y aquí es cuando os pido ayuda. ¿Cómo se os ocurre que puedo mejorar el servidor?

## Info Bonus
Después de haberte leído todo el post aquí viene como crear un servidor de Minecraft mucho más sencillo. En el portal de Azure, desde la galería te permite crear un [servidor de Minecraft](http://azure.microsoft.com/en-us/marketplace/partners/microsoft/minecraftserver/). Únicamente tendrás que elegir nombre del servidor, nombre de usuario y la contraseña. Y a jugar!

Esto ha sido todo. Espero que os haya gustado y pongáis alguna cosa en práctica.

¡Nos vemos en el futuro!
