---
layout: post
current: post
cover: assets/images/posts/actualizando-ghost-a-la-1-0-0/casper-2.png
navigation: True
title: "Actualizando Ghost a la 1.0.0"
date: 2017-07-24 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Por fin ha salido **la versión estable de Ghost, la 1.0.0**, y nos hemos actualizado. Vamos a ver mis primeras impresiones.

## Versión 1.0.0

La versión 1.0.0 de Ghost supone un cambio brutal con las versiones alpha 0.11.x que teníamos disponibles hasta ahora. Pese a que la esencia de la plataforma no cambia hemos experimentado muchas mejoras y nueva funcionalidad.

### Casper 2.0.0

Una de las novedades que trae la versión 1.0.0 de Ghost es la **actualización de Casper**, el tema por defecto de Ghost, a la 2.0.0.

Esta es la versión de Casper de la 0.11.x:

![Casper 1.0.0](/assets/images/posts/actualizando-ghost-a-la-1-0-0/casper-1.png)

Y este es el nuevo diseño de Casper 2.0.0:

![Casper 2.0.0](/assets/images/posts/actualizando-ghost-a-la-1-0-0/casper-2.png)

Este nuevo tema es mucho más atractivo ya que incluye las imágenes de los post en la página principal. Además, muestra los post en forma de tarjetas que varían de tamaño. El aspecto es sin duda mucho mejor que el que ofrecía Casper 1.3.4.

Otra característica que ha mejorado con el nuevo tema es el menú. Antes el menú estaba oculto tras el botón de hamburguesa, ahora aparece en la parte superior, más visible y accesible.

### Soporte para tablas en Markdown

Han añadido soporte a las tablas en Markdown. En versiones anteriores de la 0.11.x no estaban soportadas.

## *Desfeatures nuevas*

Una *desfeature* (algo en lo que ha empeorado) es en el editor de post a la hora de añadir las imágenes.

Antes si subías un markdown con un hueco preparado para una imagen con la estructura `![alt_text](url_image)` en el editor te aparecía un cuadro para poder hacer *Drag&Drop* y cargar directamente la imagen.

Esta funcionalidad ha desaparecido, ahora puedes hacer *Drag&Drop* pero la imagen se añade donde tengas el curso. Esto te impide reutilizar el markdown directamente ya tienes que eliminar tu estructura `![alt_text](url_image)`.

**Nota:** El resto del editor ha mejorado, permitiéndote una mejor edición de las *cursivas*, **negritas** y otros aspectos de markdown.

## Breaking Changes

La versión estable de Ghost rompe completamente con las versiones alpha. Por tanto para actualizarse **es necesario crear una nueva instancia con Ghost 1.0.0 y migrar los datos.**

Simplemente debemos copiar la carpeta `content/images/` a nuestro nuevo sitio y exportar e importar la información desde el panel de configuración de Ghost. No es difícil, pero requiere crear una nueva instancia.

[Aquí](https://docs.ghost.org/docs/migrating-to-ghost-1-0-0) podéis consultar la guía de migración.

## Desplegando en Azure

En mi caso he optado por desplegarlo en una máquina virtual de Linux en Azure.

He escogido una máquina con Ubuntu 16.04 LTS A1 y he seguido la [guía de instalación](https://docs.ghost.org/v1.0.0/docs/installing-ghost-via-the-cli) con Ghost-Cli.

**Nota:** Es importante abrir el puerto 80 de la máquina virtual. Además, si vais a personalizar el dominio necesitáis configurar IP estática cuando creáis la máquina.

## Resultado: muy contento

Estoy muy contento con la nueva versión de Ghost, aunque aun tengo que ajustar algunas cosas.

La migración de datos me ha traído algunas cosas que ya tenía como la configuración de Google Analytics, cabecera, etc. Por tanto pese a ser Breaking Changes, la migración no me ha llevado más de media hora. Lo más lento ha sido copiar las imágenes por FTP.

Tengo ganas de explorar a fondo esta versión y ver que otras cosas ofrece.

¡Nos vemos en el futuro!
