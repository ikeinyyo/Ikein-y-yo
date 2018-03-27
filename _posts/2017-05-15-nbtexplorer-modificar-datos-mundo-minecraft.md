---
layout: post
current: post
cover: assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/level-dat.jpg
navigation: True
title: "NBTExplorer: Cómo modificar los datos de un mundo de Minecraft"
date: 2017-05-15 12:00:00
tags: minecraft
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! **Cuando creamos un mundo de Minecraft hay parámetros que ya no podemos cambiar**. Hoy vamos a ver una herramienta que nos va a permitir modificar alguno de ellos.

## NBTExplorer

NBTExplorer es una herramienta que nos va a permitir **explorar los archivos binarios** donde se almacenan los datos de nuestro mundo de Minecraft. Además, vamos a poder **editar opciones** que no se pueden editar desde el propio juego.

Es una herramienta de código abierto alojada en [GitHub](https://github.com/jaquadro/NBTExplorer). También podemos encontrar más información sobre NBTExplorer en el [foro de Minecraft](http://www.minecraftforum.net/forums/mapping-and-modding/minecraft-tools/1262665-nbtexplorer-nbt-editor-for-windows-and-mac).

Podemos descargar NBTExplorer desde el listado de [releases](https://github.com/jaquadro/NBTExplorer/releases).

## Editar los datos del mundo

Al abrir NBTExplorer nos aparecen todos los mundos que tengamos guardados en la carpeta de instalación por defecto de Minecraft. Aunque **podemos abrir cualquier otro mundo o carpeta de instalación desde la pestaña de *File***.

![NBTExplorer](/assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/nbt-explorer.jpg)

Para modificar los datos del mundo tenemos que acceder al archivo *level.dat*.

![Modificar level.dat](/assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/level-dat.jpg)

Vamos a ver qué tipo de opciones podemos modificar desde NBTExplorer.

**Nota:** Es importante guardar los cambios antes de cerrar el programa.

### Permitir comandos

**Cuando creas un mundo de Minecraft puedes habilitar el uso de trucos** (comandos) desde más opciones del mundo, pero es algo que **no se puede cambiar** desde el juego.

En muchos casos necesitas utilizar los trucos para cambiar *gamerules* del juego con las que te sientes más cómodos, hacer pruebas o incluso presentarte nuevos retos o nuevas formas de jugar.

Con el NBTExplorer podemos modificar la opción de permitir o no los trucos. Basta con hacer doble click sobre el dato **allowCommands** para editarlo.

* **0** - No permitir comandos
* **1** - Permitir comandos

![Editar AllowCommands](/assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/allow-commands.jpg)

### Dificultad

La dificultad en Minecraft se puede editar desde las opciones del juego. Pero también la podemos bloquear para impedir que se pueda cambiar. Esto es algo que también se puede modificar desde NBTExplorer.

El valor **Difficulty** nos indica la dificultad del juego. Tiene estos posibles valores:

* **0** - Pacífico (Peaceful)
* **1** - Fácil (Easy)
* **2** - Normal (Normal)
* **3** - Difícil (Hard)

Además, también **podemos cambiar la opción que bloquea la edición de la dificultad** desde el juego. Cambiando el valor de **DifficultyLocked**.

* **0** - Dificultad no bloqueada
* **1** - Dificultad bloqueada

![Editar la dificultad](/assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/difficulty.jpg)

### Modo Hardcore

Si creas un mundo **en modo hardcore ya no se puede cambiar el modo de juego**. En modo hardcore si mueres ya no podrás volver a jugar en ese mundo.

Si llevas un mundo muy avanzado es posible que quieras cambiar el modo y seguir jugando como una partida normal.

Podemos cambiar el modo de juego editando el valor de **hardcore**.

* **0** - Modo normal
* **1** - Modo hardcore

![Editar modo Hardcore](/assets/images/posts/nbtexplorer-modificar-datos-mundo-minecraft/hardcore.jpg)

## Otros campos

Como podéis ver hay otros muchos campos dentro de level.dat, pero es importante ir con cuidado al modificarlos. Tenemos que estar seguros de lo que estamos haciendo. **Recomiendo hacer una copia de seguridad del mundo** antes de modificarlo.

Yo os he presentado los campos que son seguros de modificar y que es más habitual que necesitemos cambiar.

> Es importante crear una copia de seguridad del mundo antes de modificarlo.

Desde NBTExplorer se puede modificar otros muchos campos como los relacionados con la generación del mundo o con el personaje.

## Referencias

* [**GitHub NBTExplorer**]( https://github.com/jaquadro/NBTExplorer) - Código fuente alojado en GitHub.
* [**Listado de versiones de NBTExplorer**](https://github.com/jaquadro/NBTExplorer/releases) - Listado con las *releases* de NBTExplorer disponibles para descargar.
* [**Foro de Minecraft sobre NBTExplorer**]( http://www.minecraftforum.net/forums/mapping-and-modding/minecraft-tools/1262665-nbtexplorer-nbt-editor-for-windows-and-mac) - Más información sobre NBTExplorer en el foro de Minecraft.
* [**Justin Aquadro**](https://twitter.com/trawk) - Twitter del creador de NBTExplorer.

Espero que esto os sirva para *arreglar* algunos de vuestros mundos en los que hayáis configurado alguna de las opciones anteriores que no se pueden cambiar.

¡Nos vemos en el futuro!
