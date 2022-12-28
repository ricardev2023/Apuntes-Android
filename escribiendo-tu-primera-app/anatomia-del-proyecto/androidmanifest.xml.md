---
description: Explicación del archivo AndroidManifest.xml
---

# AndroidManifest.xml

{% embed url="https://developer.android.com/guide/topics/manifest/manifest-intro" %}
Fuente: developer.android.com
{% endembed %}

## ¿QUE ES ANDROID MANIFEST?

El archivo de manifiesto describe información esencial de tu aplicación para las herramientas de creación de Android, el sistema operativo Android y Google Play.

Todos los proyectos de apps deben tener un archivo `AndroidManifest.xml` (con ese mismo nombre) en la raíz del proyecto.

Entre otras muchas cosas, el manifiesto debe declarar:

* El **nombre del paquete** de la aplicación, que normalmente coincide con el espacio de nombres de tu código.
* Los **componentes** de la aplicación, que incluyen todas las actividades, servicios, receptores de emisiones y proveedores de contenido.&#x20;
* Los **permisos** que necesita la aplicación para acceder a las partes protegidas del sistema o a otras aplicaciones.
* Las funciones de hardware y software que requiere la aplicación y afectan a la **compatibilidad** con dispositivos que pueden instalar la aplicación desde Google Play.

## FUNCIONES DEL ARCHIVO

### Nombre del Paquete

El elemento raíz del archivo de manifiesto requiere un atributo para el nombre del paquete de tu aplicación (que normalmente coincide con la estructura del directorio del proyecto: el espacio de nombres de Java).

Se utiliza `package` como palabra reservada:

```kotlin
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.android.appdeejemplo"
    android:versionCode="1"
    android:versionName="1.0">
```

Mientras compilas tu aplicación en el paquete de aplicación final (APK), las herramientas de compilación de Android utilizan el atributo `package` para dos cosas:

