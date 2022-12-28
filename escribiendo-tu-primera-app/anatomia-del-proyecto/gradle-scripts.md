---
description: Archivos dentro del directorio Gradle scripts.
---

# Gradle scripts

{% embed url="https://developer.android.com/studio/build" %}
Fuente: developer.android.com
{% endembed %}

## ¿QUE ES GRADLE?

> Android Studio usa [Gradle](http://www.gradle.org/), un paquete de herramientas de compilación avanzadas, para automatizar y administrar el proceso de compilación y, al mismo tiempo, definir configuraciones de compilación personalizadas y flexibles.

En resumen, Gradle es el elemento que se encarga de la construcción de la aplicación.&#x20;

Para modificar la configuración de compilación debemos modificar los archivos `settings.gradle` o `gradle.build`. Estos archivos de texto sin formato usan lenguaje específico de dominio (DSL) para describir y manipular la lógica de compilación mediante [Groovy](http://groovy-lang.org/), un lenguaje dinámico para la máquina virtual Java (JVM), o una [secuencia de comandos de Kotlin](https://kotlinlang.org/docs/command-line.html#run-scripts), que es una variante del lenguaje Kotlin.

## ARCHIVOS DE CONFIGURACIÓN

### settings.gradle (Archivo de configuración de Gradle)

Se encuentra en el directorio raíz del proyecto.&#x20;

Este archivo de configuración define la configuración del repositorio a nivel del proyecto y le informa a Gradle qué módulos debe incluir al compilar tu app. Los proyectos con varios módulos deben especificar cada módulo que formará parte de la compilación final.

Su estructura es la siguiente:

```kotlin
pluginManagement {
/*
El bloque pluginManagement {repositories {...}} configura los repositorios que 
gradle utiliza para buscar o descargar los plugins de gradle y sus dependencias.
Gradle viene preconfigurado para dar soporte a los siguientes respositorios
remotos:
    JCenter, Maven Central, and Ivy.
Tambien se pueden utilizar repositorios locales o definir otros repositorios
remotos. 
El código de abajo define los respositorios para buscar las dependencias.
*/
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
    }
}
dependencyResolutionManagement {
/*
El bloque dependencyResolutionManagement {repositories {...}} es donde se 
configuran los repositorios y dependencias utilizados por todos los módulos
en el proyecto, tales como las librerías que utiliza para crear su app.
Sin embargo, se debe configurar las dependencias específicas de cada módulo
en cada archivo build.gradle específico de módulo.
En un archivo vacío se incluyen los repositorios de abajo pero no se incluye
ninguna dependencia. 
*/
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}
rootProject.name = "App de ejemplo"
include ':app'l
```

### gradle.build (Archivo de compilación de nivel superior)

Se encuentra en el directorio raíz del proyecto.&#x20;

De forma predeterminada, el archivo de compilación de nivel superior usa el bloque `plugins` para definir las dependencias de Gradle comunes en todos los módulos del proyecto.&#x20;

Además contiene código para limpiar el directorio de compilación.

Su estructura es:

```kotlin
plugins {
/*
Utilice "apply false" en este archivo para añadir un plugin de Gradle como
dependencia de construcción pero no aplicarla al proyecto actual.
No utilice "apply false" en los subproyectos.
*/
    id("com.android.application") version "7.3.1" apply false
    id("com.android.library") version "7.3.1" apply false
    id("org.jetbrains.kotlin.android") version "1.7.20" apply false
}
```

### gradle.build (Archivo de compilación de nivel módulo)

Se encuentra en cada directorio `project/module/`.&#x20;

Te permite configurar ajustes de compilación para el módulo específico en el que se encuentra.

La configuración de esos ajustes de compilación te permite proporcionar opciones de empaquetado personalizadas, como tipos de compilación y variantes de productos adicionales, y anular las configuraciones en el `manifiesto` de la app o en `build.gradle` de nivel superior.&#x20;

{% hint style="info" %}
Este es el que va a tener las configuraciones personalizadas de nuestra app y el que más vamos a modificar.

Es normal incluso en aplicaciones grandes tener solo un módulo a no ser que queramos personalizar las dependencias de diferentes partes del proyecto. Cosa que no suele pasar.
{% endhint %}

En el siguiente ejemplo se ven algunos ajustes básicos:

```kotlin
/*
La primera sección llama al plugin de Gradle "Android" permitiendo que se 
utilice el bloque "android" más abajo.
*/
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
}
/*
El bloque android es donde se configuran todas las opciones de compilación
específicas de Android.
*/
android {

    /*
    El espacion de nombres de la App se utiliza para acceder a los recursos
    de la App.
    */
    namespace = "com.example.myapp"
    /*
    La SDK de compilación especifica el nivel de la API de Android que se debe
    utilizar para compilar la App. Esto significa que la App puede utilizar 
    características de ese nivel de API o inferior.
    */
    compileSdk = 33
    /*
    El bloque defaultConfig encapsula las configuraciones por defecto y las 
    entradas para todas las variantes de compilación. 
    Puede sobreescribir atributos de main/AndroidManifest.xml de manera dinámica.
    Puede configurar diferentes valores para diferentes versiones de la App.
    */

    defaultConfig {

        // Identifica el paquete para su publicación
        applicationId = "com.example.myapp"

        // Define el nivel mínimo de API para correr la App.
        minSdk = 21

        // Especifica el nivel de API utilizado para testear.
        targetSdk = 33

        // Define el número de versión de la App.
        versionCode = 1

        // Define el nombre (user-friendly) de la versión de la App.
        versionName = "1.0"
    }
    /*
    En el bloque buildTypes es donde se pueden configurar varios tipos de
    compilaciones. Por defecto se definen dos tipos: debug y lanzamiento.
    El tipo "debug" no se muestra explicitamente en la configuración pero
    incluye herramientas de testeo y está firmado con la clave debug.
    El tipo "lanzamiento" tiene configurado ProGuard y no está firmado por defecto.
    */
    buildTypes {
        /*
        Por defecto, Android Studio configura la construcción de "lanzamiento" con 
        la opción de reducir código activada (utilizando minifyEnabled) y las reglas
        por defecto de ProGuard activas.
        */
        getByName("release") {
            isMinifyEnabled = true
            proguardFiles(
                getDefaultProguardFile("proguard-android.txt"),
                "proguard-rules.pro"
            )
        }
    }
    /*
    El bloque productFlavors permite configurar diferentes tipos de versiones de
    la App. Esto permite anular el bloque defaultConfig con configuraciones
    específicas. Es opcional y no se crean por defecto.
    
    En el ejemplo se crea una versión gratuita y otra de pago. Cada una de ellas
    especifica su propio ID de aplicación para que puedan coexistir en la Google
    Play Store o en el teléfono Android de manera simulanea.
    
    Si quiere declarar product flavors debe declarar tambien sus dimensiones y
    asignar cada flavor a una dimensión.
    */
    flavorDimensions += "tier"
    productFlavors {
        create("free") {
            dimension = "tier"
            applicationId = "com.example.myapp.free"
        }

        create("paid") {
            dimension = "tier"
            applicationId = "com.example.myapp.paid"
        }
    }
}
/*
El bloque de dependencias es la configuración a nivel módulo. Son las 
dependencias que se requieren para construir el módulo en sí.
*/
dependencies {
    implementation(project(":lib"))
    implementation("androidx.appcompat:appcompat:1.5.1")
    implementation(fileTree(mapOf("dir" to "libs", "include" to listOf("*.jar"))))
}
```

### Archivos de propiedades

#### gradle.properties

Aquí puedes configurar ajustes de Gradle para todo el proyecto, como el tamaño máximo de la pila de `daemon de Gradle`.

#### local.properties

Configura las propiedades del entorno local para el sistema de compilación, incluidas las siguientes:

* `ndk.dir`: Ruta de acceso al NDK. Esta propiedad dejó de estar disponible. Las versiones descargadas del NDK se instalan en el directorio `ndk`, dentro del directorio del SDK de Android.
* `sdk.dir`: Ruta de acceso al SDK.
* `cmake.dir`: Ruta de acceso a CMake.
* `ndk.symlinkdir`: En Android Studio 3.5 y versiones posteriores, crea un symlink al NDK que puede ser más corto que la ruta del NDK instalado.
