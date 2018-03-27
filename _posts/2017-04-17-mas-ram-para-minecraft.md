---
layout: post
current: post
cover: assets/images/posts/mas-ram-para-minecraft/arguments.jpg
navigation: True
title: "Más RAM para Minecraft"
date: 2017-04-17 12:00:00
tags: minecraft
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hoy vamos a ver cómo configurar Minecraft para poder consumir más memoria RAM.

## ¿Para qué?

Si como yo, habéis jugando con *mods* o tenéis vuestro mundo con un montón de mecanismos con *pistones*, *hoppers* y *redstone* por todos los lados sabrás que a veces la memoria RAM se queda un poco justa. Y es que **Minecraft por defecto dedica solo 1Gb de RAM**. Pero eso lo podemos cambiar.

## ¿Cómo aumento el máximo de RAM?

La verdad es que no hay una forma *user friendly* de hacerlo en las settings.

Desde el nuevo launcher **desplegamos el menú hamburguesa** y nos aparecerá una pestaña con las opciones del launcher llamada **Launcher options**.

![Launcher Options](/assets/images/posts/mas-ram-para-minecraft/launcher.jpg)

**Importante:** En esta pestaña tenemos que habilitar las opciones avanzadas.

Ahora simplemente hacemos click en el perfil que queremos modificar. En mi caso voy a editar el perfil del *forge* para que Minecraft utilice hasta 8Gb de RAM.

Para ello tenemos que habilitar la edición de los argumentos que se le pasan a la máquina virtual de Java **(JVM arguments)**. Esto nos va a permitir **modificar los argumentos con los que se lanza la máquina virtual de Java que ejecuta Minecraft**.

![JVM arguments](/assets/images/posts/mas-ram-para-minecraft/arguments.jpg)


Para modificar la memoria RAM dedicada nos interesan dos argumentos:
**-Xmx** y *-Xmn* que corresponden con la memoria máxima y memoria mínima que va a utilizar Minecraft.

**Nota:** Lo simplificamos como memoria máxima y mínima aunque es un poco más complejo que esto, tiene que ver con el *heap* de Java. Podéis saber más en la [documentación]( https://docs.oracle.com/cd/E13150_01/jrockit_jvm/jrockit/jrdocs/refman/optionX.html).

La nomenclatura para estos parámetros es:

`-Xms<size>[g|G|m|M|k|K]`

`-Xmx<size>[g|G|m|M|k|K]`


Así que basta con cambiar el valor del argumento **-Xmx** a **-Xmx8G** para que como máximo pueda llegar a 8Gb.

En mi caso quedarían así los argumentos de la JVM.

`-Xmx8G -XX:+UseConcMarkSweepGC -XX:+CMSIncrementalMode -XX:-UseAdaptiveSizePolicy -Xmn128M`

**Nota:** Estos argumentos tendremos que editarlo por cada perfil de Minecraft que queramos jugar.

Y eso es todo por hoy. ¡Nos vemos en el futuro!
