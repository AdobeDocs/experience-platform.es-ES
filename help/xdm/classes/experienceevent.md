---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;mapa de identidad;mapa de identidad;mapa de identidad;diseño de esquema;mapa;mapa;esquema de unión;unión
solution: Experience Platform
title: Clase XDM ExperienceEvent
topic-legacy: overview
description: Este documento proporciona información general sobre la clase XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: 9b63b38e664e5776ca638f8ed407896f185bcab0
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] es una clase XDM estándar que le permite crear una instantánea con marca de tiempo del sistema cuando se produce un evento específico o cuando se alcanza un determinado conjunto de condiciones.

Un evento de experiencia es un registro de hechos de lo que ha sucedido, que incluye el momento y la identidad de la persona implicada. Los eventos pueden ser explícitos (acciones humanas directamente observables) o implícitos (se generan sin una acción humana directa) y se registran sin agregación ni interpretación. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Platform, consulte la [información general de XDM](../home.md#data-behaviors).

La propia clase [!DNL XDM ExperienceEvent] proporciona varios campos relacionados con series temporales a un esquema. Los valores de algunos de estos campos se rellenan automáticamente cuando se introducen datos:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Propiedad | Descripción |
| --- | --- |
| `_id` | Identificador de cadena único generado por el sistema para el evento. Este campo se utiliza para rastrear la exclusividad de un evento individual, evitar la duplicación de datos y buscar ese evento en servicios descendentes. Dado que este campo se genera a partir del sistema, no se debe proporcionar un valor explícito durante el consumo de datos.<br><br>Es importante distinguir que este campo  **no** presenta una identidad relacionada con una persona individual, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) en su lugar. |
| `eventMergeId` | El ID del lote ingestado que provocó que se creara el registro. El sistema rellena automáticamente este campo tras la ingesta de datos. |
| `eventType` | Cadena que indica el tipo de evento principal del registro. Los valores aceptados y sus definiciones se proporcionan en la sección [apéndice](#eventType). |
| `identityMap` | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para el individuo al que se aplica el evento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en los  [conceptos básicos de la ](../schema/composition.md#identityMap) composición de esquemas para obtener más información sobre su caso de uso. |
| `timestamp` | Marca de fecha y hora ISO 8601 del momento en que se produjo el evento, con el formato [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).<br><br>Esta marca de tiempo  **** solo puede representar la observación del propio evento y debe ocurrir en el pasado. Si los casos de uso de segmentación requieren el uso de marcas de tiempo que puedan producirse en el futuro (como una fecha de salida), estos valores deben restringirse en cualquier otra parte del esquema de eventos de experiencia. |

## Mezclas compatibles {#mixins}

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../mixins/name-updates.md) para obtener más información.

El Adobe proporciona varias mezclas estándar para su uso con la clase [!DNL XDM ExperienceEvent]. A continuación se presenta una lista de algunas mezclas que se utilizan habitualmente para la clase:

* [[!UICONTROL End User ID Details]](../mixins/event/enduserids.md)
* [[!UICONTROL Environment Details]](../mixins/event/environment-details.md)

## Apéndice

La siguiente sección contiene información adicional sobre la clase [!UICONTROL XDM ExperienceEvent].

### Valores aceptados para xdm:eventType {#eventType}

La siguiente tabla describe los valores aceptados para `xdm:eventType`, junto con sus definiciones:

| Valor | Definición |
| --- | --- |
| `advertising.completes` | Se ha visto hasta el final un recurso de medios temporizados. Esto no significa necesariamente que el usuario haya visto todo el vídeo, ya que el usuario podría haber omitido. |
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
