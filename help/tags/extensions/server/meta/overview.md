---
title: Información general sobre la extensión API Meta Conversions
description: Obtenga información acerca de la extensión de la API de metaconversiones para el reenvío de eventos en Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# [!DNL Meta Conversions API] información general sobre extensiones

El [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) le permite conectar los datos de marketing del lado del servidor a [!DNL Meta] para optimizar la segmentación de anuncios, reducir el coste por acción y medir los resultados. Los eventos están vinculados a una [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) Los ID y se procesan de forma similar a los eventos del lado del cliente.

Uso del [!DNL Meta Conversions API] , puede aprovechar las capacidades de la API en su [reenvío de eventos](../../../ui/event-forwarding/overview.md) reglas para enviar datos a [!DNL Meta] de Adobe Experience Platform Edge Network. Este documento explica cómo instalar la extensión y utilizar sus funcionalidades en un reenvío de eventos [regla](../../../ui/managing-resources/rules.md).

## Requisitos previos

Se recomienda encarecidamente utilizar [!DNL Meta Pixel] y el [!DNL Conversions API] para compartir y enviar los mismos eventos del lado del cliente y del lado del servidor, respectivamente, ya que esto puede ayudar a recuperar eventos que no recogieron [!DNL Meta Pixel]. Antes de instalar el [!DNL Conversions API] extensión, consulte la guía de la [[!DNL Meta Pixel] extensión](../../client/meta/overview.md) para ver los pasos necesarios para integrarlo en las implementaciones de etiquetas del lado del cliente.

