---
description: Explicación del concepto de Grid Layout
---

# Grid Layout

{% embed url="https://developer.android.com/reference/android/widget/GridLayout" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `ViewGroup`.

Un Layout que coloca sus hijos en un enrejillado rectangular (como unas coordenadas).

### Estructura

El enrejillado está compuesto por un conjunto de lineas de una anchura infinitesimal que separa la zona que ocupa el Layout en diferentes celdas.

Las líneas del enrejillado se llaman **índices** y en un enrejillado con **N** columnas, tendremos **N + 1** índices, **desde 0 hasta N**.

#### Especificación de filas y columnas

Un hijo ocupa una o más celdas contiguas, esto se define con los atributos `rowSpec` y `columnSpec`.&#x20;

Cada uno de estos atributos define cuantas filas y columnas va a ocupar un hijo.

{% hint style="info" %}
**IMPORTANTE**

Aunque en un Grid Layout no se espera que las celdas que ocupa una View las pueda ocupar otra, Android Studio no impide que esto ocurra. Esto es un error de diseño y puede afectar de manera indeterminada al resultado final.
{% endhint %}

#### Asignación de celda por defecto

Si a un hijo no se le asignan los índices de fila y una columna, GridLayout asignará una localización por defecto teniendo en cuenta sus atributos `orientation`, `rowCount` and `columnCount`&#x20;

#### **Espacio**

El espacio entre hijos tendrá que ser especificado utilizando márgenes con los parámetros: `leftMargin`, `topMargin`, `rightMargin` and `bottomMargin`.

Cuando la propiedad `useDefaultMargins` está definida, se colocarán los márgenes por defecto alrededor de los hijos, basado en la guía de estilo de UI que se esté utilizando.

#### Distribución del espacio sobrante

Desde API 21, el exceso de espacio se gestiona con el principio del **peso**.

En caso de que no se hayan especificado pesos, se respetarán las convenciones anteriores.

#### **Interpretación de GONE**

Para el propósito del Layout, se tratan las Views cuya visibilidad es GONE como si tuvieran cero anchura y altura.&#x20;

Esto difiere de la política de ignorar las Views marcadas como GONE pero es necesario para el buen funcionamiento de este Layout.

## USO DESDE XML

{% hint style="danger" %}
**IMPORTANTE**

Google recomienda el uso de **Constraint Layout** en exclusiva, sin embargo, se puede dar el caso de que un **Relative Layout** sea más sencillo de implementar y más útil.
{% endhint %}

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<GridLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".GridLayoutActivity"
    android:layout_rowWeight="5"
    android:layout_columnWeight="4">
</GridLayout>
```
{% endcode %}

## ATRIBUTOS

### android:alignmentMode

Define el modo de alineamiento entre, alienar limites de los hijos o alienar márgenes.

### android:columnCount

El número máximo de columnas que se pueden crear automáticamente al crear hijos.

### android:columnOrderPreserved

Cuando está marcado como true, fuerza los límites de las columnas en el mismo orden que los índices.

### android:orientation

No se utiliza durante el **Layout**, solo para definir los parámetros de filas y columnas cuando estas no se definen en los atributos.

### android:rowCount

El número máximo de filas que se pueden crear automáticamente al crear hijos.

### android:rowOrderPreserved

Cuando está marcado como true, fuerza los límites de las filas en el mismo orden que los índices.

### android:useDefaultMargins

Indica que se debe utilizar los márgenes por defecto cuando no se indican en los atributos.

### android:layout\_column

Indica en que columna se va a empezar a pintar la View.&#x20;

Las columnas se empiezan a contar desde arriba.

### android:layout\_columnSpan

Indica el número de celdas que ocupa una View de izquierda a derecha.

### android:layout\_columnWeight

La proporción relativa de espacio horizontal que se debe dar a una View cuando se reparta el espacio excesivo.

### android:layout\_gravity

Define como se deben colocar los componentes dentro de su grupo.

### android:layout\_row

Indica en que fila se va a empezar a pintar la View.&#x20;

Las filas se empiezan a contar desde arriba.

### android:layout\_rowSpan

Indica el número de celdas que ocupa una View de arriba a abajo.

### android:layout\_rowWeight

La proporción relativa de espacio vertical que se debe dar a una View cuando se reparta el espacio excesivo.

## EJEMPLO

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<GridLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".GridLayoutActivity"
    android:layout_rowWeight="5"
    android:layout_columnWeight="4">
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="0"
        android:layout_column="0"
        android:layout_rowWeight="1"
        android:layout_columnWeight="1"
        android:layout_rowSpan="1"
        android:layout_columnSpan="1"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="0"
        android:layout_column="1"
        android:layout_rowWeight="1"
        android:layout_columnWeight="1"
        android:layout_rowSpan="1"
        android:layout_columnSpan="1"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="0"
        android:layout_column="2"
        android:layout_rowWeight="1"
        android:layout_columnWeight="1"
        android:layout_rowSpan="1"
        android:layout_columnSpan="1"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="0"
        android:layout_column="3"
        android:layout_rowWeight="2"
        android:layout_columnWeight="1"
        android:layout_rowSpan="2"
        android:layout_columnSpan="1"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="1"
        android:layout_column="0"
        android:layout_rowWeight="1"
        android:layout_columnWeight="3"
        android:layout_rowSpan="1"
        android:layout_columnSpan="3"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="2"
        android:layout_column="0"
        android:layout_rowWeight="2"
        android:layout_columnWeight="1"
        android:layout_rowSpan="3"
        android:layout_columnSpan="1"
        />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="2"
        android:layout_column="1"
        android:layout_rowWeight="1"
        android:layout_columnWeight="3"
        android:layout_rowSpan="1"
        android:layout_columnSpan="3"
        />
    <View
    android:background="@color/primary"
    android:layout_margin="1dp"
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:layout_row="3"
    android:layout_column="1"
    android:layout_rowWeight="1"
    android:layout_columnWeight="3"
    android:layout_rowSpan="1"
    android:layout_columnSpan="3"
    />
    <View
        android:background="@color/primary"
        android:layout_margin="1dp"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_row="4"
        android:layout_column="1"
        android:layout_rowWeight="1"
        android:layout_columnWeight="3"
        android:layout_rowSpan="1"
        android:layout_columnSpan="3"
        />
</GridLayout>
```
{% endcode %}

&#x20;                                                 ![](<../../.gitbook/assets/image (20).png>)

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
