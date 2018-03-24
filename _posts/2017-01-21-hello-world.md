---
layout: post
current: post
cover: False
navigation: True
title: "Hola Mundo: un blog en Ghost"
date: 2017-01-21 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Empezamos una nueva aventura esta vez junto a Ikeín.

##  ¿De qué va esto?
En esta nueva etapa vamos a tener un blog en el que hablar en general de todo lo que me gusta: programar, Minecraft y otras aficiones... además de hablar mucho de Ikeín.
Para empezar, os voy a contar mi experiencia desplegando un blog de Ghost en Azure.
## Ghost en Azure

Antes de decidirme por Ghost (por cambiar un poco de Wordpress) miré algunas de las soluciones que nos ofrece Azure en el tema de blogs y CMS. Que como podemos ver son muchas.

![Azure Marketplace](/assets/images/hello-world/blogs.PNG)

Al final me decidí a probar Ghost por su simplicidad y DNN por su complejidad.

### Ghost
Hace tiempo que quería probar Ghost como plataforma de blogs. Tras echarle un vistazo he visto cosas que me han gustado mucho y otras que no.

Votos a favor

* Diseño muy simple y limpio.
* Creación de los post en Markdown.

Votos en contra

* No he encontrado opción de plugins. Entiendo que no la tiene.
* Instalación de temas tediosa: copiar los temas en el servidor a través de FTP.
* Personalización: dentro del tema por defecto no hay muchas cosas que se puedan personalizar.
* Despliegue en Azure (directamente desde el Marketplace de Azure).

**UPDATE:** Al parecer en versiones más recientes se puede instalar los temas desde lad Settings arrastrando el Zip.

### DNN
Descartado casi inmediatamente después de completar la instalación porque es demasiado complejo para un blog. Es un CMS muy potente como para usarlo simplemente para mantener este blog. No compensa la curva de aprendizaje y configuración. Además, requiere una instancia de SQL Server en Azure para poder funcionar.

## Me quedo con Ghost
Pese a todos los problemas que le he visto a Ghost me apetece probarlo. Además, siempre tendré mis post en markdown y la migración a otro servicio no debería ser difícil.

Después de probar muchos temas decidí quedarme con [Boo](https://github.com/tenoku/boo), muy silimiar a Casper que viene por defecto, pero haciendo algún cambio, por ejemplo, en el menú lateral.

La primera vez que probé Ghost fue desplegando directamente desde el Marketplace de Azure y no tuve ningún problema. Después de todas las pruebas decidí crear una nueva instancia y borrar la anterior. Por algún motivo que desconozco jamás volvió a funcionar…

Tras mucho tiempo recreando el servicio, instalando en el servidor sqlite, reinstalando node, lanzando comandos de bower no conseguí que funcionara.

Pero encontré en el [repositorio de GitHub de Ghost](https://github.com/felixrieseberg/Ghost-Azure) un botón mágico.

![Botón de Azure Deploy](/assets/images/hello-world/button.png)

El botón este nos lanza el despliegue de Azure desde un repositorio de git. Nos lleva a una url de este estilo:

 `https://deploy.azure.com?repository=https://github.com/felixrieseberg/Ghost-Azure#/form/setup`

![Azure Deploy](/assets/images/hello-world/azuredeploy.png)

Y por fin, cuando termina esta instalación todo funciona perfectamente y aquí estamos.

Al parecer la instalación del Marketplace de Azure [está desactualizada](https://github.com/felixrieseberg/Ghost-Azure/issues/19). De esta forma desplegamos directamente desde el [GitHub de Ghost para Azure](https://github.com/felixrieseberg/Ghost-Azure).

## Conclusión
Se dice que muchas veces menos, es más. Vamos a ver qué tal se comporta esta plataforma de blogs ligera y sencilla. De momento me gusta lo de hacer los post en Markdown y lo simple que es todo.
Un saludo y ¡Nos vemos en el futuro!
