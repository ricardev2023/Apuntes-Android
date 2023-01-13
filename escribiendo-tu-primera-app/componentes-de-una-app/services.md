---
description: Explicación del concepto de Services.
---

# Services

### Definición

Un `Service` es un componente de una aplicación que puede realizar operaciones de larga ejecución en segundo plano y que no proporciona una interfaz de usuario.

{% embed url="https://developer.android.com/guide/components/services?hl=es-419" %}
Fuente: developer.android
{% endembed %}

Otro componente de la aplicación puede iniciar un servicio y continuar ejecutándose en segundo plano aunque el usuario cambie a otra aplicación. Además, un componente puede enlazarse con un servicio para interactuar con él e incluso realizar una comunicación entre procesos (IPC).&#x20;

{% hint style="info" %}
Por ejemplo, un servicio puede manejar transacciones de red, reproducir música, realizar I/O de archivos o interactuar con un proveedor de contenido, todo en segundo plano.
{% endhint %}

### Tipos de Servicios

Estos son los tres tipos diferentes de servicios:

* **Primer plano** -> Un servicio en primer plano realiza una operación que el usuario puede notar. Por ejemplo, una aplicación de audio usa un servicio en primer plano para reproducir una pista de audio. Los servicios en primer plano deben mostrar una notificación. Estos servicios continúan ejecutándose incluso si el usuario deja de interactuar con la aplicación.
* **Segundo plano** -> Un servicio en segundo plano realiza una operación que el usuario no nota directamente. Por ejemplo, si una aplicación usa un servicio para comprimir su almacenamiento, suele tratarse de un servicio en segundo plano.
* **Enlace** -> Un servicio es de _enlace_ cuando un componente de la aplicación se vincula a él llamando a `bindService()`. Un servicio de enlace ofrece una interfaz cliente-servidor que permite que los componentes interactúen con el servicio, envíen solicitudes, reciban resultados e incluso lo hagan en distintos procesos con la comunicación entre procesos (IPC).&#x20;