>[!NOTE]
>
>La sección sobre [deduplicación de eventos](#deduplication) más adelante en este documento se explican los pasos para garantizar que el mismo evento no se utilice dos veces, ya que puede recibirse tanto desde el explorador como desde el servidor.

Para utilizar la variable [!DNL Conversions API] extensión, debe tener acceso al reenvío de eventos y tener un válido [!DNL Meta] cuenta con acceso a [!DNL Ad Manager] y [!DNL Event Manager]. Específicamente, debe copiar el ID de un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (o [crear un nuevo [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) en su lugar) para que la extensión se pueda configurar en su cuenta de.

## Instalación de la extensión

Para instalar el [!DNL Meta Conversions API] extensión, vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione la opción **[!UICONTROL Catálogo]** pestaña. Busque la variable [!UICONTROL API de metaconversiones] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![El [!UICONTROL Instalar] botón seleccionado para la [!UICONTROL API de metaconversiones] en la IU de recopilación de datos.](../../../images/extensions/server/meta/install.png)

En la vista de configuración que aparece, debe proporcionar el [!DNL Pixel] ID que copió anteriormente para vincular la extensión a su cuenta. Puede pegar el ID directamente en la entrada o utilizar un elemento de datos en su lugar.

También debe proporcionar un token de acceso para utilizar [!DNL Conversions API] específicamente. Consulte la [!DNL Conversions API] documentación sobre [generación de un token de acceso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) para ver los pasos para obtener este valor.

Cuando termine, seleccione **[!UICONTROL Guardar]**

![El [!DNL Pixel] El ID proporcionado como elemento de datos en la vista de configuración de la extensión.](../../../images/extensions/server/meta/configure.png)

La extensión está instalada y ahora puede utilizar sus funcionalidades en las reglas de reenvío de eventos.

## Configuración de una regla de reenvío de eventos {#rule}

Esta sección explica cómo usar el [!DNL Conversions API] en una regla genérica de reenvío de eventos. En la práctica, debe configurar varias reglas para enviar todos los mensajes aceptados [eventos estándar](https://developers.facebook.com/docs/meta-pixel/reference) mediante [!DNL Meta Pixel] y [!DNL Conversions API].

>[!NOTE]
>
>Los eventos deben ser [enviado en tiempo real](https://www.facebook.com/business/help/379226453470947?id=818859032317965) o lo más cerca posible del tiempo real para una mejor optimización de la campaña publicitaria.

Comience a crear una nueva regla de reenvío de eventos y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione **[!UICONTROL Extensión de API de metaconversiones]** para la extensión, seleccione **[!UICONTROL Enviar evento de API de conversiones]** para el tipo de acción.

![El [!UICONTROL Enviar vista de página] Tipo de acción seleccionado para una regla de la IU de recopilación de datos.](../../../images/extensions/server/meta/select-action.png)

Aparecen controles que permiten configurar los datos de evento que se envían a [!DNL Meta] a través de [!DNL Conversions API]. Estas opciones se pueden introducir directamente en las entradas proporcionadas o puede seleccionar elementos de datos existentes para representar los valores. Las opciones de configuración se dividen en cuatro secciones principales, como se describe a continuación.

| Sección Config | Descripción |
| --- | --- |
| [!UICONTROL Parámetros de evento del servidor] | Información general sobre el evento, incluida la hora en que se produjo y la acción de origen que lo activó. Consulte la [!DNL Meta] documentación para desarrolladores para obtener más información sobre [parámetros de evento estándar](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) aceptado por el [!DNL Conversions API].<br><br>Si utiliza ambos [!DNL Meta Pixel] y el [!DNL Conversions API] para enviar eventos, asegúrese de incluir un **[!UICONTROL Nombre del evento]** (`event_name`) y **[!UICONTROL ID de evento]** (`event_id`) con cada evento, ya que estos valores se utilizan para [deduplicación de eventos](#deduplication).<br><br>También tiene la opción de **[!UICONTROL Habilitar uso limitado de datos]** para ayudar a cumplir con las exclusiones de los clientes. Consulte la [!DNL Conversions API] documentación sobre [opciones de procesamiento de datos](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) para obtener más información sobre esta función. |
| [!UICONTROL Parámetros de información del cliente] | Datos de identidad del usuario que se utilizan para atribuir el evento a un cliente. Algunos de estos valores deben tener un cifrado hash para poder enviarlos a la API.<br><br>Para garantizar una buena conexión API común y una alta calidad de coincidencia de eventos (EMQ), se recomienda enviar todos los [parámetros de información de cliente aceptados](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) junto con eventos de servidor. Estos parámetros también deben ser [priorizadas en función de su importancia e impacto en EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Datos personalizados] | Datos adicionales que se utilizarán para la optimización de la entrega de anuncios, proporcionados en forma de objeto JSON. Consulte la [[!DNL Conversions API] documentación](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) para obtener más información sobre las propiedades aceptadas para este objeto.<br><br>Si envía un evento de compra, debe utilizar esta sección para proporcionar los atributos necesarios `currency` y `value`. |
| [!UICONTROL Evento de prueba] | Esta opción se utiliza para comprobar si la configuración está provocando que reciba eventos de servidor [!DNL Meta] como se esperaba. Para utilizar esta función, seleccione la **[!UICONTROL Enviar como evento de prueba]** y, a continuación, proporcione un código de evento de prueba de su elección en la entrada siguiente. Una vez implementada la regla de reenvío de eventos, si configuró la extensión y la acción correctamente, debería ver las actividades que aparecen dentro de la variable **[!DNL Test Events]** ver en [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para añadir la acción a la configuración de regla.

![[!UICONTROL Conservar cambios] seleccionado para la configuración de acción.](../../../images/extensions/server/meta/keep-changes.png)

Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**. Por último, publique un nuevo reenvío de eventos [generar](../../../ui/publishing/builds.md) para habilitar los cambios realizados en la biblioteca.

## Deduplicación de eventos {#deduplication}

Como se menciona en el [sección de requisitos previos](#prerequisites), se recomienda utilizar tanto la variable [!DNL Meta Pixel] extensión de etiquetas y [!DNL Conversions API] extensión de reenvío de eventos para enviar los mismos eventos desde el cliente y el servidor en una configuración redundante. Esto puede ayudar a recuperar eventos que no fueron recogidos por una extensión u otra.

Si envía diferentes tipos de eventos desde el cliente y el servidor sin superposición entre los dos, la anulación de duplicación no es necesaria. Sin embargo, si un solo evento lo comparten ambos [!DNL Meta Pixel] y el [!DNL Conversions API], debe asegurarse de que estos eventos redundantes se dedupliquen para que la creación de informes no se vea afectada negativamente.

Al enviar eventos compartidos, asegúrese de incluir un ID y un nombre de evento con cada evento que envíe desde el cliente y el servidor. Cuando se reciben varios eventos con el mismo ID y nombre, [!DNL Meta] emplea automáticamente varias estrategias para deduplicarlas y conservar los datos más relevantes. Consulte la [!DNL Meta] documentación sobre [deduplicación para [!DNL Meta Pixel] y [!DNL Conversions API] eventos](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) para obtener más información sobre este proceso.

## Pasos siguientes

En esta guía se explica cómo enviar datos de eventos del lado del servidor a [!DNL Meta] uso del [!DNL Meta Conversions API] extensión. Desde aquí, se recomienda ampliar la integración conectando más [!DNL Pixels] y compartir más eventos cuando corresponda. Realizar cualquiera de las siguientes acciones puede ayudar a mejorar aún más el rendimiento de su anuncio:

* Conectar cualquier otro [!DNL Pixels] que aún no están conectados a un [!DNL Conversions API] integración.
* Si envía ciertos eventos exclusivamente a través de [!DNL Meta Pixel] en el lado del cliente, envíe estos mismos eventos a [!DNL Conversions API] también desde el lado del servidor.

Consulte la [!DNL Meta] documentación sobre [prácticas recomendadas para [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obtener más información sobre cómo implementar de forma eficaz su integración. Para obtener información más general sobre las etiquetas y el reenvío de eventos en Adobe Experience Cloud, consulte [información general sobre etiquetas](../../../home.md).
