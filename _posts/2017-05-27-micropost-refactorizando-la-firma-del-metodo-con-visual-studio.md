---
layout: post
current: post
cover: assets/images/posts/micropost-refactorizando-la-firma-del-metodo-con-visual-studio/edit.jpg
navigation: True
title: "[Micropost] Refactorizando la firma del método con Visual Studio"
date: 2017-05-27 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! Hoy tenemos un nuevo Micropost en el que vamos a ver una de las funciones de *refactoring* que tiene Visual Studio.

Podéis disfrutar del resto de [Micropost]( http://www.ikeinyyo.com/tag/micropost/) del blog.

## Refactorizando la firma del método

Imaginemos que tenemos la clase `Matrix` que representa un matriz. La forma habitual de trabajar con una matriz es a través de *filas y columnas*. En el desarrollo inicial, los métodos para modificar la matriz se han implementado indicando primero la columna y luego la fila.

La situación ha provocado muchos problemas ya que otros desarrolladores se han confundido a la hora de trabajar con la matriz. Necesitamos refactorizar el orden de los argumentos de todos los métodos.

``` csharp
public class Matrix
{
    private int[][] matrix;

    private void SetValue(int column, int row, int value)
    {
        matrix[row][column] = value;
    }

    private void InitializeRow(int row, int value)
    {
        for (int i = 0; i < matrix[row].Length; i++)
        {
            SetValue(i, row, value);
        }
    }
}
```

Vamos a refactorizar el método `SetValue`. Nos situamos en el método y le damos a **Edit > Refactor > Reorder Parameters** o pulsamos **Ctrl+R, O**.

![Refactor desde el Menú](/assets/images/posts/micropost-refactorizando-la-firma-del-metodo-con-visual-studio/edit.jpg)

Nos aparece una ventana en la que podemos reordenar los parámetros e incluso borrarlos. Para nuestro ejemplo vamos a poner en primer lugar el parámetro `row` y en segundo lugar el `column`.

![Ventana de reorder](/assets/images/posts/micropost-refactorizando-la-firma-del-metodo-con-visual-studio/reorder.jpg)

Como podemos ver, **el refactor no cambia simplemente la firma del método, sino que se encarga también de cambiar el orden de los parámetros donde se está llamando al método**. El código nos queda de la siguiente forma.

``` csharp
public class Matrix
{
    private int[][] matrix;

    private void SetValue(int row, int column, int value)
    {
        matrix[row][column] = value;
    }

    private void InitializeRow(int row, int value)
    {
        for (int i = 0; i < matrix[row].Length; i++)
        {
            SetValue(row, i, value);
        }
    }
}
```

Con esta opción de Visual Studio ya no tenemos excusas para no refactorizar la firma de los métodos si vemos que es necesario: Visual Studio lo hace por nosotros.

¡Nos vemos en el futuro!
