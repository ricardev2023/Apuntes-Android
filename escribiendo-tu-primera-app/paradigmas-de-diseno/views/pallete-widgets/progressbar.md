---
description: Explicación del concepto de ProgressBar
---

# ProgressBar

{% embed url="https://developer.android.com/reference/android/widget/ProgressBar" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `View`.

Es una interfaz de usuario que indica el progreso de una operación. Una ProgressBar soporta dos modos:

### Progreso indeterminado

Utilice el modo indeterminado cuando no sabe cuanto va a durar la operación que se está realizando.&#x20;

Es el modo por defecto y muestra una animación cíclica sin indicar una cantidad concreta de progreso.

### Progreso determinado

Utilice el modo determinado cuando quiere mostrar la cantidad específica de progreso que está ocurriendo.&#x20;

## USO EN XML

Exiten varios tipos de `ProgressBar` en función de los estilos que se le asignen a la `View`. Estos estilos vienen preinstalados en Android y se pueden diferenciar en:

* **Circulares**
* **Horizontales**
* **Holo** -> Un diseño de Android más clásico. [Dio paso a Material Design](https://www.elespanol.com/elandroidelibre/20170101/holo-material-design-siguiente-cambio-diseno-android/182732170\_0.html).
* **Material** -> El estilo que se aplica a la libreria `Material Design` de Android. Es el estilo por defecto.
* **DeviceDefault** -> La que esté seleccionada en el Dispositivo. Esto incluye los temas que puedan encontrarse instalados en un equipo.

Es por eso que podemos encontrar las siguientes (y más) opciones en un XML:

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>

<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:layout_margin="15dp">

        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="30dp"
            style="@android:style/Widget.ProgressBar.Small"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.ProgressBar"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.ProgressBar.Large"/>

        <View
            android:id="@+id/divider"
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:paddingBottom="30dp"
            android:background="?android:attr/listDivider" />

        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.DeviceDefault.ProgressBar.Large"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.Material.ProgressBar.Large"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="30dp"
            style="@android:style/Widget.Holo.ProgressBar.Large"/>

        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.ProgressBar.Horizontal"
            android:indeterminate="true"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.DeviceDefault.ProgressBar.Horizontal"
            android:indeterminate="true"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.Material.ProgressBar.Horizontal"
            android:indeterminate="true"/>
        <ProgressBar
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:paddingBottom="15dp"
            style="@android:style/Widget.Holo.ProgressBar.Horizontal"
            android:indeterminate="true"/>

    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                               ![](<../../../../.gitbook/assets/image (11).png>)

## ATRIBUTOS

### android:animationResolution

Define el tiempo en milisegundos que pasa entre cada frame de la animación. Puede ser un `Integer`.

### android:indeterminate

Define si la `ProgressBar` va a tener progreso determinado (`false`) o indeterminado (`true`).

### android:indeterminateBehaviour

Define el comportamiento de la animación cuando el progreso en indeterminado. Puede ser:

* **cycle** -> Va hasta el valor definido y luego del valor definido a 0.
* **repeat** -> La animación vuelve a empezar cada vez que llega al valor definido.

### android:indeterminateDrawable

Define el drawable a utilizar en la animación de indeterminado. Un drawable animable (animatable) da más control al desarrollador sobre la animación.

### android:indeterminateDuration <a href="#attr_android-indeterminateduration" id="attr_android-indeterminateduration"></a>

Define la duración de la animación de progreso indeterminado.&#x20;

Solo afecta a la animación si el drawable no es "animatable". Es un `Integer`.

### android:indeterminateOnly <a href="#attr_android-indeterminateonly" id="attr_android-indeterminateonly"></a>

Restringe la `ProgressBar` a modo indeterminado exclusivamente. Es un `Booleano`.

### android:indeterminateTint <a href="#attr_android-indeterminatetint" id="attr_android-indeterminatetint"></a>

Define el color que se aplica al indicador de progreso indeterminado.

### android:indeterminateTintMode <a href="#attr_android-indeterminatetintmode" id="attr_android-indeterminatetintmode"></a>

Es el modo en el que se aplica el color. En el siguiente enlace podrá encontrar las [opciones](https://developer.android.com/reference/android/widget/ProgressBar#attr\_android:indeterminateTintMode).

### android:interpolator <a href="#attr_android-interpolator" id="attr_android-interpolator"></a>

Define la aceleración de la curva para la animación del modo indeterminado si el drawable no es "animatable".

### android:max <a href="#attr_android-max" id="attr_android-max"></a>

Define el valor máximo de Progreso.

### android:maxHeight <a href="#attr_android-maxheight" id="attr_android-maxheight"></a>

Atributo opcional para dotar de una altura máxima a esta `View`.

### android:maxWidth <a href="#attr_android-maxwidth" id="attr_android-maxwidth"></a>

Atributo opcional para dotar de una anchura máxima a esta `View`.

### android:min <a href="#attr_android-min" id="attr_android-min"></a>

Define el valor mínimo de Progreso.

### android:minHeight <a href="#attr_android-minheight" id="attr_android-minheight"></a>

Atributo opcional para dotar de una altura mínima a esta `View`.

### android:minWidth <a href="#attr_android-minwidth" id="attr_android-minwidth"></a>

Atributo opcional para dotar de una anchura mínima a esta `View`.

### android:progress <a href="#attr_android-progress" id="attr_android-progress"></a>

Define el progreso por defecto. Puede ser un Integer entre min y max.

### android:progressBackgroundTint <a href="#attr_android-progressbackgroundtint" id="attr_android-progressbackgroundtint"></a>

Define el color que se aplica al fondo del indicador de progreso.

### android:progressBackgroundTintMode <a href="#attr_android-progressbackgroundtintmode" id="attr_android-progressbackgroundtintmode"></a>

Es el modo en el que se aplica el color. En el siguiente enlace podrá encontrar las [opciones](https://developer.android.com/reference/android/widget/ProgressBar#attr\_android:progressBackgroundTintMode).

### android:progressDrawable <a href="#attr_android-progressdrawable" id="attr_android-progressdrawable"></a>

Define el drawable a utilizar en la animación de determinado. Un drawable animable (animatable) da más control al desarrollador sobre la animación.

### android:progressTint <a href="#attr_android-progresstint" id="attr_android-progresstint"></a>

Define el color que se aplica al indicador de progreso determinado.

### android:progressTintMode <a href="#attr_android-progresstintmode" id="attr_android-progresstintmode"></a>

Es el modo en el que se aplica el color. En el siguiente enlace podrá encontrar las [opciones](https://developer.android.com/reference/android/widget/ProgressBar#attr\_android:progressTintMode).

### android:secondaryProgress <a href="#attr_android-secondaryprogress" id="attr_android-secondaryprogress"></a>

Define un progreso secundario. Debe estar contenido entre 0 y max.&#x20;

Este progreso se dibuja entre el progreso principal y el fondo. Es muy útil para ver cuanto del recurso se ha guardado ya en el buffer.

### android:secondaryProgressTint <a href="#attr_android-secondaryprogresstint" id="attr_android-secondaryprogresstint"></a>

Define el color que se aplica al indicador de progreso secundario.

### android:secondaryProgressTintMode <a href="#attr_android-secondaryprogresstintmode" id="attr_android-secondaryprogresstintmode"></a>

Es el modo en el que se aplica el color. En el siguiente enlace podrá encontrar las [opciones](https://developer.android.com/reference/android/widget/ProgressBar#attr\_android:secondaryProgressTintMode).

## CONFIGURACIÓN DETERMINADO

{% hint style="success" %}
Es recomendable incluir los ProgressBar con progreso determinado en e XML dando un progreso avanzado, de esta manera se puede ver el diseño sin tener que esperar a programar el código.

Una vez hecho esto, en código se pone a cero.
{% endhint %}

### Creamos el elemento visual

Para crearlo debemos darle un diseño, un estilo, un id y comprobar que todo ello está a nuestro gusto. Esto se hace en el layout.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>

<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:layout_margin="15dp">
        <ProgressBar
            android:id="@+id/pbEjemplo"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="15dp"
            style="@android:style/Widget.Material.ProgressBar.Horizontal"
            android:max="100"
            android:progress="47"
            android:secondaryProgress="78"
            android:progressTint="@color/purple_700"
            android:secondaryProgressTint="@color/purple_500"
            android:backgroundTint="@color/purple_200"/>
    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                                   ![](<../../../../.gitbook/assets/image (32).png>)

### Configuración inicial en Código

Ahora que ya tenemos nuestro ProgressBar listo, debemos configurarlo en código para que se inicie desde el principio:

```kotlin
val pb = findViewById<ProgressBar>(R.id.pbEjemplo)
pb.max = 100
pb.progress = 0
pb.secondaryProgress = 0
```

### Configurar comportamiento

Hasta ahora, hemos configurado todas nuestras Views desde el `onCreate()`. Sin embargo, sabemos que después de `onCreate()` viene `onStart()` y, por tanto, si configuramos el movimiento de la `ProgressBar` en `onCreate()`, no lo vamos a poder ver.

&#x20;Para solucionar este problema vamos a introducir un concepto nuevo:

#### Corrutinas

{% embed url="https://developer.android.com/topic/libraries/architecture/coroutines?hl=es-419" %}
Fuente: developer.android
{% endembed %}

Las corutinas nos permiten gestionar procesos de una manera asíncrona y hacer que nuestra App se mueva más rápido.

No se va a explicar aquí su funcionamiento, solo el código para utilizarlas en este caso concreto:

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ProgressBar
import kotlinx.coroutines.GlobalScope
import kotlinx.coroutines.launch
import java.lang.Thread.sleep


class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val pb = findViewById<ProgressBar>(R.id.pbEjemplo)
        pb.max = 100
        pb.progress = 0
        pb.secondaryProgress = 0

        GlobalScope.launch {
            progressManager(pb)
        }
    }
    private fun progressManager(pb: ProgressBar){
        while (pb.progress < pb.max) {
            sleep(500L)
            pb.incrementProgressBy(2)
            pb.incrementSecondaryProgressBy(4)
        }
    }
}
```
{% endcode %}

{% hint style="info" %}
La función progressManager(ProgressBar) debe contener el código que gestiona el avance del progreso, por ejemplo, la cantidad de datos descargados.&#x20;

En el ejemplo se hace por tiempo para que vean que en este punto del código, se puede incluir código arbitrario.
{% endhint %}

![](<../../../../.gitbook/assets/image (14).png>)                               ![](<../../../../.gitbook/assets/image (1).png>) ![](<../../../../.gitbook/assets/image (17).png>)                               ![](<../../../../.gitbook/assets/image (23).png>)
