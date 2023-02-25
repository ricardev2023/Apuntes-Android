---
description: Explicación del concepto de Relative Layout
---

# Relative Layout

{% embed url="https://developer.android.com/guide/topics/ui/layout/relative?hl=es-419" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/reference/android/widget/RelativeLayout" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `ViewGroup`.

**RelativeLayout** es un grupo de vistas que muestra vistas secundarias en posiciones relativas. La posición de cada vista puede especificarse como relativa a elementos del mismo nivel (como a la izquierda de otra vista o por debajo de ella) o en posiciones relativas al área **`RelativeLayout`** superior (como alineada a la parte inferior, izquierda o central).

## USO DESDE XML

{% hint style="danger" %}
**IMPORTANTE**

Google recomienda el uso de **Constraint Layout** en exclusiva, sin embargo, se puede dar el caso de que un **Relative Layout** sea más sencillo de implementar y más útil.
{% endhint %}

Si utilizamos un Relative Layout sin darle ninguna posición relativa a los elementos que se encuentran en su interior, se alinearán todos en la esquina superior izquierda.&#x20;

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".RelativeLayoutActivity">
    <View
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/teal_700"/>
    <View
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/teal_200"/>
</RelativeLayout>
```
{% endcode %}

&#x20;                                             ![](<../../.gitbook/assets/image (4).png>)

## ATRIBUTOS

{% embed url="https://developer.android.com/reference/android/widget/RelativeLayout.LayoutParams" %}
Fuente: developer.android
{% endembed %}

Los atributos más importantes de un Relative Layout son los que se muestran en el enlace superior. Estos son los atributos de la clase **RelativeLayout.LayoutParams** y son fundamentales para indicar donde se posicionan las **Views** dentro del **Layout**.

{% hint style="info" %}
Las tarjetas están copiada y traducida del enlace.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><code>android:layout_above</code></td><td><p>Posiciona la View con su borde inferior sobre el borde superior de la View referenciada.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_alignBaseline</code></td><td><p>Posiciona la View con su <a href="linear-layout.md#atributos">Baseline</a> a la altura de la Baseline de la View referenciada.</p><p><strong>Solo funciona con TextViews.</strong></p></td></tr><tr><td><code>android:layout_alignBottom</code></td><td><p>Posiciona la View con su borde inferior alineado con el borde inferior de la View referenciada.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_alignEnd</code></td><td><p>Posiciona la View con su borde final alineado con el borde final de la View referenciada.</p><p><strong>En nuestra escritura es el derecho pero en otros casos como el hebreo puede ser el izquierdo.</strong><br><strong>Esto lo hace en el eje X, no en el Y.</strong></p></td></tr><tr><td><code>android:layout_alignLeft</code></td><td><p>Posiciona la View con su borde izquierdo alineado con el borde izquierdo de la View referenciada.</p><p> <strong>Esto lo hace en el eje X, no en el Y.</strong></p></td></tr><tr><td><code>android:layout_alignParentBottom</code></td><td><p>Si es <strong>true</strong>, posiciona la View con su borde inferior alineado con el borde inferior del padre.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_alignParentEnd</code></td><td><p>Si es <strong>true</strong>, posiciona la View con su borde final alineado con el borde final del padre.</p><p><strong>En nuestra escritura es el derecho pero en otros casos como el hebreo puede ser el izquierdo.</strong></p><p><strong>Esto lo hace en el eje X, no en el Y.</strong></p></td></tr><tr><td><code>android:layout_alignParentLeft</code></td><td><p>Si es <strong>true</strong>, posiciona la View con su borde izquierdo alineado con el borde izquierdo del padre.</p><p><strong>Esto lo hace en el eje X, no en el Y.</strong></p></td></tr><tr><td><code>android:layout_alignParentRight</code></td><td>Si es <strong>true</strong>, posiciona la View con su borde derecho alineado con el borde derecho del padre.<br><strong>Esto lo hace en el eje X, no en el Y.</strong></td></tr><tr><td><code>android:layout_alignParentStart</code></td><td><p>Si es <strong>true</strong>, posiciona la View con su borde inicial alineado con el borde inicial del padre.</p><p><strong>En nuestra escritura es el izquierdo pero en otros casos como el hebreo puede ser el derecho.</strong></p><p><strong>Esto lo hace en el eje X, no en el Y.</strong> </p></td></tr><tr><td><code>android:layout_alignParentTop</code></td><td><p>Si es <strong>true</strong>, posiciona la View con su borde superior alineado con el borde superior del padre.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_alignRight</code></td><td><p>Posiciona la View con su borde derecho alineado con el borde derecho de la View referenciada.</p><p><strong>Esto lo hace en el eje X, no en el Y.</strong> </p></td></tr><tr><td><code>android:layout_alignStart</code></td><td><p>Posiciona la View con su borde inicial alineado con el borde inicial de la View referenciada.</p><p><strong>En nuestra escritura es el izquierdo pero en otros casos como el hebreo puede ser el derecho.</strong></p><p><strong>Esto lo hace en el eje X, no en el Y.</strong> </p></td></tr><tr><td><code>android:layout_alignTop</code></td><td><p>Posiciona la View con su borde superior sobre el borde superior de la View referenciada.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_alignWithParentIfMissing</code></td><td>Si es true, el padre es utilizado como referencia si la referencia no se puede encontrar.</td></tr><tr><td><code>android:layout_below</code></td><td><p>Posiciona la View con su borde superior bajo el borde inferior de la View referenciada.</p><p><strong>Esto lo hace en el eje Y, no en el X.</strong></p></td></tr><tr><td><code>android:layout_centerHorizontal</code></td><td>Si es <strong>true</strong>, se centra la View en el <strong>eje X</strong> respecto del padre.</td></tr><tr><td><code>android:layout_centerInParent</code></td><td>Si es <strong>true</strong>, se centra la View tanto en el <strong>eje X como en el eje Y</strong> respecto del padre.</td></tr><tr><td><code>android:layout_centerVertical</code></td><td>Si es <strong>true</strong>, se centra la View en el <strong>eje Y</strong> respecto del padre.</td></tr><tr><td><code>android:layout_toEndOf</code></td><td>Posiciona la View con su borde inicial junto a el borde final de la View referenciada.<br><strong>Esto lo hace en el eje X, no en el Y.</strong></td></tr><tr><td><code>android:layout_toLeftOf</code></td><td><p>Posiciona la View con su borde derecho junto a el borde izquierdo de la View referenciada.</p><p><strong>Esto lo hace en el eje X, no en el Y.</strong></p></td></tr><tr><td><code>android:layout_toRightOf</code></td><td><p>Posiciona la View con su borde izquierdo junto a el borde derecho de la View referenciada.</p><p><strong>Esto lo hace en el eje X, no en el Y.</strong> </p></td></tr><tr><td><code>android:layout_toStartOf</code></td><td><p>Posiciona la View con su borde final junto a el borde inicial de la View referenciada.</p><p><strong>Esto lo hace en el eje X, no en el Y.</strong> </p><p></p></td></tr></tbody></table>

## EJEMPLO

Vamos a utilizar **Relative Layout** para crear un **Layout** de una App con **Views básicas.**

<figure><img src="../../.gitbook/assets/Galaxy S10 (1).png" alt=""><figcaption><p>Layout creado con Lunacy</p></figcaption></figure>

Como vemos en la imagen de arriba, la App tiene una paleta de colores con tres colores principales que vamos a llamar:

* primary
* light\_primary
* dark\_primary

La imagen es una muestra aproximada de como debe quedar el Layout, sin embargo, es muy dificil que quede exactamente así ya que con **Relative Layout no se pueden utilizar los Weights como se ha hecho en Linear Layout.**

El archivo de Layout queda como sigue:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".RelativeLayoutActivity">
    <View
        android:id="@+id/vA"
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:background="@color/primary"
        android:layout_alignParentTop="true"
        android:layout_marginBottom="10dp"/>
    <View
        android:id="@+id/vB"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@color/dark_primary"
        android:layout_below="@id/vA"
        android:layout_marginEnd="10dp"
        android:layout_marginBottom="10dp"/>
    <View
        android:id="@+id/vC"
        android:layout_width="300dp"
        android:layout_height="100dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vA"
        android:layout_toRightOf="@+id/vB"
        android:layout_marginBottom="10dp"/>
    <View
        android:id="@+id/vD"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_marginBottom="10dp"
        android:layout_marginEnd="10dp"/>
    <View
        android:id="@+id/vE"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_toRightOf="@id/vD"
        android:layout_marginBottom="10dp"
        android:layout_marginEnd="10dp"/>
    <View
        android:id="@+id/vF"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_toRightOf="@id/vE"
        android:layout_marginBottom="10dp"
        android:layout_marginEnd="10dp"/>
    <View
        android:id="@+id/vG"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_toRightOf="@id/vF"
        android:layout_marginBottom="10dp"
        android:layout_marginEnd="10dp"/>
    <View
        android:id="@+id/vH"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_toRightOf="@id/vG"
        android:layout_marginBottom="10dp"
        android:layout_marginEnd="10dp"/>
    <View
        android:id="@+id/vI"
        android:layout_width="60dp"
        android:layout_height="250dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vB"
        android:layout_toRightOf="@id/vH"
        android:layout_marginBottom="10dp" />
    <View
        android:id="@+id/vJ"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:background="@color/dark_primary"

        android:layout_below="@id/vD"/>
    <View
        android:id="@+id/vK"
        android:layout_width="110dp"
        android:layout_height="180dp"
        android:background="@color/light_primary"
        android:layout_below="@id/vJ"/>
    <View
        android:id="@+id/vL"
        android:layout_width="300dp"
        android:layout_height="89dp"
        android:background="@color/primary"
        android:layout_below="@id/vJ"
        android:layout_toRightOf="@id/vK"/>

    <View
        android:id="@+id/vM"
        android:layout_width="300dp"
        android:layout_height="89dp"
        android:layout_below="@id/vL"
        android:layout_toRightOf="@id/vK"
        android:background="@color/dark_primary" />

</RelativeLayout>
```
{% endcode %}

{% hint style="danger" %}
Vamos a ver cómo, con **Relative Layout**, no podemos conseguir el **Responsive Design** que sí que se consigue con **Linear Layout** y con **Constraint Layout** como veremos en la siguiente página.
{% endhint %}

&#x20;                                              ![](<../../.gitbook/assets/image (38).png>)

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>
