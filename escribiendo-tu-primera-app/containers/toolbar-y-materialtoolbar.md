---
description: Explicación del concepto de Toolbar y MaterialToolbar
---

# Toolbar y MaterialToolbar

## DEFINICIÓN

### Toolbar

{% embed url="https://developer.android.com/reference/androidx/appcompat/widget/Toolbar" %}
Fuente: developer.android
{% endembed %}

Hereda de `ViewGroup`.

Una Toolbar estandar para su uso como parte del contenido de la App.

Una Toolbar es una generalización de una Action Bar que puede ser utilizada dentro del Layout de la App.

{% hint style="info" %}
**ACTION BAR VS TOOLBAR**

Mientras que las `ActionBar` son tradicionalmente parte de la ventana decorativa de una `Activity` y son controladas por el **Framework**, una `Toolbar` puede ponerse en cualquier nivel de anidamiento dentro de la **jerarquía de Views**.

Una aplicación puede decidir **utilizar una `Toolbar` como `ActionBar`** utilizando el método `setSupportActionBar()`.
{% endhint %}

Una Toolbar además está orientada a soportar un set de elementos muy concretos que, de inicio a fin (izquierda a derecha en paises latinos) son:

* **Un botón de Navegación ->** Puede ser una flecha arriba, un botón de menú, cerrar, colapsar, hecho o cualquier otro icono de la elección de la App. Este botón debe ser utilizado siempre para acceder a otros destinos de navegación dentro de la App.
* **Un logo de marca ->** Puede ser de alto como la barra y todo lo ancho que se quiera.
* **Un título y un subtítulo ->** El título debe indicar en que parte de la App nos encontramos. El subtítulo dará más información al respecto.
* **Una o más Custom Views ->** Se pueden añadir algunas Views propias de la App como iconos.
* **Un Action Menu ->** Se colocará siempre al final de la Toolbar ofreciendo algunas de las acciones más típicas en la App con un overflow menu.&#x20;

{% hint style="success" %}
RECOMENDACIÓN

Desde API 21 se recomienda no utilizar el logo de la App sino decantarse hacia un esquema de colores visualmente sugerente.
{% endhint %}

### MaterialToolbar

{% embed url="https://developer.android.com/reference/com/google/android/material/appbar/MaterialToolbar" %}
Fuente: developer.android
{% endembed %}

Hereda de `Toolbar`.

Es una Toolbar que implementa algunas de las características de Material, tales como títulos centrados u Overlays para los temas oscuros.

## EJEMPLO

En los ejemplos anteriores ya se ha visto el uso de estas Toolbars como parte del `AppBarLayout`.

Básicamente, la `Toolbar` es el contenedor físico de los elementos que hemos hablado antes pero el AppBarLayout es el que le da funcionalidad a esos elementos.&#x20;

Si no existe un `AppBarLayout`, se debe dar funcionalidad a todos los elementos de la Toolbar por separado.

El ejemplo más claro es el que hemos visto en la entrada anterior, de NavigationView.

{% content-ref url="navigationview-y-bottomnavigationview.md" %}
[navigationview-y-bottomnavigationview.md](navigationview-y-bottomnavigationview.md)
{% endcontent-ref %}
