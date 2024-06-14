---
title: Información general sobre la extensión de la API de conversiones en tiempo real de Trade Desk
description: Obtenga información acerca de la extensión de la API de Conversiones en tiempo real de Trade Desk para el reenvío de eventos en Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 8000bbf36e6763b8fca17c2ae0d5c2fe53bc6964
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API] información general sobre extensiones

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) permite enviar eventos a [!DNL The Trade Desk] para aprovechar el retargeting y la atribución.

Puede usar el complemento [!DNL The Trade Desk Real-Time Conversions API] extensión para enviar datos del Edge Network de Adobe Experience Platform a [!DNL The Trade Desk] mediante la utilización de las capacidades de la API en su [reenvío de eventos](../../../ui/event-forwarding/overview.md) reglas.

Uso de [!DNL The Trade Desk Real-Time Conversions API] , puede aprovechar las capacidades de la API en su [reenvío de eventos](../../../ui/event-forwarding/overview.md) reglas para enviar datos a [!DNL The Trade Desk] del Edge Network de Adobe Experience Platform.

Lea este documento para aprender a instalar la extensión y utilizar sus funcionalidades en un reenvío de eventos [regla](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Esta extensión y página de documentación la mantiene [!DNL The Trade Desk] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente.

## Requisitos previos {#prerequisites}

Debe tener un ID del anunciante, un ID de UPixel y un ID de rastreador relevantes dentro de su [!DNL The Trade Desk] para configurar la cuenta de [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Si es un comerciante, también deberá obtener su ID de comerciante.

## Instalación y configuración de [!DNL The Trade Desk] API de conversiones en tiempo real {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o seleccione una propiedad existente para editarla.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** , seleccione la pestaña **[!UICONTROL La Oficina de Comercio]** Tarjeta API de conversiones en tiempo real y, a continuación, seleccione **[!UICONTROL Instalar]**.

![El catálogo de extensiones que muestra [!DNL The Trade Desk] instalación de resalte de tarjeta de extensión.](../../../images/extensions/server/tradedesk/install-extension.png)

En la pantalla siguiente, introduzca la variable [!UICONTROL ID del anunciante]y, opcionalmente, un [!UICONTROL ID de comerciante]. Puede pegar el ID directamente en estas entradas o utilizar un elemento de datos en su lugar. Estos servirán como valores predeterminados utilizados al realizar una llamada de evento a [!DNL The Trade Desk] API de conversiones en tiempo real. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

Para obtener información sobre cómo crear elementos de datos y ponerlos a disposición de las extensiones de la propiedad de etiquetas, siga los [Creación de elementos de datos](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) tutorial.

![El [!DNL The Trade Desk] página de configuración de la extensión con [!UICONTROL ID del anunciante] y [!UICONTROL ID de comerciante] campos resaltados.](../../../images/extensions/server/tradedesk/configure-extension.png)

La extensión está instalada y ahora puede utilizar sus funcionalidades en las reglas de reenvío de eventos.

## Configuración de una regla de reenvío de eventos {#rule}

Una vez que haya instalado y configurado la extensión de, puede empezar a crear reglas de reenvío de eventos que determinen cómo y cuándo se enviarán los eventos a [!DNL The Trade Desk].

Debe considerar la posibilidad de configurar varias reglas para enviar todos los mensajes aceptados [solicitar propiedades](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) mediante [!DNL The Trade Desk] y [!DNL The Trade Desk] API de conversiones en tiempo real.

>[!NOTE]
>
>Los eventos deben enviarse en tiempo real o lo más cerca posible del tiempo real.

Crear un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) en la propiedad de reenvío de eventos. En **[!UICONTROL Acciones]**, añada una nueva acción y establezca la extensión en **[!UICONTROL La Oficina de Comercio]**. A continuación, seleccione **[!UICONTROL Conversión en tiempo real]** para el **[!UICONTROL Tipo de acción]**.

![La vista Reglas de propiedad de reenvío de eventos, con los campos necesarios para agregar una configuración de acción de regla de reenvío de eventos resaltados.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Después de la selección, aparecen controles adicionales para configurar aún más los datos de evento que se enviarán a [!DNL The Trade Desk]. Seleccionar **[!UICONTROL Conservar cambios]** para guardar la regla.

Las opciones de configuración se dividen en tres secciones principales, como se describe a continuación:

**[!UICONTROL Propiedades de solicitud básicas]**

| Entrada | Descripción |
| --- | --- |
| ID de rastreador | El ID de plataforma del rastreador de eventos. |
| ID de UPixel | El ID de píxel universal para el evento. |
| URL de referente | Dirección URL del sitio web desde el que se produjo el evento, si lo hay. |
| Nombre del evento | El tipo de evento definido por la plataforma de socio. |
| Valor | El valor de seguimiento de ingresos en una cadena decimal (por ejemplo, &quot;19,98&quot;). |
| Moneda | Código de divisa en formato ISO. |
| IP del cliente | La dirección IP del cliente IPv4 o IPv6. |
| ID de anuncio | ID único de publicidad del evento. |
| Tipo de ID de anuncio | El tipo de ID de publicidad especificado en la propiedad AD ID: TDID, IDFA, AAID, DAID, NAID, IDL, EUID o UID2. |
| Impresión | Una cadena de 36 caracteres (incluidos guiones) que sirve como ID único para la impresión a la que se atribuye el evento. |
| ID de pedido | El identificador de pedido asociado del evento. |
| td1-td10 | Diez propiedades dinámicas personalizadas numeradas secuencialmente que se pueden utilizar para proporcionar metadatos de conversión adicionales. |

{style="table-layout:auto"}

![El [!DNL Basic Request Properties] sección que muestra la entrada de datos de ejemplo en los campos.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Consulte la [!DNL The Trade Desk] documentación para desarrolladores para obtener más información sobre [solicitar propiedades](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) aceptado por [!DNL The Trade Desk] API de conversiones en tiempo real.

**[!UICONTROL Parámetros de solicitud de objeto]**

Lea la siguiente sección para obtener más información sobre los parámetros de solicitud con formato JSON como Elementos, Privacidad y Procesamiento de datos.

![El [!DNL Object Request Parameters] que muestra los campos disponibles.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Consulte la [Evento de conversiones en tiempo real](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) para obtener más información sobre [!UICONTROL Parámetros de solicitud de objeto] y sus propiedades.

**[!UICONTROL Anulaciones de configuración]**

>NOTA
>
>El [!UICONTROL Anulaciones de configuración] Los campos de permiten configurar un [!DNL Advertiser ID] y/o [!DNL Merchant ID] en cada regla.

| Entrada | Descripción |
| --- | --- |
| ID del anunciante | El ID del anunciante que desea anular el ID del anunciante proporcionado en la configuración de la extensión. |
| ID de comerciante | El ID del comerciante que desea anular el ID del comerciante proporcionado en la configuración de la extensión. |

![El [!DNL Configuration Overrides] que muestra los campos disponibles.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**. Por último, publique un nuevo reenvío de eventos [generar](../../../ui/publishing/builds.md) para habilitar los cambios realizados en la biblioteca.

## Pasos siguientes

En esta guía se explica cómo enviar datos de eventos del lado del servidor a [!DNL The Trade Desk] uso del [!DNL The Trade Desk] Extensión de la API de conversiones en tiempo real. A partir de aquí, se recomienda ampliar la integración creando reglas distintas que envíen eventos de conversión específicos según corresponda por campaña. Para obtener más información sobre las funcionalidades de reenvío de eventos en [!DNL Adobe Experience Platform], lea la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).

Consulte la [!DNL The Trade Desk] documentación sobre [prácticas recomendadas para [!DNL The Trade Desk] API de conversiones en tiempo real](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obtener más información sobre cómo implementar de forma eficaz su integración.

Para obtener más información sobre cómo depurar la implementación con la herramienta Experience Platform Debugger y la herramienta de monitorización del reenvío de eventos, lea la [información general de Adobe Experience Platform Debugger](../../../../debugger/home.md) y [Monitorización de actividades en el reenvío de eventos](../../../ui/event-forwarding/monitoring.md).
