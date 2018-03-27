---
layout: post
current: post
cover: assets/images/posts/entorno-git-consola-mac/colors-and-branch.png
navigation: True
title: "Entorno de Git en la consola de Mac"
date: 2017-07-03 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hace poco que me he comprado un MacBook Pro y aun estoy acostumbrándome a su uso.

Además del sistema operativo quiero probar cual es la experiencia de usuario a la hora de programar. Hoy vamos a ver cómo he creado mi entorno de Git para trabajar con la consola.

## Expectativas

A mí me gusta utilizar Git a través de la consola de comandos. Cuando decidí probar Mac me imaginaba que usaría bastante más la consola de comando de lo que la uso en Windows. Cosa que me gusta.

**Mi expectativa al instalar Git en Mac era tener una experiencia similar a la que tengo con Git Bash para Windows**: coloreado de los elementos, nombre de la rama, autocompletado de los comandos, Git Credentials Manager, etc… Pero me encontré con una terminal sosa (aun **usando iTerm**) sin ninguna de estas características.

Como he comentado antes llevo poco tiempo con el Mac pero ya he conseguido crearme un entorno de consola para trabajar con Git con el que me siento cómodo. Os voy a enseñar cómo lo he conseguido.

## Instalar Git

En mi caso he hecho la instalación de Git a través de *brew*.

`brew install git`

Con esto **ya podríamos empezar a trabajar con Git**. Pero no es suficiente.

## Coloreado

Para el coloreado de la consola tan solo es necesario añadir la siguiente configuración en el `~/.bash_profile`:

```bash
export CLICOLOR='true'
export LSCOLORS="gxfxcxdxbxCgCdabagacad"
export EDITOR=vi
```


**Nota:** También he configurado *vi* como editor por defecto de Unix.

### Nombre de la rama

Para mí es **imprescindible tener el nombre de la rama actual visible en todo momento**. Para ello tenemos que añadir, también en el `~/.bash_profile`, las siguientes líneas:

```bash
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PS1='\[$(tput setaf 7)\]\u@\[$(tput setaf 2)\]\h:\[$(tput setaf 4)\]\w\[$(tput setaf 1)\]$(parse_git_branch)\[$(tput sgr0)\] $ '
```

Junto con el coloreado del paso anterior ya tenemos una consola bastante más agradable de utilizar y con la información de la rama siempre visible.

![Consola](/assets/images/posts/entorno-git-consola-mac/colors-and-branch.png)

## Autocompletado

Tenemos una consola más bonita y que nos muestra el nombre de nuestra rama actual… Pero aún no es del todo usable: **no tenemos autocompletado de comandos ni ramas**.

Esto es muy sencillo de solucionar, primero tenemos que instalar `bash-completion`:

`brew install bash-completion`

Y por último añadir el siguiente código en el `~/.bash_profile`:

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

## Git Credential Manager

Git Crendential Manager for Mac es una herramienta de Microsoft que nos permite almacenar las credenciales de Git de forma segura. Además nos ofrece un inicio de sesión seguro para acceder a los repositorios alojados en VSTS.

**Nota:** En su versión para Windows nos ofrece un inicio de sesión para otros servicios como GitHub o Bitbucket.

Esto nos permite realizar acciones sobre un repositorio de Git en VSTS sin necesidad de usar las credenciales alternativas de Git sino utilizando el propio inicio de sesión de Microsoft.

Git Credential Manager se puede instalar también desde *brew*:


`brew update`

`brew install git-credential-manager`

`git-credential-manager install`

Ahora deberíamos poder acceder a un repositorio en VSTS a través de nuestro login con Microsoft.

## Conclusiones

Con el Mac he vuelto al maravilloso mundo de la consola de comandos. Con lo que hemos visto hoy podemos tener un entorno de Git similar a lo que yo estaba acostumbrado en Windows. De momento me siento cómodo con él, aunque supongo que lo iré mejorando con el tiempo. ¡Os mantendré informados!

## Referencias

### Instalar Git

* [Installing Git on Mac](https://git-scm.com/book/en/v1/Getting-Started-Installing-Git#Installing-on-Mac)

### Coloreado y nombre de la rama

* [Terminal tuning for Git developers in Mac](http://www.harecoded.com/terminal-tuning-for-git-developers-in-mac-2364711)

### Autocompletado

* [Install Bash git completion](https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion)

### Git Manager Credentials

* [Documentación](https://github.com/Microsoft/Git-Credential-Manager-for-Mac-and-Linux)

* [Instalación en Mac](https://github.com/Microsoft/Git-Credential-Manager-for-Mac-and-Linux/blob/master/Install.md#how-to-install)

Y esto ha sido todo. Espero seguir pudiendo disfrutar de la experiencia de programar en Mac. ¡Nos vemos en el futuro!
