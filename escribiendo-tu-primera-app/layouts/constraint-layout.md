---
description: Explicación del concepto de Constraint Layout
---

# Constraint Layout

{% embed url="https://developer.android.com/reference/androidx/constraintlayout/widget/ConstraintLayout" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/training/constraint-layout?hl=es-419#constrain-chain" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Hereda de `ViewGroup`.

Es un **ViewGroup** que permite posicionar y dimensionar widgets de una manera flexible.

Es similar a `RelativeLayout` en cuanto a que se presentan todas las vistas de acuerdo con las relaciones entre las vistas del mismo nivel y el diseño de nivel superior, pero es más flexible que `RelativeLayout` y más fácil de usar con el editor de diseño de Android Studio.

{% hint style="info" %}
Google recomienda el uso de este ViewGroup por encima del resto.
{% endhint %}

En la actualidad hay varios tipos de constraints (restricciones) que se pueden utilizar:

* Posicionamiento relativo
* Márgenes
* Centrar posición en diferentes ejes
* Posición circular
* Comportamiento de visibilidad
* Restricciones de dimensiones
* Cadenas
* Objetos virtuales de ayuda (helpers)
* Optimizadores

## USO DESDE XML

Cuando se crea una nueva vista, por defecto el archivo de Layout se crea sobre la base de un Constraint Layout.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ConstraintLayoutActivity">

</androidx.constraintlayout.widget.ConstraintLayout>
```
{% endcode %}

## ATRIBUTOS

{% embed url="https://developer.android.com/reference/androidx/constraintlayout/widget/ConstraintLayout.LayoutParams" %}
Fuente: developer.android
{% endembed %}

Los atributos más importantes de un Relative Layout son los que se muestran en el enlace superior. Estos son los atributos de la clase **ConstraintLayout.LayoutParams** y son fundamentales para indicar donde se posicionan las **Views** dentro del **Layout**.

{% hint style="info" %}
Lo que se muestra a continuación es copiado y traducido de la guía de desarrolladores de Android. Se puede encontrar en el siguiente [enlace](https://developer.android.com/reference/androidx/constraintlayout/widget/ConstraintLayout#developer-guide).
{% endhint %}

### Posición relativa <a href="#relative-positioning" id="relative-positioning"></a>

El posicionamiento relativo es uno de los bloques de construcción básico para crear Layouts en Constraint Layout. Estas restricciones permiten posicionar un Widget en referencia a otro.

Estas restricciones pueden ser:

* En el eje X -> izquierda, derecha, inicio y fin (left, right, start and end sides)
* En el eje Y -> arriba abajo y baseline (top, bottom sides and text baseline)

El concepto general es posicionar un lado del Wodget con respecto a otro lado de otro Widget.

Por ejemplo, para pomer el botón B a la derecha del botón A:

```xml
<Button 
android:id="@+id/buttonA"/>
<Button 
android:id="@+id/buttonB"
app:layout_constraintLeft_toRightOf="@+id/buttonA"/>
        
```

A continuación se muestra una lista de las posibles restricciones en cuanto a posición relativa:

* `layout_constraintLeft_toLeftOf`
* `layout_constraintLeft_toRightOf`
* `layout_constraintRight_toLeftOf`
* `layout_constraintRight_toRightOf`
* `layout_constraintTop_toTopOf`
* `layout_constraintTop_toBottomOf`
* `layout_constraintBottom_toTopOf`
* `layout_constraintBottom_toBottomOf`
* `layout_constraintBaseline_toBaselineOf`
* `layout_constraintStart_toEndOf`
* `layout_constraintStart_toStartOf`
* `layout_constraintEnd_toStartOf`
* `layout_constraintEnd_toEndOf`

Todas las anteriores toman como referencia el atributo `id` de otro Widget o el padre (`parent`) que hará referencia al contenedor padre.

### Márgenes <a href="#margins" id="margins"></a>

Si los márgenes laterales son utilizados, éstos se aplicarán a las restricciones correspondientes si existen. Los márgenes habituales del Layout son los utilizados para estas restricciones:

* `android:layout_marginStart`
* `android:layout_marginEnd`
* `android:layout_marginLeft`
* `android:layout_marginTop`
* `android:layout_marginRight`
* `android:layout_marginBottom`
* `layout_marginBaseline`

Tenga en cuenta que los márgenes solo pueden ser positivos o iguales a cero y deben contener unidad de medida.

### Márgenes conectados a Widgets GONE <a href="#margins-when-connected-to-a-gone-widget" id="margins-when-connected-to-a-gone-widget"></a>

Cuando la visibilidad del objetivo de una restricción es `View.GONE`, se puede indicar un valor diferente de margen para estas ocasiones.

* `layout_goneMarginStart`
* `layout_goneMarginEnd`
* `layout_goneMarginLeft`
* `layout_goneMarginTop`
* `layout_goneMarginRight`
* `layout_goneMarginBottom`
* `layout_goneMarginBaseline`

### Centrar posiciones y desvíos <a href="#centering-positioning-and-bias" id="centering-positioning-and-bias"></a>

Un aspecto muy útil de Constraint Layout es como se enfrenta a restricciones "imposibles".&#x20;

Si yo le pido a un botón que se pegue al lado derecho del padre así como al lado izquierdo, a no ser que el Layout sea de la misma anchura que el botón, estas restricciones actuarán como fuerzas contrapuestas que centrarán el botón en el eje X.

Esto aplica de la misma manera desde el punto de vista vertical.

### Desvios (bias)

Lo habitual en el caso anterior es centrar el Widget, sin embargo, el comportamiento anterior se puede modificar favoreciendo que se aproxime más a un lado o al otro utilizando los atributos bias:

* `layout_constraintHorizontal_bias`
* `layout_constraintVertical_bias`

Utilizando bias se pueden construir UIs que se adapten mejor a diferentes tamaños de pantallas.

### Posicionamiento Circular <a href="#circular-positioning-added-in-1.1" id="circular-positioning-added-in-1.1"></a>

{% hint style="info" %}
Añadido en 1.1
{% endhint %}

Se puede restringir el centro de un Widget en relación con el centro de otro, utilizando un ángulo y una distancia. Esto permite colocar widgets en un circulo.

Los atributos utilizados son los siguientes:&#x20;

* `layout_constraintCircle` -> Referencia el id de otro Widget
* `layout_constraintCircleRadius` -> La distancia entre centros de Widgets.
* `layout_constraintCircleAngle` -> El ángulo en el que debe estar el widget (en grados de 0 a 360).

### Comportamiento de Visibilidad <a href="#visibility-behavior" id="visibility-behavior"></a>

**Constraint Layout** tiene una forma específica de gestionar los Widgets marcados como `View.GONE`.

Los Widgets `GONE`, como es usual, no se muestran en pantalla aunque si que forman parte del Layout en sí con una distinción importante:

* Sus dimensiones van a ser consideradas cero (como si de un punto se tratara).
* Si tienen restricciones a otros widgets serán respetadas, sin embargo, los márgenes serán igual a cero.

Este comportamiento permite crear Layouts en los que se puede marcar temporalmente widgets como `GONE` sin romper el Layout, cosa que puede ser especialmente útil para hacer animaciones sencillas.

### Restricciones de dimensiones  <a href="#dimensions-constraints" id="dimensions-constraints"></a>

#### Dimensiones mínimas en Constraint Layout

Se pueden definir dimensiones minimas y máximas para el propio **Constraint Layout**:

* `android:minWidth`&#x20;
* `android:minHeight`&#x20;
* `android:maxWidth`&#x20;
* `android:maxHeight`

Estas dimensiones serán utilizadas cuando las dimensiones de **Constraint Layout** se fijan a `WRAP-CONTENT`.&#x20;

#### Restricciones de dimensiones de Widgets

Las dimensiones de los Widgets puesden especificarse con `android:layout_width` y `android:layout_height` de tres maneras diferentes:

* Utilizando unas dimensiones específicas.
* Utilizando `WRAP_CONTENT`.
* Utilizando 0dp que equivale a `MATCH_CONSTRAINT`.

Las dos primeras funcionan igual que en el resto de Layouts.

La última, en cambio, cambiará el tamaño del Widget para cumplir con las limitaciones que están definidas.

{% hint style="danger" %}
**IMPORTANTE**

`MATCH_PARENT` no es recomendable para Widgets contenidos en ConstraintLayout.&#x20;

El mismo comportamiento se puede conseguir con `MATCH_CONSTRAINT` definiendo las restricciones con respecto a los límites de parent.
{% endhint %}

#### WRAP\_CONTENT : reforzando restricciones

{% hint style="info" %}
Añadido en 1.1
{% endhint %}

Si una dimensión está marcada como WRAP\_CONTENT, antes de la versión 1.1 se trataba como una dimensión literal, es decir, las restricciones no iban a limitar las dimensiones resultantes.

A partir de la versión 1.1 se introducen los siguientes atributos con el fin de reforzar las restricciones:

* `app:layout_constrainedWidth="true|false"`
* `app:layout_constrainedHeight="true|false"`

#### MATCH\_CONSTRAINT: dimensiones&#x20;

{% hint style="info" %}
Añadido en 1.1
{% endhint %}

Cuando una dimensión está marcada como MATCH\_CONSTRAINT, el comportamiento por defecto es que el tamaño resultante ocupe todo el espacio disponible. Sin embargo, existen algunos modificadores extra:

* `layout_constraintWidth_min` y `layout_constraintHeight_min`  -> marca el mínimo tamaño para esta dimensión.
* `layout_constraintWidth_max` y `layout_constraintHeight_max` -> marca el mínimo tamaño para esta dimensión.
* `layout_constraintWidth_percent` y `layout_constraintHeight_percent` -> marca el tamaño de la dimensión como un porcentaje del padre.

#### Min y Max

El valor indicado para min y max puede ser una **dimensión en dp** o "`wrap`" que utiliza el valor de WRAP\_CONTENT

#### Dimensión en porcentaje

Para usar el porcentaje, necesita definir lo siguiente:

* La dimensión debe estar definida como `MATCH_CONSTRAINT` (0dp)
* Se debe definir una de las siguientes o las dos:
  * `app:layout_constraintWidth_default="percent"`
  * `app:layout_constraintHeight_default="percent"`
* Una vez tengo lo anterior puedo utilizar los siguientes atributos:
  * `layout_constraintWidth_percent`
  * `layout_constraintHeight_percent`

El valor debe encontrase entre 0 y 1.

#### Ratio

Tambien puede definir una dimension de un Widget como un ratio de otro Widget.&#x20;

Para hacer esto:

* debe tener al menos una dimensión en 0dp&#x20;
* definir el atributo `layout_constraintDimensionRatio`

El ratio puede ser expresado como un valor de coma flotante que representa un ratio entre altura y anchura o un ratio en forma anchura:altura.

Tambien se puede utilizar un ratio si las dos dimensiones estan definidas como 0dp.

En este caso, el sistema define la dimensión máxima que satisface el ratio y las restricciones.

### Cadenas <a href="#chains" id="chains"></a>

Las cadenas proporcionan comportamientos semejantes a un grupo de Widgets en un solo eje ( X o Y). El otro eje se puede restringir de manera independiente.

#### Crear una cadena

Una serie de Widgets son considerados una cadena si se encuentra unidos entre ellos con una conexión bidireccional.

#### Cabeza de la cadena

Las cadenas se controlan mediante atributos que se definen en el primer elemento de la cadena, el "cabeza" de cadena.

El "cabeza" es el elemento de más a la izquierda en cadenas horizontales y el de más arriba en cadenas verticales.

#### Márgenes en cadenas

Si se especifican márgenes en conexiones, estos serán tenidos en cuenta, en el caso de cadenas "abiertas", los márgenes serán deducidos del espacio que contienen.

#### Estilo de Cadena

Cuando definimos el atributo:&#x20;

* `layout_constraintHorizontal_chainStyle`
* `layout_constraintVertical_chainStyle`

En el primer elemento de una cadena, el comportamiento cambiará de acuerdo al estilo especificado en toda la cadena.

Existen varios estilos:

* `CHAIN_SPREAD` -> Los elementos ocupan todo el espacio de manera equitativa. Es el estilo por defecto.
* Cadena con pesos (weights) -> en el modo `CHAIN_SPREAD`, si alguno de los Widgets está definido como `MATCH_CONSTRAINT`, se repartiran el espacio disponible.
* `CHAIN_SPREAD_INSIDE` -> Similar al anterior pero sin dejar espacio con los bordes del padre.
* `CHAIN_PACKED` -> Los elementos de la cadena se colocan pegados los unos a los otros, dejando el espacio en los laterales. Los atributos bias afectaran a la posición de los elementos en conjunto.

#### Cadena con pesos (weigths)

El comportamiento por defecto de una cadena es separar sus elementos de igual manera en el espacio disponible. Si uno o más elementos están utilizando `MATCH_CONSTRAINT`, van a utilizar el espacio libre (de igual manera entre ellos).

El atributo&#x20;

* `layout_constraintHorizontal_weight`
* `layout_constraintVertical_weight`

Controla como se distribuye el espacio entre los elementos que utilizan ese `MATCH_CONSTRAINT`.

#### Márgenes y cadenas

Cuando se utilizan márgenes en elementos de una cadena, el margen se va sumando.

Por ejemplo, en una cadena horizontal, si un elemento tiene definido un margen derecho de 10dp y el siguiente elemento un margen izquierdo de 5dp, el margen total entre ellos será de 15dp.

### Virtual Helper objects <a href="#virtual-helper-objects" id="virtual-helper-objects"></a>

Además de las capacidades intrínsecas que se han detallado previamente, tambien se pueden utilizar **objetos helper** en **Constraint Layout** para ayudarnos con el Layout.

Existen 3 tipos:

* Guidelines
* Barriers
* Groups

#### Guidelines

{% embed url="https://developer.android.com/reference/androidx/constraintlayout/widget/Guideline" %}
Fuente: developer.android
{% endembed %}

Puede agregar una guía vertical u horizontal en la que sea posible restringir las vistas; la guía será invisible para los usuarios de la aplicación.&#x20;

Puede colocar la guía dentro del diseño según las unidades de dp o porcentaje, en relación con el borde del diseño.

#### Barriers

{% embed url="https://developer.android.com/reference/androidx/constraintlayout/widget/Barrier" %}
Fuente: developer.android
{% endembed %}

Como sucede con las guías, una barrera es una línea invisible respecto de la cual puedes restringir vistas. Sin embargo, la barrera no define su propia posición, sino que se desplaza en función de la posición de las vistas que contiene.&#x20;

Esto es útil si deseas restringir una vista a un conjunto de vistas en lugar de a una vista específica.

#### Groups

{% embed url="https://developer.android.com/reference/androidx/constraintlayout/widget/Group" %}
Fuente: developer.android
{% endembed %}

Un grupo permite controlar la visibilidad de varios Widgets al mismo tiempo.

### Optimizer (_in 1.1_) <a href="#optimizer-in-1.1" id="optimizer-in-1.1"></a>

Con el optimizador uno puede decidir que optimizaciones se aplican utilizando el tag:

* app:layout\_optimizationLevel

Los niveles de optimización son:

* none -> No se aplica ninguna optimización.
* standard -> Por defecto. Solo restricciones directas y barreras.
* direct -> Optimiza solo las restricciones directas.
* barrier -> Optimiza solo las barreras.
* chain -> Optimiza las cadenas (experimental)
* dimensions -> Optimiza las dimensiones (experimental), reduciendo el número de medidas en elementos con `MATCH_CONSTRAINT`.

Este atributo es una máscara, es decir, usted decide si activar o desactivar las optimizaciones listando las que uno considere.

## EJEMPLO

En vista a todo lo anterior, se va a hacer un ejemplo parecido al que se ha visto en la página anterior.

<figure><img src="../../.gitbook/assets/Galaxy S10.png" alt=""><figcaption><p>Layout creado con Lunacy</p></figcaption></figure>

Como podemos ver, es un layout a base de Views muy sencillo pero que permite utilizar todo el poder de Constraint Layout.

{% code title="activity_main.xml" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_height="match_parent"
    android:layout_width="match_parent">
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ConstraintLayoutActivity">

    <View
        android:id="@+id/v17"
        android:layout_width="240dp"
        android:layout_height="50dp"
        android:layout_marginStart="15dp"
        android:layout_marginTop="15dp"
        android:background="@color/darkPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v18"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v13" />

    <View
        android:id="@+id/v18"
        android:layout_width="80dp"
        android:layout_height="50dp"
        android:layout_marginTop="15dp"
        android:layout_marginEnd="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v17"
        app:layout_constraintTop_toBottomOf="@+id/v15" />

    <View
        android:id="@+id/v12"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginStart="15dp"
        android:layout_marginTop="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toStartOf="@+id/v13"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v10" />

    <View
        android:id="@+id/v13"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v14"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v12"
        app:layout_constraintTop_toBottomOf="@+id/v10" />

    <View
        android:id="@+id/v16"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:layout_marginEnd="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v15"
        app:layout_constraintTop_toBottomOf="@+id/v10" />

    <View
        android:id="@+id/v14"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toStartOf="@+id/v15"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v13"
        app:layout_constraintTop_toBottomOf="@+id/v10" />

    <View
        android:id="@+id/v15"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v16"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v14"
        app:layout_constraintTop_toBottomOf="@+id/v10" />

    <View
        android:id="@+id/v1"
        android:layout_width="150dp"
        android:layout_height="100dp"
        android:layout_marginTop="25dp"
        android:background="@color/accent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <View
        android:id="@+id/v24"
        android:layout_width="150dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:layout_marginBottom="25dp"
        android:background="@color/accent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v17" />

    <View
        android:id="@+id/v3"
        android:layout_width="80dp"
        android:layout_height="50dp"
        android:layout_marginTop="15dp"
        android:layout_marginEnd="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v2"
        app:layout_constraintTop_toBottomOf="@+id/v1" />

    <View
        android:id="@+id/v2"
        android:layout_width="240dp"
        android:layout_height="50dp"
        android:layout_marginStart="15dp"
        android:layout_marginTop="15dp"
        android:background="@color/darkPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v3"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v1" />

    <View
        android:id="@+id/v4"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginStart="15dp"
        android:layout_marginTop="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toStartOf="@+id/v5"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v2" />

    <View
        android:id="@+id/v5"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v6"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v4"
        app:layout_constraintTop_toBottomOf="@+id/v2" />

    <View
        android:id="@+id/v6"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toStartOf="@+id/v7"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v5"
        app:layout_constraintTop_toBottomOf="@+id/v2" />

    <View
        android:id="@+id/v7"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:background="@color/lightPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v8"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v6"
        app:layout_constraintTop_toBottomOf="@+id/v2" />

    <View
        android:id="@+id/v8"
        android:layout_width="50dp"
        android:layout_height="100dp"
        android:layout_marginTop="15dp"
        android:layout_marginEnd="15dp"
        android:background="@color/primary"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v7"
        app:layout_constraintTop_toBottomOf="@+id/v2" />

    <View
        android:id="@+id/v9"
        android:layout_width="50dp"
        android:layout_height="150dp"
        android:layout_marginStart="15dp"
        android:layout_marginTop="15dp"
        android:background="@color/darkPrimary"
        app:layout_constraintEnd_toStartOf="@+id/v10"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/v4" />

    <View
        android:id="@+id/v11"
        android:layout_width="50dp"
        android:layout_height="150dp"
        android:layout_marginTop="15dp"
        android:layout_marginEnd="15dp"

        android:background="@color/darkPrimary"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v10"
        app:layout_constraintTop_toBottomOf="@+id/v4" />

    <View
        android:id="@+id/v10"
        android:layout_width="200dp"
        android:layout_height="150dp"
        android:layout_marginTop="15dp"
        android:background="@color/accent"
        app:layout_constraintEnd_toStartOf="@+id/v11"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/v9"
        app:layout_constraintTop_toBottomOf="@+id/v4" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_begin="29dp" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_begin="364dp" />


</androidx.constraintlayout.widget.ConstraintLayout>
</ScrollView>
```
{% endcode %}

![](<../../.gitbook/assets/image (7) (2).png>)                               ![](<../../.gitbook/assets/image (21).png>)

![](<../../.gitbook/assets/image (2) (1).png>)                               ![](<../../.gitbook/assets/image (9) (1).png>)

&#x20;                                                     ![](<../../.gitbook/assets/image (11).png>)

{% hint style="success" %}
Como podemos ver, el uso de **Constraint Layout** nos permite obtener un **diseño Responsivo** sin necesidad de añadir más código para ello.
{% endhint %}
