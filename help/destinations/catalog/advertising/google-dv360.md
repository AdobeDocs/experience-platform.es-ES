---
keywords: DoubleClick Administrador de ofertas;DoubleClick administrador de ofertas;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Destino de conexión de Google Display y Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de objetivo de redireccionamiento y audiencia en las fuentes de inventario de dispositivos móviles, de vídeo y de visualización.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] connection

[!DNL Display & Video 360], anteriormente conocido como  [!DNL DoubleClick Bid Manager], es una herramienta que se utiliza para ejecutar campañas digitales con objetivo de redireccionamiento y audiencia en todas las fuentes de inventario de visualización, vídeo y móvil.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de destinos [!DNL Google Display & Video 360]:

* Puede enviar las [identidades](../../../identity-service/namespaces.md) siguientes a [!DNL Google Ads] destinos: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID de cookie de Google, IDFA, GAID, ID de Roku, ID de Microsoft e ID de Amazon Fire TV.
   * Google utilizará [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para los usuarios de destinatario en California y el ID de cookie de Google para todos los demás usuarios.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* La plataforma no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

### Tipo de exportación {#export-type}

**Exportación**  de segmentos: está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Display & Video 360] destino en Platform. Asegúrese de que Google haya completado el proceso de lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear el [!DNL Google Display & Video 360] destino en la plataforma, debe ponerse en contacto con Google para solicitar que se ponga el Adobe en la lista de proveedores de datos permitidos y que se agregue su cuenta a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID**  de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **Tipo** de cuenta: use  **[!DNL Invite advertiser]** para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360 o  **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.

## Configurar destino

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Google Display & Video 360] y seleccione **[!UICONTROL Configurar]**.

![Destino de Connect Google Display y Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre [!UICONTROL Activar] y [!UICONTROL Configurar], consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la [!UICONTROL Información básica] para el destino, así como los casos de uso de mercadotecnia que deben aplicarse a este destino.

![Información básica Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Utilice `Invite Advertiser` para permitir que las audiencias se compartan solamente con una marca específica de su cuenta de Display &amp; Video 360.
   * Utilice `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **[!UICONTROL ID]** de cuenta: Rellene su ID  **[!DNL Invite partner]** o  **[!DNL Invite advertiser]** cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Al configurar un [!DNL Google Display & Video 360] destino, trabaje con su [!DNL Google Account Manager] o representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos a [!DNL Google Display & Video 360]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Display & Video 360], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Display & Video 360], compruebe su cuenta [!DNL Google Display & Video 360]. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.