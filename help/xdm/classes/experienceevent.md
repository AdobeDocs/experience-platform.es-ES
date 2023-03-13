---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;identityMap;identity map;Identity Map;Identity Map;Diseño de esquema;Map;event modeling;event modeling;best practice;event;events;
solution: Experience Platform
title: Clase XDM ExperienceEvent
description: Este documento proporciona información general sobre la clase XDM ExperienceEvent y prácticas recomendadas para el modelado de datos de evento.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] clase

[!DNL XDM ExperienceEvent] es una clase estándar de modelo de datos de experiencia (XDM) que le permite crear una instantánea con marca de tiempo del sistema cuando se produce un evento específico o se ha alcanzado un conjunto determinado de condiciones.

Un Evento de experiencia es un registro de hechos de lo que ocurrió, incluido el momento y la identidad de la persona involucrada. Los eventos pueden ser explícitos (acciones humanas directamente observables) o implícitos (planteados sin una acción humana directa) y se registran sin agregación ni interpretación. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Platform, consulte la [Información general de XDM](../home.md#data-behaviors).

El [!DNL XDM ExperienceEvent] proporciona varios campos relacionados con series temporales a un esquema. Dos de estos campos (`_id` y `timestamp`) son **obligatorio** para todos los esquemas basados en la clase, mientras que el resto son opcionales. Los valores de algunos de los campos se rellenan automáticamente cuando se incorporan datos.

![La estructura de ExperienceEvent de XDM tal como aparece en la IU de Platform](../images/classes/experienceevent/structure.png)

| Propiedad | Descripción |
| --- | --- |
| `_id`<br>**(Requerido)** | Un identificador de cadena único para el evento. Este campo se utiliza para realizar un seguimiento de la exclusividad de un evento individual, evitar la duplicación de datos y buscar ese evento en los servicios descendentes. En algunos casos, `_id` puede ser un [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si está transmitiendo datos desde una conexión de origen o ingiriendo directamente desde un archivo de Parquet, debe generar este valor concatenando una cierta combinación de campos que hacen que el evento sea único, como un ID principal, una marca de tiempo, un tipo de evento, etc. El valor concatenado debe ser un `uri-reference` formatted string, lo que significa que se debe eliminar cualquier carácter de dos puntos. Después, el valor concatenado debe tener un cifrado hash con SHA-256 u otro algoritmo de su elección.<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el propio registro de datos. Los datos de identidad relativos a una persona deben quedar relegados a [campos de identidad](../schema/composition.md#identity) proporcionadas por grupos de campos compatibles. |
| `eventMergeId` | Si se usa la variable [SDK web de Adobe Experience Platform](../../edge/home.md) para introducir datos, representa el ID del lote introducido que provocó la creación del registro. El sistema rellena automáticamente este campo tras la ingesta de datos. No se admite el uso de este campo fuera del contexto de una implementación de SDK web. |
| `eventType` | Cadena que indica el tipo o la categoría del evento. Este campo se puede utilizar si desea distinguir distintos tipos de eventos dentro del mismo esquema y conjunto de datos, como distinguir un evento de vista de producto de un evento de complemento al carro de compras para una compañía minorista.<br><br>Los valores estándar para esta propiedad se proporcionan en [sección del apéndice](#eventType), incluidas las descripciones de su caso de uso previsto. Este campo es una enumeración ampliable, lo que significa que también puede utilizar sus propias cadenas de tipo de evento para categorizar los eventos que está rastreando.<br><br>`eventType` limita el uso de un solo evento por visita en la aplicación y, por lo tanto, debe utilizar campos calculados para que el sistema sepa qué evento es el más importante. Para obtener más información, consulte la sección sobre [prácticas recomendadas para campos calculados](#calculated). |
| `producedBy` | Valor de cadena que describe el productor o el origen del evento. Este campo se puede utilizar para filtrar ciertos productores de eventos si es necesario con fines de segmentación.<br><br>Algunos valores sugeridos para esta propiedad se proporcionan en la variable [sección del apéndice](#producedBy). Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas para representar a diferentes productores de eventos. |
| `identityMap` | Campo de asignación que contiene un conjunto de identidades con espacio de nombres para el individuo al que se aplica el evento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../profile/home.md), no intente actualizar manualmente el contenido del campo en las operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en la [conceptos básicos de composición de esquemas](../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `timestamp`<br>**(Requerido)** | Una marca de tiempo ISO 8601 de cuándo se produjo el evento, con el formato establecido por [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Esta marca de tiempo debe pertenecer al pasado. Consulte la sección siguiente sobre [marcas de tiempo](#timestamps) para conocer las prácticas recomendadas sobre el uso de este campo. |

{style="table-layout:auto"}

## Prácticas recomendadas para el modelado de eventos

Las siguientes secciones tratan sobre las prácticas recomendadas para diseñar esquemas XDM (Experience Data Model) basados en eventos en Adobe Experience Platform.

### Marcas de hora {#timestamps}

La raíz `timestamp` de un esquema de evento puede **solamente** representan la observación del evento mismo, y deben ocurrir en el pasado. Si los casos de uso de la segmentación requieren el uso de marcas de tiempo que puedan producirse en el futuro, estos valores deben restringirse en cualquier parte del esquema de Experience Event.

Por ejemplo, si un negocio del sector de los viajes y la hostelería está modelando un evento de reserva de vuelo, el nivel de clase `timestamp` representa el momento en el que se observó el evento de reserva. Otras marcas de tiempo relacionadas con el evento, como la fecha de inicio de la reserva de viaje, deben capturarse en campos independientes proporcionados por grupos de campos estándar o personalizados.

![Esquema de evento de experiencia de ejemplo con la reserva de vuelo y la fecha de inicio resaltadas.](../images/classes/experienceevent/timestamps.png)

Al mantener la marca de tiempo en el nivel de clase separada de otros valores de fecha y hora relacionados en los esquemas de evento, puede implementar casos de uso de segmentación flexible, al tiempo que conserva una cuenta con marca de tiempo de los recorridos del cliente en la aplicación de experiencia.

### Uso de campos calculados {#calculated}

Ciertas interacciones en las aplicaciones de experiencia pueden dar como resultado varios eventos relacionados que técnicamente comparten la misma marca de tiempo de evento y, por lo tanto, se pueden representar como un único registro de evento. Por ejemplo, si un cliente ve un producto en su sitio web, esto puede dar como resultado un registro de evento que tenga dos posibilidades `eventType` values: un evento de &quot;vista de producto&quot; (`commerce.productViews`) o un evento genérico de &quot;vista de página&quot; (`web.webpagedetails.pageViews`). En estos casos, puede utilizar campos calculados para capturar los atributos más importantes cuando se capturan varios eventos en una sola visita.

[Preparación de datos de Adobe Experience Platform](../../data-prep/home.md) permite asignar, transformar y validar datos desde y hacia XDM. Uso de los disponibles [funciones de asignación](../../data-prep/functions.md) proporcionado por el servicio puede invocar operadores lógicos para priorizar, transformar o consolidar datos de registros de varios eventos cuando se incorporan en Experience Platform. En el ejemplo anterior, puede designar `eventType` como un campo calculado que priorizaría una &quot;vista de producto&quot; sobre una &quot;vista de página&quot; siempre que se produzcan ambos.

Si está introduciendo manualmente datos en Platform a través de la interfaz de usuario de, consulte la guía sobre [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para ver los pasos específicos sobre cómo crear campos calculados.

Si está transmitiendo datos a Platform mediante una conexión de origen, puede configurar el origen para que utilice campos calculados en su lugar. Consulte la [documentación de su origen particular](../../sources/home.md) para obtener instrucciones sobre cómo implementar campos calculados al configurar la conexión.

## Grupos de campos de esquema compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../field-groups/name-updates.md) para obtener más información.

El Adobe proporciona varios grupos de campos estándar para su uso con el [!DNL XDM ExperienceEvent] clase. A continuación se muestra una lista de algunos grupos de campos utilizados comúnmente para la clase:

* [[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferencias de saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Detalles de marketing de campaña]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Acciones de tarjeta]](../field-groups/event/card-actions.md)
* [[!UICONTROL Detalles del canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Detalles de comercio]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Detalles de depósito]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Detalles de intercambio de dispositivos]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Reserva de restaurante]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Detalles del ID del usuario final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalles del entorno]](../field-groups/event/environment-details.md)
* [[!UICONTROL Reserva de vuelo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentimiento de IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Reserva de alojamiento]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Detalles de solicitud de presupuesto]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Detalles de reserva]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Detalles web]](../field-groups/event/web-details.md)

