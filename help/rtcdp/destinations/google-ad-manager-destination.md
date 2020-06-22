---
title: Destino del administrador de publicidad de Google
seo-title: Destino del administrador de publicidad de Google
description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
seo-description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Destino del administrador de publicidad de Google

## Información general

Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de los destinos del Administrador de publicidad de Google:

* Puede enviar las siguientes [identidades](../../identity-service/namespaces.md) a los destinos del Administrador de publicidad de Google: **ID de cookie de Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* Actualmente, CDP en tiempo real de Adobe no incluye una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Ad Manager y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a CDP en tiempo real de Adobe.

## Requisitos previos

### Permitir lista

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar el primer destino de Google Ad Manager en Adobe Real-time CDP. Asegúrese de que Google haya completado el proceso de lista de permitidos descrito a continuación antes de crear un destino.

Antes de crear el destino de Google Ad Manager en Adobe Real-time CDP, debe ponerse en contacto con Google para que Adobe se ponga en lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** de red: esta es su cuenta con Google Ad Manager
* **ID** del vínculo de Audiencia: esta es su cuenta con Google Ad Manager
* El tipo de cuenta. **DFP por comprador** de Google **o** AdX.

## Crear destino

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione Administrador de publicidad de Google y, a continuación, **[!UICONTROL Crear destino]**.
   ![Destino de Connect Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la información  básica del destino. <br>

   ![Información básica Google Ad Manager](/help/rtcdp/destinations/assets/ad-manager-setup-step.png)
* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Usar `DFP by Google` para DoubleClick para editores
   * Usar `AdX buyer` para Google AdX
* **[!UICONTROL ID]** de cuenta: Rellene su ID de cuenta con Google. Puede ser su ID de red o su ID de vínculo de Audiencia. Normalmente, se trata de un ID de ocho dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos de uso de mercadotecnia definidos por Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos.

> [!NOTE]
>
> Al configurar un destino de Google Ad Manager, trabaje con su administrador de cuentas de Google o con un representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos en Google Ad Manager

Para obtener instrucciones sobre cómo activar segmentos en el Administrador de publicidad de Google, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).