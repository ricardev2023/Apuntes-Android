---
description: Explicación de los conceptos View y ViewGroup.
---

# Views y ViewGroups

La clase **View** representa el bloque básico de construcción de los elementos visuales de la IU.

La clase **ViewGroup**, por contra, es la clase base de los Layouts que son contenedores invisibles que almacenan otras **Views**.

{% embed url="https://developer.android.com/reference/kotlin/android/view/View" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/reference/kotlin/android/view/ViewGroup" %}
Fuente: developer.android
{% endembed %}

## VIEW

Una View ocupa un area rectangular en la pantalla y es responsable del dibujado de dicho elemento visual así como de la gestión de eventos (por ejemplo onClickListeners).

La clase View es, a su vez, la clase base para todos los componentes interactivos de la IU (botones, textos, campos de texto...)

### Utilizar Views <a href="#using-views" id="using-views"></a>

Todas las Views en una ventana están estructuradas en un único arbol.&#x20;

Se pueden añadir views directamente desde código o añadiendolas al arbol de Views en un [archivo de layout XML](../anatomia-del-proyecto/res.md#layout) (que es la forma preferida de hacerlo).

Hay muchas subclases de Views que actuan como controladores o son capaces de mostrar texto, imágenes u otro contenido.

Una vez creado un arbol de Views, hay algunas operaciones a realizar:

* **Definir propiedades**: Por ejemplo, en un TextView, definir el texto a mostrar. Existen muchas propiedades diferentes en función de la subclase de view a utilizar.
* **Definir el foco**: El foco, o la atención, de la aplicación se gestiona de manera automática en base al input del usuario. Sin embargo se puede forzar el foco en una View concreta llamando a `requestFocus`.
* **Definir listeners**: Los listeners permiten modificar la View cuando una situación concreta se da en dicha View. Por ejemplo, un `onClickListener` reaccionará cuando se clique sobre la View.
* **Definir visibilidad**: Se pueden mostrar u ocultar las Views utilizando `setVisibility()`.

### Implementar una View Customizada <a href="#implementing-a-custom-view" id="implementing-a-custom-view"></a>

Se pueden implementar Views customizadas que pueden ser creadas por uno mismo o por terceros.

Para implementarlas, usualmente se sobreescribiran méodos estandar que el Framework utiliza en todas las vistas. Sin embargo, no es necesario sobreescribirlos todos, con sobreescribir onDraw(android.graphics.Canvas) es suficiente.

{% hint style="danger" %}
En la documentación de Android se entra en profundidad en la implementación de Views. Esto se sale del Scope de ésta página, pero se encuentra en el [enlace](https://developer.android.com/reference/kotlin/android/view/View).
{% endhint %}

## VIEWGROUP

Un ViewGroup es una View especial que contiene otras Views llamadas hijos. Es la clase base de los Layouts y los contenedores de Views.&#x20;

### LayoutParams

La clase ViewGroup tambien define la clase `android.view.ViewGroup.LayoutParams` que sirve como clase base para los parámetros del Layout.

Esta clase describe cuanto de grande va a ser la View tanto de ancho como de alto. Para ambas dimensiones puede ser uno de los siguientes valores:

* MATCH\_PARENT -> La View será tan grande como su padre (menos el Padding).
* WRAP\_CONTENT -> La View será tan grande como sea necesario para el contenido de la misma (más el Padding)
* Un número exacto.

Existen subclases de LayoutParams para las diferentes subclases de ViewGroup. Por ejemplo, no son los mismos parámetros para AbsoluteLayout que RelativeLayout.
