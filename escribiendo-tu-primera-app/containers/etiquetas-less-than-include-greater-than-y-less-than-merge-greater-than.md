---
description: Explicación del concepto de las etiquetas <include> y <merge>
---

# etiquetas \<include> y \<merge>

{% embed url="https://developer.android.com/develop/ui/views/layout/improving-layouts/reusing-layouts?hl=es-419" %}
Fuente: developer.android
{% endembed %}

{% embed url="https://developer.android.com/guide/topics/resources/layout-resource?hl=es-419" %}
Fuente: developer.android
{% endembed %}

## DEFINICIÓN

Las etiquetas `<include>` y `<merge>` facilitan la reutilización de diseños. Esto permite crear diseños complejos como `NavigationViews` o `Toolbars` que se reutilicen en las diferentes **Activities**.

### \<include>

La etiqueta `<include>` permite agregar un **Layout** dentro de otro.&#x20;

### \<merge>

La etiqueta `<merge>` se utiliza como **elemento superior en el Layout** que se va a utilizar dentro de otro Layout y permite que no se utilicen **ViewGroups redundantes**.

Por ejemplo, si yo creo un `LinearLayout` vertical y le añado un **Layout** cuyo elemento superior (necesario para que funcione) es un `LinerLayout` vertical, lo que estoy haciendo es **anidar dos LinearLayouts verticales que lo único que van a hacer es afectar al rendimiento de la App**.

Para evitarlo, en el **Layout** que se va a incluir con la etiqueta `<include>` se puede utilizar la etiqueta `<merge>` en vez de un **ViewGroup**.

## EJEMPLO

