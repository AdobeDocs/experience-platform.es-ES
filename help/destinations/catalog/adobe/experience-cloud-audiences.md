---
title: (Beta) Audiencias del Experience Cloud
description: Aprenda a compartir segmentos desde Experience Platform a varias soluciones de Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---

# (Beta) [!UICONTROL Audiencias de Experience Cloud] conexión

Este destino le permite compartir segmentos desde Experience Platform a varias soluciones de Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo.

![Destino de Audiencias del Experience Cloud, resaltado en el catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Este destino reemplaza al [integración heredada de uso compartido de segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de Experience Platform a varias soluciones de Experience Cloud.
>* Este destino se encuentra actualmente en fase beta. La documentación y la funcionalidad están sujetas a cambios.


## Casos de uso y ventajas {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!UICONTROL Audiencias de Experience Cloud] Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Habilitar casos de uso de Data Management Platform {#dmp-use-cases}

En Audience Manager, puede utilizar segmentos de Experience Platform para casos de uso de Data Management Platform, como:

* Añadir [datos de terceros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) a sus segmentos;
* [Modelado algorítmico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Active los segmentos a destinos basados en cookies que aún no sean compatibles con el catálogo de destinos de Experience Platform.

### Control granular de segmentos exportados {#segments-control}

Utilice la nueva integración de uso compartido de segmentos autoservicio mediante el destino de Audiencias del Experience Cloud para seleccionar qué segmentos exportar a Audience Manager y más allá. Esto le permite determinar qué segmentos desea compartir con otras soluciones de Experience Cloud y qué segmentos desea mantener exclusivamente en Experience Platform.

La integración heredada de uso compartido de segmentos no permitía un control granular de qué segmentos debían exportarse al Audience Manager y más allá.

### Uso compartido de segmentos de Experience Platform con otras soluciones de Experience Cloud {#share-segments-with-other-solutions}

Además de compartir segmentos con Audience Manager, la tarjeta de destino Audiencias de Experience Platform le permite compartir segmentos con cualquier otra solución de Experience Cloud que haya aprovisionado, como:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
> * Este destino está disponible para [Adobe Real-time Customer Data Platform Prime y Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.
> * Necesita una licencia de Audience Manager para habilitar el [Casos de uso de Data Management Platform](#dmp-use-cases) mencionado anteriormente.
> * Usted *no necesita* una licencia de Audience Manager para compartir segmentos de Experience Platform con Adobe Advertising Cloud, Adobe Target, Marketo y otras soluciones de Experience Cloud, mencionadas en la [sección anterior](#share-segments-with-other-solutions).


### Para clientes que utilizan la solución heredada de uso compartido de segmentos

Si ya está compartiendo segmentos de Experience Platform a Audience Manager y otras soluciones de Experience Cloud a través de [integración heredada de uso compartido de segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), debe ponerse en contacto con el Servicio de atención al cliente o con el equipo de su cuenta de Adobe para deshabilitar la integración heredada. Los equipos del Servicio de atención al cliente y de la cuenta de Adobe AAM deben presentar un ticket de Jira (consulte ticket de plantilla-52354) para deshabilitar la integración.

El tiempo de respuesta para resolver el ticket de desabastecimiento para los clientes de la versión beta es de seis días hábiles o menos. Una vez deshabilitada la integración heredada existente, puede continuar con [creación de una conexión](#connect) a través de la tarjeta de destino de autoservicio.

>[!IMPORTANT]
>
>La exportación de segmentos de Experience Platform a sus otras soluciones se detendrá en el tiempo entre la resolución del ticket Jira y el momento en que se establece una nueva conexión a través de la tarjeta de destino. Puede minimizar este tiempo de inactividad creando la conexión a través de la tarjeta de destino tan pronto como se cierre el ticket Jira.

## Limitaciones y llamadas conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas y llamadas importantes en la versión beta de la tarjeta Audiencias del Experience Cloud:

* [Supervisión de flujos de datos](/help/dataflows/ui/monitor-destinations.md) no es compatible.
* Al conectarse al destino, puede ver una opción para lo siguiente [habilitar alertas de flujo de datos](#enable-alerts). Aunque esté visible en la interfaz de usuario de, la variable **no se admite la opción habilitar alertas** en la versión beta.
* **No se admiten rellenos**. La primera exportación a soluciones de Audience Manager u otros Experience Cloud no incluye una población histórica de los segmentos.
* En la versión beta, puede crear lo siguiente **una única conexión de destino al destino de Audiencias del Experience Cloud**, en todos los entornos limitados que pertenecen a su organización de Experience Platform.
* Hay un **latencia de cuatro horas** entre el momento en que los datos se activan en Experience Platform y el momento en que están listos para utilizarse en Audience Manager y otras soluciones de Experience Cloud.

## Identidades admitidas {#supported-identities}

Los perfiles que se exportan a [!UICONTROL Audiencias de Experience Cloud] Los destinos de se asignan a las identidades descritas en la siguiente tabla. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| ECID | Experience Cloud ID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| GAID | ID de publicidad de Google | Los perfiles introducidos en Experience Platform con una identidad principal de Google Advertising ID (GAID) se pueden exportar a este destino. |
| IDFA | Apple ID para anunciantes | Los perfiles introducidos en Experience Platform con una identidad principal de Apple ID para anunciantes (IDFA) se pueden exportar a este destino. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Los perfiles introducidos en Experience Platform con una identidad principal de dirección de correo electrónico con hash se pueden exportar a este destino. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con claves de las identidades enumeradas en la sección anterior. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

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


## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino. Tenga en cuenta que [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) es obligatorio y no [paso de programación](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) está disponible para este destino.

## Validar exportación de datos {#exported-data}

Para validar que la exportación de datos se ha realizado correctamente, puede comprobar que los segmentos han llegado correctamente a la solución de Experience Cloud deseada.

### Validar datos en el Audience Manager

Los segmentos del Experience Platform aparecen en Audience Manager como [señales](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [rasgos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), y [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Puede comprobar en Audience Manager si los datos han aparecido tal como se describe en los vínculos de la documentación anteriores.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

La gobernanza de datos en Experience Platform la aplican ambos [etiquetas de uso de datos](/help/data-governance/labels/reference.md) y acciones de marketing.
Las etiquetas de uso de datos se transferirán a las aplicaciones, pero las acciones de marketing no. Esto significa que, una vez que aterrizan en Audience Manager, los segmentos de Experience Platform se pueden exportar a cualquier destino disponible. En Audience Manager, puede utilizar [controles de exportación de datos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para bloquear la exportación de segmentos a determinados destinos.

### Administración de permisos en Audience Manager

Los segmentos y rasgos del Audience Manager están sujetos a [Controles de acceso basados en roles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=es) (RBAC).

Los segmentos exportados desde Experience Platform se asignan a una fuente de datos específica en Audience Manager llamada **[!UICONTROL Segmentos de Experience Platform]**.

Para permitir que solo determinados usuarios tengan acceso a los segmentos, puede aplicar controles de acceso a los segmentos que pertenecen a la fuente de datos. Debe establecer nuevos permisos de control de acceso en Audience Manager para estos segmentos y rasgos creados a partir de segmentos de Experience Platform.
