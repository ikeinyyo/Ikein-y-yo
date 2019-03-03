---
layout: post
current: post
cover: assets/images/posts/mis-comandos-de-git-2/header.jpg
navigation: True
title: "Mis comandos de Git - Parte 2"
date: 2019-03-02 12:00:00
tags: git tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Ya escribí un post de los comandos que me he hecho para trabajar con Git. Lo tenéis disponible en [este mismo blog](https://www.ikeinyyo.com/mis-comandos-de-git). Desde entonces, he añadido unos cuantos comandos más que me parecen bastante interesantes y me agilizan a la hora de trabajar con la consola de comandos.

Al igual que el resto de comandos, los he añadido al .bashrc (o .bash_profile).

Os dejo el enlace al [.basrc](https://github.com/maktub82/.bashrc/blob/master/.bashrc) que tengo actualmente.

## gtree

Este comando me sirve para poder mostrar el árbol de git de forma visual en la consola de comandos.

```bash
gtree() {
  git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative --branches;
}
```

Me parece muy útil poder visualizar el árbol visual de Git en alguna situación y sobre todo para poder explicar qué está pasando en el repositorio.

## guser

En mi día a día, utilizo el mismo PC para acceder a diferentes repositorios de Git. Algunos están en mi Github, otros en mi Azure DevOps personal y otros en el de Plain Concepts.

Esto hace que **no quiera configurar el usuario a nivel global**. Así que lo configuro a nivel de repositorio. Para ahorra tiempo he creado el comando `guser` que me configura el usuario según el que indique.

```bash
guser() {
  case $1 in
    plain)
      git config user.email "mail@plainconcepts.com";
      git config user.name "Sergio Gallardo Sales";
      ;;
    github)
      git config user.email "mail@personal.com";
      git config user.name "maktub82";
      ;;
    vsts)
      git config user.email "mail@personal.com";
      git config user.name "Sergio Gallardo Sales";
      ;;
  esac
}
```

De esta forma puedo configurar rápidamente el usuario que quiero utilizar en cada repositorio.

## gundo

Este comando, simplemente, deshace los cambios en el directorio de trabajo.

```bash
gundo() {
  git checkout .;
}
```

## gcache

Otro comando muy útil es el `gcache` que elimina del directorio todos los archivos que no estén trackeados por git.

Esto me permite limpiar los proyectos, eliminando las carpetas `/bin`, `/obj` , `node_modules`, etc... todo aquello que no esté en el repositorio de git.

```bash
gcache() {
	git clean -dfx;
}
```

## gupdate

Como no soy la persona más cuidadosa del mundo, a veces hago commits donde no debo hacerlos. Por tanto, si quiero actualizarme una rama, es posible que la tenga contaminada con algo que no debería estar ahí.

Para eso me he creado el comando `gupdate`, que, después de hacer un `fetch` para actualizarme las ramas remotas, me borra la rama actual y vuelve a hacer un `checkout` a esa misma rama para **asegurar que estoy alineado con el repositorio remoto** y sin nada que pueda estar contaminando el repositorio. Para esto, me apoyo en una rama temporal.

```bash
gupdate() {
  git fetch;
  current_branch=$(git symbolic-ref --short -q HEAD);
  git checkout -b tmp
  git branch -D $current_branch;
  git checkout $current_branch
  git branch -D tmp;
}
```

## ¿Seguimos?

Y de momento, esos son los nuevos comandos que he añadido. Los utilizo en mi día a día para trabajar de forma más ágil con Git.

Estoy seguro que **saldrán más comandos en el futuro para sentirme más cómo trabajando con Git en consola**.
