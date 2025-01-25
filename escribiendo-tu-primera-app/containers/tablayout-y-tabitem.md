---
description: Explicación de los conceptos de TabLayout y TabItem.
---

# TabLayout y TabItem

## DEFINICIÓN

### TabLayout

{% embed url="https://developer.android.com/reference/com/google/android/material/tabs/TabLayout" %}
Fuente: developer.android
{% endembed %}

Hereda de `HorizontalScrollView`.

TabLayout provee un layout horizontal para mostrar pestañas.

Para crear las pestañas que se van a mostrar se hace con instancias `TabLayout.Tab`.  Se crean las nuevas pestañas con `NewTab()`.

Una vez creadas se puede cambiar la etiqueta o el icono con `TabLayout.Tab.setText(int)` y `TabLayout.Tab.setIcon(int)` respectivamente.

Para mostrar las pestañas se deben añadir al Layout utilizando alguno de los métodos `addTab(Tab)`.

TabLayout provides a horizontal layout to display tabs.

### TabItem

{% embed url="https://developer.android.com/reference/com/google/android/material/tabs/TabItem" %}
Fuente: developer.android
{% endembed %}

Hereda de `View`.

Un TabItem es una View especial que permite declarar pestañas para un TabLayout desde el archivo de Layout.

Esta View no se incluye al TabLayout sino que es un Dummy que permite definir el número de pestañas, el texto o el icono.

## INTEGRACIÓN

### ViewPager2

{% embed url="https://developer.android.com/guide/navigation/navigation-swipe-view-2?hl=es-419" %}
Fuente: developer.android
{% endembed %}

La integración con ViewPager2 es directa y muy sencilla.

Se va a utilizar como ejemplo el proyecto de la entrada de ViewPager2:

{% content-ref url="viewpager2.md" %}
[viewpager2.md](viewpager2.md)
{% endcontent-ref %}

#### Añadir un TabLayout al Layout

Lo primero que debemos hacer es añadir un TabLayout sobre el ViewPager2 como se ve en el siguiente ejemplo:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tlPrueba"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/pager"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/tlPrueba" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
{% endcode %}

#### TabLayoutMediator

Después se configura el `TabLayoutMediator` para que exista relación entre el `TabLayout` y el `ViewPager2`:

```kotlin
TabLayoutMediator(binding.tlPrueba, binding.pager) { tab, position ->
    tab.text = "${(position + 1)}"
}.attach()
```

#### Con esto lo tenemos todo hecho

{% code title="MainActivity.kt" %}
```kotlin
package com.example.fragmentpagerapp

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import com.example.fragmentpagerapp.adapter.MyFragmentStateAdapter
import com.example.fragmentpagerapp.databinding.ActivityMainBinding
import com.example.fragmentpagerapp.model.CharacterProvider
import com.example.fragmentpagerapp.transformer.ZoomOutPageTransformer
import com.google.android.material.tabs.TabLayoutMediator

private lateinit var binding: ActivityMainBinding

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        val pagerAdapter = MyFragmentStateAdapter(this, CharacterProvider.characterList)
        binding.pager.adapter = pagerAdapter
        binding.pager.setPageTransformer(ZoomOutPageTransformer())

        TabLayoutMediator(binding.tlPrueba,
            binding.pager) {
                tab, position ->
            tab.text = "${(position + 1)}"
        }.attach()
    }
}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/tab_layout.gif" alt=""><figcaption></figcaption></figure>
