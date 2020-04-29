---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía del usuario de Perfil del cliente en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: ab289f07475abcbe966c723423825fd392eb3615

---


# Guía del usuario de Perfil del cliente en tiempo real

El Perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

Este documento sirve como guía para interactuar con el Perfil del cliente en tiempo real en la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía del usuario requiere conocer los distintos servicios de la plataforma de experiencia que se utilizan para administrar el Perfil de los clientes en tiempo real. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio](../../identity-service/home.md)de identidad: Permite el Perfil del cliente en tiempo real al enlazar identidades de orígenes de datos dispares que se están ingeriendo en la plataforma.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

## Perfil general

En la interfaz de usuario [de la plataforma de](http://platform.adobe.com)experiencia, haga clic en **Perfiles** en el panel de navegación izquierdo para abrir la ficha _Información general_ en el espacio de trabajo de _Perfiles_ . Esta ficha muestra varias utilidades que proporcionan información de alto nivel sobre el almacén de Perfiles, incluida la audiencia direccionable total, el número de registros de Perfiles que se ingerieron durante la última semana, así como estadísticas sobre registros exitosos y fallidos para el mismo período de tiempo.

![](../images/user-guide/profile-overview.png)

## Muestras de perfil de Vista

Haga clic en **Examinar** para vista de una lista de muestra de perfiles disponibles. Este ejemplo incluye hasta 50 perfiles del recuento total de [perfiles](#profile-count). Los ejemplos se actualizan mediante un trabajo automático que recoge nuevos datos de perfil a medida que se ingesta. Cada perfil de la lista muestra su ID, nombre, apellidos y correo electrónico personal. Al hacer clic en el ID de un perfil de la lista, se muestran sus detalles en el visor de [Perfil](#profile-viewer).

![](../images/user-guide/profile-samples.png)

Puede personalizar los atributos que se muestran en la lista haciendo clic en el icono del selector de columnas. Esto muestra una lista desplegable que contiene atributos de perfil comunes que puede agregar o eliminar.

![](../images/user-guide/column-selector.png)

### Recuento de Perfiles {#profile-count}

El recuento de perfiles muestra el número total de perfiles que su organización tiene en la plataforma de experiencia, después de que la directiva de combinación predeterminada de su organización haya combinado fragmentos de perfil para formar un único perfil para cada cliente individual. En otras palabras, su organización puede tener varios fragmentos de perfil relacionados con un único cliente que interactúa con su marca en diferentes canales, pero estos fragmentos se combinarán (según la política de combinación predeterminada) y devolverá un recuento de perfiles &quot;1&quot; porque todos están relacionados con el mismo individuo.

El recuento de perfiles también incluye tanto perfiles con atributos (datos de registros) como perfiles (como perfiles de Adobe Analytics) que solo contienen datos de series temporales (eventos). El recuento se actualiza periódicamente para proporcionar un número total actualizado de perfiles dentro de la plataforma. Cada vez que una ingestión de perfiles aumenta o disminuye el recuento en más de un 5%, se activa automáticamente un trabajo para actualizar el recuento. Si su organización está utilizando la transmisión por flujo continuo, los trabajos se programan para que se ejecuten cada hora a fin de recoger los datos recién ingestados.

![](../images/user-guide/profile-count.png)

### Búsqueda de Perfiles

Si conoce una identidad vinculada para un perfil en particular (como su dirección de correo electrónico), puede buscar ese perfil haciendo clic en **Buscar un perfil**. Esta es la forma más fiable de acceder a un perfil específico, independientemente de si aparece en la lista de muestras.

![](../images/user-guide/find-a-profile.png)

En el cuadro de diálogo que aparece, seleccione una Área de nombres de ID adecuada en la lista desplegable (&quot;Correo electrónico&quot; en este ejemplo) e introduzca el valor de ID siguiente antes de hacer clic en **Aceptar**. Si se encuentra, los detalles del perfil de destino aparecen en el visor de perfil, tal como se describe en la sección siguiente.

![](../images/user-guide/find-a-profile-details.png)

### Visor de Perfiles {#profile-viewer}

Al seleccionar o buscar un perfil específico, se abre la pantalla _Detalle_ del visor de perfil. Esta página muestra información sobre el perfil seleccionado, como los atributos básicos del perfil, las identidades vinculadas y los canales de contacto disponibles. La información de perfil mostrada se ha combinado desde varios fragmentos de perfil para formar una sola vista del cliente individual.

![](../images/user-guide/profile-viewer-detail.png)

El visor de perfil también proporciona fichas que le permiten realizar vistas de eventos y pertenencias a segmentos asociados con este perfil, si existe.

![](../images/user-guide/profile-viewer-events-seg.png)

## Combinar directivas

Haga clic en **Combinar directivas** para vista de una lista de directivas de combinación que pertenezcan a su organización. Cada directiva de la lista muestra su nombre, tanto si es la directiva de combinación predeterminada como si no, y el esquema al que se aplica.

![](../images/user-guide/profile-merge-policies.png)

Para obtener más información sobre cómo trabajar con políticas de combinación en la interfaz de usuario, consulte la guía [del usuario](merge-policies.md)Combinar directivas.

## esquema de Unión

Haga clic en Esquema **de** Unión para vista de los esquemas de unión para el almacén de datos de perfil. Un esquema de unión es una combinación de todos los campos del Modelo de datos de experiencia (XDM) de la misma clase, cuyos esquemas se han habilitado para su uso en el Perfil del cliente en tiempo real. Haga clic en una clase de la lista izquierda para vista de la estructura de su esquema de unión en el lienzo.

![](../images/user-guide/profile-union-schema.png)

Consulte la sección sobre esquemas de unión en la guía [de composición de](../../xdm/schema/composition.md) esquemas para obtener más información sobre los esquemas de unión y su función en el Perfil de clientes en tiempo real.

## Pasos siguientes

Al leer esta guía, ahora sabe cómo realizar vistas y administrar los datos de Perfil mediante la interfaz de usuario de la plataforma de experiencia. Para obtener información sobre cómo aprovechar los datos de Perfil de clientes en tiempo real para generar segmentos de audiencia, consulte la documentación [de](../../segmentation/home.md)segmentación.