---
description: Explicación del concepto de VideoView.
---

# VideoView

{% embed url="https://developer.android.com/reference/android/widget/VideoView" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `SurfaceView`.

Reproduce un archivo de video.&#x20;

* Una VideoView puede reproducir videos desde varias fuentes, desde resources hasta content providers.&#x20;
* Se encarga de controlar el tamaño del video, por lo que puede ser utilizada en cualquier tipo de layout.
* Además ofrece opciones como escalado y tinte.

### Información técnica

{% hint style="info" %}
Esta información aparece en el enlace de arriba como información util.

En esta guía no la vamos a utilizar, sin embargo, se la dejo traducida para facilitarle la vida.
{% endhint %}

#### Estado

Una `VideoView` no mantiene su estado cuando pasa a segundo plano, en particular no almacena:

* Posición de la reproducción actual.
* Estado de la reproducción actual.
* Pistas seleccionadas.
* Subtitulos añadidos.

Las aplicaciones deben almacenar y luego recuperar estos datos en su propia [`Activity.onSaveInstanceState(Bundle)`](https://developer.android.com/reference/android/app/Activity#onSaveInstanceState\(android.os.Bundle\)) y [`Activity.onRestoreInstanceState(Bundle)`](https://developer.android.com/reference/android/app/Activity#onRestoreInstanceState\(android.os.Bundle\)).

#### Audio

Tambien hay que tener en cuenta que el id de la sesión de audio (que se obtiene con [`getAudioSessionId()`](https://developer.android.com/reference/android/widget/VideoView#getAudioSessionId\(\))) puede cambiar después de restaurar el `VideoView`.

Por defecto, `VideoView` solicita el foco de audio con [`AudioManager#AUDIOFOCUS_GAIN`](https://developer.android.com/reference/android/media/AudioManager#AUDIOFOCUS\_GAIN). Para cambiar este comportamiento debe utilizar [`setAudioFocusRequest(int)`](https://developer.android.com/reference/android/widget/VideoView#setAudioFocusRequest\(int\)).

Los atributos de audio utilizados por defecto son [`AudioAttributes#USAGE_MEDIA`](https://developer.android.com/reference/android/media/AudioAttributes#USAGE\_MEDIA) y [`AudioAttributes#CONTENT_TYPE_MOVIE`](https://developer.android.com/reference/android/media/AudioAttributes#CONTENT\_TYPE\_MOVIE). Para modificarlos utilice [`setAudioAttributes(android.media.AudioAttributes)`](https://developer.android.com/reference/android/widget/VideoView#setAudioAttributes\(android.media.AudioAttributes\)).

## USO DESDE XML

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
        <VideoView
            android:id="@+id/vvUrl"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            android:layout_marginBottom="10dp"/>

        <View
            android:id="@+id/divider"
            android:layout_width="match_parent"
            android:layout_height="10dp"
            android:background="?android:attr/listDivider" />

        <VideoView
            android:id="@+id/vvProject"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="100dp"/>
    </LinearLayout>
</ScrollView>
```
{% endcode %}

&#x20;                                               ![](<../../../../.gitbook/assets/image (8).png>)

{% hint style="danger" %}
No se muestra nada en las VideoViews por que es necesario configurar la VideoView antes de poder hacer uso de ella.
{% endhint %}

## CONFIGURACIÓN

Vamos a diferenciar la configuración entre la reproducción de un video local y uno online.

### Video Online

#### Solicitar permiso de Internet

En primer lugar se debe ir al `AndroidManifest.xml` y solicitar permisos para el uso de Internet. Esto se hace con la siguiente línea de código:

```xml
<manifest>
....
<uses-permission android:name="android.permission.INTERNET" />

<application>
.....
```

#### Código en kotlin

Después de eso hay que realizar varios pasos en `MainActivity.kt`, concretamente dentro del `OnCreate`:

* Primero creo una variable del tipo VideoView y la relaciono con el id de mi View:

```kotlin
val vvUrl: VideoView = findViewById(R.id.vvUrl)
```

* Después creo una instancia de la clase `MediaController()` con el contexto definido en su constructor:

```kotlin
val mcUrl = MediaController(this)
```

* Ahora relacionamos nuestro `MediaController` con nuestra `View` y viceversa:

```kotlin
mcUrl.setAnchorView(vvUrl)
vvUrl.setMediaController(mcUrl)
```

* Por último le indicamos a nuestra VideoView el recurso que queremos reproducir:

```kotlin
vvUrl.setVideoPath("https://mivideodeejemplo.com")
```

&#x20;                                                 ![](<../../../../.gitbook/assets/image (89).png>)

### Video Local

Para reproducir un recurso local los pasos son los mismos, lo único que cambia es el `VideoPath` del final:

```kotlin
val vvProject: VideoView = findViewById(R.id.vvProject)
val mcProject = MediaController(this)
val path = "android.resource://" + packageName + "/" + R.raw.vid_ejemplo

mcProject.setAnchorView(vvProject)
vvProject.setMediaController(mcProject)

vvProject.setVideoURI(Uri.parse(path))
```

&#x20;                                              ![](<../../../../.gitbook/assets/image (30).png>)

## CODIGO

Con todo hecho, el código nos quedaría de la siguiente manera:

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
        <VideoView
            android:id="@+id/vvUrl"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            android:layout_marginBottom="10dp"/>

        <View
            android:id="@+id/divider"
            android:layout_width="match_parent"
            android:layout_height="10dp"
            android:background="?android:attr/listDivider" />

        <VideoView
            android:id="@+id/vvProject"
            android:layout_width="match_parent"
            android:layout_height="400dp"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="100dp"/>
    </LinearLayout>
</ScrollView>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import android.net.Uri
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.MediaController
import android.widget.VideoView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val vvUrl: VideoView = findViewById(R.id.vvUrl)
        val mcUrl = MediaController(this)

        mcUrl.setAnchorView(vvUrl)
        vvUrl.setMediaController(mcUrl)

        vvUrl.setVideoPath("https://mivideodeejemplo.com")

        val vvProject: VideoView = findViewById(R.id.vvProject)
        val mcProject = MediaController(this)
        val path = "android.resource://" + packageName + "/" + R.raw.vid_ejemplo

        mcProject.setAnchorView(vvProject)
        vvProject.setMediaController(mcProject)

        vvProject.setVideoURI(Uri.parse(path))

    }
}
```
{% endcode %}
