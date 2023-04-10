---
title: (Beta) Audiencias de Experience Cloud
description: Aprenda a compartir segmentos de Experience Platform a varias soluciones de Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---


# (Beta) [!UICONTROL Audiencias de Experience Cloud] connection

Este destino le permite compartir segmentos de Experience Platform en varias soluciones de Experience Cloud, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo.

![Destino de Audiencias de Experience Cloud, resaltado en el catálogo de destinos.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Este destino reemplaza a la variable [integración de uso compartido de segmentos heredados](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de Experience Platform a varias soluciones de Experience Cloud.
>* Este destino está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.


## Casos de uso y beneficios {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!UICONTROL Audiencias de Experience Cloud] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Habilitar casos de uso de la plataforma de gestión de datos {#dmp-use-cases}

En Audience Manager, puede utilizar segmentos de Experience Platform para casos de uso de la plataforma de gestión de datos, como:

* Agregar [datos de terceros](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) a sus segmentos;
* [Modelado algorítmico](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Active los segmentos en destinos basados en cookies que aún no sean compatibles con el catálogo de destinos de Experience Platform.

### Control granular de segmentos exportados {#segments-control}

Utilice la nueva integración de uso compartido de segmentos de autoservicio a través del destino Audiencias de Experience Cloud para seleccionar qué segmentos exportar a Audience Manager y más allá. Esto le permite determinar qué segmentos desea compartir con otras soluciones de Experience Cloud y qué segmentos desea mantener en Experience Platform exclusivamente.

La integración heredada del uso compartido de segmentos no permitía un control granular de qué segmentos se deberían exportar al Audience Manager y más allá.

### Compartir segmentos de Experience Platform con otras soluciones de Experience Cloud {#share-segments-with-other-solutions}

Además de compartir segmentos con Audience Manager, la tarjeta de destino Audiencias de Experience Platform le permite compartir segmentos con cualquier otra solución de Experience Cloud para la que esté aprovisionado, como:

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
> * Necesita una licencia de Audience Manager para habilitar el [Casos de uso de la plataforma de gestión de datos](#dmp-use-cases) mencionado más arriba.
> * You *no es necesario* una licencia de Audience Manager para compartir segmentos de Experience Platform con Adobe Advertising Cloud, Adobe Target, Marketo y otras soluciones de Experience Cloud, mencionadas en la [sección anterior](#share-segments-with-other-solutions).


### Para clientes que utilizan la solución heredada de uso compartido de segmentos

Si ya está compartiendo segmentos de Experience Platform a Audience Manager y otras soluciones de Experience Cloud a través del [integración de uso compartido de segmentos heredados](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), debe ponerse en contacto con el Servicio de atención al cliente o con el equipo de la cuenta de Adobe para deshabilitar la integración heredada. Los equipos de atención al cliente y cuenta de Adobe deben presentar un ticket de Jira (consulte el ticket de plantilla AAM-52354) para desactivar la integración.

El tiempo de respuesta para resolver el ticket de desaprovisionamiento para los clientes beta es de seis días hábiles o menos. Una vez deshabilitada la integración heredada existente, puede continuar con [creación de una conexión](#connect) mediante la tarjeta de destino de autoservicio.

>[!IMPORTANT]
>
>La exportación de segmentos de Experience Platform a otras soluciones se detendrá en el tiempo entre la resolución de tickets de Jira y el momento en que se establezca una nueva conexión a través de la tarjeta de destino. Puede minimizar este tiempo de inactividad creando la conexión a través de la tarjeta de destino tan pronto como se cierre el ticket de Jira.

## Limitaciones y llamadas conocidas {#known-limitations}

Tenga en cuenta las siguientes limitaciones conocidas y llamadas importantes en la versión beta de la tarjeta Audiencias de Experience Cloud:

* [Supervisión de flujos de datos](/help/dataflows/ui/monitor-destinations.md) no es compatible.
* Al conectarse al destino, puede ver una opción para [habilitar alertas de flujo de datos](#enable-alerts). Aunque visible en la interfaz de usuario, la variable **no se admite la opción habilitar alertas** en la versión beta.
* **Los rellenos no son compatibles**. La primera exportación a Audience Manager u otras soluciones de Experience Cloud no incluye una población histórica de los segmentos.
* En la versión beta, puede crear **una conexión de destino única con el destino Audiencias de Experience Cloud**, en todos los entornos limitados pertenecientes a la organización de Experience Platform.
* Hay un **latencia de cuatro horas** entre el momento en que se activan los datos en el Experience Platform y el momento en que están listos para utilizarse en el Audience Manager y en otras soluciones de Experience Cloud.

## Identidades compatibles {#supported-identities}

Los perfiles que se exportan a la variable [!UICONTROL Audiencias de Experience Cloud] el destino se asigna a las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| ECID | Experience Cloud ID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| GAID | Google Advertising ID | Los perfiles introducidos en el Experience Platform con una identidad principal de Google Advertising ID (GAID) se pueden exportar a este destino. |
| IDFA | Apple ID para anunciantes | Los perfiles introducidos en el Experience Platform con la identidad principal de Apple ID para anunciantes (IDFA) se pueden exportar a este destino. |
| email_lc_sha256 | Direcciones de correo electrónico con hash con el algoritmo SHA256 | Los perfiles introducidos en el Experience Platform con una identidad principal de dirección de correo electrónico con hash se pueden exportar a este destino. |

{style="table-layout:auto"}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) que contienen las identidades enumeradas en la sección anterior. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

>[!IMPORTANT]
> 
>En la versión beta, puede crear una única conexión de destino al destino Audiencias de Experience Cloud, en todos los entornos limitados que pertenezcan a la organización de Experience Platform.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, seleccione **[!UICONTROL Configuración]** en la vista de tarjeta de destino del catálogo y seleccione **[!UICONTROL Conectarse al destino]**.

![Vista de la opción Connect to destination para el destino Audiencias de Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Configure la nueva pantalla de destino mostrando los ajustes opcionales y requeridos para conectarse al destino Audiencias de Experience Cloud .](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.


## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino. Tenga en cuenta que no [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) es obligatorio y no [paso de programación](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) está disponible para este destino.

## Validación de la exportación de datos {#exported-data}

Para validar una exportación de datos correcta, puede comprobar que los segmentos han llegado correctamente a la solución de Experience Cloud deseada.

### Validación de datos en el Audience Manager

Los segmentos del Experience Platform aparecen en Audience Manager como [señales](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [características](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)y [segmentos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Puede comprobar en Audience Manager si los datos han aparecido como se describe en los vínculos de documentación anteriores.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](/help/data-governance/home.md).

El control de datos en el Experience Platform es impuesto por ambas [etiquetas de uso de datos](/help/data-governance/labels/reference.md) y acciones de marketing.
Las etiquetas de uso de datos se transferirán a aplicaciones, pero las acciones de marketing no. Esto significa que, una vez que llegan al Audience Manager, los segmentos del Experience Platform se pueden exportar a cualquier destino disponible. En Audience Manager, puede utilizar [controles de exportación de datos](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) para bloquear la exportación de segmentos a determinados destinos.

### Administración de permisos en el Audience Manager

Los segmentos y las características del Audience Manager están sujetos a [Controles de acceso basados en roles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=es) (RBAC).

Los segmentos exportados desde el Experience Platform se asignan a una fuente de datos específica en el Audience Manager llamado **[!UICONTROL Segmentos del Experience Platform]**.

Para permitir que solo ciertos usuarios tengan acceso a los segmentos, puede aplicar controles de acceso a los segmentos pertenecientes a la fuente de datos. Debe definir nuevos permisos de control de acceso en Audience Manager para estos segmentos y rasgos creados a partir de segmentos de Experience Platform.