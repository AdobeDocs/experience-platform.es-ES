---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;mapa de identidad;mapa de identidad;mapa de identidad;diseño de esquema;mapa;mapa;modelado de eventos;modelado de eventos;prácticas recomendadas;evento;eventos;
solution: Experience Platform
title: Clase XDM ExperienceEvent
description: Este documento proporciona información general sobre la clase XDM ExperienceEvent y prácticas recomendadas para el modelado de datos de eventos.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: e4e87fdb5f6dfbca882f924d38397a904d8b0cff
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] clase

[!DNL XDM ExperienceEvent] es una clase estándar del Modelo de datos de experiencia (XDM) que le permite crear una instantánea con marca de tiempo del sistema cuando se produce un evento específico o cuando se alcanza un conjunto determinado de condiciones.

Un evento de experiencia es un registro de hechos de lo que ha sucedido, que incluye el momento y la identidad de la persona implicada. Los eventos pueden ser explícitos (acciones humanas directamente observables) o implícitos (se generan sin una acción humana directa) y se registran sin agregación ni interpretación. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de la Plataforma, consulte [Información general de XDM](../home.md#data-behaviors).

La variable [!DNL XDM ExperienceEvent] proporciona a un esquema varios campos relacionados con series temporales. Dos de estos campos (`_id` y `timestamp`) **obligatorio** para todos los esquemas basados en la clase, mientras que el resto son opcionales. Los valores de algunos de los campos se rellenan automáticamente cuando se introducen datos.

![La estructura de XDM ExperienceEvent tal como aparece en la interfaz de usuario de Platform](../images/classes/experienceevent/structure.png)

| Propiedad | Descripción |
| --- | --- |
| `_id`<br>**(Requerido)** | Identificador de cadena único para el evento. Este campo se utiliza para rastrear la exclusividad de un evento individual, evitar la duplicación de datos y buscar ese evento en servicios descendentes. En algunos casos, `_id` puede ser [Identificador único universal (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si transmite datos desde una conexión de origen o realiza la ingesta directamente desde un archivo de parquet, debe generar este valor concatenando una combinación determinada de campos que hagan que el evento sea único, como un ID principal, una marca de tiempo, un tipo de evento, etc. El valor concatenado debe ser un `uri-reference` cadena con formato , lo que significa que se deben eliminar los caracteres de dos puntos. Después, el valor concatenado debe tener un cifrado hash con SHA-256 u otro algoritmo de su elección.<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de los datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) proporcionado por grupos de campos compatibles en su lugar. |
| `eventMergeId` | Si se usa la variable [SDK web de Adobe Experience Platform](../../edge/home.md) para introducir datos, esto representa el ID del lote ingestado que provocó la creación del registro. El sistema rellena automáticamente este campo tras la ingesta de datos. No se admite el uso de este campo fuera del contexto de una implementación de SDK web. |
| `eventType` | Cadena que indica el tipo o la categoría del evento. Este campo se puede utilizar si desea distinguir diferentes tipos de eventos dentro del mismo esquema y conjunto de datos, como distinguir un evento de vista de producto de un evento de complemento del carro de compras para una empresa minorista.<br><br>Los valores estándar de esta propiedad se proporcionan en la variable [apéndice, sección](#eventType), incluidas las descripciones de su caso de uso previsto. Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas de tipo de evento para categorizar los eventos que rastrea. También puede [desactive cualquiera de los valores sugeridos estándar](../ui/fields/enum.md#standard-fields) para este campo si no se ajustan a sus casos de uso.<br><br>`eventType` limita el uso de un solo evento por visita en la aplicación y, por lo tanto, debe utilizar campos calculados para que el sistema sepa qué evento es más importante. Para obtener más información, consulte la sección sobre [prácticas recomendadas para campos calculados](#calculated). |
| `producedBy` | Un valor de cadena que describe el productor o el origen del evento. Este campo se puede utilizar para filtrar ciertos productores de eventos si es necesario para fines de segmentación.<br><br>Algunos valores sugeridos para esta propiedad se proporcionan en la sección [apéndice, sección](#producedBy). Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas para representar a diferentes productores de eventos. |
| `identityMap` | Campo de mapa que contiene un conjunto de identidades con espacio de nombres para la persona a la que se aplica el evento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en la [conceptos básicos de la composición del esquema](../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `timestamp`<br>**(Requerido)** | Marca de tiempo ISO 8601 del momento en que se produjo el evento, con el formato establecido en [RFC 3339, sección 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Esta marca de tiempo debe suceder en el pasado. Consulte la sección siguiente en [marcas de tiempo](#timestamps) para conocer las prácticas recomendadas sobre el uso de este campo. |

{style=&quot;table-layout:auto&quot;}

## Prácticas recomendadas para el modelado de eventos

Las siguientes secciones tratan sobre las prácticas recomendadas para diseñar los esquemas del Modelo de datos de experiencia (XDM) basados en eventos en Adobe Experience Platform.

### Marcas de hora {#timestamps}

La raíz `timestamp` campo de un esquema de eventos puede **only** representan la observación del propio evento, y debe ocurrir en el pasado. Si los casos de uso de segmentación requieren el uso de marcas de tiempo que puedan producirse en el futuro, estos valores deben restringirse en cualquier otra parte del esquema de eventos de experiencia.

Por ejemplo, si un negocio de la industria de viajes y hospitalidad está modelando un evento de reserva de vuelos, el nivel de clase `timestamp` representa la hora en la que se observó el evento de reserva. Otras marcas de tiempo relacionadas con el evento, como la fecha de inicio de la reserva de viajes, deben capturarse en campos separados proporcionados por grupos de campos estándar o personalizados.

![Un esquema de evento de experiencia de ejemplo con Reserva de vuelo y Fecha de inicio resaltadas.](../images/classes/experienceevent/timestamps.png)

Al mantener la marca de tiempo de nivel de clase separada de otros valores de fecha y hora relacionados en los esquemas de eventos, puede implementar casos de uso de segmentación flexible y, al mismo tiempo, preservar una cuenta con marca de tiempo de los recorridos del cliente en su aplicación de experiencia.

### Uso de campos calculados {#calculated}

Ciertas interacciones en las aplicaciones de experiencia pueden dar como resultado varios eventos relacionados que técnicamente comparten la misma marca de tiempo de evento y, por lo tanto, pueden representarse como un solo registro de evento. Por ejemplo, si un cliente visualiza un producto en el sitio web, esto puede generar un registro de evento que tenga dos posibles `eventType` valores: un evento de &quot;vista de producto&quot; (`commerce.productViews`) o un evento genérico de &quot;vista de página&quot; (`web.webpagedetails.pageViews`). En estos casos, puede utilizar campos calculados para capturar los atributos más importantes cuando se capturan varios eventos en una sola visita.

[Preparación de datos de Adobe Experience Platform](../../data-prep/home.md) permite asignar, transformar y validar datos desde y hacia XDM. Uso de los [funciones de asignación](../../data-prep/functions.md) proporcionado por el servicio, puede invocar operadores lógicos para priorizar, transformar y/o consolidar datos de registros de eventos múltiples al ingerirlos en Experience Platform. En el ejemplo anterior, puede designar `eventType` como campo calculado que daría prioridad a una &quot;vista de producto&quot; sobre una &quot;vista de página&quot; cada vez que se produjeran ambos.

Si está introduciendo datos manualmente en Platform a través de la interfaz de usuario, consulte la guía de [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para ver pasos específicos sobre cómo crear campos calculados.

Si está transmitiendo datos a Platform mediante una conexión de origen, puede configurar la fuente para que utilice campos calculados en su lugar. Consulte la [documentación de su fuente particular](../../sources/home.md) para obtener instrucciones sobre cómo implementar campos calculados al configurar la conexión.

## Grupos de campos de esquema compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../field-groups/name-updates.md) para obtener más información.

Adobe proporciona varios grupos de campos estándar para su uso con la variable [!DNL XDM ExperienceEvent] Clase . A continuación se muestra una lista de algunos grupos de campos que se utilizan con más frecuencia para la clase :

* [[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferencias de saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Detalles de marketing de campaña]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Acciones de tarjeta]](../field-groups/event/card-actions.md)
* [[!UICONTROL Detalles del canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Detalles del comercio]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Detalles del depósito]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Detalles del comercio de dispositivos]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Reserva de comedor]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Detalles del ID de usuario final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalles del entorno]](../field-groups/event/environment-details.md)
* [[!UICONTROL Reserva de vuelo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentimiento TCF 2.0 de IAB]](../field-groups/event/iab.md)
* [[!UICONTROL Reserva de alojamiento]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Detalles de solicitud de cotización]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Detalles de la reserva]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Detalles web]](../field-groups/event/web-details.md)

