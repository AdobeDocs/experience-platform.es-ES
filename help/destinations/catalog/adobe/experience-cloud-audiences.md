---
title: Audiencias de Experience Cloud
description: Aprenda a compartir audiencias de Real-time Customer Data Platform con varias aplicaciones de Experience Cloud.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 23c4bce542bba76ea4badba43a7ce3e6f7fe9e49
workflow-type: tm+mt
source-wordcount: '1780'
ht-degree: 3%

---


# [!UICONTROL Audiencias de Experience Cloud] conexión

>[!AVAILABILITY]
>
> Este destino está disponible para [Adobe Real-time Customer Data Platform Prime y Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) clientes.

Utilice este destino para activar audiencias de Real-Time CDP a Audience Manager y Adobe Analytics.

Para enviar audiencias a Adobe Analytics, necesita una licencia de Audience Manager. Para obtener más información, consulte la [Introducción al Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=es).

Para enviar audiencias a otras soluciones de Adobe, utilice las conexiones directas de Real-Time CDP a [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) y [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Este destino reemplaza al [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) desde Real-time Customer Data Platform hasta varias soluciones de Experience Cloud.
> 
>Si ya está compartiendo audiencias de Real-Time CDP con Audience Manager y otras soluciones de Experience Cloud a través de [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)No obstante, debe ponerse en contacto con el Servicio de atención al cliente para deshabilitar la integración heredada antes de utilizar este destino.

![Destino de Audiencias del Experience Cloud, resaltado en el catálogo de destinos.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Casos de uso y ventajas {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!UICONTROL Audiencias de Experience Cloud] Destino. Estos son ejemplos de casos de uso que los clientes de Real-Time CDP pueden solucionar mediante este destino.

### Habilitar casos de uso de Data Management Platform {#dmp-use-cases}

En Audience Manager, puede utilizar las audiencias de Real-Time CDP para casos de uso de la plataforma de gestión de datos, como:

* Agregando [datos de terceros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) a sus segmentos;
* [Modelado algorítmico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Activar las audiencias en destinos basados en cookies que aún no son compatibles con el catálogo de destinos de Real-Time CDP.

### Control granular de audiencias exportadas {#segments-control}

Para seleccionar qué audiencias exportar a Audience Manager y posteriores, utilice la nueva integración de uso compartido de audiencias de autoservicio a través del destino de Audiencias de Experience Cloud.  Esto le permite determinar qué audiencias desea compartir con otras soluciones de Experience Cloud y qué audiencias desea mantener exclusivamente en Real-Time CDP.

La integración heredada de uso compartido de audiencias no permitía un control granular sobre qué audiencias debían exportarse a Audience Manager y más allá.

### Uso compartido de audiencias de Real-Time CDP con Adobe Analytics {#share-audiences-with-analytics}

Las audiencias que envía al destino de Audiencias de Experience Cloud no aparecen automáticamente en Adobe Analytics.

Para poder enviar audiencias a Adobe Analytics, debe [implementación del servicio de ID de Experience Cloud para Analytics y Audience Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=en).

>[!IMPORTANT]
>
>Para enviar audiencias de Real-Time CDP a Adobe Analytics a través del destino de Audiencias de Experience Cloud, debe tener una licencia de Audience Manager.

### Uso compartido de audiencias de Real-Time CDP con otras soluciones de Experience Cloud {#share-segments-with-other-solutions}

Puede utilizar la tarjeta de destino Audiencias de Real-Time CDP para compartir audiencias con otras soluciones de Experience Cloud.

Sin embargo, Adobe recomienda encarecidamente utilizar las siguientes tarjetas de destino específicas si desea compartir audiencias con estas soluciones:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
> * Necesita una licencia de Audience Manager para habilitar el [Casos de uso de Data Management Platform](#dmp-use-cases) mencionado anteriormente.
> * Usted *hacer* necesita una licencia de Audience Manager para compartir audiencias de Real-Time CDP con Adobe Analytics.
> * Usted *no necesita* una licencia de Audience Manager para compartir audiencias de Real-Time CDP con Adobe Advertising Cloud, Adobe Target, Marketo y otras soluciones de Experience Cloud, mencionadas en la [sección anterior](#share-segments-with-other-solutions).

### Para clientes que utilizan la solución heredada de uso compartido de audiencias

Si ya está compartiendo audiencias de Real-Time CDP con Audience Manager y otras soluciones de Experience Cloud a través de [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), debe ponerse en contacto con el Servicio de atención al cliente para deshabilitar la integración heredada.

El tiempo de respuesta para resolver el ticket de desabastecimiento es de seis días hábiles o menos. Una vez deshabilitada la integración heredada existente, puede continuar con [crear una conexión](#connect) a través de la tarjeta de destino de autoservicio.

>[!IMPORTANT]
>
>La exportación de audiencias de Real-Time CDP a sus otras soluciones se detiene en el tiempo entre la resolución del ticket y el momento en que se establece una nueva conexión a través de la tarjeta de destino. Puede minimizar este tiempo de inactividad creando la conexión a través de la tarjeta de destino después de cerrar el ticket.

## Limitaciones y llamadas conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas y llamadas importantes al utilizar la tarjeta Audiencias del Experience Cloud:

* Actualmente, solo se admite un destino de Audiencias de Experience Cloud. Si se intenta configurar una segunda conexión de destino, se producirá un error.
* Al conectarse al destino, puede ver una opción para lo siguiente [habilitar alertas de flujo de datos](../../ui/alerts.md). Aunque esté visible en la interfaz de usuario de, la variable **actualmente no se admite la opción habilitar alertas**.
* **Compatibilidad con relleno de audiencia**: la primera exportación a soluciones de Audience Manager u otros Experience Cloud incluye una población histórica de las audiencias. Usuarios de [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) Los usuarios que configuran este destino deben esperar una diferencia de relleno de aproximadamente seis horas.

### Latencia al activar audiencias {#audience-activation-latency}

Hay una latencia de cuatro horas entre el momento en que las audiencias se activan por primera vez en Real-Time CDP y el momento en que están listas para utilizarse en Audience Manager y otras soluciones de Experience Cloud.

Las audiencias pueden tardar hasta 24 horas en estar totalmente disponibles en Audience Manager para todos los casos de uso. Las audiencias de Audiencias de Experience Cloud pueden tardar hasta 48 horas en aparecer en los informes de Audience Manager.

Los metadatos, como los nombres de audiencias, están disponibles en Audience Manager pocos minutos después de configurar la exportación al destino de Audiencias del Experience Cloud.

## Identidades admitidas {#supported-identities}

Los perfiles que se exportan a [!UICONTROL Audiencias de Experience Cloud] Los destinos de se asignan a las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| GAID | ID de publicidad de Google | Los perfiles introducidos en Real-Time CDP con una identidad principal de Google Advertising ID (GAID) se pueden exportar a este destino. |
| IDFA | Apple ID para anunciantes | Los perfiles introducidos en Real-Time CDP con una identidad principal de Apple ID para anunciantes (IDFA) se pueden exportar a este destino. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Los perfiles introducidos en Real-Time CDP con una identidad principal de dirección de correo electrónico con hash se pueden exportar a este destino. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencia puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia con claves de las identidades enumeradas en la sección anterior. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Cuando se actualiza un perfil en Real-Time CDP en función de la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Configuración de]** en la vista tarjeta de destino del catálogo, y seleccione **[!UICONTROL Conectar con destino]**.

![Consulte la opción Conectar con destino para el destino de Audiencias de Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Configure la nueva pantalla de destino que muestra la configuración necesaria y opcional para conectarse al destino de Audiencias del Experience Cloud.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino. No [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) es obligatorio y no [paso de programación](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) está disponible para este destino.

## Validar exportación de datos {#exported-data}

Para validar que la exportación de datos se haya realizado correctamente, puede comprobar que las audiencias hayan llegado correctamente a la solución de Experience Cloud deseada.

### Validar datos en el Audience Manager

Las audiencias de Real-Time CDP aparecen en Audience Manager como [señales](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [rasgos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits), y [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). Puede comprobar en Audience Manager si los datos han aparecido tal como se describe en los vínculos de la documentación anteriores.

Los nombres de los segmentos comienzan a rellenarse en Audience Manager 15 minutos después de que las audiencias se hayan enviado desde Real-Time CDP.

La población de segmentos comienza a fluir al Audience Manager en un plazo de 6 horas desde que se envía desde Real-Time CDP y se actualiza cada 24 horas en Audience Manager.

La población completa será visible en Audience Manager después de 72 horas y las poblaciones seguirán fluyendo a Audience Manager a menos que la audiencia se elimine del destino en Real-Time CDP.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Real-Time CDP] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

La gobernanza de datos en Real-Time CDP la aplican ambos [etiquetas de uso de datos](/help/data-governance/labels/reference.md) y acciones de marketing.
Las etiquetas de uso de datos se transfieren a las aplicaciones, pero las acciones de marketing no. Esto significa que, una vez que llegan a Audience Manager, las audiencias de Real-Time CDP se pueden exportar a cualquier destino disponible. En Audience Manager, puede utilizar [controles de exportación de datos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) para impedir que las audiencias se exporten a determinados destinos.

Audiencias marcadas con el [!DNL HIPAA] las acciones de marketing no se envían de Real-Time CDP al Audience Manager.

### Administración de permisos en Audience Manager

Las audiencias y características de Audience Manager están sujetas a [Controles de acceso basados en roles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

Las audiencias exportadas desde Real-Time CDP se asignan a una fuente de datos específica en el Audience Manager llamada **[!UICONTROL Segmentos de Experience Platform]**.

Para permitir que solo determinados usuarios tengan acceso a las audiencias, puede aplicar controles de acceso a las audiencias que pertenezcan a la fuente de datos. Establezca nuevos permisos de control de acceso en Audience Manager para estas audiencias y características creadas a partir de segmentos de Real-Time CDP.