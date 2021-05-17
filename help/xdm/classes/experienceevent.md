---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;mapa de identidad;mapa de identidad;mapa de identidad;diseño de esquema;mapa;mapa;esquema de unión;unión
solution: Experience Platform
title: Clase XDM ExperienceEvent
topic-legacy: overview
description: Este documento proporciona información general sobre la clase XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] es una clase estándar del Modelo de datos de experiencia (XDM) que le permite crear una instantánea con marca de tiempo del sistema cuando se produce un evento específico o cuando se alcanza un conjunto determinado de condiciones.

Un evento de experiencia es un registro de hechos de lo que ha sucedido, que incluye el momento y la identidad de la persona implicada. Los eventos pueden ser explícitos (acciones humanas directamente observables) o implícitos (se generan sin una acción humana directa) y se registran sin agregación ni interpretación. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Platform, consulte la [información general de XDM](../home.md#data-behaviors).

La propia clase [!DNL XDM ExperienceEvent] proporciona varios campos relacionados con series temporales a un esquema. Los valores de algunos de estos campos se rellenan automáticamente cuando se introducen datos:

![](../images/classes/experienceevent/structure.png)

| Propiedad | Descripción |
| --- | --- |
| `_id` | Identificador de cadena único para el evento. Este campo se utiliza para rastrear la exclusividad de un evento individual, evitar la duplicación de datos y buscar ese evento en servicios descendentes.<br><br>En algunos casos,  `_id` puede ser un identificador único  [universal (UUID)](https://tools.ietf.org/html/rfc4122) o un identificador único  [global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0). En la preparación de datos de Adobe Experience Platform, este valor se puede generar utilizando las funciones de asignación [`uuid` o `guid`](../../data-prep/functions.md#special-operations).<br><br>Si transmite datos desde una conexión de origen o realiza la ingesta directamente desde un archivo de parquet, debe generar este valor concatenando ciertos campos combinados que hagan que el evento sea único, como un ID principal, una marca de tiempo, un tipo de evento, etc.<br><br>Es importante distinguir que  **este campo no representa una identidad relacionada con una persona** individual, sino el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) proporcionados por mezclas compatibles. |
| `eventMergeId` | Si utiliza el [Adobe Experience Platform Web SDK](../../edge/home.md) para introducir datos, esto representa el ID del lote ingerido que provocó la creación del registro. El sistema rellena automáticamente este campo tras la ingesta de datos. No se admite el uso de este campo fuera del contexto de una implementación de SDK web. |
| `eventType` | Cadena que indica el tipo o la categoría del evento. Este campo se puede utilizar si desea distinguir diferentes tipos de eventos dentro del mismo esquema y conjunto de datos, como distinguir un evento de vista de producto de un evento de complemento del carro de compras para una empresa minorista.<br><br>Los valores estándar de esta propiedad se proporcionan en la  [sección](#eventType) del apéndice, incluidas las descripciones de su caso de uso previsto. Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas de tipo de evento para categorizar los eventos que rastrea. |
| `producedBy` | Un valor de cadena que describe el productor o el origen del evento. Este campo se puede utilizar para filtrar ciertos productores de eventos si es necesario para fines de segmentación.<br><br>Algunos valores sugeridos para esta propiedad se proporcionan en la  [sección](#producedBy) del apéndice. Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas para representar a diferentes productores de eventos. |
| `identityMap` | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para el individuo al que se aplica el evento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en los  [conceptos básicos de la ](../schema/composition.md#identityMap) composición de esquemas para obtener más información sobre su caso de uso. |
| `timestamp` | Marca de fecha y hora ISO 8601 del momento en que se produjo el evento, con el formato [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Esta marca de tiempo debe suceder en el pasado. Consulte la sección siguiente en [timestamps](#timestamps) para conocer las prácticas recomendadas sobre el uso de este campo. |

## Prácticas recomendadas para el modelado de eventos

Las siguientes secciones tratan sobre las prácticas recomendadas para diseñar los esquemas del Modelo de datos de experiencia (XDM) basados en eventos en Adobe Experience Platform.

### Marcas de hora {#timestamps}

El campo raíz `timestamp` de un esquema de eventos puede **solo** representar la observación del propio evento y debe producirse en el pasado. Si los casos de uso de segmentación requieren el uso de marcas de tiempo que puedan producirse en el futuro, estos valores deben restringirse en cualquier otra parte del esquema de eventos de experiencia.

Por ejemplo, si un negocio de la industria de viajes y hospitalidad está modelando un evento de reserva de vuelo, el campo de nivel de clase `timestamp` representa el momento en que se observó el evento de reserva. Otras marcas de tiempo relacionadas con el evento, como la fecha de inicio de la reserva de viajes, deben capturarse en campos separados proporcionados por mezclas estándar o personalizadas.

![](../images/classes/experienceevent/timestamps.png)

Al mantener la marca de tiempo de nivel de clase separada de otros valores de fecha y hora relacionados en los esquemas de eventos, puede implementar casos de uso de segmentación flexible y, al mismo tiempo, preservar una cuenta con marca de tiempo de los recorridos del cliente en su aplicación de experiencia.

### Uso de campos calculados

Ciertas interacciones en las aplicaciones de experiencia pueden dar como resultado varios eventos relacionados que técnicamente comparten la misma marca de tiempo de evento y, por lo tanto, pueden representarse como un solo registro de evento. Por ejemplo, si un cliente visualiza un producto en su sitio web, esto puede generar un registro de evento que contenga tanto atributos de &quot;vista de producto&quot; como atributos de &quot;vista de página&quot; genéricos superpuestos. En estos casos, se pueden utilizar campos calculados para capturar los atributos más importantes cuando se capturan varios eventos en un registro.

[Adobe Experience Platform Data ](../../data-prep/home.md) Preppermite asignar, transformar y validar datos desde y hacia XDM. Al utilizar las [funciones de asignación](../../data-prep/functions.md) disponibles que proporciona el servicio, puede invocar operadores lógicos para priorizar, transformar y/o consolidar datos de registros de eventos múltiples al ingerirlos en Experience Platform.

Si está introduciendo datos manualmente en Platform a través de la interfaz de usuario, consulte la guía sobre [asignación de un archivo CSV a XDM](../../ingestion/tutorials/map-a-csv-file.md) para ver los pasos específicos sobre cómo crear campos calculados.

Si está transmitiendo datos a Platform mediante una conexión de origen, puede configurar la fuente para que utilice campos calculados en su lugar. Consulte la [documentación de su origen particular](../../sources/home.md) para obtener instrucciones sobre cómo implementar campos calculados al configurar la conexión.

## Grupos de campos de esquema compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Para obtener más información, consulte el documento [field group name updates](../field-groups/name-updates.md) .

Adobe proporciona varios grupos de campos estándar para su uso con la clase [!DNL XDM ExperienceEvent]. A continuación se muestra una lista de algunos grupos de campos utilizados con frecuencia para la clase :

* [[!UICONTROL Detalles del ID de usuario final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalles del entorno]](../field-groups/event/environment-details.md)

## Apéndice

La siguiente sección contiene información adicional sobre la clase [!UICONTROL XDM ExperienceEvent].

### Valores aceptados para `eventType` {#eventType}

La siguiente tabla describe los valores aceptados para `eventType`, junto con sus definiciones:

| Valor | Definición |
| --- | --- |
| `advertising.completes` | Se ha visto hasta el final un recurso de medios temporizados. Esto no significa necesariamente que el usuario haya visto todo el vídeo, ya que el usuario podría haber omitido el vídeo. |
| `advertising.timePlayed` | Describe la cantidad de tiempo que un usuario emplea en un recurso de medios temporizados específico. |
| `advertising.federated` | Indica si un evento de experiencia se creó mediante una federación de datos (uso compartido de datos entre clientes). |
| `advertising.clicks` | Haga clic en las acciones de un anuncio. |
| `advertising.conversions` | Acciones predefinidas realizadas por un cliente que déclencheur un evento para la evaluación del rendimiento. |
| `advertising.firstQuartiles` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal del 25% de su duración. |
| `advertising.impressions` | Impresión(s) de un anuncio a un cliente con el potencial de ser visto. |
| `advertising.midpoints` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 50% de su duración. |
| `advertising.starts` | Se ha empezado a reproducir un anuncio de vídeo digital. |
| `advertising.thirdQuartiles` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 75% de su duración. |
| `web.webpagedetails.pageViews` | Una página web ha recibido una o más vistas. |
| `web.webinteraction.linkClicks` | Se ha seleccionado un vínculo una o más veces. |
| `commerce.checkouts` | Se ha producido un evento de cierre de compra para una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la marca de tiempo y la página/experiencia a la que se hace referencia para cada evento se utilizan para identificar cada evento individual (paso), representado en orden. |
| `commerce.productListAdds` | Se ha agregado un producto a la lista de productos o al carro de compras. |
| `commerce.productListOpens` | Se ha inicializado o creado una nueva lista de productos (carro de compras). |
| `commerce.productListRemovals` | Una o más entradas de producto se han eliminado de una lista de productos o de un carro de compras. |
| `commerce.productListReopens` | Un cliente ha reactivado una lista de productos (carro de compras) que ya no era accesible (abandonada), por ejemplo, mediante una actividad de remarketing. |
| `commerce.productListViews` | Una lista de productos o un carro de compras ha recibido una o más vistas. |
| `commerce.productViews` | Un producto ha recibido una o más vistas. |
| `commerce.purchases` | Se ha aceptado una solicitud. Esta es la única acción necesaria en una conversión de comercio. Un evento de compra debe tener una lista de productos referenciada. |
| `commerce.saveForLaters` | Se ha guardado una lista de productos para su uso futuro, como una lista de deseos de productos. |
| `delivery.feedback` | Eventos de comentarios de un envío, como un envío de correo electrónico. |
| `message.feedback` | Eventos de comentarios como enviados/rechazados/errores para mensajes enviados a un cliente. |
| `message.tracking` | Eventos de seguimiento como acciones de apertura/clic/personalizadas en mensajes enviados a un cliente. |

### Valores sugeridos para `producedBy` {#producedBy}

La siguiente tabla describe algunos valores aceptados para `producedBy`:

| Valor | Definición |
| --- | --- |
| `self` | Self |
| `system` | Sistema |
| `salesRef` | Representante de ventas |
| `customerRep` | Representante del cliente |