* Aplica este nombre como espacio de nombres para la clase `R.java` generada de tu app (se usa para acceder a los [recursos de la aplicación](https://developer.android.com/guide/topics/resources/overview)).
*   Usa este nombre para resolver cualquier nombre de clase relativo que se declare en el archivo de manifiesto.

    Ejemplo: Con el manifiesto anterior, se resuelve una actividad declarada como `<activity android:name=".MainActivity">` y pasa a ser `com.example.android.appdeejemplo.MainActivity`.

Como tal, el nombre del atributo `package` del manifiesto siempre debe coincidir con el nombre de paquete básico de tu proyecto, en el cual conservas tus actividades y otros tipos de código de la app.

Sin embargo, ten en cuenta que, una vez compilado el APK, el atributo `package` también representa el ID único de tu aplicación. Después de que las herramientas de compilación realizan las tareas anteriores basadas en el nombre `package`, sustituyen el valor `package` por el asignado a la propiedad `applicationId` en el archivo `build.gradle` de tu proyecto (utilizado en los proyectos de Android Studio). Este valor final del atributo `package` debe ser único, ya que es la única forma garantizada de identificar tu aplicación en el sistema y en Google Play.

La distinción entre el nombre `package` en el manifiesto y el objeto `applicationId` en el archivo `build.gradle` puede ser un poco confusa. Sin embargo, si son iguales, no deberás preocuparte.

### Componentes de la aplicación <a href="#components" id="components"></a>

Por cada [componente de app](https://developer.android.com/guide/components/fundamentals#Components) que crees en tu aplicación, deberás declarar un elemento XML correspondiente en el archivo de manifiesto:

* `<activity>` para cada subclase de `Activity`.
* `<service>` para cada subclase de `Service`.
* `<receiver>` para cada subclase de `BroadcastReceiver`.
* `<provider>` para cada subclase de `ContentProvider`.

Si incluyes en subclases cualquiera de estos componentes sin declararlo en el archivo de manifiesto, el sistema no podrá iniciarlo.

El nombre de la subclase debe especificarse con el atributo `name`, utilizando la designación del paquete completo. Por ejemplo, una subclase `Activity` podría declararse de la siguiente manera:

```kotlin
<manifest ... >
    <application ... >
        <activity android:name="com.example.myapp.MainActivity" ... >
        </activity>
    </application>
</manifest>
```

Sin embargo, se pueden utilizar rutas relativas empezando con un punto:

```
<manifest package="com.example.myapp" ... >
    <application ... >
        <activity android:name=".MainActivity" ... >
            ...
        </activity>
    </application>
</manifest>
```

Si algunos componentes de tu aplicación están en subpaquetes (como en `com.example.myapp.purchases`), el valor `name` debe agregar los nombres de los subpaquetes que faltan (como `".purchases.PayActivity"`).

#### **Filtros de intents**

Las actividades, servicios y receptores de emisión de una aplicación se activan mediante _`intents`_. Una **intent** es un mensaje definido por un objeto `Intent` que describe una acción que se realizará, incluidos los datos sobre los que se debe actuar, la categoría del componente que debe realizar la acción y otras instrucciones.

Cuando una aplicación emite una **intent** al sistema, el sistema localiza un componente de la aplicación que puede manejar la **intent** según las declaraciones del _**filtro de intent**_ en el archivo de manifiesto de cada aplicación.&#x20;

El sistema lanza una instancia del componente correspondiente y pasa el objeto `Intent` a ese componente. Si más de una aplicación puede manejar la intent, entonces el usuario puede seleccionar qué aplicación usar.

Un componente de aplicación puede tener cualquier número de filtros de intent (definidos con el elemento `<intent-filter>`), cada uno de los cuales describe una capacidad diferente de ese componente.

#### **Íconos y etiquetas**

Algunos elementos del manifiesto tienen atributos `icon` y `label` para mostrar un pequeño ícono y una etiqueta de texto, respectivamente, a los usuarios según el componente de aplicación correspondiente.

En cada caso, el ícono y la etiqueta establecidos en un elemento superior se convierten en la configuración predeterminada de `icon` y `label` para todos los elementos inferiores. Por lo tanto, el ícono y la etiqueta establecidos en el elemento `<application>` son el ícono y la etiqueta predeterminados para cada componente de la aplicación (como todas las actividades).

El ícono y la etiqueta que se establecen en el `<intent-filter>` de un componente se muestran al usuario siempre que ese componente se presenta como una opción para cumplir una **intent**.&#x20;

De forma predeterminada, este ícono se hereda de cualquier ícono que se declare para el componente superior (ya sea el elemento `<activity>` o `<application>`), pero es posible que quieras cambiar el ícono por un **filtro de intent** si proporcionas una acción única que te gustaría indicar mejor en el cuadro de diálogo del selector.

### Permisos <a href="#perms" id="perms"></a>

Las aplicaciones de Android deben solicitar **permiso** para acceder a datos del usuario confidenciales (como contactos y SMS) o a determinadas funciones del sistema (como la cámara y el acceso a Internet). Cada permiso se identifica con una etiqueta única. Por ejemplo, en el manifiesto de una app que necesite enviar mensajes SMS debe incluirse esta línea:

```kotlin
<manifest ... >
    <uses-permission android:name="android.permission.SEND_SMS"/>
    ...
</manifest>
```

A partir de Android 6.0 (nivel de API 23), el usuario puede aprobar o rechazar algunos permisos durante el tiempo de ejecución. No obstante, sin importar qué versión de Android admita tu aplicación, debes declarar todas las solicitudes de permisos con un elemento `<uses-permission>` en el manifiesto. Si se otorga el permiso, la aplicación puede usar las funciones protegidas. De lo contrario, los intentos de acceder a esas funciones fallarán.

### Compatibilidad con dispositivos <a href="#compatibility" id="compatibility"></a>

En el archivo de manifiesto, también puedes declarar qué tipos de funciones de hardware y software requiere tu aplicación y, por lo tanto, qué tipos de dispositivos admite. Google Play Store no permite que tu app se instale en dispositivos que no tienen las funciones o la versión del sistema que requiere tu app.

Hay varias etiquetas de manifiesto que definen qué dispositivos son compatibles con tu app. A continuación, se incluyen algunas de las más comunes.

#### **\<uses-feature>**

El elemento `<uses-feature>` te permite declarar funciones de hardware y software que necesita tu app. Por ejemplo, si tu aplicación no puede funcionar un dispositivo que no tiene un sensor de brújula, puedes declarar el sensor como obligatorio con la siguiente etiqueta de manifiesto:

```kotlin
<manifest ... >
    <uses-feature android:name="android.hardware.sensor.compass"
                  android:required="true" />
    ...
</manifest>
```

#### **\<uses-sdk>**

Cada versión siguiente de la plataforma suele agregar nuevas API que no están disponibles en la versión anterior. Para indiciar la versión mínima con la que tu app es compatible, tu manifiesto debe incluir la etiqueta `<uses-sdk>` y su atributo `minSdkVersion`.

Sin embargo, ten en cuenta que los atributos del elemento `<uses-sdk>` son anulados por las propiedades correspondientes del archivo `build.gradle`. Por lo tanto, si usas Android Studio, debes especificar los valores `minSdkVersion` y `targetSdkVersion` allí como ya vimos en el apartado de [**Gradle scripts**](gradle-scripts.md#gradle.build-archivo-de-compilacion-de-nivel-modulo):

<pre class="language-kotlin"><code class="lang-kotlin"><strong>// gradle.build (Archivo de compilación de nivel módulo)
</strong><strong>
</strong><strong>android {
</strong>  defaultConfig {
    applicationId 'com.example.myapp'

    // Defines the minimum API level required to run the app.
    minSdkVersion 15

    // Specifies the API level used to test the app.
    targetSdkVersion 28

    ...
  }
}
</code></pre>

## OTRA INFORMACIÓN

En el enlace del principio se puede encontrar más información sobre el manifiesto.
