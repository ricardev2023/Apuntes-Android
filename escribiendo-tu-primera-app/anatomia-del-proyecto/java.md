---
description: Explicación del directorio Java.
---

# Java

## ¿QUE ES EL DIRECTORIO JAVA?

En el directorio Java se almacenaran todos los archivos de código de nuestras actividades y los código fuente auxiliar (como por ejemplo archivos de clases).

{% hint style="info" %}
Se llama Java por que tradicionalmente las aplicaciones de Android sólo se podían programar en Java.

Sin embargo, actualmente esta es la carpeta que almacena el código fuente sea en lenguaje Java o en Kotlin.
{% endhint %}

Podemos encontrar tres carpetas dentro del directorio:

* `com.example.android.appdeejemplo` -> En esta subcarpeta es en la que encontramos las actividades. En un proyecto recien creado tendremos solo la `MainActivity.kt`:

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

* `com.example.android.appdeejemplo (androidTest)` -> Son los test instrumentalizados.
* `com.example.android.appdeejemplo (Test)` -> Son los test unitarios.

{% embed url="https://developer.android.com/studio/test/test-in-android-studio?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## JAVA (GENERATED)

Es un directorio que se genera automáticamente al construir la App en el compilador. Contiene la configuración de la construcción:

```kotlin
/**
 * BuildConfig.kt
 * Automatically generated file. DO NOT MODIFY
 */
package com.example.android.appdeejemplo;

public final class BuildConfig {
  public static final boolean DEBUG = Boolean.parseBoolean("true");
  public static final String APPLICATION_ID = "com.example.android.appdeejemplo";
  public static final String BUILD_TYPE = "debug";
  public static final int VERSION_CODE = 1;
  public static final String VERSION_NAME = "1.0";
}
```
