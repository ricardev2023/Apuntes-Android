---
description: Explicación del contenido del directorio res.
---

# Res

{% embed url="https://developer.android.com/guide/topics/resources/providing-resources?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## ¿QUE ES EL DIRECTORIO RES?

El directorio res almacena todos los recursos (resources) que se utilizan en la App. Estos recursos son las imagenes, los colores, los layouts, las strings...

## CONTENIDO

Cuando se crea un Proyecto tendremos una serie de subdirectorios creados en la carpeta. Sin embargo, esto no significa que no se vayan a utilizar más en función de nuestras necesidades.

{% hint style="danger" %}
No se deben guardar archivos de recursos directamente en el directorio res sino en los subdirectorios. Sino se producirá un error de compilación.
{% endhint %}

Según la documentación de Google podemos tener los siguientes subdirectorios:

### animator

Archivos XML donde se definen **animaciones de propiedades**.

El sistema de animación de propiedades es un marco de trabajo robusto que te permite animar casi cualquier cosa. Puedes definir una animación para cambiar cualquier propiedad de un objeto a lo largo del tiempo, más allá de que se renderice en la pantalla o no.

{% embed url="https://developer.android.com/guide/topics/graphics/prop-animation?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### anim

Archivos XML donde se definen **animaciones de vistas**.

Puedes usar el sistema de animación de vista para realizar animaciones interpoladas en vistas. La animación de interpolación calcula la animación con datos como el punto de inicio, el punto de fin, el tamaño, la rotación y otros aspectos comunes de una animación.

Pueden almacenarse también las animaciones de propiedades pero es mejor diferenciarlas en su respectiva carpeta.

{% embed url="https://developer.android.com/guide/topics/graphics/view-animation?hl=es-419#tween-animation" %}
Fuente: developer.android
{% endembed %}

### color

Archivos XML que define una lista del estado de colores.&#x20;

Un `ColorStateList` es un objeto que puedes definir en formato XML y aplicar como color, pero que cambiará de color según el estado del objeto `View` al que se aplique.

{% embed url="https://developer.android.com/guide/topics/resources/color-list-resource?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### drawable

Archivos de mapas de bits o imágenes vectoriales en XML que se utilizan como recursos de elementos de diseño.

Un recurso de elementos de diseño es un concepto general para un gráfico que se puede dibujar en la pantalla y puedes obtener con APIs

{% embed url="https://developer.android.com/guide/topics/resources/drawable-resource?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### mipmap

Archivos de elementos de diseño que varían en función de la resolución del dispositivo.&#x20;

{% embed url="https://developer.android.com/training/multiscreen/screendensities?hl=es-419#mipmap" %}
Fuente: developer.android
{% endembed %}

### layout

Archivos en formato XML que definen el diseño de una interfaz de usuario.

Hay un archivo Layout por cada archivo de Activity en el directorio Java.&#x20;

{% embed url="https://developer.android.com/guide/topics/resources/layout-resource?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### menu

Archivos en formato XML que definen menús de aplicaciones, como un menú de opciones, un menú contextual o un submenú.

{% embed url="https://developer.android.com/guide/topics/resources/menu-resource?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### raw

Archivos que se guardan sin procesar.

### values

Archivos XML que contienen valores simples, como strings, valores enteros y colores.

Los archivos de recursos XML en otros subdirectorios `res/` definen un único recurso basado en el nombre del archivo en formato XML, mientras que los archivos del directorio `values/` describen varios recursos. En el caso de un archivo de este directorio, cada campo secundario del elemento `<resources>` define un único recurso. Por ejemplo, un elemento `<string>` crea un recurso `R.string`, y un elemento `<color>` crea un recurso `R.color`.

A continuación se incluyen algunas convenciones de asignación de nombres de archivos para los recursos que puedes crear en este directorio:

* arrays.xml para arrays de recursos ([arrays escritos](https://developer.android.com/guide/topics/resources/more-resources?hl=es-419#TypedArray))
* colors.xml para [valores de color](https://developer.android.com/guide/topics/resources/more-resources?hl=es-419#Color)
* dimens.xml para [valores de dimensión](https://developer.android.com/guide/topics/resources/more-resources?hl=es-419#Dimension)
* strings.xml para [valores de strings](https://developer.android.com/guide/topics/resources/string-resource?hl=es-419)
* styles.xml para [estilos](https://developer.android.com/guide/topics/resources/style-resource?hl=es-419)

### xml

Archivos en formato XML que se pueden leer en tiempo de ejecución. Aquí se guardan los archivos de configuración como por ejemplo el siguiente:

{% embed url="https://developer.android.com/guide/topics/search/searchable-config?hl=es-419" %}
Fuente: developer.android
{% endembed %}

### font

Archivos de fuentes, con extensiones como `.ttf`, `.otf` o `.ttc`, o archivos en formato XML que incluyan un elemento `<font-family>`.

{% embed url="https://developer.android.com/guide/topics/ui/look-and-feel/fonts-in-xml?hl=es-419" %}
Fuente: developer.android
{% endembed %}

