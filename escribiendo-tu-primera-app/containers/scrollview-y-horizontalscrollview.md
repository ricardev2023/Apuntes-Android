---
description: Explicación de los conceptos de ScrollView y HorizontalScrollView
---

# ScrollView y HorizontalScrollView

## DEFINICIÓN

### ScrollView

{% embed url="https://developer.android.com/reference/android/widget/ScrollView" %}
Fuente: developer.android
{% endembed %}

Hereda de `FrameLayout`.

Es un ViewGroup que permite que el Layout que se encuentra en su interior pueda ser scroleable.

Es recomendable que ScrollView tenga solo un hijo dentro debido a que es un `FrameLayout`.&#x20;

Si es necesario introducir más de una View en su interior, entonces tendrá que añadir un **ViewGroup** en su interior para que se cumpla que solo tiene un único hijo directo.

Solo soporta scroll vertical.

### HorizontalScrollView

{% embed url="https://developer.android.com/reference/android/widget/HorizontalScrollView" %}
Fuente: developer.android
{% endembed %}

Hereda de `FrameLayout`.

Es un ViewGroup que permite que el Layout que se encuentra en su interior pueda ser scroleable.

Es recomendable que ScrollView tenga solo un hijo dentro debido a que es un `FrameLayout`.&#x20;

Si es necesario introducir más de una View en su interior, entonces tendrá que añadir un **ViewGroup** en su interior para que se cumpla que solo tiene un único hijo directo.

Solo soporta scroll horizontal.

### NestedScrollView

{% embed url="https://developer.android.com/reference/androidx/core/widget/NestedScrollView.html" %}
Fuente: developer.android
{% endembed %}

Hereda de `FrameLayout`.

Es un ScrollView más moderno que puede funcionar tanto de padre como de hijo de otro ViewGroup.

Solo soporta scroll vertical.

{% hint style="success" %}
**RECOMENDACIÓN**

Es recomendable utilizar `NestedScrollView` siempre que se necesite un Scroll Vertical ya que es más configurable por el usuario y soporta las necesidades de **Material Design** en cuanto a Scrolling.
{% endhint %}

## EJEMPLO

Ya se han utilizado ScrollViews en diferentes ejemplos de esta guía así que vamos a coger uno para verlo:

### ScrollView

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/im_pyramidhead" />

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/shapeable_image"/>

    </LinearLayout>


</ScrollView>
```

<figure><img src="../../.gitbook/assets/scrollview-video.gif" alt=""><figcaption><p>ScrollView</p></figcaption></figure>

### HorizontalScrollView

```
<?xml version="1.0" encoding="utf-8"?>
<HorizontalScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="horizontal">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/im_pyramidhead" />

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:src="@drawable/shapeable_image"/>

    </LinearLayout>


</HorizontalScrollView>
```

<figure><img src="../../.gitbook/assets/horizontalscrollview-video.gif" alt=""><figcaption><p>HorizontalScrollView</p></figcaption></figure>
