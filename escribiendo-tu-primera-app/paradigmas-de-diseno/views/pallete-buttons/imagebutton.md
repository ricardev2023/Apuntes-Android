---
description: Explicación del concepto de ImageButton.
---

# ImageButton

{% embed url="https://developer.android.com/reference/android/widget/ImageButton" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `ImageView`.

Muestra un botón con una imagen en vez de un texto que puede ser clicado por el usuario.

Por norma general es igual que un `Button` pero con una imagen en vez de texto, por este motivo, el estilo por defecto que se aplica a la clase `Button` tambien se aplica a la clase `ImageButton`.

La imagen que se muestra se define en el archivo de layout XML con el atributo `android:srcCompat` o en código con el método `setImageResource(int)`.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="30dp"
    android:orientation="vertical">

    <ImageButton
        android:id="@+id/ibtEjemplo"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_car"
        android:backgroundTint="@color/purple_200"/>

</LinearLayout>
```
{% endcode %}

{% code title="MainActivity.kt" %}
```kotlin
package com.example.android.appdeejemplo

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ImageButton
import android.widget.Toast

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val bEjemplo = findViewById<ImageButton>(R.id.ibtEjemplo)
        bEjemplo.setOnClickListener {
            Toast.makeText(this, "Botón Pulsado", Toast.LENGTH_SHORT).show()
        }
    }
}
```
{% endcode %}

![](<../../../../.gitbook/assets/image (60).png>)
