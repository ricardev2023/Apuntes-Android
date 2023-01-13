---
description: Explicación del concepto de Content Provider.
---

# Content Provider

{% embed url="https://developer.android.com/guide/topics/providers/content-provider-basics?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Un proveedor de contenido administra el acceso a un repositorio central de datos. Los proveedores de contenido están principalmente orientados a que los usen otras aplicaciones que acceden al proveedor usando un objeto de cliente del proveedor.&#x20;

Juntos, los proveedores y clientes de proveedores ofrecen una interfaz estándar y uniforme para los datos que también manipula la comunicación dentro del proceso y el acceso seguro a los datos.

Se utilizan content providers en dos casos:

* Para acceder a un proveedor de contenido existente en otra aplicación.
* Cuando decides crear un proveedor de contenido nuevo en tu aplicación a fin de compartir datos con otras aplicaciones.

## FUNCIONAMIENTO

Un proveedor de contenido presenta datos a aplicaciones externas en forma de una o más tablas que son similares a las tablas de una base de datos relacional. Una fila representa una instancia de algún tipo de datos que recopila el proveedor, y cada columna de la fila representa un ítem individual de los datos recopilados para una instancia.

El proveedor de contenido organiza el acceso a la capa de almacenamiento de los datos en tu aplicación para una serie de API y componentes diferentes:

<figure><img src="../../.gitbook/assets/content-provider-tech-stack.png" alt=""><figcaption><p>Fuente: developer.android</p></figcaption></figure>

* Compartir con otras aplicaciones el acceso a los datos de tu aplicación
* Enviar datos a un widget
* Mostrar sugerencias personalizadas de búsqueda para tu aplicación mediante el marco de trabajo de búsqueda usando `SearchRecentSuggestionsProvider`
* Sincronizar los datos de la aplicación con tu servidor mediante una implementación de `AbstractThreadedSyncAdapter`
* Cargar datos en tu IU usando `CursorLoader`
