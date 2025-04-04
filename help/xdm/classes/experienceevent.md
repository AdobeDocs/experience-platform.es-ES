---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;identityMap;identity map;Identity Map;Identity Map;Diseño de esquema;Map;event modeling;event modeling;best practice;event;events;
solution: Experience Platform
title: Clase XDM ExperienceEvent
description: Obtenga información acerca de la clase XDM ExperienceEvent y las prácticas recomendadas para el modelado de datos de evento.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] clase

[!DNL XDM ExperienceEvent] es una clase estándar de modelo de datos de experiencia (XDM). Utilice esta clase para crear una instantánea con marca de tiempo del sistema cuando se produzca un evento específico o cuando se haya alcanzado un conjunto determinado de condiciones.

Un Evento de experiencia es un registro de hechos de lo que ocurrió, incluido el momento y la identidad de la persona involucrada. Los eventos pueden ser explícitos (acciones humanas directamente observables) o implícitos (planteados sin una acción humana directa) y se registran sin agregación ni interpretación. Para obtener más información de alto nivel sobre el uso de esta clase en el ecosistema de Experience Platform, consulte la [descripción general de XDM](../home.md#data-behaviors).

La propia clase [!DNL XDM ExperienceEvent] proporciona varios campos relacionados con series temporales a un esquema. Dos de estos campos (`_id` y `timestamp`) son **obligatorios** para todos los esquemas basados en esta clase, mientras que el resto son opcionales. Los valores de algunos de los campos se rellenan automáticamente cuando se incorporan datos.

![Estructura de ExperienceEvent de XDM tal como aparece en la interfaz de usuario de Experience Platform.](../images/classes/experienceevent/structure.png)

| Propiedad | Descripción |
| --- | --- |
| `_id`<br>**(obligatorio)** | El campo Clase de evento de experiencia `_id` identifica de forma exclusiva los eventos individuales que se incorporan a Adobe Experience Platform. Este campo se utiliza para realizar un seguimiento de la exclusividad de un evento individual, evitar la duplicación de datos y buscar ese evento en los servicios descendentes.<br><br>Cuando se detectan eventos duplicados, las aplicaciones y los servicios de Experience Platform pueden administrar la duplicación de forma diferente. Por ejemplo, los eventos duplicados en el servicio de perfiles se pierden si el evento con el mismo `_id` ya existe en el almacén de perfiles.<br><br>En algunos casos, `_id` puede ser un [Identificador único universal (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) o un [Identificador único global (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si está transmitiendo datos desde una conexión de origen o ingiriendo directamente desde un archivo de Parquet, debe generar este valor concatenando una cierta combinación de campos que hagan que el evento sea único. Algunos ejemplos de eventos que se pueden concatenar son el ID principal, la marca de tiempo, el tipo de evento, etc. El valor concatenado debe ser una cadena con formato `uri-reference`, lo que significa que se deben eliminar los caracteres de dos puntos. Después, el valor concatenado debe tener un cifrado hash con SHA-256 u otro algoritmo de su elección.<br><br>Es importante distinguir que **este campo no representa una identidad relacionada con una persona individual**, sino más bien el registro de datos en sí. Los datos de identidad relacionados con una persona deben relegarse a [campos de identidad](../schema/composition.md#identity) proporcionados por grupos de campos compatibles. |
| `eventMergeId` | Si se usa [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) para la ingesta de datos, representa el identificador del lote ingerido que provocó la creación del registro. El sistema rellena automáticamente este campo tras la ingesta de datos. No se admite el uso de este campo fuera del contexto de una implementación de Web SDK. |
| `eventType` | Cadena que indica el tipo o la categoría del evento. Este campo se puede utilizar si desea distinguir distintos tipos de eventos dentro del mismo esquema y conjunto de datos, como distinguir un evento de vista de producto de un evento de complemento al carro de compras para una compañía minorista.<br><br>Los valores estándar para esta propiedad se proporcionan en la [sección del apéndice](#eventType), con descripciones de su caso de uso previsto. Este campo es una enumeración ampliable, lo que significa que también puede utilizar sus propias cadenas de tipo de evento para categorizar los eventos que está rastreando.<br><br>`eventType` le limita a utilizar un solo evento por visita en la aplicación y, por lo tanto, debe utilizar campos calculados para que el sistema sepa qué evento es el más importante. Para obtener más información, consulte la sección sobre [prácticas recomendadas para campos calculados](#calculated). |
| `producedBy` | Valor de cadena que describe el productor o el origen del evento. Este campo se puede utilizar para filtrar ciertos productores de eventos si es necesario con fines de segmentación.<br><br>Algunos valores sugeridos para esta propiedad se proporcionan en la [sección del apéndice](#producedBy). Este campo es una enumeración extensible, lo que significa que también puede utilizar sus propias cadenas para representar a diferentes productores de eventos. |
| `identityMap` | Campo de asignación que contiene un conjunto de identidades con espacio de nombres para el individuo al que se aplica el evento. El sistema actualiza automáticamente este campo a medida que se incorporan los datos de identidad. Para utilizar correctamente este campo para [Perfil del cliente en tiempo real](../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.<br /><br />Consulte la sección sobre mapas de identidad en los [conceptos básicos de la composición de esquemas](../schema/composition.md#identityMap) para obtener más información sobre su caso de uso. |
| `timestamp`<br>**(obligatorio)** | Una marca de tiempo ISO 8601 de cuándo ocurrió el evento, con el formato [RFC 3339, sección 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Esta marca de tiempo **debe** se produjo en el pasado, pero **debe** tener lugar a partir de 1970. Consulte la sección siguiente sobre [marcas de tiempo](#timestamps) para conocer las prácticas recomendadas sobre el uso de este campo. |

{style="table-layout:auto"}

## Prácticas recomendadas para el modelado de eventos

Las siguientes secciones tratan sobre las prácticas recomendadas para diseñar esquemas XDM (Experience Data Model) basados en eventos en Adobe Experience Platform.

### Marcas de hora {#timestamps}

El campo raíz `timestamp` de un esquema de evento puede **solamente** representar la observación del propio evento y debe ocurrir en el pasado. Sin embargo, el evento **debe** tener lugar a partir de 1970. Si los casos de uso de la segmentación requieren el uso de marcas de tiempo que puedan producirse en el futuro, estos valores deben restringirse en cualquier parte del esquema de Experience Event.

Por ejemplo, si un negocio del sector de viajes y hospitalidad está modelando un evento de reserva de vuelo, el campo de nivel de clase `timestamp` representa el momento en el que se observó el evento de reserva. Otras marcas de tiempo relacionadas con el evento, como la fecha de inicio de la reserva de viaje, deben capturarse en campos independientes proporcionados por grupos de campos estándar o personalizados.

![Esquema de evento de experiencia de ejemplo con la reserva de vuelo y la fecha de inicio resaltadas.](../images/classes/experienceevent/timestamps.png)

Al mantener la marca de tiempo en el nivel de clase separada de otros valores de fecha y hora relacionados en los esquemas de evento, puede implementar casos de uso de segmentación flexible, al tiempo que conserva una cuenta con marca de tiempo de los recorridos del cliente en la aplicación de experiencia.

### Uso de campos calculados {#calculated}

Ciertas interacciones en las aplicaciones de experiencia pueden dar como resultado varios eventos relacionados que técnicamente comparten la misma marca de tiempo de evento y, por lo tanto, se pueden representar como un único registro de evento. Por ejemplo, si un cliente ve un producto en su sitio web, esto puede generar un registro de evento que tenga dos valores `eventType` potenciales: un evento de &quot;vista de producto&quot; (`commerce.productViews`) o un evento de &quot;vista de página&quot; genérico (`web.webpagedetails.pageViews`). En estos casos, puede utilizar campos calculados para capturar los atributos más importantes cuando se capturan varios eventos en una sola visita.

Use [Preparación de datos de Adobe Experience Platform](../../data-prep/home.md) para asignar, transformar y validar datos desde y hacia XDM. Con las [funciones de asignación](../../data-prep/functions.md) disponibles que proporciona el servicio, puede invocar a los operadores lógicos para priorizar, transformar o consolidar datos de registros de varios eventos cuando se incorporen a Experience Platform. En el ejemplo anterior, puede designar `eventType` como un campo calculado que daría prioridad a una &quot;vista de producto&quot; sobre una &quot;vista de página&quot; siempre que se produzcan ambos.

Si está ingiriendo datos manualmente en Experience Platform a través de la interfaz de usuario, consulte la guía de [campos calculados](../../data-prep/ui/mapping.md#calculated-fields) para ver los pasos específicos sobre cómo crear campos calculados.

Si está transmitiendo datos a Experience Platform mediante una conexión de origen, puede configurar el origen para que utilice campos calculados en su lugar. Consulte la [documentación de su origen en particular](../../sources/home.md) para obtener instrucciones sobre cómo implementar campos calculados al configurar la conexión.

## Grupos de campos de esquema compatibles {#field-groups}

>[!NOTE]
>
>Los nombres de varios grupos de campos han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../field-groups/name-updates.md) para obtener más información.

Adobe proporciona varios grupos de campos estándar para su uso con la clase [!DNL XDM ExperienceEvent]. A continuación se muestra una lista de algunos grupos de campos utilizados comúnmente para la clase:

* [[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferencias de saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Detalles de marketing de campaña]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Acciones de tarjeta]](../field-groups/event/card-actions.md)
* [[!UICONTROL Detalles de canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Detalles de Commerce]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Detalles de depósito]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Detalles de intercambio de dispositivos]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Reserva de restaurante]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Detalles del identificador de usuario final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Detalles del entorno]](../field-groups/event/environment-details.md)
* [[!UICONTROL Reserva de vuelo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentimiento de IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Reserva de alojamiento]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Detalles de interacción de MediaAnalytics]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Detalles de solicitud de presupuesto]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Detalles de la reserva]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Detalles web]](../field-groups/event/web-details.md)

## Apéndice

La siguiente sección contiene información adicional sobre la clase [!UICONTROL XDM ExperienceEvent].

### Valores aceptados para `eventType` {#eventType}

En la tabla siguiente se describen los valores aceptados de `eventType`, junto con sus definiciones:

| Valor | Definición |
| --- | --- |
| `advertising.clicks` | Este evento rastrea cuándo se produce una acción para seleccionar un anuncio. |
| `advertising.completes` | Este evento rastrea cuándo se ha visto un recurso de medios cronometrados hasta su finalización. Esto no significa necesariamente que el usuario haya visto todo el vídeo, ya que podría haberse saltado algunas partes. |
| `advertising.conversions` | Este evento rastrea una acción predefinida realizada por un cliente que almacena en déclencheur un evento para la evaluación del rendimiento. |
| `advertising.federated` | Este evento rastrea si se creó un Evento de experiencia mediante federación de datos (uso compartido de datos entre clientes). |
| `advertising.firstQuartiles` | Este evento rastrea cuándo se ha reproducido un anuncio de vídeo digital a velocidad normal durante el 25 % de su duración. |
| `advertising.impressions` | Este evento rastrea las impresiones de un anuncio para un cliente con el potencial de ser visto. |
| `advertising.midpoints` | Este evento rastrea cuándo se ha reproducido un anuncio de vídeo digital a lo largo del 50 % de su duración a velocidad normal. |
| `advertising.starts` | Este evento rastrea cuándo ha comenzado a reproducirse un anuncio de vídeo digital. |
| `advertising.thirdQuartiles` | Este evento rastrea cuándo se ha reproducido un anuncio de vídeo digital a velocidad normal durante el 75 % de su duración. |
| `advertising.timePlayed` | Este evento rastrea la cantidad de tiempo que un usuario dedica a un recurso de medios cronometrados específico. |
| `application.close` | Este evento rastrea cuándo se cerró una aplicación o se envió a segundo plano. |
| `application.launch` | Este evento rastrea cuándo se inició o se puso en primer plano una aplicación. |
| `click` | **Obsoleto** En su lugar, use `decisioning.propositionInteract`. |
| `commerce.backofficeCreditMemoIssued` | Este evento rastrea cuándo se ha emitido un aviso de crédito a un cliente. |
| `commerce.backofficeOrderCancelled` | Este evento rastrea cuándo se ha finalizado un proceso de compra iniciado anteriormente antes de completarse. |
| `commerce.backofficeOrderItemsShipped` | Este evento registra cuándo se han enviado físicamente los artículos comprados al cliente. |
| `commerce.backofficeOrderPlaced` | Este evento rastrea la colocación de un pedido. |
| `commerce.backofficeShipmentCompleted` | Este evento rastrea la finalización correcta de todo el proceso de envío. |
| `commerce.checkouts` | Este evento rastrea cuándo se ha producido un evento de cierre de compra para una lista de productos. Puede haber más de un evento de cierre de compra si hay varios pasos en el proceso. Si hay varios pasos, la marca de tiempo y la página/experiencia de referencia para cada evento se utilizan para identificar cada evento individual (paso), representado en orden. |
| `commerce.productListAdds` | Este evento rastrea cuándo se ha agregado un producto a la lista de productos o al carro de compras. |
| `commerce.productListOpens` | Este evento rastrea cuándo se ha inicializado o creado una nueva lista de productos (carro de compras). |
| `commerce.productListRemovals` | Este evento rastrea cuándo se ha eliminado una entrada de producto de una lista de productos o un carro de compras. |
| `commerce.productListReopens` | Este evento rastrea cuándo un cliente ha reactivado una lista de productos (carro de compras) que ya no era accesible (abandonada), como, por ejemplo, mediante una actividad de remarketing. |
| `commerce.productListViews` | Este evento rastrea cuándo una lista de productos o un carro de compras ha recibido una vista. |
| `commerce.productViews` | Este evento rastrea cuándo un producto ha recibido una o más vistas. |
| `commerce.purchases` | Este evento rastrea cuándo se ha aceptado un pedido. Esta es la única acción necesaria en una conversión comercial. Un evento de compra debe tener una lista de productos a la que se haga referencia. |
| `commerce.saveForLaters` | Este evento rastrea cuándo se ha guardado una lista de productos para uso futuro, como una lista de deseos de productos. |
| `decisioning.propositionDisplay` | Este evento se utiliza cuando Web SDK envía automáticamente información sobre lo que se muestra en una página. Sin embargo, no necesita este tipo de evento si ya incluye información de visualización de otras formas, como con las visitas individuales superiores e inferiores de la página. Para la parte inferior de las visitas individuales de página, puede elegir cualquier tipo de evento que desee. |
| `decisioning.propositionDismiss` | Este tipo de evento se utiliza cuando se descarta un mensaje en la aplicación o una tarjeta de contenido de Adobe Journey Optimizer. |
| `decisioning.propositionFetch` | Se utiliza para indicar que un evento se utiliza principalmente para recuperar la toma de decisiones. Adobe Analytics eliminará este evento automáticamente. |
| `decisioning.propositionInteract` | Este tipo de evento se utiliza para rastrear interacciones, como clics, en contenido personalizado. |
| `decisioning.propositionSend` | Este evento registra cuándo se ha decidido enviar a un cliente potencial una recomendación u oferta para su consideración. |
| `decisioning.propositionTrigger` | Los eventos de este tipo se almacenan en el almacenamiento local mediante [Web SDK](../../web-sdk/home.md), pero no se envían a Experience Edge. Cada vez que se cumple un conjunto de reglas, se genera un evento y se almacena en el almacenamiento local (si esa configuración está habilitada). |
| `delivery.feedback` | Este evento realiza un seguimiento de los eventos de comentarios de un envío, como un envío por correo electrónico. |
| `directMarketing.emailBounced` | Este evento rastrea cuándo rebotó un correo electrónico a una persona. |
| `directMarketing.emailBouncedSoft` | Este evento rastrea cuándo ha rebotado suavemente un correo electrónico a una persona. |
| `directMarketing.emailClicked` | Este evento rastrea cuándo una persona hizo clic en un vínculo en un correo electrónico de marketing. |
| `directMarketing.emailDelivered` | Este evento rastrea cuándo se entregó correctamente un correo electrónico al servicio de correo electrónico de una persona. |
| `directMarketing.emailOpened` | Este evento rastrea cuándo una persona ha abierto un correo electrónico de marketing. |
| `directMarketing.emailSent` | Este evento rastrea cuándo se ha enviado un correo electrónico de marketing a una persona. |
| `directMarketing.emailUnsubscribed` | Este evento rastrea cuándo una persona canceló la suscripción a un correo electrónico de marketing. |
| `display` | **Obsoleto** En su lugar, use `decisioning.propositionDisplay`. |
| `inappmessageTracking.dismiss` | Este evento rastrea cuándo se descartó un mensaje en la aplicación. |
| `inappmessageTracking.display` | Este evento rastrea cuándo se ha mostrado un mensaje en la aplicación. |
| `inappmessageTracking.interact` | Este evento rastrea cuándo se ha interactuado con un mensaje en la aplicación. |
| `leadOperation.callWebhook` | Este evento rastrea cuándo se llamó a un webhook en respuesta a un posible cliente. |
| `leadOperation.changeCampaignStream` | Este evento significa un cambio en la estrategia de marketing o participación de un posible cliente empresarial en particular. |
| `leadOperation.changeEngagementCampaignCadence` | Este evento rastrea cuándo se ha producido un cambio en la frecuencia con la que un posible cliente se involucra como parte de una campaña. |
| `leadOperation.convertLead` | Este evento rastrea cuándo se convirtió un posible cliente. |
| `leadOperation.interestingMoment` | Este evento rastrea cuándo se grabó un momento interesante para una persona. |
| `leadOperation.mergeLeads` | Este evento rastrea cuándo se consolidó la información de varios posibles clientes que hacen referencia a la misma entidad. |
| `leadOperation.newLead` | Este evento rastrea cuándo se creó un posible cliente. |
| `leadOperation.scoreChanged` | Este evento rastrea cuándo se cambió el valor del atributo de puntuación del posible cliente. |
| `leadOperation.statusInCampaignProgressionChanged` | Este evento rastrea cuándo ha cambiado el estado de un posible cliente en una campaña. |
| `listOperation.addToList` | Este evento rastrea cuándo se añadió una persona a una lista de marketing. |
| `listOperation.removeFromList` | Este evento rastrea cuándo se eliminó una persona de una lista de marketing. |
| `media.adBreakComplete` | Este evento indica la finalización de una pausa publicitaria. |
| `media.adBreakStart` | Este evento indica el inicio de una pausa publicitaria. |
| `media.adComplete` | Este evento indica la finalización de un anuncio. |
| `media.adSkip` | Este evento indica cuándo se ha omitido un anuncio. |
| `media.adStart` | Este evento indica el inicio de un anuncio. |
| `media.bitrateChange` | Este evento indica cuándo se produce un cambio en la velocidad de bits. |
| `media.bufferStart` | El tipo de evento `media.bufferStart` se envía cuando comienza el almacenamiento en búfer. No hay ningún tipo de evento `bufferResume` específico; se considera que el almacenamiento en búfer se reanudó cuando se envía un evento `play` después de un evento `bufferStart`. |
| `media.chapterComplete` | Este evento indica la finalización de un capítulo. |
| `media.chapterSkip` | Este evento se activa cuando un usuario salta hacia delante o hacia atrás a otra sección o capítulo. |
| `media.chapterStart` | Este evento indica el inicio de un capítulo. |
| `media.downloaded` | Este evento rastrea cuándo se ha producido el contenido descargado del medio. |
| `media.error` | Este evento indica cuándo se ha producido un error durante la reproducción del contenido. |
| `media.pauseStart` | Este evento rastrea cuándo se ha producido un evento `pauseStart`. Este evento se activa cuando un usuario inicia una pausa en la reproducción de contenido. No hay ningún tipo de evento de reanudación. Se infiere una reanudación cuando envía un evento de reproducción después de `pauseStart`. |
| `media.ping` | El tipo de evento `media.ping` se usa para indicar el estado de reproducción en curso. Para el contenido principal, este evento debe enviarse cada 10 segundos durante la reproducción, empezando 10 segundos después del inicio de la reproducción. Para el contenido de publicidad, debe enviarse cada segundo durante el seguimiento de la publicidad. Los eventos ping no deben incluir el mapa de parámetros en el cuerpo de la solicitud. |
| `media.play` | El tipo de evento `media.play` se envía cuando el reproductor pasa al estado `playing` desde otro estado, como `buffering,` `paused` (cuando el usuario lo reanuda) o `error` (cuando se recupera), incluidos escenarios como la reproducción automática. Este evento se activa mediante la llamada de retorno `on('Playing')` del reproductor. |
| `media.sessionComplete` | Este evento se envía cuando se llega al final del contenido principal. |
| `media.sessionEnd` | El tipo de evento `media.sessionEnd` notifica al backend de Media Analytics que cierre inmediatamente una sesión cuando un usuario abandone la visualización y es poco probable que vuelva. Si no se envía este evento, la sesión se cerrará tras 10 minutos de inactividad o 30 minutos sin movimiento del cabezal de reproducción. Se ignorarán todas las llamadas de medios subsiguientes con ese ID de sesión. |
| `media.sessionStart` | El tipo de evento `media.sessionStart` se envía con la llamada de inicio de sesión. Al recibir una respuesta, el ID de sesión se extrae del encabezado Ubicación y se utiliza para todas las llamadas de evento subsiguientes al servidor de recopilación. |
| `media.statesUpdate` | Este evento rastrea cuándo se ha producido un evento `statesUpdate`. Las funcionalidades de seguimiento de estado del reproductor se pueden adjuntar a un flujo de audio o vídeo. Los estados estándar son: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` y `inFocus`. |
| `opportunityEvent.addToOpportunity` | Este evento registra cuándo se añadió una persona a una oportunidad. |
| `opportunityEvent.opportunityUpdated` | Este evento rastrea cuándo se actualizó una oportunidad. |
| `opportunityEvent.removeFromOpportunity` | Este evento rastrea cuándo se eliminó una persona de una oportunidad. |
| `personalization.request` | **Obsoleto** En su lugar, use `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Este evento rastrea cuándo una persona abrió una aplicación desde una notificación push. |
| `pushTracking.customAction` | Este evento rastrea cuándo una persona seleccionó una acción personalizada en una notificación push. |
| `web.formFilledOut` | Este evento rastrea cuándo una persona ha rellenado un formulario en una página web. |
| `web.webinteraction.linkClicks` | El evento indica que Web SDK ha registrado automáticamente un clic en vínculo. |
| `web.webpagedetails.pageViews` | Este tipo de evento es el método estándar para marcar la visita como una vista de página. |
| `location.entry` | Este evento rastrea la entrada de una persona o dispositivo en una ubicación específica. |
| `location.exit` | Este evento rastrea la salida de una persona o dispositivo desde una ubicación específica. |

{style="table-layout:auto"}

### Valores sugeridos para `producedBy` {#producedBy}

En la tabla siguiente se describen algunos valores aceptados para `producedBy`:

| Valor | Definición |
| --- | --- |
| `self` | Self |
| `system` | Sistema |
| `salesRef` | Representante de ventas |
| `customerRep` | Representante del cliente |
