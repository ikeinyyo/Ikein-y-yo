---
layout: post
current: post
cover: False
navigation: True
title: "Cómo crear un tipo no nulable (C#)"
date: 2017-03-22 12:00:00
tags: tech
class: post-template
subclass: 'post'
author: maktub82
---

¡Hola a todos! En este post vamos a ver cómo hacer un tipo no nulable. Todos hemos utilizado alguna vez tipos que no admiten nulos como por ejemplo `DateTime` pero no muchas veces hemos necesitado **crear un tipo no nulable**. Es un problema al que me acabo de enfrentar por primera vez desde que programo en C#.


## ¿Cómo hacemos un objeto no nulable?

Estoy trabajando en un proyecto en el que me interesa que un objeto no pueda ser nulo.

Como no sabía como hacerlo me puse a buscar en Internet cómo hacer que un tipo no admita nulos. Encontré [esta](http://stackoverflow.com/questions/6365459/create-non-nullable-types-in-c-sharp) respuesta en StackOverflow.

![Respuesta de StackOverflow](/assets/images/posts/como-crear-un-tipo-no-nulable/answer.jpg)

Esperaba que tuviera que añadir algún tipo de atributo, alguna herencia rara, magia negra... Pero no, era mucho más simple: **no tenía que hacer una clase sino un *struct***.

> Para crear un **tipo no nulable** tenemos que hacer un **struct**.

## No te creo. Seguro que no es así...

Eso es lo que pensaba yo. Cuando leí la respuesta pensaba que el señor Miguel Angelo nos estaba tomando el pelo a todos. Así que decidí mirar tipos no nulables como `TimeSpan`, `DateTime` o `int` y estas son sus definiciones de tipos.

```csharp
public struct TimeSpan : IComparable, IComparable<TimeSpan>, IEquatable<TimeSpan>, IFormattable { ... }
public struct DateTime : IComparable, IFormattable, IConvertible, ISerializable, IComparable<DateTime>, IEquatable<DateTime> { ... }
public struct Int32 : IComparable, IFormattable, IConvertible, IComparable<Int32>, IEquatable<Int32> { ... }
```

Efectivamente los tipos `TimeSpan`, `DateTime` y `int` realmente son structs.

## Un pequeño ejemplo

Vamos a ver un ejemplo sencillo de un *struct* y cómo utilizarlo. En primer lugar, vamos a ver el tipo `Person`.

```csharp
public struct Person
{
    public Person(string name) : this(name, string.Empty, 0)
    {
    }

    public Person(string name, string surname) : this(name, surname, 0)
    {
    }

    public Person(string name, string surname, int age)
    {
        Name = name;
        Surname = string.Empty;
        Age = age;
    }

    public int Age { get; }
    public string Name { get; }
    public string Surname { get; }

    public string GetFullName => $"{Name} {Surname}";
    public void Birthday()
    {
        Age++;
    }
}
```

Como podemos ver usar un struct no nos impide tener constructor, propiedades y métodos. La única limitación que tenemos en este aspecto es que todas las propiedades se tienen que asignar antes de que el objeto termine de construirse. Es decir que el constructor debe asignar valor a todas las propiedades.

**Nota**: Ojo, no todas las propiedades tienen que asignarse a través de un parámetro en el constructor, podemos usar valores por defecto.

No nos valdría algo como esto:

```csharp
public Person(string name, string surname)
{
    Name = name;
    Surname = string.Empty;
}
```
Pero sí algo como esto:

```csharp
public Person(string name, string surname)
{
    Name = name;
    Surname = string.Empty;
    Age = 0;
}
```

> Todas las propiedades deben asignarse cuando se construye un objeto.

Una vez tenemos nuestro tipo ya podemos usarlo. En la práctica vamos a tener la misma experiencia que al trabajar con una clase, salvo que no vamos a poder nular el objeto.

**Advertencia:** Es importante tener en cuenta que cuando se pasen objetos de nuestro tipo por parámetro vamos a pasarlos **por valor no por referencia** con todo lo que eso conlleva. Podrían surgir también algunas complicaciones al trabajar con nuestros objetos por valor. **Hay que tener cuidado con esto**.

Si necesitáramos poder nular el objeto siempre podríamos usar el modificador `?` para convertir de `Person` a `Person?`.

```csharp
void Example()
{
    Person person = new Person("Sergio", "Gallardo", 25);
    person.Birthday();

    Person? nullablePerson = null;
}
```

## struct Conclusiones { }

La verdad es que después de ver esto me da por pensar si siempre hacemos un uso responsable de las clases. Yo nunca me he planteado hacer un *struct* en vez de una clase, pero quizás sería algo que nos deberíamos plantear más a menudo. Hay muchas veces que creamos clases que simplemente son contenedores de información.

> ¿Deberíamos usar los *structs* más a menudo?

El hecho es que el ***struct* suena al pasado**, suena a cuando en la universidad estábamos empezando a programar y aun no sabíamos lo que es una clase. Sinceramente yo lo veo así pero quizás es el momento de ver en qué escenario podemos o debemos utilizar *structs*. De momento yo ya he encontrado uno y podré decir que **una vez en C# creé un *struct***.

¿Qué opináis vosotros de los *structs*? ¿Los estamos infravalorando? ¿Se deberían usar más?

¡Nos vemos en el futuro!
