---
keywords: Publicidades de Google;publicidades de Google;adwords de Google;Google AdWords;Google Adwords
title: Conexión de Google Ads
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# [!DNL Google Ads] connection

[!DNL Google Ads], anteriormente conocido como  [!DNL Google AdWords], es un servicio de publicidad en línea que permite a las empresas pagar por publicidad en búsquedas basadas en texto, visualizaciones gráficas,  [!DNL YouTube] vídeos y visualizaciones móviles dentro de la aplicación.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de destinos [!DNL Google Ads]:

* Puede enviar las [identidades](../../../identity-service/namespaces.md) siguientes a [!DNL Google Ads] destinos: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID de cookie de Google, IDFA, GAID, ID de Roku, ID de Microsoft e ID de Amazon Fire TV.
   * Google utilizará [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para los usuarios de destinatario en California y el ID de cookie de Google para todos los demás usuarios.
* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* La plataforma no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ads] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

### Tipo de exportación {#export-type}

**Exportación**  de segmentos: está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos

### Cuenta existente [!DNL Google Ads]

>[!IMPORTANT]
>
> [!DNL Google] ha desaprobado nuevas integraciones de  [!DNL Google Ads] cookies con proveedores de terceros. Para realizar los pasos de lista de permitidos en la siguiente sección, debe tener una integración existente con [!DNL Google Ads]. Como resultado, el método recomendado para utilizar [!DNL Google Ads] es configurar una integración [!DNL Google Customer Match]. Para obtener más información sobre la creación de una integración [!DNL Google Customer Match], lea el tutorial sobre la creación de una conexión [[!DNL Google Customer Match]](./google-customer-match.md).

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Ads] destino en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación haya sido completado por [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ads] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se ponga en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID**  de cuenta: es el ID de cuenta de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  del cliente: es el ID de cuenta de cliente de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* El tipo de cuenta: **AdWords**
* **ID**  de Google AdWords: Este es su ID con  [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Configurar destino

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Google Ads] y seleccione **[!UICONTROL Configurar]**.

![Destino de Connect Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la [!UICONTROL Información básica] para el destino.

![Información básica de Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: AdWords es la única opción disponible.
* **[!UICONTROL ID]** de cuenta: Rellene su ID de cuenta con  [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

## Activar segmentos a [!DNL Google Ads]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ads], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Ads], compruebe su cuenta [!DNL Google Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.