---
layout: post
current: post
cover: assets/images/posts/mis-comandos-de-git/header.jpg
navigation: True
title: "Mis comandos de Git"
date: 2017-01-27 12:00:00
tags: git tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hoy vengo a hablar de cómo trabajo yo con Git.

Hay muchas formas de trabajar con Git y cada uno debe hacerlo cómo más cómodo se encuentre. En mi caso es a través de la consola de comandos. Creo que utilizar la consola de comando te da más control de lo que está sucediendo además de que te ayuda a asimilar mejor los conceptos de Git.

Para agilizar un poco mi forma de trabajar he creado algunos comandos nuevos.

**Update:** [Aquí](https://www.ikeinyyo.com/mis-comandos-de-git-2) tenéis la segunda parte.

## .bashrc

Hay muchas formas de crear nuestros propios comandos. En mi caso he optado por la más sencilla de todas. He añadido el código de los comandos en el .bashrc como métodos. De esta forma cuando trabajo con mi consola de comandos de bash siempre los tengo disponibles.

Os dejo el enlace al [.basrc](https://github.com/maktub82/.bashrc/blob/master/.bashrc) que tengo actualmente.

### goto

En mi .bashrc lo primero que aparece es un método goto que me permite crear alias a directorios y navegar a ellos. El goto es creación de mi compañero [Martín Candela](https://twitter.com/RellikCC) y lo podéis encontrar en su [Github](https://github.com/Rellikiox/goto). Simplemente le he hecho algunas modificaciones para poder trabajar más fácilmente con los _paths_ en Windows.

## gclean

El primer comando me sirve para navegar a una rama _limpia_. Muchas veces si has trabajado con algunos cambios o por error has hecho algún commit en alguna rama que no te interesaba cuando quieres volver a ella lo más sencillo es hacer un `fetch` para obtener posibles cambios en el repositorio remoto, borrar la rama y hacer un checkout a ella para estar sincronizado.

Básicamente nos ahorramos el hacer el `fetch`, `pull` y lidiar con algún posible commit que no queríamos y está _ensuciando_ nuestra rama.

El código es el siguiente:

```bash
gclean() {
	if [ $# = 0 ]; then
    git fetch;
		git branch -D "develop";
		git checkout "develop";
  else
		git fetch;
		git branch -D $1;
		git checkout $1;
	fi
}
```

**Nota:** El código es mejorable, pero... es bash 😝

Como vemos este script admite un parámetro con el nombre de la rama. Si no ponemos nada por defecto lo hará sobre `develop`.

Lo primero que hacemos es un `fetch`, borramos la rama y nos movemos a ella de nuevo. Fácil. Navegamos a una rama actualizada y libre de posible _basura_.

## gnewf / gnewb

Este par de comandos me sirven para crear ramas. En mi empresa trabajamos siguiendo la convención de nombres de `feature/id_feature` para las ramas de features y `bug/id_bug` para las ramas de bug fixing.

```bash
gnewf() {
	git checkout -b "feature/"$1;
}

gnewb() {
	git checkout -b "bug/"$1;
}
```

En este caso simplemente nos ahorramos escribir todo lo de `git checkout -b` y el prefijo de la rama. Sencillo, pero nos ahorra tiempo.

## gbclean

Cuando termino de trabajar con una rama y se completa la Pull Request la rama remota se borra, pero sigo teniendo mi rama en local.

Esto hace que al final navegar entre las ramas con la consola de comandos sea tedioso porque se van acumulando y raramente me acuerdo de borrarlas.

Para eso tenemos este comando. Nos permite borrar todas las ramas locales excepto en la que estamos.

```bash
gbclean() {
	branches=$(git branch | grep -v \* | xargs);
	git branch -D $branches;
}
```

Básicamente listamos las ramas con `git brach` y las filtramos con `grep` para obtener todos los nombres de las ramas. A continuación, las borramos todos con `git brach -D`.

## gsquash

Este es el último comando que he añadido a mi lista. Me sirve para hacer _squash_.

Lo primero que hago es un `fetch` para poder traerme algún posible cambio del repositorio remoto y luego hago el rebase interactivo contra el recién actualizado `origin/develop`.

```bash
gsquash() {
  git fetch;
  if [ $# = 0 ]; then
    git rebase -i origin/develop;
  else
    git rebase -i "origin/"$1;
	fi
}
```

## ¿Alguna idea nueva?

Esto es todo. De momento con estos nuevos comandos me siento muy cómodo. Hace que trabajar con la consola sea un poco más sencillo y rápido.

Pero como siempre, me gustaría seguir mejorándolo. Así que estoy abierto a sugerencias tanto de comandos como de una mejor forma de incluirlos que no sea en el .bashrc.

¡Nos vemos en el futuro!
