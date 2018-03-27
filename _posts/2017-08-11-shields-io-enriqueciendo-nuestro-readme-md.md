---
layout: post
current: post
cover: assets/images/posts/shields-io-enriqueciendo-nuestro-readme-md/header.jpg
navigation: True
title: "Shields.io - Enriqueciendo el readme.md"
date: 2017-08-11 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hoy vengo a hablar de esos iconos que vemos muchas veces en los *readme* de GitHub que indican cosas como el número de descargas, el estado de la *build*, la cobertura de los tests, etc.

Esto no es ni más ni menos que [Shields.io](https://shields.io/).

## Cómo funciona Shields.io

[Shields](https://shields.io/) es una plataforma que nos ofrece una serie de etiquetas para añadir en nuestros *readme* o webs que nos ofrece información de distinto ámbito.

El funcionamiento es muy sencillo. Esta web nos ofrece una imagen generada con la información obtenida de diferentes fuentes de datos como Twitter, Github, VSTS, etc.

Por ejemplo podemos poner una etiqueta con los seguidores en Twitter.

[![Twitter Follow](https://img.shields.io/twitter/follow/maktub82.svg?style=social&label=Follow)](https://twitter.com/maktub82)

Esto es básicamente una imagen generada con una serie de parámetros en la URL.

```html
// Formato
https://img.shields.io/twitter/follow/USER_TWITTER.svg?style=social&label=Follow
```

Para añadirlo en el markdown podemos crear un enlace que contenga como contenido esta imagen y apunte a nuestro twitter.

```markdown
[![Twitter Follow](https://img.shields.io/twitter/follow/maktub82.svg?style=social&label=Follow)](https://twitter.com/maktub82)

// Siguiendo este formato
![ [alt_image](url_image_shields_io) ](url_enlace)
```

De esta forma podemos añadir cualquier etiqueta de Shields en nuestros markdowns. Ahora vamos a ver alguna de las opciones que nos ofrece.

## Build

Shields nos ofrece etiquetas para diferentes plataformas de [Build](https://shields.io/#build).

[![Travis](https://img.shields.io/travis/rust-lang/rust.svg?flat-square)]()

```markdown
![Travis](https://img.shields.io/travis/USER/REPO.svg)

![Jenkins](https://img.shields.io/jenkins/s/https/jenkins.qa.ubuntu.com/view/Precise/view/All%20Precise/job/precise-desktop-amd64_default.svg)

![Magnum CI](https://img.shields.io/magnumci/ci/96ffb83fa700f069024921b0702e76ff.svg)

```

### Cómo configurarlo en VSTS

Para poder configurar esta etiqueta de Build en VSTS tenemos que ir a la configuración de la build y activar la opción de *Badge*.

```markdown
![Visual Studio Team Services](https://img.shields.io/vso/build/TEAM_NAME/PROJECT_ID/BUILD_DEFINITION_ID.svg)
```

![VSTS Badge](/assets/images/posts/shields-io-enriqueciendo-nuestro-readme-md/vsts-config.png)

Al pulsar sobre *Show url...* podemos obtener los parámetros de la URL para rellenar los datos necesarios en Shields.

![VSTS Badge](/assets/images/posts/shields-io-enriqueciendo-nuestro-readme-md/vsts-url-data.png)

### Cobertura de código

Además de ofrecer el estado de la Build nos ofrecen la cobertura de código para muchas plataformas como Jenkins, Codecov, TeamCity, etc.

![Jenkins coverage](https://img.shields.io/jenkins/c/https/jenkins.qa.ubuntu.com/view/Utopic/view/All/job/address-book-service-utopic-i386-ci.svg?style=flat-square)

## Downloads

Otra de las etiquetas que podemos poner es el número de [descargas](https://shields.io/#downloads). De nuevo, está disponible en múltiples plataformas.

[![NuGet](https://img.shields.io/nuget/dt/Microsoft.AspNetCore.Mvc.svg?style=flat-square)]()

Algunas de las plataformas disponibles son GitHub, npm, NuGet, SourceForge, etc.

```markdown
![NuGet](https://img.shields.io/nuget/dt/Microsoft.AspNetCore.Mvc.svg?style=flat-square)
![npm](https://img.shields.io/npm/dw/localeval.svg?style=flat-square)
![Github All Releases](https://img.shields.io/github/downloads/atom/atom/total.svg?style=flat-square)
![SourceForge](https://img.shields.io/sourceforge/dm/sevenzip.svg?style=flat-square)
```

## Otras etiquetas

Además de las etiquetas para las Builds y las descargas, Shields nos ofrece otras muchas.

Tenemos la opción de añadir una etiqueta con el versionado de nuestros proyectos.

[![GitHub tag](https://img.shields.io/github/tag/expressjs/express.svg?style=flat-square)]()

También podemos añadir etiquetas de carácter social. Como los seguidores de Twitter o las estrellas en GitHub.

[![GitHub followers](https://img.shields.io/github/followers/maktub82.svg?style=social&label=Follow)](https://github.com/maktub82)

Y otras muchas cosas más:

[![GitHub pull requests](https://img.shields.io/github/issues-pr/cdnjs/cdnjs.svg?style=flat-square)]()

[![Github file size](https://img.shields.io/github/size/webcaetano/craft/build/craft.min.js.svg?style=flat-square)]()

[![Docker Stars](https://img.shields.io/docker/stars/_/ubuntu.svg?style=flat-square)]()

[![Chrome Web Store](https://img.shields.io/chrome-web-store/stars/nimelepbpejjlbmoobocpfnjhihnpked.svg?style=flat-square)]()

Podéis ver el listado completo en la página de [shields.io](https://shields.io/).

## Etiquetas personalizadas

Otra opción que tenemos es la de personalizar nuestras propias etiquetas siguiendo este patrón.

```markdown

https://img.shields.io/badge/TAG-VALUE-COLOR.svg

[![No Country for Geeks](https://img.shields.io/badge/Colaborando%20en-No%20Country%20for%20Geeks-orange.svg)](http://www.nocountryforgeeks.com/author/gallardo)
```

[![No Country for Geeks](https://img.shields.io/badge/Colaborando%20en-No%20Country%20for%20Geeks-orange.svg)](http://www.nocountryforgeeks.com/author/gallardo)

De esta forma podemos poner enlaces más vistosos.

## En resumen...

Como veis, es una gran forma de darle un poco de vida a nuestros *readme* y posts.

Podemos añadir mucha información para proyectos colaborativos como el estado de la build, las pull requerst, la cobertura de código, etc. gracias a la gran cantidad de plataformas que soporta.

Creo que voy a empezar a añadir alguna de estas etiquetas en los proyectos en los que participe. Os animo a hacer lo mismo.

Un saludo y ¡nos vemos en el futuro!

[![Twitter URL](https://img.shields.io/twitter/url/http/maktub82.svg?style=social)](https://twitter.com/maktub82)