## Apéndice

La siguiente sección contiene información adicional sobre [!UICONTROL ExperienceEvent de XDM] clase.

### Valores aceptados para `eventType` {#eventType}

En la tabla siguiente se describen los valores aceptados para `eventType`, junto con sus definiciones:

| Valor | Definición |
| --- | --- |
| `advertising.clicks` | Acciones de clic de un anuncio. |
| `advertising.completes` | Un recurso de medios cronometrados se ha visto hasta su finalización. Esto no significa necesariamente que el usuario haya visto todo el vídeo, ya que podría haberse saltado algunas partes. |
| `advertising.conversions` | Acciones predefinidas realizadas por un cliente que déclencheur un evento para la evaluación del rendimiento. |
| `advertising.federated` | Indica si se creó un evento de experiencia mediante federación de datos (uso compartido de datos entre clientes). |
| `advertising.firstQuartiles` | Se ha reproducido el 25 % de la duración de un anuncio de vídeo digital a velocidad normal. |
| `advertising.impressions` | Impresiones de un anuncio para un cliente con el potencial de ser visto. |
| `advertising.midpoints` | Se ha reproducido el 50 % de la duración de un anuncio de vídeo digital a velocidad normal. |
| `advertising.starts` | Ha comenzado a reproducirse un anuncio de vídeo digital. |
| `advertising.thirdQuartiles` | Se ha reproducido el 75 % de la duración de un anuncio de vídeo digital a velocidad normal. |
| `advertising.timePlayed` | Describe la cantidad de tiempo que un usuario dedica a un recurso de medios cronometrados específico. |
| `application.close` | Se cerró una solicitud o se envió en segundo plano. |
| `application.launch` | Se inició o se puso en primer plano una aplicación. |
| `commerce.checkouts` | Se ha producido un evento de cierre de compra para una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en el proceso. Si hay varios pasos, la marca de tiempo y la página/experiencia de referencia para cada evento se utilizan para identificar cada evento individual (paso), representado en orden. |
| `commerce.productListAdds` | Se ha agregado un producto a la lista de productos o al carro de compras. |
| `commerce.productListOpens` | Se ha inicializado o creado una nueva lista de productos (carro de compras). |
| `commerce.productListRemovals` | Se han eliminado una o más entradas de producto de una lista de productos o un carro de compras. |
| `commerce.productListReopens` | Un cliente ha reactivado una lista de productos (carro de compras) a la que ya no se podía acceder (abandonada), por ejemplo, mediante una actividad de remarketing. |
| `commerce.productListViews` | Una lista de productos o un carro de compras han recibido una o más vistas. |
| `commerce.productViews` | Un producto ha recibido una o más vistas. |
| `commerce.purchases` | Se ha aceptado un pedido. Esta es la única acción necesaria en una conversión comercial. Un evento de compra debe tener una lista de productos a la que se haga referencia. |
| `commerce.saveForLaters` | Se ha guardado una lista de productos para uso futuro, como una lista de deseos de productos. |
| `decisioning.propositionDisplay` | Se ha mostrado una propuesta de toma de decisiones a una persona. |
| `decisioning.propositionInteract` | Una persona interactuó con una propuesta de toma de decisiones. |
| `delivery.feedback` | Eventos de comentarios de una entrega, como un envío por correo electrónico. |
| `directMarketing.emailBounced` | Se ha devuelto un correo electrónico a una persona. |
| `directMarketing.emailBouncedSoft` | Un correo electrónico a una persona se ha devuelto sin problemas. |
| `directMarketing.emailClicked` | Una persona hizo clic en un vínculo de un correo electrónico de marketing. |
| `directMarketing.emailDelivered` | Se ha entregado correctamente un correo electrónico al servicio de correo electrónico de la persona |
| `directMarketing.emailOpened` | Una persona ha abierto un correo electrónico de marketing. |
| `directMarketing.emailUnsubscribed` | Una persona ha cancelado la suscripción a un correo electrónico de marketing. |
| `inappmessageTracking.dismiss` | Se ha descartado un mensaje en la aplicación. |
| `inappmessageTracking.display` | Se ha mostrado un mensaje en la aplicación. |
| `inappmessageTracking.interact` | Se ha interactuado con un mensaje en la aplicación. |
| `leadOperation.callWebhook` | Se llamó a un webhook en respuesta a un posible cliente. |
| `leadOperation.convertLead` | Se ha convertido un posible cliente. |
| `leadOperation.interestingMoment` | Se grabó un momento interesante para una persona. |
| `leadOperation.newLead` | Se ha creado un posible cliente. |
| `leadOperation.scoreChanged` | Se ha cambiado el valor del atributo de puntuación del posible cliente. |
| `leadOperation.statusInCampaignProgressionChanged` | El estado de un posible cliente en una campaña ha cambiado. |
| `listOperation.addToList` | Se agregó una persona a una lista de marketing. |
| `listOperation.removeFromList` | Se ha quitado una persona de una lista de marketing. |
| `message.feedback` | Eventos de comentarios como sent/bounce/error para mensajes enviados a un cliente. |
| `message.tracking` | Seguimiento de eventos como acciones de apertura/clic/personalizado en mensajes enviados a un cliente. |
| `opportunityEvent.addToOpportunity` | Se ha agregado una persona a una oportunidad. |
| `opportunityEvent.opportunityUpdated` | Se ha actualizado una oportunidad. |
| `opportunityEvent.removeFromOpportunity` | Se ha eliminado a una persona de una oportunidad. |
| `pushTracking.applicationOpened` | Una persona abrió una aplicación desde una notificación push. |
| `pushTracking.customAction` | Una persona hizo clic en una acción personalizada en una notificación push. |
| `web.formFilledOut` | Una persona rellenó un formulario en una página web. |
| `web.webinteraction.linkClicks` | Se ha seleccionado un vínculo una o más veces. |
| `web.webpagedetails.pageViews` | Una página web ha recibido una o más vistas. |

{style="table-layout:auto"}

### Valores sugeridos para `producedBy` {#producedBy}

En la tabla siguiente se describen algunos valores aceptados para `producedBy`:

| Valor | Definición |
| --- | --- |
| `self` | Self |
| `system` | Sistema |
| `salesRef` | Representante de ventas |
| `customerRep` | Representante del cliente |
