---
description: Explicación del concepto de View Binding.
---

# View Binding

{% embed url="https://developer.android.com/topic/libraries/view-binding?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

La _vinculación de vista_ es una función que permite escribir más fácilmente código que interactúa con las vistas.&#x20;

Una vez que la vinculación de vista está habilitada en un módulo, genera una _clase de vinculación_ para cada archivo de diseño XML presente en ese módulo. Una instancia de una clase de vinculación contiene referencias directas a todas las vistas que tienen un ID en el diseño correspondiente.

En la mayoría de los casos, la vinculación de vistas reemplaza a `findViewById`.

{% hint style="success" %}
Esta función es más moderna que `findViewById` y, aunque el futuro es **Jetpack Compose**, es la forma estandar de trabajar cuando lo hacemos con **Views**.
{% endhint %}

### Diferencias con FindViewById

**View Binding** tiene ventajas importantes frente al uso de `findViewById`:

* **Seguridad frente a valores nulos:** Debido a que la vinculación de vista crea referencias directas a las vistas, no hay riesgo de una excepción de puntero nulo debido a un ID de vista no válido. Además, cuando una vista solo está presente en algunas configuraciones de un diseño, el campo que contiene su referencia en la clase de vinculación se marca con `@Nullable`.
* **Seguridad de tipos:** Los campos de cada clase de vinculación tienen tipos que coinciden con las vistas a las que hacen referencia en el archivo XML. Esto significa que no hay riesgo de una excepción de transmisión de clase.

Estas diferencias significan que las incompatibilidades entre tu diseño y tu código harán que falle la compilación durante el momento de compilación en lugar de hacerlo en el tiempo de ejecución.

### Diferencia con Data Binding

{% embed url="https://medium.com/@Estequiel/c%C3%B3mo-utilizar-data-binding-en-android-bb06e644bea7" %}
Fuente: medium
{% endembed %}

{% embed url="https://developer.android.com/topic/libraries/data-binding?hl=es-419" %}
Fuente: developer.android
{% endembed %}

{% hint style="info" %}
Esto es parte de Android Jetpack.
{% endhint %}

La vinculación de vistas y la [vinculación de datos](https://developer.android.com/topic/libraries/data-binding?hl=es-419) generan clases de vinculación que puedes usar para hacer referencia a vistas directamente. Sin embargo, la vinculación de vistas está diseñada para procesar casos de uso más simples y proporciona los siguientes beneficios por sobre la vinculación de datos:

* **Compilación más rápida:** la vinculación de vistas no requiere procesamiento de anotaciones, por lo que los tiempos de compilación son más rápidos.
* **Facilidad de uso:** la vinculación de vistas no requiere archivos de diseño XML etiquetados especialmente, por lo que es más rápido adoptarlos en tus apps. Una vez que habilites la vinculación de vista en un módulo, se aplicará automáticamente a todos los diseños de ese módulo.

En cambio, la vinculación de vista tiene las siguientes limitaciones en comparación con la vinculación de datos:

* La vinculación de vistas no admite [variables ni expresiones de diseño](https://developer.android.com/topic/libraries/data-binding/expressions?hl=es-419), por lo que no se puede usar para declarar contenido de IU dinámico directamente desde archivos de diseño XML.
* La vinculación de vista no admite la [vinculación de datos bidireccional](https://developer.android.com/topic/libraries/data-binding/two-way?hl=es-419).

Debido a estas consideraciones, en algunos casos es mejor usar la vinculación de vistas y la vinculación de datos en un proyecto. Puedes usar la vinculación de datos en diseños que requieren funciones avanzadas y usar la vinculación de vista en diseños que no lo requieren.

## CONFIGURACIÓN

Para utilizar esta herramienta en nuestro proyecto debemos seguir una serie de pasos.

### Presentación del proyecto

En primer lugar voy a presentarles el proyecto que vamos a migrar a View Binding:

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

        <TextView
            android:id="@+id/tvPrueba"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Prueba con View Binding"
            android:textSize="20sp"
            android:padding="15dp"/>
        <com.nitish.typewriterview.TypeWriterView
            android:id="@+id/typerPrueba"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
        <Button
            android:id="@+id/btPrueba"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Boton de prueba"/>

    </LinearLayout>
</ScrollView>
```
{% endcode %}

### build.gradle (app)

Lo primero que tenemos que hacer para que se pueda utilizar **View Binding** en nuestro proyecto es incluir la siguiente línea en nuestro archivo `build.gradle` a nivel de app.

```groovy
android {
        ...
        viewBinding {
            enabled = true
        }
    }
```

{% hint style="warning" %}
No olviden pulsar en **Sync Now** para que los cambios surtan efecto.
{% endhint %}

### Main Activity

A continuación debemos configurar correctamente la Main Activity.

#### variable binding

En primer lugar debemos declarar una variable en el contexto de la clase MainActivity del tipo ActivityMainBinding  privada (private) y que se inicializará tarde (lateinit).

```kotlin
private lateinit var binding: ActivityMainBinding
```

{% hint style="danger" %}
**IMPORTANTE**

Si se habilita View Binding, el propio sistema genera una clase de vinculación para cada archivo de layout presente en el proyecto.

Su nomenclatura es, el nombre del archivo de layout en formato clase, seguido de la palabra Binding.

**EJEMPLOS:**

`activity_main.xml` -> `ActivityMainBinding`

`activity_buttons.xml` -> `ActivityButtonsBinding`
{% endhint %}

#### Vincular la clase de vinculación

Después, ya dentro del OnCreate, nos encontramos con la necesidad de vincular el layout con la Activity.

Cuando utilizamos findViewById, solo necesitamos añadir la siguiente línea:

```kotlin
setContentView(R.layout.activity_button)
```

Sin embargo, para **vincular la Binding class**, necesitamos realizar un procedimiento un poco más complejo:

```kotlin
binding = ActivityMainBinding.inflate(layoutInflater)
setContentView(binding.root)
```

* Inicializamos la variable **binding** con el **layoutInflater**.
* el **ContentView** es ahora el root de la vinculación.

#### Referencia a las Views

Una vez hecho esto, en vez de crear una variable para cada View dentro del layout, hacemos referencia a ellas como miembros de la clase **ActivityMainBinding**.

```kotlin
binding.typerPrueba.animateText(prueba)

binding.btPrueba.setOnClickListener {
    if (binding.typerPrueba.isAnimationRunning) {
        binding.typerPrueba.stopAnimation()
    }
    else {
        binding.typerPrueba.animateText(prueba)
    }
}
```

## CÓDIGO

A continuación dejo el código completo del ejemplo:

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Toast
import com.example.android.appdeejemplo.databinding.ActivityMainBinding


class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        val prueba = "Prueba de texto animado." +
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor " +
                "incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud " +
                "exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute " +
                "irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla " +
                "pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia " +
                "deserunt mollit anim id est laborum."


        binding.typerPrueba.animateText(prueba)

        binding.btPrueba.setOnClickListener {
            if (binding.typerPrueba.isAnimationRunning) {
                binding.typerPrueba.stopAnimation()
                Toast.makeText(this, "Se ha parado la animacion", 
                Toast.LENGTH_SHORT).show()
            }
            else {
                binding.typerPrueba.animateText(prueba)
                Toast.makeText(this, "Se ha reiniciado la animación", 
                Toast.LENGTH_SHORT).show()
            }
        }
    }
}
```
{% endcode %}

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

        <TextView
            android:id="@+id/tvPrueba"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Prueba con View Binding"
            android:textSize="20sp"
            android:padding="15dp"/>
        <com.nitish.typewriterview.TypeWriterView
            android:id="@+id/typerPrueba"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
        <Button
            android:id="@+id/btPrueba"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Boton de prueba"/>

    </LinearLayout>
</ScrollView>
```
{% endcode %}

![](<../../../.gitbook/assets/image (15) (1).png>)                              ![](<../../../.gitbook/assets/image (51).png>)

&#x20;                                                   ![](<../../../.gitbook/assets/image (20) (1).png>)
