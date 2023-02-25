---
description: Explicación del concepto de Linear Layout
---

# Linear Layout

## DEFINICIÓN

{% embed url="https://developer.android.com/guide/topics/ui/layout/linear?hl=es-419" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/reference/kotlin/android/widget/LinearLayout" %}
Fuente: developer.android
{% endembed %}

Hereda de `ViewGroup`.

**LinearLayout** es un grupo de vistas que alinea todos los elementos secundarios en una única dirección, de manera vertical u horizontal.

## USO DESDE XML

Este Layout ya lo hemos utilizado en múltiples ocasiones en los ejemplos anteriores.

{% hint style="danger" %}
IMPORTANTE

Google recomienda el uso de **Constraint Layout** en exclusiva, sin embargo, se puede dar el caso de que un **Linear Layout** sea más sencillo de implementar y más útil.
{% endhint %}

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    
</LinearLayout>
```
{% endcode %}

## ATRIBUTOS

{% hint style="info" %}
**DEFINICIÓN DE BASELINE**

Baseline es un término que proviene de la tipografía y es la línea imaginaria sobre la que se apoyan las letras.&#x20;

Por tanto, es un término que sólo se puede aplicar a **TextViews**.
{% endhint %}

### android:baselineAligned

Cuando su valor es `false`, previene los hijos de alinear su Baseline.

### android:baselineAlignedChildIndex

Cuando un Linear Layout es parte de otro Layout que si que está alineado, se puede especificar con cual de sus TextView hijos alinearse.

### android:gravity

Define como se tiene que posicionar el contenido de un objeto dentro de sus límites.

### android:measureWithLargestChild

Cuando su valor es `true`, se considera a todos los hijos que tienen un peso (weight) como que su tamaño es el menor del hijo más grande.

### android:orientation

Define si los elementos se estructurarán en una fila (`horizontal`) o en una columna (`vertical`).

### android:weightSum

Define el valor máximo de suma de pesos.

## EJEMPLO

A continuación se va a mostrar un ejemplo de Linear Layout vertical y horizontal combinados.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <View
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:background="@color/purple_200"
        android:layout_marginBottom="5dp"/>
    <View
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:background="@color/purple"
        android:layout_marginBottom="5dp"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:orientation="horizontal">
        <View
            android:layout_width="200dp"
            android:layout_height="match_parent"
            android:background="@color/blue"
            android:layout_marginEnd="5dp"/>
        <View
            android:layout_width="100dp"
            android:layout_height="match_parent"
            android:background="@color/blue_light"
            android:layout_marginEnd="5dp"/>
    </LinearLayout>
    <View
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:background="@color/purple_200"
        android:layout_marginBottom="5dp"/>
    <View
        android:layout_width="200dp"
        android:layout_height="50dp"
        android:background="@color/purple"
        android:layout_marginBottom="5dp"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:orientation="horizontal"
        android:weightSum="3">
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/teal_200"
            android:layout_marginEnd="5dp"
            android:layout_weight="2"/>
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/teal_700"
            android:layout_marginEnd="5dp"
            android:layout_weight="1"/>
    </LinearLayout>

</LinearLayout>
```
{% endcode %}

{% hint style="info" %}
Se va a mostrar tanto en formato vertical como en horizontal para introducir el concepto de **Responsive Design** en el siguiente apartado.
{% endhint %}

&#x20;                                               ![](<../../.gitbook/assets/image (43).png>)                                     &#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Como vemos, hay una serie de elementos que se agrandan hasta ocupar el espacio total mientras que otros no. Incluso hay algunos que desaparecen al colocar el móvil en modo horizontal.

## RESPONSIVE DESIGN

{% embed url="https://developer.android.com/guide/topics/large-screens/migrate-to-responsive-layouts?hl=es-419" %}
Fuente: developer.android
{% endembed %}

El diseño responsivo se basa en que con un solo diseño se pueda presentar el mismo Layout en diferentes dispositivos de la manera correcta.

Con Linear Layout se puede aplicar una pequeña parte de estos diseños responsivos utilizando el atributo `android:weightSum`.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:weightSum="8">
    <View
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:background="@color/purple_200"
        android:layout_marginBottom="5dp"
        android:layout_weight="1"/>
    <View
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:background="@color/purple"
        android:layout_marginBottom="5dp"
        android:layout_weight="1"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:orientation="horizontal"
        android:layout_weight="2"
        android:weightSum="4">
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/blue"
            android:layout_marginEnd="5dp"
            android:layout_weight="2"/>
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/blue_light"
            android:layout_marginEnd="5dp"
            android:layout_weight="1"/>
    </LinearLayout>
    <View
        android:layout_width="100dp"
        android:layout_height="0dp"
        android:background="@color/purple_200"
        android:layout_marginBottom="5dp"
        android:layout_weight="1"/>
    <View
        android:layout_width="200dp"
        android:layout_height="0dp"
        android:background="@color/purple"
        android:layout_marginBottom="5dp"
        android:layout_weight="1"/>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:orientation="horizontal"
        android:weightSum="3"
        android:layout_weight="1">
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/teal_200"
            android:layout_marginEnd="5dp"
            android:layout_weight="2"/>
        <View
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:background="@color/teal_700"
            android:layout_marginEnd="5dp"
            android:layout_weight="1"/>
    </LinearLayout>
</LinearLayout>
```
{% endcode %}

&#x20;                                               ![](<../../.gitbook/assets/image (3).png>)

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Como podemos ver, en este caso si que se ven todos los elementos con las mismas proporciones se coloque como se coloque el dispositivo.
