---
keywords: DoubleClick Gestor de ofertas;DoubleClick Gestor de ofertas;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Conexión de Google Display y Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en todas las fuentes de inventario de dispositivos de visualización, vídeo y móviles.
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] connection

## Información general {#overview}

[!DNL Display & Video 360], anteriormente conocido como  [!DNL DoubleClick Bid Manager], es una herramienta que se utiliza para ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en las fuentes de inventario de dispositivos móviles, de vídeo y de visualización.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de destinos [!DNL Google Display & Video 360]:

* Las audiencias activadas se crean mediante programación en la plataforma Google.
* [!DNL Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| UUID de AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como  [!DNL Device ID]. ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Google utiliza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para dirigirse a los usuarios de California, y el ID de cookie de Google para el resto de los usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| MAID | Microsoft Advertising ID. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar el primer destino [!DNL Google Display & Video 360] en Platform. Asegúrese de que Google haya completado el proceso de lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear el [!DNL Google Display & Video 360] destino en Platform, debe ponerse en contacto con Google para solicitar que el Adobe se incluya en la lista de proveedores de datos permitidos y que su cuenta se agregue a la lista de permitidos . Póngase en contacto con Google y proporcione la siguiente información:

* **ID de cuenta** : es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  de cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **El tipo** de cuenta: utilice  **[!DNL Invite advertiser]** para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360 o  **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.

## Configurar destino

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL Google Display & Video 360] y seleccione **[!UICONTROL Configure]**.

![Conectar el destino de Google Display y Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre [!UICONTROL Activate] y [!UICONTROL Configure], consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Setup** del flujo de trabajo de creación de destino, rellene [!UICONTROL Basic Information] para el destino, así como las acciones de marketing que deben aplicarse a este destino.

![Información básica Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Name]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Account Type]**: Seleccione una opción, en función de su cuenta con Google:
   * Utilice `Invite Advertiser` para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360.
   * Utilice `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Rellene su ID de  **[!DNL Invite partner]** cuenta  **[!DNL Invite advertiser]** o con Google. Normalmente, se trata de un ID de seis o siete dígitos.
* **[!UICONTROL Marketing action]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Al configurar un destino [!DNL Google Display & Video 360], trabaje con su [!DNL Google Account Manager] o representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos en [!DNL Google Display & Video 360]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Display & Video 360], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Display & Video 360] , compruebe su cuenta [!DNL Google Display & Video 360]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.