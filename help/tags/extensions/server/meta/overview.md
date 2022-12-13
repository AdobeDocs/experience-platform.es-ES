---
title: Información general sobre la extensión de la API de conversión de metadatos
description: Obtenga información sobre la extensión de la API de Meta conversiones para el reenvío de eventos en Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# [!DNL Meta Conversions API] información general de la extensión

La variable [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) le permite conectar los datos de marketing del lado del servidor a [!DNL Meta] tecnologías para optimizar el targeting de anuncios, reducir el coste por acción y medir los resultados. Los eventos están vinculados a un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID y se procesan de forma similar a los eventos del lado del cliente.

Al usar la variable [!DNL Meta Conversions API] , puede aprovechar las capacidades de la API en su [reenvío de eventos](../../../ui/event-forwarding/overview.md) reglas para enviar datos a [!DNL Meta] de Adobe Experience Platform Edge Network. Este documento explica cómo instalar la extensión y utilizar sus capacidades en un reenvío de eventos [regla](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Si está intentando enviar eventos a [!DNL Meta] desde el lado del cliente en lugar de desde el lado del servidor, utilice el [[!DNL Meta Pixiel] extensión de etiqueta](../../client/meta/overview.md) en su lugar.

## Requisitos previos

Para utilizar la extensión de , debe tener acceso al reenvío de eventos y tener una [!DNL Meta] cuenta con acceso a [!DNL Ad Manager] y [!DNL Event Manager]. Específicamente, debe copiar el ID de un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (o [crear una nueva [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) ) para que la extensión se pueda configurar en su cuenta de .

## Instalación de la extensión

Para instalar el [!DNL Meta Conversions API] , vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** desde el panel de navegación izquierdo. Desde aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Catálogo]** pestaña . Busque la variable [!UICONTROL API de metadatos] tarjeta y, a continuación, seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Instalar] botón seleccionado para la variable [!UICONTROL API de metadatos] en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/meta/install.png)

En la vista de configuración que aparece, debe proporcionar la variable [!DNL Pixel] ID que ha copiado anteriormente para vincular la extensión a su cuenta de . Puede pegar el ID directamente en la entrada o puede utilizar un elemento de datos en su lugar.

También debe proporcionar un token de acceso para utilizar la variable [!DNL Conversions API] específicamente. Consulte la [!DNL Conversions API] documentación sobre [generación de un token de acceso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) para ver los pasos sobre cómo obtener este valor.

Cuando termine, seleccione **[!UICONTROL Guardar]**

![La variable [!DNL Pixel] ID proporcionado como elemento de datos en la vista de configuración de la extensión.](../../../images/extensions/server/meta/configure.png)

La extensión está instalada y ahora puede emplear sus capacidades en las reglas de etiquetas.

## Configuración de una regla de reenvío de eventos {#rule}

Comience a crear una nueva regla de reenvío de eventos y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione **[!UICONTROL Extensión de la API de Meta Conversions]** para la extensión, seleccione **[!UICONTROL Enviar evento de API de conversiones]** para el tipo de acción.

![La variable [!UICONTROL Enviar vista de página] tipo de acción que se está seleccionando para una regla en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/meta/select-action.png)

Aparecen controles que permiten configurar los datos de evento a los que se enviarán [!DNL Meta] a través de la variable [!DNL Conversions API]. Estas opciones se pueden introducir directamente en las entradas proporcionadas o se pueden seleccionar elementos de datos existentes para representar los valores. Las opciones de configuración se dividen en cuatro secciones principales, tal como se describe a continuación.

| Sección Config | Descripción |
| --- | --- |
| [!UICONTROL Parámetros de eventos del servidor] | Información general sobre el evento, incluido el tiempo en que se produjo y la acción de origen que lo activó. Consulte la [[!DNL Conversions API] documentación](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) para obtener más información sobre estos parámetros.<br><br>También tiene la opción de **[!UICONTROL Habilitar uso limitado de datos]** para ayudarle a cumplir con las exclusiones de los clientes. Consulte la [!DNL Conversions API] documentación sobre [opciones de procesamiento de datos](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) para obtener más información sobre esta función. |
| [!UICONTROL Parámetros de información del cliente] | Datos de identidad de usuario que se utilizan para atribuir el evento a un cliente. Algunos de estos valores deben tener un cifrado hash para poder enviarse a la API. Consulte la [[!DNL Conversions API] documentación](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) para obtener más información sobre estos parámetros. |
| [!UICONTROL Datos personalizados] | Datos adicionales que se utilizarán para la optimización del envío de anuncios, proporcionados en forma de objeto JSON. Consulte la [[!DNL Conversions API] documentación](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) para obtener más información sobre las propiedades aceptadas para este objeto.<br><br>Si está enviando un evento de compra, debe utilizar esta sección para proporcionar los atributos necesarios `currency` y `value`. |
| [!UICONTROL Evento de prueba] | Esta opción se utiliza para verificar si la configuración está causando que los eventos del servidor sean recibidos por [!DNL Meta] según lo esperado. Para utilizar esta función, seleccione la opción **[!UICONTROL Enviar como evento de prueba]** y, a continuación, proporcione el código de evento de prueba que elija en la entrada siguiente. Una vez implementada la regla de reenvío de eventos, si ha configurado la extensión y la acción correctamente, debería ver las actividades que aparecen dentro de la variable **[!DNL Test Events]** ver en [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla.

![[!UICONTROL Conservar cambios] seleccionado para la configuración de la acción.](../../../images/extensions/server/meta/keep-changes.png)

Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**. Finalmente, publicar un nuevo reenvío de eventos [versión](../../../ui/publishing/builds.md) para habilitar los cambios realizados en la biblioteca.

## Pasos siguientes

Esta guía describe cómo enviar datos de eventos del lado del servidor a [!DNL Meta] usando la variable [!DNL Meta Conversions API] extensión. Para obtener más información sobre las etiquetas y el reenvío de eventos, consulte la [información general sobre las etiquetas](../../../home.md).
