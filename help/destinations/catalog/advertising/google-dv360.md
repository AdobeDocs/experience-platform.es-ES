---
keywords: DoubleClick Gestor de ofertas;DoubleClick Gestor de ofertas;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Conexión de pantalla y vídeo de Google 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en todas las fuentes de inventario de dispositivos de visualización, vídeo y móviles.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 3154020d5be029c738c3a5bfe52ae975a15be2ec
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] connection

## Información general {#overview}

[!DNL Display & Video 360], anteriormente conocido como [!DNL DoubleClick Bid Manager], es una herramienta que se utiliza para ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en todas las fuentes de inventario de pantalla, vídeo y dispositivos móviles.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Display & Video 360] destinos:

* Las audiencias activadas se crean mediante programación en la plataforma Google.
* [!DNL Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado el [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Identidades compatibles {#supported-identities}

[!DNL Google Ad Manager] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| UUID de AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Uso de Google [UUID de AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para dirigirse a usuarios de California y al ID de cookie de Google para el resto de usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| MAID | ID de publicidad de Microsoft. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

## Requisitos previos {#prerequisites}

### Permitir inclusión en la lista {#allow-listing}

>[!NOTE]
>
>La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Display & Video 360] destino en Platform. Asegúrese de que Google haya completado el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear la variable [!DNL Google Display & Video 360] en Platform, debe ponerse en contacto con Google para solicitar que se incluya el Adobe en la lista de proveedores de datos permitidos y que su cuenta se añada a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **Su tipo de cuenta**: use **[!DNL Invite advertiser]** para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360 o que se utilicen **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, en función de su cuenta con Google:
   * Uso `Invite Advertiser` para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360.
   * Uso `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **[!UICONTROL ID de cuenta]**: Rellene su **[!DNL Invite partner]** o **[!DNL Invite advertiser]** ID de cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.

>[!NOTE]
>
>Al configurar un [!DNL Google Display & Video 360] destino, trabaje con su [!DNL Google Account Manager] o representante de Adobes para comprender qué tipo de cuenta tiene.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados

Para verificar si los datos se han exportado correctamente a la variable [!DNL Google Display & Video 360] destino, compruebe su [!DNL Google Display & Video 360] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecta {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando las cuentas de cliente no cumplen con las [requisitos previos](#prerequisites). Para solucionar este problema, póngase en contacto con Google y asegúrese de que su cuenta esté incluida en la lista de permitidos.