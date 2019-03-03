---
layout: post
current: post
cover: assets/images/posts/squash-or-not-squash/squash-pr.jpg
navigation: True
title: "Squash or not Squash"
date: 2017-04-24 12:00:00
tags: git tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! El otro día hablando con [Alejandro Campos](https://twitter.com/alejacma) sobre el uso de Git nos surgió una duda: **¿hacer un _squash_ es lo mismo que quedarse con el último _commit_?** La verdad es que es algo que no sé así que vamos a descubrirlo.

## ¿Qué es un squash?

Por simplificar diremos que un **_squash_ es juntar los cambios de varios commits en uno solo**.

En mi caso la forma que tengo de incluir código en mi rama develop es mediante Pull Request. Yo trabajo en mi rama local y hago cuantos _commits_ quiera. Antes de hacer la Pull Request hago un _squash_ y junto todos esos cambios en un _commit_.

## ¿Cómo trabaja Git?

Si leemos la [documentación](https://git-scm.com/book/es/v1/Empezando-Fundamentos-de-Git) oficial de Git podemos ver que para Git los cambios son instantáneas de cómo están los archivos en ese momento. Veamos que dice la documentación de Git:

> Sistemas como CVS, Subversion, Perforce, Bazaar, etc. modelan la información que almacenan como un conjunto de archivos y las modificaciones hechas sobre cada uno de ellos a lo largo del tiempo.

![CVS](/assets/images/posts/squash-or-not-squash/cvs.png)

> Cada vez que confirmas un cambio, o guardas el estado de tu proyecto en Git, él básicamente hace una foto del aspecto de todos tus archivos en ese momento, y guarda una referencia a esa instantánea.

![Git](/assets/images/posts/squash-or-not-squash/git.png)

Visto que el último _commit_ es una instantánea del estado del proyecto en ese momento **¿por qué no pensar que subir el último _commit_ equivale a hacer el squash de todos los _commits_ anteriores?**

**Nota:** Conceptualmente son cosas muy diferentes pero quiero comprobar si el código que se acaba subiendo es el mismo.

## Demo

Vamos a hacer una prueba sencilla reproduciendo los _commits_ de la imagen anterior. Partimos desde la [rama master](https://github.com/ikeinyyo/Squash/tree/master) con 3 ficheros: a.md, b.md, c.md.

![Git](/assets/images/posts/squash-or-not-squash/git.png)

Creamos la rama [changes](https://github.com/ikeinyyo/Squash/tree/changes) y aplicamos todos los cambios sobre los ficheros hasta llegar al estado deseado.

![Rama changes](/assets/images/posts/squash-or-not-squash/changes.jpg)

### Squash

Tenemos todos los cambios creados en esa rama. Ahora vamos a crear la rama [squash](https://github.com/ikeinyyo/Squash/tree/squash) en la que **haremos un _squash_ de estos commits**, manteniendo a la rama changes ajena a estos cambios.

`git rebase -i origin/master`

```
pick 07f01bc Version 2
s 2636059 Version 3
s ae0ce02 Version 4
s 4ac0698 Version 5
```

Una vez que hemos hecho el _squash_ y hemos subido la rama vamos a crear una [Pull Request](https://github.com/ikeinyyo/Squash/pull/1/files) contra _master_ a ver qué cambios nos genera.

![Pull Request - Squash](/assets/images/posts/squash-or-not-squash/squash-pr.jpg)

Como podemos ver en la Pull Request solo tenemos 1 _commit_ y los cambios en los ficheros nos dejan la rama _master_ en el estado deseado.

### Último _Commit_

Ahora vamos a ver qué pasa cuando subimos sólo el último _commit_. Para hacer esto posible creamos la rama lastCommit desde _master_ y hacemos un [_cherry-pick_](https://git-scm.com/docs/git-cherry-pick) para traernos solamente el último _commit_.

`git cherry-pick 4ac0698`

Al hacer un _cherry-pick_ nos aparecen conflictos en B y C. Esto no parece muy normal, si de verdad Git guarda instantáneas del código simplemente debería sobrescribir B y C con los cambios del último _commit_. De hecho me extraña más que no haya un conflicto en A ya que el último _commit_ está referenciando el estado de A del commit anterior. Recordemos el gráfico.

![Git](/assets/images/posts/squash-or-not-squash/git.png)

Más raro aun es en la resolución de conflictos que me ofrece quedarme con los cambios del Source (mi último _commit_) o con los del Target (mi rama _lastCommit_) pero en Result me aparece el estado anterior al último _commit_ de B, es decir, B1.

![Conflictos](/assets/images/posts/squash-or-not-squash/conflict-b.jpg)

Como vemos pasan cosas muy raras cuando intentamos traernos solo el último _commit_ de una serie de cambios. **Si alguien me explica por qué pasan estas cosas le estaré agradecido.**

Para seguir con el experimento vamos a resolver los conflictos y hacer la Pull Request.

![Pull Request - Last Commit](/assets/images/posts/squash-or-not-squash/lastCommit-pr.jpg)

Viendo esta Pull Request **se me hace difícil creer que Git almacene instantáneas del estado del repositorio en vez de los diferenciales**. Como vemos, hemos conseguido llevar al estado deseado tanto B como C gracias a la resolución de conflictos. Pero A parece que no ha sufrido ningún cambio respecto a master.

Tanto los conflictos como la Pull Request **se explicarían perfectamente si Git almacenara los diferenciales en cada commit**. Porque los conflictos se han originado con el estado inmediatamente anterior y el último _commit_ no aplicaba cambios sobre A, por eso en la Pull Request no hay ni rastro de A.

## Impresiones y conclusiones

Como comentaba antes, se me hace **difícil creer que Git funcione como dice que funciona**. Para más información os dejo la [documentación](https://git-scm.com/book/es/v1/Empezando-Fundamentos-de-Git). El comportamiento que he observado es más propio de un sistema que almacene los diferenciales entre _commits_. **Entiendo que Git no nos está mintiendo así que me gustaría que alguien me explicara todo esto**.

Os he dejado el repositorio con este ejemplo en el [GiiHub de Ikeín y yo](https://github.com/ikeinyyo/Squash) con las ramas y las Pull Request para que podáis jugar con ellas.

> Lo que si hemos demostrado es que no es lo mismo, a nivel del estado final del repositorio, subir sólo el último _commit_ que hacer un _squash_ de los cambios.

Me encantaría que en los comentarios alguien pudiera explicarme el porqué de estos comportamiento tan raros.

Un saludo y…

¡Nos vemos en el futuro!
