---
title: (Beta) Audiencias del Experience Cloud
description: Aprenda a compartir audiencias de Experience Platform a varias soluciones de Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 2%

---

# (Beta) [!UICONTROL Audiencias de Experience Cloud] conexión

Este destino le permite compartir audiencias de Experience Platform a varias soluciones de Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo.

![Destino de Audiencias del Experience Cloud, resaltado en el catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Este destino reemplaza al [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de Experience Platform a varias soluciones de Experience Cloud.
>* Este destino se encuentra actualmente en fase beta. La documentación y la funcionalidad están sujetas a cambios.

## Casos de uso y ventajas {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!UICONTROL Audiencias de Experience Cloud] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Habilitar casos de uso de Data Management Platform {#dmp-use-cases}

En Audience Manager, puede utilizar audiencias de Experience Platform para casos de uso de Data Management Platform, como:

* Añadir [datos de terceros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) a sus segmentos;
* [Modelado algorítmico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Active las audiencias a destinos basados en cookies que aún no sean compatibles con el catálogo de destinos de Experience Platform.

### Control granular de audiencias exportadas {#segments-control}

Utilice la nueva integración de uso compartido de audiencias de autoservicio mediante el destino de Audiencias de Experience Cloud para seleccionar qué audiencias exportar a Audience Manager y más allá. Esto le permite determinar qué audiencias desea compartir con otras soluciones de Experience Cloud y qué audiencias desea mantener exclusivamente en Experience Platform.

La integración heredada de uso compartido de audiencias no permitía un control granular sobre qué audiencias debían exportarse a Audience Manager y más allá.

### Uso compartido de audiencias de Experience Platform con otras soluciones de Experience Cloud {#share-segments-with-other-solutions}

Además de compartir audiencias con Audience Manager, la tarjeta de destino Audiencias de Experience Platform le permite compartir audiencias con cualquier otra solución de Experience Cloud que haya seleccionado, como:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
> * Este destino está disponible para [Adobe Real-time Customer Data Platform Prime y Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.
> * Necesita una licencia de Audience Manager para habilitar el [Casos de uso de Data Management Platform](#dmp-use-cases) mencionado anteriormente.
> * Usted *no necesita* una licencia de Audience Manager para compartir audiencias de Experience Platform con Adobe Advertising Cloud, Adobe Target, Marketo y otras soluciones de Experience Cloud, mencionadas en la [sección anterior](#share-segments-with-other-solutions).

### Para clientes que utilizan la solución heredada de uso compartido de audiencias

Si ya está compartiendo audiencias de Experience Platform a Audience Manager y otras soluciones de Experience Cloud a través de [integración heredada de uso compartido de audiencias](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), debe ponerse en contacto con el Servicio de atención al cliente o con el equipo de su cuenta de Adobe para deshabilitar la integración heredada. Los equipos del Servicio de atención al cliente y de la cuenta de Adobe AAM deben presentar un ticket de Jira (consulte ticket de plantilla-52354) para deshabilitar la integración.

El tiempo de respuesta para resolver el ticket de desabastecimiento para los clientes de la versión beta es de seis días hábiles o menos. Una vez deshabilitada la integración heredada existente, puede continuar con [creación de una conexión](#connect) a través de la tarjeta de destino de autoservicio.

>[!IMPORTANT]
>
>La exportación de audiencias de Experience Platform a sus otras soluciones se detendrá en el tiempo entre la resolución del ticket Jira y el momento en que se establece una nueva conexión a través de la tarjeta de destino. Puede minimizar este tiempo de inactividad creando la conexión a través de la tarjeta de destino tan pronto como se cierre el ticket Jira.

## Limitaciones y llamadas conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas y llamadas importantes en la versión beta de la tarjeta Audiencias del Experience Cloud:

* [Supervisión de flujos de datos](/help/dataflows/ui/monitor-destinations.md) no es compatible.
* Al conectarse al destino, puede ver una opción para lo siguiente [habilitar alertas de flujo de datos](#enable-alerts). Aunque esté visible en la interfaz de usuario de, la variable **no se admite la opción habilitar alertas** en la versión beta.
* **No se admiten rellenos**. La primera exportación a soluciones de Audience Manager u otras soluciones de Experience Cloud no incluye una población histórica de las audiencias.
* En la versión beta, puede crear lo siguiente **una única conexión de destino al destino de Audiencias del Experience Cloud**, en todos los entornos limitados que pertenecen a su organización de Experience Platform.

### Latencia al activar audiencias {#audience-activation-latency}

Hay una latencia de cuatro horas entre el momento en que las audiencias se activan por primera vez en Experience Platform y el momento en que están listas para utilizarse en soluciones de Audience Manager y otras soluciones de Experience Cloud para determinados casos de uso.

Las audiencias pueden tardar hasta 24 horas en estar totalmente disponibles en Audience Manager Experience Cloud para todos los casos de uso y hasta 48 horas en aparecer en los informes de Audience Manager.

Los metadatos, como los nombres de audiencias, están disponibles en Audience Manager pocos minutos después de configurar la exportación al destino de Audiencias del Experience Cloud.

## Identidades admitidas {#supported-identities}

Los perfiles que se exportan a [!UICONTROL Audiencias de Experience Cloud] Los destinos de se asignan a las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| GAID | ID de publicidad de Google | Los perfiles introducidos en Experience Platform con una identidad principal de Google Advertising ID (GAID) se pueden exportar a este destino. |
| IDFA | Apple ID para anunciantes | Los perfiles introducidos en Experience Platform con una identidad principal de Apple ID para anunciantes (IDFA) se pueden exportar a este destino. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Los perfiles introducidos en Experience Platform con una identidad principal de dirección de correo electrónico con hash se pueden exportar a este destino. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe todas las audiencias que puede exportar a este destino.

Todos los destinos admiten la activación de audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md).

Además, este destino también admite la activación de las audiencias que se describen en la tabla siguiente.

| Tipo de audiencia | Descripción |
---------|----------|
| Cargas personalizadas | Audiencias introducidas en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia con claves de las identidades enumeradas en la sección anterior. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

>[!IMPORTANT]
> 
>En la versión beta, puede crear una única conexión de destino al destino de Audiencias del Experience Cloud en todos los entornos limitados que pertenezcan a su organización de Experience Platform.

### Autenticar en el destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Configuración de]** en la vista tarjeta de destino del catálogo, y seleccione **[!UICONTROL Conectar con destino]**.

![Consulte la opción Conectar con destino para el destino de Audiencias de Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Configure la nueva pantalla de destino que muestra la configuración necesaria y opcional para conectarse al destino de Audiencias del Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.


## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino. Tenga en cuenta que [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) es obligatorio y no [paso de programación](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) está disponible para este destino.

## Validar exportación de datos {#exported-data}

Para validar que la exportación de datos se haya realizado correctamente, puede comprobar que las audiencias hayan llegado correctamente a la solución de Experience Cloud deseada.

### Validar datos en el Audience Manager

Las audiencias de Experience Platform aparecen en Audience Manager como [señales](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [rasgos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), y [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Puede comprobar en Audience Manager si los datos han aparecido tal como se describe en los vínculos de la documentación anteriores.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

La gobernanza de datos en Experience Platform la aplican ambos [etiquetas de uso de datos](/help/data-governance/labels/reference.md) y acciones de marketing.
Las etiquetas de uso de datos se transferirán a las aplicaciones, pero las acciones de marketing no. Esto significa que, una vez que llegan a Audience Manager, las audiencias de Experience Platform se pueden exportar a cualquier destino disponible. En Audience Manager, puede utilizar [controles de exportación de datos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para impedir que las audiencias se exporten a determinados destinos.

### Administración de permisos en Audience Manager

Las audiencias y características de Audience Manager están sujetas a [Controles de acceso basados en roles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=es) (RBAC).

Las audiencias exportadas desde Experience Platform se asignan a una fuente de datos específica en Audience Manager llamada **[!UICONTROL Segmentos de Experience Platform]**.

Para permitir que solo determinados usuarios tengan acceso a las audiencias, puede aplicar controles de acceso a las audiencias que pertenezcan a la fuente de datos. Debe establecer nuevos permisos de control de acceso en Audience Manager para estas audiencias y características creadas a partir de segmentos del Experience Platform.
