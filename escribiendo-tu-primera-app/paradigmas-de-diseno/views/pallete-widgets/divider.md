---
description: Explicación del concepto de Divider.
---

# Divider

{% embed url="https://developer.android.com/reference/com/google/android/material/divider/MaterialDivider" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://m2.material.io/components/dividers" %}
Fuente: material design
{% endembed %}

## DEFINICIÓN

Un `divider` es un `View` normal y corriente con unas características concretas que lo definen como `divider`.&#x20;

En la actualidad, se utilizan los `MaterialDividers` en vez de los `Dividers` normales pero en la Pallete Widgets el que aparece es el normal.

Existen dos tipos:

* **Divider Horizontal**
* **Divider Vertical**

## USO DESDE XML

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:layout_margin="15dp">

        <View
            android:id="@+id/divider"
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="?android:attr/listDivider" />
        <View
            android:id="@+id/divider2"
            android:layout_width="5dp"
            android:layout_height="260dp"
            android:background="?android:attr/listDivider" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="PRUEBA 1"/>
        <View
            android:id="@+id/divider3"
            android:layout_width="5dp"
            android:layout_height="260dp"
            android:background="?android:attr/listDivider" />
        <View
            android:id="@+id/divider4"
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="?android:attr/listDivider" />
    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                         ![](<../../../../.gitbook/assets/image (33).png>)

{% hint style="info" %}
Para saber más vea los enlaces de la parte superior de la página.
{% endhint %}
