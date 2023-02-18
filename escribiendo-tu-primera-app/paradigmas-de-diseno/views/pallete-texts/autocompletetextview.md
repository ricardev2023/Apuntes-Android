---
description: Explicación del concepto de AutoCompleteTextView.
---

# AutoCompleteTextView

{% embed url="https://developer.android.com/reference/android/widget/AutoCompleteTextView" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `EditText`.

Una View de texto editable que muestra sugerencias automáticas para completar el texto mientras el usuario está escribiendo.&#x20;

Estas sugerencias se muestran en forma de `drop down menu` en el que el usuario puede seleccionar un item que reemplace el contenido que había introducido.

El `drop down menu` se puede quitar en cualquier momento pulsando el botón **atrás** o si no se ha seleccionado nada del menú pulsando **enter**.

La lista de opciones disponibles se obtiene de un data adapter y aparece solamente si se cumple el número de carácteres mínimos definidos en el `treshold`.

## USO DESDE XML

El uso desde XML es el mismo que en los casos anteriores. Sin embargo, en el caso del `AutoCompleteTextView`, es necesario configurar el adapter en código para que no se comporte como un EditText normal y corriente.

{% code title="" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="10dp"
    android:orientation="vertical">


    <AutoCompleteTextView
        android:id="@+id/actvEjemplo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="20sp"
        android:hint="Introduzca país de origen" />
    
</LinearLayout>
```
{% endcode %}

## PROGRAMAR ADAPTER

### Array de sugerencias

Las diferentes opciones de autocompletado que damos al usuario deben estar guardadas en un `Array`. Este `Array` se puede definir en tres lugares diferentes:

* **En el código de la MainActivity** -> Es lo que se suele ver en ejemplos sencillos pero no es nada recomendable pues va en contra de las buenas prácticas de Android.
* **En el fichero de resources strings.xml** -> Es más adecuado, es lo que las buenas prácticas dicta y facilita el mantenimiento de la App.
* **En una base de datos** -> Es la opción más compleja pero la más segura.

En el ejemplo utilizaremos el fichero strings.xml para almacenar nuestro Array de Strings:

{% code title="values/strings.xml" %}
```xml
<resources>
    <string name="app_name">App de ejemplo</string>
    <string name="texto_de_prueba">TEXTO DE PRUEBA</string>
    <string-array name="country_array">
        <item>Andorra</item>
        <item>España</item>
        <item>Francia</item>
        <item>Portugal</item>
    </string-array>
</resources>
```
{% endcode %}

### Adapter

Una vez tenemos nuestro StringArray tenemos que implementar el adapter en el código de MainActivity, para ello utilizamos el siguiente código:

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.AutoCompleteTextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val actvEjemplo: AutoCompleteTextView = findViewById(R.id.actvEjemplo)
        val countryArray: Array<String> = resources.getStringArray(R.array.country_array)
        val adapter: ArrayAdapter<String> = ArrayAdapter<String>(this,
            android.R.layout.simple_dropdown_item_1line, countryArray)

        actvEjemplo.setAdapter(adapter)
    }
}
```
{% endcode %}

## MultiAutoCompleteTextView

{% embed url="https://developer.android.com/reference/kotlin/android/widget/MultiAutoCompleteTextView" %}
Fuente: developer.android
{% endembed %}

En este caso, la MultiAutoCompleteTextView ofrece sugerencias para cada substring en la caja de texto.

Es indispensable definir un tokenizer para que el sistema sepa cómo se separan las diferentes substrings:

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.MultiAutoCompleteTextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val mactvEjemplo: MultiAutoCompleteTextView = findViewById(R.id.mactvEjemplo)
        val ccaaArray: Array<String> = resources.getStringArray(R.array.ccaa_array)
        val ccaaAdapter: ArrayAdapter<String> = ArrayAdapter(this,
            android.R.layout.simple_dropdown_item_1line, ccaaArray)

        mactvEjemplo.setAdapter(ccaaAdapter)
        mactvEjemplo.setTokenizer(MultiAutoCompleteTextView.CommaTokenizer())

    }
}
```
{% endcode %}

## EJEMPLO COMPLETO

Ahora vamos a combinar las dos opciones que hemos visto en ésta página en una sola aplicación.

{% code title="strings.xml" %}
```xml
<resources>
    <string name="app_name">App de ejemplo</string>
    <string name="texto_de_prueba">TEXTO DE PRUEBA</string>
    <string-array name="country_array">
        <item>Andorra</item>
        <item>España</item>
        <item>Francia</item>
        <item>Portugal</item>
    </string-array>
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
</resources>
```
{% endcode %}

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="10dp"
    android:orientation="vertical">

    <AutoCompleteTextView
        android:id="@+id/actvEjemplo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="20sp"
        android:hint="Introduzca país de origen"
        android:visibility="visible"/>

    <MultiAutoCompleteTextView
        android:id="@+id/mactvEjemplo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="20sp"
        android:hint="Introduzca Comunidad Autónoma"
        android:visibility="visible"/>
</LinearLayout>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.AutoCompleteTextView
import android.widget.MultiAutoCompleteTextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val actvEjemplo: AutoCompleteTextView = findViewById(R.id.actvEjemplo)
        val countryArray: Array<String> = resources.getStringArray(R.array.country_array)
        val countryAdapter: ArrayAdapter<String> = ArrayAdapter<String>(this,
            android.R.layout.simple_dropdown_item_1line, countryArray)

        val mactvEjemplo: MultiAutoCompleteTextView = findViewById(R.id.mactvEjemplo)
        val ccaaArray: Array<String> = resources.getStringArray(R.array.ccaa_array)
        val ccaaAdapter: ArrayAdapter<String> = ArrayAdapter(this,
            android.R.layout.simple_dropdown_item_1line, ccaaArray)

        actvEjemplo.setAdapter(countryAdapter)
        mactvEjemplo.setAdapter(ccaaAdapter)
        mactvEjemplo.setTokenizer(MultiAutoCompleteTextView.CommaTokenizer())
    }
}
```
{% endcode %}

![](<../../../../.gitbook/assets/image (76).png>)  ![](<../../../../.gitbook/assets/image (67).png>) ![](<../../../../.gitbook/assets/image (35).png>)  ![](<../../../../.gitbook/assets/image (94).png>)  ![](<../../../../.gitbook/assets/image (68).png>)  ![](<../../../../.gitbook/assets/image (79).png>)
