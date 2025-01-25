---
description: Explicación del concepto de Spinner
---

# Spinner

{% embed url="https://developer.android.com/reference/android/widget/Spinner" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/guide/topics/ui/controls/spinner?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de:

<figure><img src="../../.gitbook/assets/herencia de spinner.png" alt=""><figcaption><p>Herencia de spinner</p></figcaption></figure>

Los **Spinner** (controles de números) ofrecen una manera rápida de seleccionar un valor de un conjunto.&#x20;

En el estado predeterminado, un **Spinner** muestra su valor actualmente seleccionado. Al tocar el control de números, se muestra un menú desplegable con todos los demás valores disponibles, de los cuales el usuario puede seleccionar uno.

Los **Spinner** heredan de `AdapterView` que son una serie de **Views** que necesitan de un **adapter** para gestionar correctamente las opciones.

{% hint style="warning" %}
MATERIAL DESIGN

Debido a una serie de errores en el desempeño de la clase Spinner, cuando se desarrollo Material Design el Spinner se quedó fuera.

Fue sustituido por:

[https://www.material.io/components/menus/android#exposed-dropdown-menus](https://www.material.io/components/menus/android#exposed-dropdown-menus)
{% endhint %}

## USO DESDE XML

A pesar de que su uso desde XML es muy sencillo, se debe tener en cuenta que es necesario un SpinnerAdapter para que el Spinner funcione correctamente:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="horizontal"
        android:layout_margin="15dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Seleccione su lugar de origen: "/>
        <Spinner
            android:id="@+id/spPrueba"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            />

    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                                ![](<../../.gitbook/assets/image (6).png>)

## ATRIBUTOS

### android:dropDownHorizontalOffset

Define la diferencia horizontal, en pixeles, entre el desplegable y la flecha.

### android:dropDownSelector

Define el drawable que se utilizará en vez de la flecha apuntando hacia abajo.

### android:dropDownVerticalOffset

Define la diferencia vertical, en pixeles, entre el desplegable y la flecha.

### android:dropDownWidth

Define la anchura del menú desplegable.

### android:gravity

Define la posición en la que se colocará el item seleccionado.

### android:popupBackground

Define el drawable que se utilizará de fondo en el menú desplegable.

### android:prompt

el texto a mostrar cuando se muestra el dialogo del Spinner.

### android:spinnerMode

Define el modo en que se muestra el Spinner, hay dos modos:

* **Dropdown ->** Las opciones se muestran al usuario como un menú desplegable.

&#x20;                                               ![](<../../.gitbook/assets/image (7).png>)

* **Dialog ->** Las opciones se muestran al usuario en forma de diálogo.

&#x20;                                                ![](<../../.gitbook/assets/image (5).png>)

## CONFIGURACIÓN

### Adapter

{% embed url="https://developer.android.com/reference/android/widget/SpinnerAdapter" %}
Fuente: developer.android
{% endembed %}

Las opciones que se muestran en el Spinner pueden provenir de cualquier fuente, sin embargo, se deben proveer con un **adapter**. Este **adapter** será:

* `SpinnerAdapter` o `ArrayAdapter` -> Si provienen de una Array.
* `CursorAdapter` -> Si vienen de una consulta a base de datos.

En este caso se va a utilizar un Array almacenado en el archivo de resources strings.xml:

```xml
<string-array name="ccaa_array">
    <item>Castilla y León</item>
    <item>Andalucía</item>
    <item>Valencia</item>
    <item>Madrid</item>
    <item>Cantabria</item>
    <item>País Vasco</item>
    <item>Asturias</item>
    <item>Canarias</item>
    <item>Galicia</item>
    <item>Castilla - La Mancha</item>
    <item>Illes Balears</item>
    <item>Navarra</item>
    <item>La Rioja</item>
    <item>Aragón</item>
    <item>Extremadura</item>
    <item>Murcia</item>
    <item>Cataluña</item>
    <item>Melilla</item>
    <item>Ceuta</item>
</string-array>
```

A continuación se va a proceder a desarrollar el Adapter, en este caso utilizaremos un ArrayAdapter:

#### Opción 1: createFromResource

Es la opción recomendada por Google

{% code title="Opción 1: createFromResource" %}
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        ArrayAdapter.createFromResource(
            this,
            R.array.ccaa_array,
            android.R.layout.simple_spinner_item
        ).also { adapter ->
            // Puede modificar el estilo de la vista del menu desplegable
            adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)
            // Por último aplicamos el adapter al Spinner
            binding.spPrueba.adapter = adapter
        }
```
{% endcode %}

#### Opción 2: ArrayAdapter normal

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        val adapter: ArrayAdapter<String> = ArrayAdapter<String>(this,
            android.R.layout.simple_spinner_dropdown_item,
            resources.getStringArray(R.array.ccaa_array))
        binding.spPrueba.adapter = adapter
```

### Listener

Cuando un usuario selecciona un elemento de menú desplegable, el objeto `Spinner` recibe un evento en relación con el elemento seleccionado.

Para definir el controlador del evento de selección para un Spinner, hay que seguir los siguientes pasos:

* implementa la interfaz `AdapterView.OnItemSelectedListener`&#x20;
* Implementar los método miembro de devolución de llamada `onItemSelected()`  y `onNothingSelected()` correspondientes.&#x20;



<pre class="language-kotlin"><code class="lang-kotlin">class MainActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {

<strong>    override fun onItemSelected(parent: AdapterView&#x3C;*>?, view: View?, pos: Int, id: Long) {
</strong>        Toast.makeText(this, "Usted ha seleccionado ${parent?.getItemAtPosition(pos)}", Toast.LENGTH_SHORT).show()
    }
    
    override fun onNothingSelected(parent: AdapterView&#x3C;*>?) {
    }
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
        
        (...)
        
        binding.spPrueba.onItemSelectedListener = this
}
</code></pre>

Para obtener el ítem seleccionado lo puede hacer con `parent?.getItemAtPosition(pos)`&#x20;

## EJEMPLO

A continuación mostraré el código completo del ejemplo de esta entrada:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="horizontal"
        android:layout_margin="15dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Seleccione su lugar de origen: "/>
        <Spinner
            android:id="@+id/spPrueba"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:gravity="end"
            />

    </LinearLayout>
</ScrollView>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.AdapterView
import android.widget.ArrayAdapter
import android.widget.Toast
import com.example.android.appdeejemplo.databinding.ActivityMainBinding


class MainActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

//        ArrayAdapter.createFromResource(
//            this,
//            R.array.ccaa_array,
//            android.R.layout.simple_spinner_item
//        ).also { adapter ->
//            // Specify the layout to use when the list of choices appears
//            adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)
//            // Apply the adapter to the spinner
//            binding.spPrueba.adapter = adapter
//        }
        val adapter: ArrayAdapter<String> = ArrayAdapter<String>(this,
            android.R.layout.simple_spinner_dropdown_item,
            resources.getStringArray(R.array.ccaa_array)
            )
        binding.spPrueba.adapter = adapter
        
        binding.spPrueba.onItemSelectedListener = this
    }

    override fun onItemSelected(parent: AdapterView<*>?, view: View?, pos: Int, id: Long) {
        Toast.makeText(this, 
        "Usted ha seleccionado ${parent?.getItemAtPosition(pos)}", 
        Toast.LENGTH_SHORT
        ).show()
    }

    override fun onNothingSelected(parent: AdapterView<*>?) {
    }
}
```
{% endcode %}

![](<../../.gitbook/assets/image (1).png>)                               ![](<../../.gitbook/assets/image (4).png>)

&#x20;                                                ![](<../../.gitbook/assets/image (3).png>)
