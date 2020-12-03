---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Destino de Google Display y Video 360
seo-title: Destino de Google Display y Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de objetivo de redireccionamiento y audiencia en las fuentes de inventario de dispositivos móviles, de vídeo y de visualización.
seo-description: 'Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de objetivo de redireccionamiento y audiencia en las fuentes de inventario de dispositivos móviles, de vídeo y de visualización. '
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Destino

## Información general

[!DNL Display & Video 360], anteriormente conocido como [!DNL DoubleClick Bid Manager], es una herramienta que se utiliza para ejecutar campañas digitales con objetivo de redireccionamiento y audiencia en todas las fuentes de inventario de visualización, vídeo y móvil.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de los [!DNL Google Display & Video 360] destinos:

* Puede enviar las siguientes [identidades](../../../identity-service/namespaces.md) a [!DNL Google Display & Video 360] destinos: ID de cookie de Google, IDFA, GAID, Roku ID, Microsoft ID y Amazon Fire TV ID.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* CDP en tiempo real no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado la funcionalidad [de sincronización de](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) ID en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a CDP en tiempo real.

### Tipo de exportación {#export-type}

**Exportación** de segmentos: está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos 

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Display & Video 360] destino en CDP en tiempo real. Asegúrese de que Google haya completado el proceso de lista de permitidos que se describe a continuación antes de crear un destino.

Antes de crear el [!DNL Google Display & Video 360] destino en CDP en tiempo real, debe comunicarse con Google para solicitar Adobes a la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **Tipo** de cuenta: utilice **[!DNL Invite advertiser]** para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360 o **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.

## Configurar destino

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Google Display & Video 360]y seleccione **[!UICONTROL Configurar]**.

![Destino de Connect Google Display y Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre [!UICONTROL Activar] y [!UICONTROL Configurar], consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la información  básica del destino, así como los casos de uso de mercadotecnia que deben aplicarse a este destino.

![Información básica Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Utilícelo `Invite Advertiser` para permitir que las audiencias se compartan únicamente con una marca específica de su cuenta de Display &amp; Video 360.
   * Utilícelo `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **[!UICONTROL ID]** de cuenta: Rellene su ID **[!DNL Invite partner]** o **[!DNL Invite advertiser]** de cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](../../../data-governance/policies/overview.md#core-actions)datos.

>[!NOTE]
>
>Al configurar un [!DNL Google Display & Video 360] destino, trabaje con su representante [!DNL Google Account Manager] o Adobe para saber qué tipo de cuenta tiene.

## Activar segmentos para [!DNL Google Display & Video 360]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Display & Video 360], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al [!DNL Google Display & Video 360] destino, compruebe su [!DNL Google Display & Video 360] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.