## Apéndice

La siguiente sección contiene información adicional sobre la variable [!UICONTROL XDM ExperienceEvent] Clase .

### Valores sugeridos para `eventType` {#eventType}

En la tabla siguiente se describen los valores sugeridos estándar para `eventType`, junto con sus definiciones:

| Valor | Definición |
| --- | --- |
| `advertising.clicks` | Haga clic en las acciones de un anuncio. |
| `advertising.completes` | Se ha visto hasta el final un recurso de medios temporizados. Esto no significa necesariamente que el usuario haya visto todo el vídeo, ya que el usuario podría haber omitido el vídeo. |
| `advertising.conversions` | Acciones predefinidas realizadas por un cliente que déclencheur un evento para la evaluación del rendimiento. |
| `advertising.federated` | Indica si un evento de experiencia se creó mediante una federación de datos (uso compartido de datos entre clientes). |
| `advertising.firstQuartiles` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal del 25% de su duración. |
| `advertising.impressions` | Impresión(s) de un anuncio a un cliente con el potencial de ser visto. |
| `advertising.midpoints` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 50% de su duración. |
| `advertising.starts` | Se ha empezado a reproducir un anuncio de vídeo digital. |
| `advertising.thirdQuartiles` | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 75% de su duración. |
| `advertising.timePlayed` | Describe la cantidad de tiempo que un usuario emplea en un recurso de medios temporizados específico. |
| `application.close` | Se cerró una aplicación o se envió al fondo. |
| `application.launch` | Se ha iniciado o introducido una aplicación en primer plano. |
| `commerce.checkouts` | Se ha producido un evento de cierre de compra para una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la marca de tiempo y la página/experiencia a la que se hace referencia para cada evento se utilizan para identificar cada evento individual (paso), representado en orden. |
| `commerce.productListAdds` | Se ha agregado un producto a la lista de productos o al carro de compras. |
| `commerce.productListOpens` | Se ha inicializado o creado una nueva lista de productos (carro de compras). |
| `commerce.productListRemovals` | Una o más entradas de producto se han eliminado de una lista de productos o de un carro de compras. |
| `commerce.productListReopens` | Un cliente ha reactivado una lista de productos (carro de compras) que ya no era accesible (abandonada), por ejemplo, mediante una actividad de remarketing. |
| `commerce.productListViews` | Una lista de productos o un carro de compras ha recibido una o más vistas. |
| `commerce.productViews` | Un producto ha recibido una o más vistas. |
| `commerce.purchases` | Se ha aceptado una solicitud. Esta es la única acción necesaria en una conversión de comercio. Un evento de compra debe tener una lista de productos referenciada. |
| `commerce.saveForLaters` | Se ha guardado una lista de productos para su uso futuro, como una lista de deseos de productos. |
| `decisioning.propositionDisplay` | Se mostró una propuesta de decisión a una persona. |
| `decisioning.propositionInteract` | Una persona interactuó con una propuesta de decisión. |
| `delivery.feedback` | Eventos de comentarios de un envío, como un envío de correo electrónico. |
| `directMarketing.emailBounced` | Un correo electrónico dirigido a una persona rebotó. |
| `directMarketing.emailBouncedSoft` | Un mensaje de correo electrónico dirigido a una persona devuelta por correo electrónico. |
| `directMarketing.emailClicked` | Una persona hizo clic en un vínculo de un correo electrónico de marketing. |
| `directMarketing.emailDelivered` | Se entregó correctamente un correo electrónico al servicio de correo electrónico de una persona |
| `directMarketing.emailOpened` | Una persona abrió un correo electrónico de marketing. |
| `directMarketing.emailUnsubscribed` | Una persona canceló la suscripción de un correo electrónico de marketing. |
| `inappmessageTracking.dismiss` | Se ha descartado un mensaje en la aplicación. |
| `inappmessageTracking.display` | Se ha mostrado un mensaje en la aplicación. |
| `inappmessageTracking.interact` | Se interactuó con un mensaje en la aplicación. |
| `leadOperation.callWebhook` | Se llamó a un enlace web en respuesta a un posible cliente. |
| `leadOperation.convertLead` | Se ha convertido un posible cliente. |
| `leadOperation.interestingMoment` | Se grabó un momento interesante para una persona. |
| `leadOperation.newLead` | Se creó un posible cliente. |
| `leadOperation.scoreChanged` | Se ha cambiado el valor del atributo de puntuación del posible cliente. |
| `leadOperation.statusInCampaignProgressionChanged` | El estado de un posible cliente en una campaña ha cambiado. |
| `listOperation.addToList` | Se agregó una persona a una lista de marketing. |
| `listOperation.removeFromList` | Se eliminó a una persona de una lista de marketing. |
| `message.feedback` | Eventos de comentarios como enviados/rechazados/errores para mensajes enviados a un cliente. |
| `message.tracking` | Eventos de seguimiento como acciones de apertura/clic/personalizadas en mensajes enviados a un cliente. |
| `opportunityEvent.addToOpportunity` | Se agregó una persona a una oportunidad. |
| `opportunityEvent.opportunityUpdated` | Se actualizó una oportunidad. |
| `opportunityEvent.removeFromOpportunity` | Una persona fue sacada de una oportunidad. |
| `pushTracking.applicationOpened` | Una persona abrió una aplicación desde una notificación push. |
| `pushTracking.customAction` | Una persona hizo clic en una acción personalizada en una notificación push. |
| `web.formFilledOut` | Una persona rellenó un formulario en una página web. |
| `web.webinteraction.linkClicks` | Se ha seleccionado un vínculo una o más veces. |
| `web.webpagedetails.pageViews` | Una página web ha recibido una o más vistas. |

{style=&quot;table-layout:auto&quot;}

### Valores sugeridos para `producedBy` {#producedBy}

En la tabla siguiente se describen los valores sugeridos estándar para `producedBy`:

| Valor | Definición |
| --- | --- |
| `self` | Self |
| `system` | Sistema |
| `salesRef` | Representante de ventas |
| `customerRep` | Representante del cliente |
