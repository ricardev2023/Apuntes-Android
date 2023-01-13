---
description: Explicación de las Activities y su ciclo de vida.
---

# Activities

Las activities son cada una de las "pantallas" que componen una aplicación de Android.

{% embed url="https://developer.android.com/guide/components/activities/intro-activities?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## PARADIGMA DE PROGRAMACIÓN MOVIL

La programación de Aplicaciones móviles difiere de las aplicaciones de escritorio desde el punto de vista de que no siempre se accede a la aplicación desde el mismo punto de inicio.

{% hint style="info" %}
**Por ejemplo:**

Si utilizase su aplicación de correo electrónico desde el icono de aplicación le llevaría a su buzón de correos recibidos.&#x20;

Sin embargo si la inicia desde una notificación push que le indica que tiene un correo nuevo se iniciaría directamente la pantalla de lectura de dicho correo.&#x20;

O incluso si utiliza un enlace para mandar un correo, se iniciaría directamente la pantalla de escribir un correo.
{% endhint %}

Para facilitar ese comportamiento, se implementaron las **activities** y su comportamiento, en vez de basarse en el paradigma funcional e iniciarse con una función main(), se basa en la programación orientada a objetos, convirtiendo cada **Activity** en una subclase de la clase **Activity** y basandose en una estructura de **ciclo de vida**.

## ¿QUE ES UNA ACTIVIDAD?

Una actividad proporciona la ventana en la que la app dibuja su Interfaz de Usuario (IU). Por lo general, esta ventana llena la pantalla, pero puede ser más pequeña y flotar sobre otras ventanas.&#x20;

<mark style="color:red;">Generalmente, una actividad implementa una pantalla en una app.</mark>

### Ejemplo sencillo

Una Aplicación sencilla que haga un examen tipo test tendría por ejemplo las siguientes actividades:

* **MainActivity**: Es la actividad por defecto. Por convenio es la que se inicia al iniciar la aplicación desde el icono de la aplicación. En este caso sería la pantalla de título del examen.
* **AboutActivity**: Sería la pantalla en la que se muestran las instrucciones del examen.
* **GameActivity**: En esta actividad se mostrarían las preguntas con sus posibles respuestas.
* **GameWonActivity**: Cuando se aprueba el examen se salta a esta actividad.
* **GameOverActivity**: Cuando no se aprueba el examen se salta a esta actividad.

{% hint style="warning" %}
Si quiere usar actividades en tu app, debe registrar información sobre estas en el manifiesto de la app y administrar los ciclos de vida de las actividades de manera apropiada.
{% endhint %}

## ACTIVIDADES EN MANIFIESTO

Para declarar tu actividad, abre tu archivo de manifiesto y agrega el elemento `<activity>` como objeto secundario del elemento `<application>`.

```kotlin
 <manifest /*...*/ >
      <application /*...*/ >
          <activity
            android:name=".MainActivity"
            android:configChanges="orientation|screenSize|smallestScreenSize|screenLayout">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
      </application /*...*/ >
      /*...*/
    </manifest >
```

## CICLO DE VIDA

{% embed url="https://developer.android.com/guide/components/activities/activity-lifecycle?hl=es" %}
Fuente: developer.android
{% endembed %}

Cuando un usuario navega por tu app, sale de ella y vuelve a entrar, las instancias de `Activity` de tu app pasan por diferentes estados de su ciclo de vida. La clase `Activity` proporciona una serie de devoluciones de llamada que permiten a la actividad saber que cambió un estado.

Dentro de los métodos de devolución de llamada de ciclo de vida, puedes declarar el comportamiento que tendrá tu actividad cuando el usuario la abandone y la reanude.&#x20;

{% hint style="info" %}
**Por ejemplo**

Si creas un reproductor de video en streaming, puedes pausar el video y cancelar la conexión de red cuando el usuario cambia a otra app.&#x20;

Cuando el usuario vuelve, puedes volver a establecer la conexión con la red y permitir que el usuario reanude el video desde el mismo punto.&#x20;
{% endhint %}

En otras palabras, cada devolución de llamada te permite realizar un trabajo específico que es apropiado para un cambio de estado en particular. Hacer el trabajo preciso en el momento adecuado y administrar las transiciones correctamente hace que tu app sea más sólida y eficiente.&#x20;

Por ejemplo, una buena implementación de las devoluciones de llamada de un ciclo de vida puede ayudar a garantizar que tu app:

* No falle si el usuario recibe una llamada telefónica o cambia a otra app mientras usa la tuya.
* No consuma recursos valiosos del sistema cuando el usuario no la use de forma activa.
* No pierda el progreso del usuario si este abandona tu app y regresa a ella posteriormente.
* No falle ni pierda el progreso del usuario cuando se gire la pantalla entre la orientación horizontal y la vertical.

<figure><img src="../../.gitbook/assets/activity_lifecycle.png" alt=""><figcaption><p>Fuente: developer.android</p></figcaption></figure>

Como podemos ver en la imagen anterior existen varios estados en el ciclo de vida de una aplicación:

### onCreate() <a href="#oncreate" id="oncreate"></a>

Debes implementar esta devolución de llamada, que se activa cuando el sistema crea la actividad por primera vez. Cuando se crea la actividad, esta entra en el estado _Created_.&#x20;

En el método `onCreate()`, ejecutas la lógica de arranque básica de la aplicación que debe ocurrir una sola vez en toda la vida de la actividad.&#x20;

Principalmente, este es el momento en el que debes llamar a `setContentView()` para definir el diseño de la interfaz de usuario de tu actividad.

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

Cuando `onCreate()` finaliza, la siguiente devolución de llamada siempre es `onStart()`.

### onStart() <a href="#onstart" id="onstart"></a>

Cuando se cierra `onCreate()`, la actividad pasa al estado Iniciada y se vuelve visible para el usuario.&#x20;

Esta devolución de llamada contiene los preparativos finales de la actividad para pasar al primer plano y convertirse en interactiva.

{% hint style="info" %}
Durante onStart() la aplicación todavía no es visible para el usuario.
{% endhint %}

{% hint style="warning" %}
Cuando la actividad pasa de estar en segundo plano a la parte superior de la pila, vuelve a pasar por este estado.

Es decir, de `onRestart()` pasa a `onStart()`.
{% endhint %}

### onResume() <a href="#onresume" id="onresume"></a>

El sistema invoca esta devolución de llamada justo antes de que la actividad comience a interactuar con el usuario.&#x20;

En este punto, la actividad es la primera de la pila de actividades y captura todo lo que el usuario ingresa. La mayor parte de la funcionalidad principal de una app se implementa en el método `onResume()`.

### onPause() <a href="#onpause" id="onpause"></a>

El sistema llama a `onPause()` cuando la actividad pierde el foco y pasa al estado Detenida. Este estado se produce, por ejemplo, cuando el usuario presiona el botón Atrás o Recientes. Cuando el sistema llama a `onPause()` para tu actividad, significa que esta aún está parcialmente visible, pero, a menudo, indica que el usuario está saliendo de la actividad y que esta pronto pasará al estado Detenida o Reanudada.

Una actividad en estado Detenida puede continuar con la actualización de la IU si el usuario espera que esta acción ocurra. Entre los ejemplos de tal actividad, se incluye mostrar una pantalla de mapa de navegación o la reproducción de un reproductor multimedia. Incluso si estas actividades pierden el foco, el usuario espera que su IU continúe actualizándose.

{% hint style="danger" %}
**No** debe utilizar `onPause()` para guardar datos de la aplicación o del usuario, realizar llamadas de red o ejecutar transacciones de base de datos.
{% endhint %}

Una vez que finalice la ejecución de `onPause()`, la siguiente devolución de llamada será `onStop()` u `onResume()`, dependiendo de lo que ocurra cuando la actividad pase al estado Detenida.

### onStop() <a href="#onstop" id="onstop"></a>

El sistema llama a `onStop()` cuando la actividad ya no es visible para el usuario, lo cual puede ocurrir porque se está eliminando la actividad, porque se inicia una nueva o porque una ya existente pasa al estado Reanudada y cubre la actividad que se detuvo. En todos estos casos, la actividad detenida ya no está visible en absoluto.

La siguiente devolución de llamada que el sistema invoca puede ser `onRestart()` (si la actividad vuelve a interactuar con el usuario) u `onDestroy()` (si esta actividad finaliza por completo).

### onRestart() <a href="#onrestart" id="onrestart"></a>

El sistema invoca esta devolución de llamada cuando una actividad en estado Detenida está por volver a iniciarse. `onRestart()` restaura el estado de la actividad desde el momento en que esta se detuvo.

Luego de esta devolución de llamada, siempre sigue `onStart()`.

### onDestroy() <a href="#ondestroy" id="ondestroy"></a>

El sistema invoca esta devolución de llamada antes de que se elimine una actividad.

Esta devolución de llamada es la última que recibe la actividad. `onDestroy()` suele implementarse a fin de garantizar que todos los recursos de una actividad se liberen cuando esta, o el proceso que la contiene, se elimina.
