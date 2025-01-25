---
description: Explicación del concepto de CardView
---

# CardView

{% embed url="https://developer.android.com/reference/androidx/cardview/widget/CardView" %}

{% embed url="https://developer.android.com/guide/topics/ui/layout/cardview?hl=es-419" %}

## DEFINICIÓN

Hereda de `FrameLayout`.

Es un **FrameLayout** pero con las esquinas redondeadas, bordes y sombras paralelas.

## USO DESDE XML

Al ser un Container, debe envolver al Layout que se quiere contener dentro de la Tarjeta:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginHorizontal="10dp"
    android:layout_marginVertical="8dp">
    
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        xmlns:app="http://schemas.android.com/apk/res-auto">

        <TextView
            android:id="@+id/tvPrueba1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:padding="15dp"
            tools:text="prueba 1"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"/>
        
    </androidx.constraintlayout.widget.ConstraintLayout>
</androidx.cardview.widget.CardView>
```

## ATRIBUTOS

### app:cardBackgroundColor

Define el color de fondo de la tarjeta.

### app:cardCornerRadius

Define el radio de las esquinas de la tarjeta.

### app:cardElevation

Define la elevación de la tarjeta, lo que a su vez, define la longitud de las sombras.

Es una opción de retrocompatibilidad, antes de Lollipop.

### app:cardMaxElevation

Define la elevación máxima de la tarjeta.

Es una opción de retrocompatibilidad, antes de Lollipop. Después no tiene efecto.

### app:cardPreventCornerOverlap

Previene que el contenido se pegue con las esquinas.

Es una opción de retrocompatibilidad, antes de Lollipop.

### app:cardUseCompatPadding

La tarjeta utiliza más Padding para pintar las sombras.

Es una opción de retrocompatibilidad, antes de Lollipop.

## EJEMPLO

Siguiendo el ejemplo del `RecyclerView` anterior, podemos sustituir los `dividers` que separaban los diferentes items por `CardViews` que dan una imagen más profesional:

```xml
<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_marginHorizontal="10dp"
    android:layout_marginVertical="8dp">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        xmlns:app="http://schemas.android.com/apk/res-auto">

        <ImageView
            android:id="@+id/ivPhoto"
            android:layout_width="150dp"
            android:layout_height="150dp"
            android:layout_margin="5dp"
            tools:background="@color/black"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"/>
        <TextView
            android:id="@+id/tvName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="25sp"
            android:textStyle="bold"
            android:padding="5dp"
            tools:text="James Sunderland"
            app:layout_constraintStart_toEndOf="@+id/ivPhoto"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintEnd_toEndOf="parent"/>

        <TextView
            android:id="@+id/tvGame"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            tools:text="Silent Hill 2"
            app:layout_constraintTop_toBottomOf="@+id/tvName"
            app:layout_constraintStart_toEndOf="@id/ivPhoto"
            app:layout_constraintEnd_toEndOf="parent"
            />
        <TextView
            android:id="@+id/tvGender"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:padding="15dp"
            tools:text="Female"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"/>

    </androidx.constraintlayout.widget.ConstraintLayout>
</androidx.cardview.widget.CardView>
```

<figure><img src="../../.gitbook/assets/cardview-video.gif" alt=""><figcaption><p>Resultado</p></figcaption></figure>
