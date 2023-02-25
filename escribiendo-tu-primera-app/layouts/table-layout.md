---
description: Explicación del concepto de Table Layout
---

# Table Layout

{% embed url="https://developer.android.com/reference/android/widget/TableLayout" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/guide/topics/ui/layout/grid?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `LinearLayout`.

Un Layout que muestra sus elementos hijos en filas y columnas.

### Estructura

Un TableLayout consiste en un número de objetos del tipo TableRow, cada uno de ellos definiendo una fila.

* Los contenedores de TableLayout no muestran líneas de bordes para las filas, columnas o celdas.
* La tabla tendrá la misma cantidad de columnas que la fila con la mayor cantidad de celdas.
* Una tabla puede dejar celdas vacías. Las celdas pueden abarcar varias columnas, igual que en HTML.
* La anchura de una columna es definida por la fila con la celda más ancha en esa columna.
* Los hijos de un TableLayout no pueden especificar un atributo `layout_width`. Su anchura es siempre `MATCH_PARENT`.
* Sin embargo si que pueden definir `layout_height`.&#x20;
* Las celdas deben ser añadidas a una fila en orden ascendente de columna.
* Los números de las columnas empiezan en 0.
* Si no se define un número de columna para una celda, esta se pondrá automáticamente en la siguiente columna.
* Si se salta una columna, esa celda se tomará como celda vacía en esa fila.

{% hint style="warning" %}
A pesar de que el hijo típico de un **TableLayout** es un **TableRow**, puede utilizar cualquier **subclase de View** como hijo de **TableLayout**.&#x20;

En este caso, ocupará una fila completa.
{% endhint %}

## USO DESDE XML

{% hint style="danger" %}
**IMPORTANTE**

Google recomienda el uso de **Constraint Layout** en exclusiva, sin embargo, se puede dar el caso de que un **Relative Layout** sea más sencillo de implementar y más útil.
{% endhint %}

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".TableLayoutActivity"
    android:padding="16dp">
    <TableRow
        android:background="@color/primary">
        <TextView
            android:layout_column="0"
            android:text="Prueba 1"/>
        <TextView
            android:layout_column="2"
            android:text="Prueba 2"/>
        <TextView
            android:layout_column="4"
            android:text="Prueba 3"/>
    </TableRow>
    <TextView
        android:text="HOLA MUNDO"
        android:background="@color/lightPrimary"/>
    <TableRow
        android:background="@color/primary">
        <TextView
            android:layout_column="1"
            android:text="Prueba 1"/>
        <TextView
            android:layout_column="3"
            android:text="Prueba 2"/>
        <TextView
            android:layout_column="5"
            android:text="Prueba 3"/>
    </TableRow>
</TableLayout>
```
{% endcode %}

&#x20;                                             ![](<../../.gitbook/assets/image (8).png>)

## ATRIBUTOS

### android:layout\_column

Define el índice de la columna en la que va la celda.

### android:collapseColumns

Se debe definir en el padre.

Define el índice de las columnas que se pueden colapsar.

### android:shrinkColumns

Se debe definir en el padre.

Define el índice de las columnas que se pueden achicar.

### android:stretchColumns

Se debe definir en el padre.

Define el índice de las columnas que se pueden extender.

## EJEMPLO

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    android:stretchColumns="1,2,3,4"
    tools:context=".TableLayoutActivity">

    <TableRow android:background="@color/primary">

        <TextView
            android:layout_column="0"
            android:text="Artículo"
            android:textAlignment="center"
            android:textStyle="bold" />

        <TextView
            android:layout_column="1"
            android:text="Cantidad"
            android:textAlignment="center"
            android:textStyle="bold" />

        <TextView
            android:layout_column="2"
            android:text="Precio"
            android:textAlignment="center"
            android:textStyle="bold" />

        <TextView
            android:layout_column="3"
            android:text="IVA"
            android:textAlignment="center"
            android:textStyle="bold" />

        <TextView
            android:layout_column="4"
            android:text="Total"
            android:textAlignment="center"
            android:textStyle="bold" />
    </TableRow>

    <TableRow>

        <TextView
            android:layout_column="0"
            android:text="Peluche Androide" />

        <TextView
            android:layout_column="1"
            android:text="1"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="2"
            android:text="15.67"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="3"
            android:text="21"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="4"
            android:text="15.67"
            android:textAlignment="textEnd" />
    </TableRow>

    <TableRow android:background="@color/lightPrimary">

        <TextView
            android:layout_column="0"
            android:text="Peluche Androide" />

        <TextView
            android:layout_column="1"
            android:text="1"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="2"
            android:text="15.67"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="3"
            android:text="21"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="4"
            android:text="15.67"
            android:textAlignment="textEnd" />
    </TableRow>

    <TableRow>

        <TextView
            android:layout_column="0"
            android:text="Peluche Androide" />

        <TextView
            android:layout_column="1"
            android:text="1"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="2"
            android:text="15.67"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="3"
            android:text="21"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="4"
            android:text="15.67"
            android:textAlignment="textEnd" />
    </TableRow>

    <TableRow android:background="@color/lightPrimary">

        <TextView
            android:layout_column="0"
            android:text="Peluche Androide" />

        <TextView
            android:layout_column="1"
            android:text="1"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="2"
            android:text="15.67"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="3"
            android:text="21"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="4"
            android:text="15.67"
            android:textAlignment="textEnd" />
    </TableRow>

    <TableRow>

        <TextView
            android:layout_column="0"
            android:text="Peluche Androide" />

        <TextView
            android:layout_column="1"
            android:text="1"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="2"
            android:text="15.67"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="3"
            android:text="21"
            android:textAlignment="textEnd" />

        <TextView
            android:layout_column="4"
            android:text="15.67"
            android:textAlignment="textEnd" />
    </TableRow>

    <View
        android:layout_width="match_parent"
        android:layout_height="2dp"
        android:background="@color/divider" />

    <TableRow>

        <TextView
            android:layout_column="2"
            android:background="@color/accent"
            android:text="Total"
            android:textAlignment="textEnd"
            android:textStyle="bold" />

        <TextView
            android:layout_column="3"
            android:background="@color/accent" />

        <TextView
            android:layout_column="4"
            android:background="@color/accent"
            android:text="78,35"
            android:textAlignment="textEnd"
            android:textStyle="bold" />
    </TableRow>
</TableLayout>
```
{% endcode %}

&#x20;                                                 ![](<../../.gitbook/assets/image (15).png>)
