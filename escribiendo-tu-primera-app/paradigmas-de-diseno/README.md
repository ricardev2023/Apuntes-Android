---
description: >-
  En esta página se van a explicar los diferentes paradigmas de diseño que han
  existido durante la vida de Android.
---

# Paradigmas de diseño

## INTRODUCCIÓN

Al momento de escribir esta página nos encontramos a principios de 2023. Esto implica que ya se han dado muchos cambios importantes en la forma en que se programa con Android.

Han existido multitud de **estándares de diseño** hasta llegar al que se encuentra ahora en vigor que es **Material Design 3**.

Sin embargo, no solo han cambiado los estándares de diseño sino que incluso en 2021 vió la luz un nuevo **paradigma de diseño** llamado **Jetpack Compose**.

**Jetpack Compose esta llamado a acabar con el antiguo paradigma basado en Views**, sin embargo aún existen multitud de empresas que siguen utilizando el paradigma anterior.

## HISTORIA DE LOS ESTÁNDARES DE DISEÑO

### Nacimiento de Android

El **23 de Septiembre de 2008** se lanza la primera versión estable de **Android 1.0**. A estas alturas, el diseño de las Apps de Google era muy parecido al lejano oeste, apostando mucho por el **esqueumorfismo**, es decir, en imitar la forma y el comportamiento de los elementos reales que se estaban copiando. Por ejemplo, una brújula.

### Diseño Holo

Con la llegada de **Android 3.0 Honeycomb** en febrero del 2011 llegaba el primer estándar de diseño. Esta actualización fue lanzada exclusivamente para tablets pero ya introdujo mejoras como la System Bar.

El diseño Holo se asienta con la llegada de **Android 4.0 Ice Cream Sandwitch** y aguantó hasta **2014**.

### Material Design

Con la salida de **Android 5.0 Lollipop en 2014**, se incluyó la presentación del **nuevo estándar de diseño: Material Design**.

Se basaba en interfaces minimalistas con colores planos donde la estrella eran las tarjetas, los botones flotantes y los menús de la hamburguesa ☰, alejándose del diseño futurista que había traído el diseño Holo.

Material Design no paró de desarrollarse en la dirección que ahora conocemos. En 2016 incluyó la barra inferior que ahora todos conocemos.

### Material Theming

En 2018 con la salida de **Android 9.0 Pie** se presenta la segunda versión de Material Design. Material Theming o **Material Design 2**.&#x20;

Material Theming le da una vuelta de tuerca a Material Design, otorgándole más expresividad mediante el uso de "temas" (de ahí el _Theming_ del nombre), compuestos por por colores, tipografías y, sobre todo, formas, algo que no había sido explotado demasiado en el Material Design original.

Google no tardó en aplicar este nuevo estándar a sus aplicaciones por lo que se convirtió en una obligación para los programadores.

### Material You

En 2021 con la salida de **Android 12**, tras la pandemia, Google presenta Material You, o lo que es lo mismo **Material Design 3**.

En este caso mucho más orientado a la personalización por parte del usuario. Aprovechando los temas que habían explotado en Material Theming, ahora el sistema podía extraer una paleta de colores del tema del dispositivo y utilizarla para la App.

Se le da más importancia tambien al uso de animaciones y transiciones.

## MATERIAL DESIGN 3

{% embed url="https://m3.material.io" %}
Fuente: Material Desgin
{% endembed %}

{% embed url="https://material.io/blog/migrating-material-3" %}
Fuente: Material Desgin
{% endembed %}

## PARADIGMAS DE DISEÑO

{% embed url="https://www2.deloitte.com/es/es/blog/todo-tecnologia/2021/programacion-imperativa-vs-declarativa-google-jetpack-compose.html" %}
Fuente: deloitte
{% endembed %}

### Android View

Desde sus inicios, la composición de la interfaz de usuario en Android está basada en la clase _View_. El bloque básico del que heredan todos los componentes de interfaz de usuario. Un objeto _View_ posee una forma rectangular y es responsable de su pintado y del manejo de eventos. A su vez es la clase base de _ViewGroup_, el elemento básico tipo contenedor (los conocidos _Layouts_) que se usa para albergar otros componentes y widgets (elementos de interfaz: botones, campos de texto, listados, etc.).

Para actualizar la interfaz de usuario en el modelo View, recorremos el árbol de vistas con funciones como _findViewById()_ y así poder cambiar los nodos mediante llamadas a métodos como _button.setText(String)_, _container.addChild(View)_ o _img.setImageBitmap(Bitmap)_. Esos métodos cambian el estado interno de la vista.

Hacer cambios de forma manual en una vista es una fuente de errores. Si un dato se procesa en varios lugares, podemos olvidar refrescar alguna de las vistas que lo muestran. También es posible crear estados ilegales, en los que dos actualizaciones entren en conflicto. Por ejemplo, una actualización podría intentar establecer un valor para un nodo que se acaba de quitar de la IU. Por lo general, la complejidad del mantenimiento de software aumenta con la cantidad de vistas que deben actualizarse.

### Jetpack Compose

n el enfoque declarativo de Compose, los widgets no exponen funciones para cambiar de estado. De hecho, los widgets no se exponen como objetos. Para actualizar la IU, se llama a la misma función que admite composición con diferentes argumentos. Eso facilita la asignación de estado a los patrones arquitectónicos. Luego, las funciones que admiten composición son responsables de transformar el estado actual de la aplicación en una IU cada vez que se actualizan los datos observables.

Con Compose, ya no se usará el elemento clásico de interfaz “View”. La unidad básica se llama “Composable” y no es una clase, es una función:

```kotlin
@Composable
fun HelloText(){
               Text(“Hello”)
}
```

Una gran diferencia en Compose es que usa modificadores en vez de los atributos que poseen los elementos View:

```kotlin
TextView(Context context, AttributeSet attrs, int defStyleAttr)
```

Aparte del listado de atributos interno de la vista, hay otros como el ancho o el alto que son externos y necesitan código aparte para ajustarlos. Además, hay un alto acoplamiento con el objeto `context`.

En cambio, los modificadores de **Compose** son usados para decorar el elemento, ya sean características internas o externas.

```kotlin
@Composable
fun HelloText() {
    Text(“Hello”, style = TextStyle(color = Color.Red))
    }
```

Una gran ventaja de **Compose** es que la función `Composable` puede recibir cualquier tipo de parámetro, mientras que un elemento _View_ usa un constructor con parámetros fijos.

En cuanto a los **callbacks y listeners**, mientras que en el modelo View hay que conectar los datos y las vistas de forma prácticamente manual, en Compose los atributos y sus cambios van en conjunción con una variable de estado:

```kotlin
val clickedState: MutableState<Boolean> = mutableStateOf(false)
 
TextButton(
            onClick = {
            clickedState.value = ! clickedState.value
            onToggle(clickedState.value)
            })
{ Text(text = if (clickedState.value) "Clicked" else "Not clicked") }
```

Otra ventaja de **Compose** es que no serán necesarios los ficheros xml de configuración de vistas. Con una simple llamada a la función `Composable`, toda la interfaz será creada según las especificaciones indicadas. Aún así, hay formas de hacer convivir los dos modelos, lo cual es una ventaja para poder ir migrando nuestras aplicaciones.
