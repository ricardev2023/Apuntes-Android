---
description: Explicación del concepto de TextView.
---

# TextView

{% embed url="https://developer.android.com/reference/android/widget/TextView" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `View`.

Los **TextView** son interfaces de usuario que muestran texto al usuario.&#x20;

## USO DESDE XML

En el archivo layout XML de la **Activity** que estemos editando, en el caso del ejemplo `activity_main.xml` es donde por regla general se van a definir las Views y los ViewGroups (estructura del layout) que componen el contenido de la **Activity**.

El ejemplo más básico de una **TextView** en la **MainActivity** sería el siguiente:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TEXTO DE PRUEBA" />

</LinearLayout>
```
{% endcode %}

{% hint style="info" %}
\<linearLayout> se corresponde con el ViewGroup. Concepto que se desarrollará más adelante en el temario.
{% endhint %}

Una vez tenemos éste código en el archivo de **layout** hay que hacer que el archivo de kotlin `MainActivity.kt`  reconozca ese archivo de layout como suyo. Para ello utilizamos el siguiente código:

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```
{% endcode %}

{% hint style="info" %}
La línea de código [`setContentView(R.layout.activity_main)`](#user-content-fn-1)[^1] hace que la **Activity** busque en la carpeta **layout** el archivo `activity_main.xml`  para componer el contenido de la **Activity**.

El resto del código no es complicado:

* El package marca la ruta completa del paquete en el que estamos trabajando.
* Los import importan componentes necesarios de diferentes bibliotecas.
* Se crea la clase **MainActivity** que hererda del tipo **AppCompatActivity()** y se sobrescribe (`override`) el método **onCreate** para añadir al propio método **onCreate** (`super.onCreate`) el `setContentView`.
{% endhint %}

El resultado es el siguiente:

![](<../../../../.gitbook/assets/image (64).png>)

## ATRIBUTOS

Como vemos arriba, ese texto es muy primitivo y no tiene ningún tipo de estilo ni de característica especial. A continuación vamos a ver algunos de los atributos que se pueden añadir a las Views del tipo TextView para hacer que sean únicas y se adapten a nuestras necesidades.

Si quieren ver todos los atributos, los pueden encontrar en el siguiente enlace:

{% embed url="https://developer.android.com/reference/android/widget/TextView#xml-attributes_1" %}
Fuente: developer.android
{% endembed %}

### android:id

Atributo heredado de View.

_ID de recurso_. Un nombre de recurso único para el elemento, que puedes usar a fin de obtener una referencia al [`View`](https://developer.android.com/reference/android/view/View) de tu aplicación.

Para el valor de ID, por lo general, debes usar esta sintaxis: `"@+id/`_`name`_`"`. El símbolo +, `+`, indica que es un nuevo ID de recurso, y la herramienta `aapt` creará un nuevo número entero de recurso en la clase `R.java`, si aún no existe. Por ejemplo:

```xml
<TextView android:id="@+id/tvTextoEjemplo"/>
```

{% hint style="info" %}
Una buena práctica para nombrar los id de recurso a lo largo del proyecto es añadir antes del nombre que le queramos dar las iniciales del tipo de View que es, en el caso de un TextView sería **tvTextoEjemplo**.

Esto no es obligatorio pero es recomendable tener un mismo diseño en todo el proyecto.
{% endhint %}

### android:layout\_width

Es un atributo obligatorio y expresa la anchura del TextView con respecto al ViewGroup padre.

Puede ser:

* **match\_parent** ->  La View será tan grande como su padre (menos el Padding).
* **wrap\_content** -> La View será tan grande como sea necesario para el contenido de la misma (más el Padding).
* Un número concreto con unidad de medida.

### android:layout\_height

Es un atributo obligatorio y expresa la altura del TextView con respecto al ViewGroup padre.

Puede ser:

* **match\_parent** ->  La View será tan grande como su padre (menos el Padding).
* **wrap\_content** -> La View será tan grande como sea necesario para el contenido de la misma (más el Padding).
* Un número concreto con unidad de medida.

### android:text

Es un atributo obligatorio y expresa el texto que se va a mostrar al usuario.

### android:drawableStart

Permite introducir un drawable como parte del texto. Es muy util para incluir iconos en los campos a rellenar para facilitar la comprensión.

Hay varias opciones para colocar el drawable, no solo en el inicio:

* **android:drawableEnd**
* **android:drawableTop**
* **android:drawableLeft**
* **android:drawableRight**
* **android:drawableBottom**

### android:drawablePadding

Marca el margen entre el elemento drawable y el texto.

### android:fontFamily <a href="#attr_android-fontfamily" id="attr_android-fontfamily"></a>

Permite seleccionar la fuente de la carpeta de fuentes del proyecto. Para ello se ha de hacer referencia a ella de la siguiente manera:

```xml
<TextView android:fontFamily="@font/roboto"/>
```

### android:gravity <a href="#attr_android-gravity" id="attr_android-gravity"></a>

Permite seleccionar la posición relativa del texto con respecto al View. Hay varias opciones:

* start
* top
* left
* right
* bottom
* end
* center / center\_horizontal / center\_vertical
* clip / clip\_horizontal / clip\_vertical
* fill / fill\_horizontal / fill\_vertical

### android:padding

Atributo heredado de View.

El padding se define como el espacio en pixeles entre el límite de la View y el contenido de la misma.&#x20;

Se puede marcar para cada uno de los cuatro lados de la View:

* **android:paddingTop**
* **android:paddingLeft**
* **android:paddingRight**
* **android:paddingBottom**

### android:textColor <a href="#attr_android-textcolor" id="attr_android-textcolor"></a>

Permite modificar el color del texto.

### android:textSize <a href="#attr_android-textsize" id="attr_android-textsize"></a>

Permite cambiar el tamaño del texto.

{% hint style="info" %}
Lo normal cuando se trata de textos en Android es utilizar la unidad de medida `sp`. &#x20;

Esta unidad de medida se traduce como Scale-independent Pixels y básicamente es una unidad de medida que escala en función de la densidad de pixeles en pantalla para que el texto tenga siempre el mismo tamaño.
{% endhint %}

### android:textStyle <a href="#attr_android-textstyle" id="attr_android-textstyle"></a>

Permite modificar el estilo del texto cambiandolo a negrita o cursiva. Puede ser:

* bold
* italic
* normal

### android:typeface <a href="#attr_android-typeface" id="attr_android-typeface"></a>

Permite modificar el tipo de fuente dentro de la misma familia. Puede ser:

* monospace
* normal
* serif
* sans

{% hint style="info" %}
Esto lo hace Android sin necesidad de tener todas estas fuentes en la carpeta fonts. Por eso es recomendable añadir unicamente la fuente Regular de cada tipo que se quiera utilizar.
{% endhint %}

### Ejemplo

Una vez hemos utilizado estos atributos (no todos) nos quedará el texto mucho más estiloso.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/tvTextoEjemplo"
        android:layout_width="match_parent"
        android:layout_height="300dp"
        android:fontFamily="@font/explora"
        android:gravity="center_horizontal|fill_vertical"
        android:text="@string/texto_de_prueba"
        android:textSize="30sp"
        android:textStyle="bold"
        android:textColor="@color/purple_700"
        />

</LinearLayout>
```
{% endcode %}

![](<../../../../.gitbook/assets/image (97).png>)

## MODIFICAR VIEWS DESDE CÓDIGO

Los atributos que se han presentado en el apartado anterior se pueden modificar desde código en el archivo `MainActivity.kt` lo que hará que se sobrescriban los atributos del mismo tipo definidos en el archivo `activity_main.xml`.

Para ello lo primero que debemos hacer es crear una variable (dentro de la función onCreate) del tipo TextView con la View que queremos modificar:

```kotlin
import android.widget.TextView

val tvTextoEjemplo:TextView? = findViewById(R.id.tvTextoEjemplo)
```

Una vez tengo la variable creada, puedo aplicar en ella todos los métodos y atributos de los objetos del tipo `TextView`.&#x20;

Estos métodos y atributos son muchos y no se van a explicar en ésta página. De la misma manera que con los atributos, los métodos se pueden encontrar en el siguiente enlace:

{% embed url="https://developer.android.com/reference/android/widget/TextView#public-methods_1" %}
Fuente: developer.android
{% endembed %}

### &#x20;Ejemplo

Aplicando algunos de éstos métodos al código podemos tener el siguiente resultado:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/tvTextoEjemplo"
        android:layout_width="match_parent"
        android:layout_height="300dp"
        android:fontFamily="@font/explora"
        android:gravity="center_horizontal|fill_vertical"
        android:text="@string/texto_de_prueba"
        android:textSize="30sp"
        android:textStyle="bold"
        android:textColor="@color/purple_700"
        />

</LinearLayout>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import android.graphics.Color
import android.graphics.Typeface
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.TextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val tvTextoEjemplo: TextView = findViewById(R.id.tvTextoEjemplo)
        tvTextoEjemplo.text = "Texto cambiado en código"
        tvTextoEjemplo.setTextColor(Color.RED)
        tvTextoEjemplo.typeface = Typeface.MONOSPACE
    }
}
```
{% endcode %}

![](<../../../../.gitbook/assets/image (63).png>)

## PROGRAMAR EVENTOS EN TEXTVIEW

{% embed url="https://developer.android.com/topic/architecture/ui-layer/events" %}
Fuente: developer.android
{% endembed %}

Como ya vimos en la página de [Componentes de una App - Views y ViewGroups](../../../componentes-de-una-app/views-y-viewgroups.md#view), las views no solo se encargan del dibujado de dicho componente sino tambien de la gestión de los eventos en dicho componente.

Para ello utilizamos los métodos que Google a puesto a nuestra disposición a tal efecto, en este caso, por ejemplo podemos hace que cuando toquemos sobre el texto, éste cambie de color e incluso cambie lo que pone.

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import android.graphics.Color
import android.graphics.Typeface
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.TextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val tvTextoEjemplo: TextView = findViewById(R.id.tvTextoEjemplo)
        tvTextoEjemplo.text = "Texto cambiado en código"
        tvTextoEjemplo.setTextColor(Color.RED)
        tvTextoEjemplo.typeface = Typeface.MONOSPACE

        tvTextoEjemplo.setOnClickListener {
            tvTextoEjemplo.text = "Texto pulsado"
            tvTextoEjemplo.setTextColor(Color.BLACK)
            Toast.makeText(this, "El texto ha cambiado, Enhorabuena", 
            Toast.LENGTH_LONG).show()
        }
    }
}
```
{% endcode %}

Cuando pulsamos en el texto, se genera el siguiente resultado:

![](<../../../../.gitbook/assets/image (110).png>)     ![](<../../../../.gitbook/assets/image (77).png>)

[^1]: 
