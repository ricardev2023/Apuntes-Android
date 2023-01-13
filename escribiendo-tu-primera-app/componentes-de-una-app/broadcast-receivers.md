---
description: Explicación del concepto de Broadcast Receiver.
---

# Broadcast Receivers

{% embed url="https://developer.android.com/guide/components/broadcasts?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## EMISIONES DE ANDROID

Todas las Apps de Android pueden recibir mensajes de emision (Broadcast messages) desde el sistema de Android u otras Aplicaciones. Para ello se utiliza el patrón de diseño de publicación y suscripción.

Estas emisiones se envían cuando ocurre un evento de interés.

El sistema de Android emite estos mensajes por ejemplo en los siguientes casos: batería por debajo del 15%, GPS activado / desactivado, modo avión activado / desactivado o conexión a una red WIFI entre otros.

Por otro lado, las Apps también pueden emitir este tipo de mensajes de manera personalizada cuando se ha dado una situación que puede afectar a otras Apps.&#x20;

Las apps pueden registrarse para recibir emisiones específicas. Cuando se envía una emisión, el sistema redirige automáticamente las emisiones a las apps que se suscribieron para recibir ese tipo de emisión particular.

Por lo general, las emisiones pueden usarse como un sistema de mensajería entre apps y fuera del flujo de usuarios normal. Sin embargo, debes tener cuidado de no abusar de la oportunidad de responder a las emisiones y ejecutar tareas en segundo plano que puedan contribuir a ralentizar el rendimiento del sistema.

{% hint style="danger" %}
Como ejemplo vemos los **Broadcast Messages** de la App de la cámara que se correspondían con ACTION\_NEW\_PICTURE y ACTION\_NEW\_VIDEO.

Estos mensajes que emitía la App de la cámara fueron eliminados en Android 7.0 debido a que las Aplicaciones se despertaban para responder a dicho mensaje y generaban problemas de rendimiento, llegando a afectar al buen funcionamiento de la Cámara.

Por este motivo es fundamental no abusar de las respuestas ante estos **Broadcast Messages**.&#x20;
{% endhint %}

## DEFINICIÓN

Los **Broadcast Receivers** son los elementos declarados en la App que se suscriben a un tipo específico de Broadcast Message y se mantienen a la escucha. Se pueden dar dos tipos:

### Broadcast Receivers en el manifiesto

Si declaras un receptor de emisión en tu manifiesto, el sistema inicia la app (si aún no está en ejecución) cuando se envía la emisión.

{% hint style="danger" %}
Si tu app se orienta a la API nivel 26 o una versión posterior, no puedes usar el manifiesto para declarar un receptor de emisiones _implícitas_ (emisiones que no se orientan específicamente a tu app), excepto por algunas emisiones implícitas que están exentas de esa restricción.&#x20;

En la mayoría de los casos, puedes usar [tareas programadas](https://developer.android.com/topic/performance/scheduling?hl=es-419) en su lugar.
{% endhint %}

### Broadcast Receivers en el contexto

Los receptores registrados en el contexto reciben emisiones siempre que su contexto de registro sea válido.&#x20;

Por ejemplo, si te registras en un contexto `Activity`, recibirás emisiones siempre y cuando no se elimine la actividad. Si te registras con el contexto de la aplicación, recibirás emisiones mientras la app esté en ejecución.

