---
keywords: Publicidades de Google;publicidades de Google;adwords de Google;Google AdWords;Google Adwords
title: Conexión de Google Ads
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por clic en publicidad en búsquedas basadas en texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 2%

---

# [!DNL Google Ads] connection

## Información general {#overview}

[!DNL Google Ads], anteriormente conocido como  [!DNL Google AdWords], es un servicio de publicidad en línea que permite a las empresas pagar por clic en publicidad en búsquedas basadas en texto, visualizaciones gráficas,  [!DNL YouTube] vídeos y visualizaciones móviles dentro de la aplicación.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de destinos [!DNL Google Ads]:

* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* [!DNL Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ads] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con el Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Identidades compatibles {#supported-identities}

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

### Cuenta existente [!DNL Google Ads]

>[!IMPORTANT]
>
> [!DNL Google] ha desaprobado nuevas integraciones de  [!DNL Google Ads] cookies con proveedores de terceros. Para realizar los pasos de lista de permitidos en la siguiente sección, debe tener una integración existente con [!DNL Google Ads]. Como resultado, el método recomendado para utilizar [!DNL Google Ads] es configurar una integración [!DNL Google Customer Match]. Para obtener más información sobre la creación de una integración [!DNL Google Customer Match], lea el tutorial sobre la creación de una conexión [[!DNL Google Customer Match]](./google-customer-match.md).

### Permitir inclusión en la lista {#allow-listing}

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar el primer destino [!DNL Google Ads] en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado por [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ads] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos . Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID** de cliente: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* El tipo de cuenta: **AdWords**
* **ID de Google AdWords**: Este es su ID con  [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: AdWords es la única opción disponible.
* **[!UICONTROL ID de cuenta]**: Rellene su ID de cuenta con  [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Ads] , compruebe su cuenta [!DNL Google Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

### 400 Mensaje de error de solicitud incorrecta {#bad-request}

Al configurar este destino, puede recibir el siguiente error:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este error se produce cuando los clientes intentan configurar el destino sin una cuenta [!DNL Google Ads] existente.

[!DNL Google] ha desaprobado nuevas integraciones de  [!DNL Google Ads] cookies con proveedores de terceros. Para realizar los pasos [allow-list](#allow-listing), debe tener una integración existente con [!DNL Google Ads].

El método recomendado para utilizar [!DNL Google Ads] es configurar una integración [[!DNL Google Customer Match]](google-customer-match.md).
