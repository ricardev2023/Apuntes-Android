---
description: Explicación del concepto de Intent.
---

# Intents

{% embed url="https://developer.android.com/guide/components/intents-filters?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Un `Intent` es un objeto de mensajería que puedes usar para solicitar una acción de otro componente de una app.&#x20;

### Casos de uso

#### **Iniciar una actividad**

Una `Activity` representa una única pantalla en una aplicación. Puedes iniciar una nueva instancia de una `Activity` pasando un `Intent` a `startActivity()`. El `Intent` describe la actividad que se debe iniciar y contiene los datos necesarios para ello.

Si deseas recibir un resultado de la actividad cuando finalice, llama a `startActivityForResult()`. La actividad recibe el resultado como un objeto `Intent` separado en la devolución de llamada de `onActivityResult()` de la actividad.&#x20;

#### **Iniciar un servicio**

Un `Service` es un componente que realiza operaciones en segundo plano sin una interfaz de usuario. Con Android 5.0 (nivel de API 21) y versiones posteriores, puedes iniciar un servicio con `JobScheduler`.

En las versiones anteriores a Android 5.0 (nivel de API 21), puedes iniciar un servicio usando métodos de la clase `Service`. Puedes iniciar un servicio para realizar una operación única (como descargar un archivo) pasando un `Intent` a `startService()`. El `Intent` describe el servicio que se debe iniciar y contiene los datos necesarios para ello.

Si el servicio está diseñado con una interfaz cliente-servidor, puedes establecer un enlace con el servicio de otro componente pasando un `Intent` a `bindService()`.&#x20;

#### **Transmitir un broadcast**

Un broadcast es un aviso que cualquier aplicación puede recibir. El sistema transmite varias emisiones de eventos, como cuando se inicia el sistema o comienza a cargarse el dispositivo.

Puedes transmitir una emisión a otras apps pasando un `Intent` a `sendBroadcast()` o `sendOrderedBroadcast()`.

## TIPOS

### Intent Explícito

Especifica qué aplicación lo administrará, ya sea incluyendo el nombre del paquete de la app de destino o el nombre de clase del componente completamente calificado.&#x20;

Normalmente, el usuario usa un **intent explícito** para iniciar un componente en su propia aplicación porque conoce el nombre de clase de la actividad o el servicio que desea iniciar.&#x20;

Por ejemplo, puedes utilizarlo para iniciar una actividad nueva en respuesta a una acción del usuario o iniciar un servicio para descargar un archivo en segundo plano.

### Intent Implícito

No nombra el componente específico, pero, en cambio, declaran una acción general para realizar, lo cual permite que un componente de otra aplicación la maneje.&#x20;

Por ejemplo, si deseas mostrar al usuario una ubicación en un mapa, puedes usar un **intent implícito** para solicitar que otra aplicación apta muestre una ubicación específica en un mapa.
