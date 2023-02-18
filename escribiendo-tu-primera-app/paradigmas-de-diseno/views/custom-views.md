---
description: En esta página se explicará como utilizar Views desarrolladas por terceros.
---

# Custom Views

## INTRODUCCIÓN

Hemos visto multitud de Views diferentes que Android Studio pone a nuestra disposición en las Palletes. Estas Views están pensadas para cubrir un gran abanico de necesidades, sin embargo, es imposible cubrir todas las situaciones posibles. Es por eso, que también se pueden utilizar **Custom Views** o, lo que es lo mismo, **Views Personalizadas**.

Estas **Custom Views pueden ser de dos tipos**:

### Crear Custom View

Puede ser que se de la situación en que necesitemos modificar ligeramente el comportamiento de una View concreta o, más complejo todavía, que ninguna de las Views que conocemos sean válidas para la situación que nos encontramos. En este caso puede ser muy útil saber crear nuestras propias Custom Views.

Por ahora, esto es algo que no domino así que dejo un **enlace al Blog de Antonio Leiva** para que le puedan echar un ojo.

{% embed url="https://devexperto.com/custom-views-android/" %}
Fuente: devexperto
{% endembed %}

### Utilizar Views de Terceros

{% embed url="https://android-arsenal.com" %}
Fuente: android arsenal
{% endembed %}

Otra posibilidad es que no queramos utilizar nuestro tiempo en el desarrollo de una **View** específica que sabemos que ya se ha implementado antes por alguien. En este caso, podemos buscar en **Github** la implementación y utilizarla.

#### Encontrar una View válida

Existen infinidad de repositorios de terceros que contienen implementaciones de Custom Views para Android. Sin embargo es muy importante saber elegir entre todas ellas. Para esto, buscamos los siguientes indicadores.

* El repositorio contiene documentación extensa con:
  * Casos de uso y ejemplos visuales
  * Explicación de su uso
  * Atributos
  * Explicación de uso de los Listeners
* El código se encuentra disponible para su análisis.

#### Utilizar la Custom View

Para el ejemplo se va a utilizar la siguiente Custom View:

{% embed url="https://github.com/NitishGadangi/TypeWriter-TextView" %}
Fuente: github
{% endembed %}

Una vez lo tenemos elegido leemos la documentación y encontramos que para utilizar la Custom View tenemos lo siguiente:

> To get a Git project into your build:
>
> **Step 1.** Add the JitPack repository to your build file
>
> Add it in your project level build.gradle at the end of repositories:
>
> ```
> 	allprojects {
> 		repositories {
> 			...
> 			maven { url 'https://jitpack.io' }
> 		}
> 	}
> ```
>
> **Step 2.** Add the dependency to app level build.gradle file
>
> ```
> 	dependencies {
> 	        implementation 'com.github.NitishGadangi:TypeWriter-TextView:v1.3'
> 	}
> ```

O lo que es lo mismo, añadimos el repositorio de maven a `settings.gradle` y después añadimos la dependencia a `build.gradle`.&#x20;

{% hint style="warning" %}
Recuerde darle al botón de **Sync Now** para que los cambios en Gradle surtan efecto.
{% endhint %}

Después de esto tenemos que añadir la View a nuestro archivo de Layout XML:

```xml
<com.nitish.typewriterview.TypeWriterView
    android:id="@+id/typerPrueba"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

Y por último debemos configurar en la View el texto animado a mostrar:

```kotlin
val typerPrueba = findViewById<TypeWriterView>(R.id.typerPrueba)
typerPrueba.animateText("Prueba de texto animado." +
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor " +
        "incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud " +
        "exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute " +
        "irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla " +
        "pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia " +
        "deserunt mollit anim id est laborum.")
```

{% hint style="success" %}
Todo lo anterior se saca facilmente de la documentación de la Custom View, si no fuera el caso, es conveniente buscar otro recurso con mejor documentación.
{% endhint %}

![](<../../../.gitbook/assets/image (25).png>)                               ![](<../../../.gitbook/assets/image (13).png>)  ![](<../../../.gitbook/assets/image (22).png>)                               ![](<../../../.gitbook/assets/image (39).png>)            &#x20;
