---
description: Explicación del concepto de SearchView.
---

# SearchView

{% embed url="https://developer.android.com/reference/kotlin/android/widget/SearchView" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/training/search/setup?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Un widget que facilita al usuario realizar búsquedas a una Proveedor de busqueda. Muestra un listado de sugerencias de resultado (si está disponible) y permite al usuario seleccionar un resultado para acceder a él.

{% hint style="info" %}
Desde Android 3.0 utilizar un `SearchView` desde la barra de la App es la forma preferida de admitir búsquedas en una App.&#x20;

La información relativa a la implementación se encuentra en el segundo enlace al principio de la página "[Como configurar una interfaz de búsqueda](https://developer.android.com/training/search/setup?hl=es-419)".
{% endhint %}

## USO DESDE XML

Para que un `SearchView` funcione de manera óptima, es importante que tenga espacio suficiente para mostrarse.

En este caso, vamos a utilizar una Activity con un SearchView y una ListView con los posibles resultados. Después configuraremos todo esto para darle vida.

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
        <SearchView
            android:id="@+id/svEjemplo"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:iconifiedByDefault="false"
            android:queryHint="Comunidad Autónoma"
            android:queryBackground="@android:color/transparent"/>

        <ListView
            android:id="@+id/lvEjemplo"
            android:layout_width="match_parent"
            android:layout_height="250dp" />
    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                            ![](<../../../../.gitbook/assets/image (12).png>)

{% hint style="info" %}
Como vemos, la ListView no se ve, sin embargo es fundamental para el buen funcionamiento de la busqueda, tal y como la vamos a configurar en este ejemplo.
{% endhint %}

## ATRIBUTOS

### android:inconifiedByDefault

Define si lo que vemos por defecto es el icono de busqueda (true) o el campo de busqueda (false).

Es indispensable ponerlo en false para poder interactuar con el campo de busqueda.

### android:imeOptions

{% hint style="info" %}
Un **editor de método de entrada (IME)** es un control para el usuario que le permite ingresar texto.&#x20;

Android proporciona un framework de método de entrada extensible que permite que las aplicaciones ofrezcan a los usuarios métodos de entrada alternativos, como teclados en pantalla o incluso entrada de voz.
{% endhint %}

Tiene las opciones en el siguiente [enlace](https://developer.android.com/reference/kotlin/android/widget/SearchView#android:imeoptions).

### android:inputType

Explicado en [Views -> Pallete Texts -> EditText](../pallete-texts/edittext.md#android-inputtype).

### android:maxWidth

Define la anchura máxima.

### android:queryHint

Una ayuda opcional que muestra un texto de ejemplo en el cuadro de busquedas cuando se encuentra vacío.

## CONFIGURACIÓN

La configuración de un `SearchView` es bastante similar a la de un `AutoCompleteTextView`:

### Definir un adaptador

Vamos a utilizar un adaptador para la ListString que modifique su contenido en función de lo que capte el Listener del Search View:

```kotlin
val lvEjemplo = findViewById<ListView>(R.id.lvEjemplo)
val adapterCCAA: ArrayAdapter<String> = ArrayAdapter(this, 
android.R.layout.simple_dropdown_item_1line, 
resources.getStringArray(R.array.ccaa_array))

lvEjemplo.adapter = adapterCCAA
```

Como en este ejemplo la lista va sobre Comunidades Autónomas en España, utilizamos un `StringArray` que se ha almacenado previamente en el archivo `strings.xml`.&#x20;

Ahora ya tenemos el contenido contra el que se va a realizar la búsqueda.

### Definir el listener

#### setOnQueryTextListener

Este listener, igual que el de las SeekBar tiene una forma curiosa pues recibe como argumento un objeto del tipo `SearchView.OnQueryTextListener{}` que contiene los siguientes controladores:

* `OnQueryTextSubmit(query: String?): Boolean`

Controla el momento en el que se envía una búsqueda dándole al botón de buscar.

* `OnQueryTextChange(query:String?): Boolean`

Controla cada cambio que se realiza en la búsqueda.

### Código

{% hint style="info" %}
En el ejemplo que vamos a poner a continuación no se puede observar el buen funcionamiento de `OnQueryTextSubmit(query: String?): Boolean` por que se ejecuta en todo momento lo programado en `OnQueryTextChange(query:String?): Boolean`.

Para verlo correctamente es recomendable que implementen la prueba en su laboratorio y comenten el contenido de la última (exceptuando la linea de return).
{% endhint %}

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
        <SearchView
            android:id="@+id/svEjemplo"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:iconifiedByDefault="false"
            android:queryHint="Comunidad Autónoma"
            android:queryBackground="@android:color/transparent"/>

        <ListView
            android:id="@+id/lvEjemplo"
            android:layout_width="match_parent"
            android:layout_height="250dp" />
    </LinearLayout>
</ScrollView>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.ListView
import android.widget.SearchView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val svEjemplo = findViewById<SearchView>(R.id.svEjemplo)
        val lvEjemplo = findViewById<ListView>(R.id.lvEjemplo)
        val adapterCCAA: ArrayAdapter<String> = ArrayAdapter(this, android.R.layout.simple_dropdown_item_1line, resources.getStringArray(R.array.ccaa_array))

        lvEjemplo.adapter = adapterCCAA

        svEjemplo.setOnQueryTextListener(object: SearchView.OnQueryTextListener{
            override fun onQueryTextSubmit(query: String?): Boolean {
                svEjemplo.clearFocus()
                if (query in resources.getStringArray(R.array.ccaa_array)) adapterCCAA.filter.filter(query)
                return false
            }
            override fun onQueryTextChange(query: String?): Boolean {
                adapterCCAA.filter.filter(query)
                return false
            }
        })
    }
}
```
{% endcode %}

![](<../../../../.gitbook/assets/image (7) (1).png>)                               ![](<../../../../.gitbook/assets/image (44).png>)

&#x20;                                                ![](<../../../../.gitbook/assets/image (36).png>)
