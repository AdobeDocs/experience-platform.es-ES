---
keywords: Publicidades de Google;publicidades de Google;adwords de Google;Google AdWords;Google Adwords
title: Conexión de Google Ads
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por clic en publicidad en búsquedas basadas en texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# [!DNL Google Ads] connection

## Información general {#overview}

[!DNL Google Ads], anteriormente conocido como  [!DNL Google AdWords], es un servicio de publicidad en línea que permite a las empresas pagar por clic en publicidad en búsquedas basadas en texto, visualizaciones gráficas,  [!DNL YouTube] vídeos y visualizaciones móviles dentro de la aplicación.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de destinos [!DNL Google Ads]:

* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* Actualmente, Platform no incluye una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ads] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con el Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

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

### Cuenta existente [!DNL Google Ads]

>[!IMPORTANT]
>
> [!DNL Google] ha desaprobado nuevas integraciones de  [!DNL Google Ads] cookies con proveedores de terceros. Para realizar los pasos de lista de permitidos en la siguiente sección, debe tener una integración existente con [!DNL Google Ads]. Como resultado, el método recomendado para utilizar [!DNL Google Ads] es configurar una integración [!DNL Google Customer Match]. Para obtener más información sobre la creación de una integración [!DNL Google Customer Match], lea el tutorial sobre la creación de una conexión [[!DNL Google Customer Match]](./google-customer-match.md).

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar el primer destino [!DNL Google Ads] en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado por [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ads] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos . Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta** : es el ID de cuenta de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  de cliente: es el ID de cuenta de cliente de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* El tipo de cuenta: **AdWords**
* **ID de Google AdWords** : Este es su ID con  [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Configurar destino

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL Google Ads] y seleccione **[!UICONTROL Configure]**.

![Conectar destino de Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Setup** del flujo de trabajo de creación de destino, rellene [!UICONTROL Basic Information] para el destino.

![Información básica de Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Account Type]**: AdWords es la única opción disponible.
* **[!UICONTROL Account ID]**: Rellene su ID de cuenta con  [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.
* **[!UICONTROL Marketing action]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

## Activar segmentos en [!DNL Google Ads]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ads], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Ads] , compruebe su cuenta [!DNL Google Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.