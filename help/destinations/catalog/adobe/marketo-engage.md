---
title: Destino de Marketo Engage
description: Marketo Engage es la única solución de administración de la experiencia del cliente (CXM) integral para marketing, publicidad, análisis y comercio. Le permite automatizar y administrar las actividades desde la administración de clientes potenciales y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 2%

---

# (Heredado) (V2) Destino de Marketo Engage {#beta-marketo-engage-destination}

## Registro de cambios de destino {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![Imagen de las dos tarjetas de destino de Marketo en una vista en paralelo.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Las mejoras en el destino de Marketo V2 incluyen las siguientes:

* En el paso **[!UICONTROL Schedule segment]** del flujo de trabajo de activación, en Marketo V1, necesitaba agregar manualmente un **ID de asignación** para exportar correctamente los datos a Marketo. Este paso manual ya no es necesario en Marketo V2.
* En el paso **[!UICONTROL Mapping]** del flujo de trabajo de activación, en Marketo V1, pudo asignar campos XDM solo a tres campos de destino en Marketo: `firstName`, `lastName` y `companyName`. Con la versión 2.0 de Marketo, ahora puede asignar campos XDM a muchos más campos en Marketo. Para obtener más información, lea la sección [atributos admitidos](#supported-attributes) más abajo.

## Información general {#overview}

[!DNL Marketo Engage] es la única solución de administración de la experiencia del cliente (CXM) de extremo a extremo para marketing, publicidad, análisis y comercio. Le permite automatizar y administrar las actividades desde la administración de clientes potenciales y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.

El destino permite a los especialistas en marketing insertar audiencias creadas en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas.

## Identidades y atributos admitidos {#supported-identities-attributes}

>[!NOTE]
>
>En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, es *obligatorio* asignar identidades y *opcional* asignar atributos. Asignar un correo electrónico o ECID desde la pestaña Área de nombres de identidad es lo más importante para garantizar que la persona coincida en Marketo. Asignar correo electrónico garantiza la tasa de coincidencia más alta.

### Identidades admitidas {#supported-identities}

| Identidad de destino | Descripción |
|---|---|
| ECID | Un área de nombres que representa ECID. Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/features/ecid.md) para obtener más información. |
| Correo electrónico | Un área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificarla en diferentes canales. |

{style="table-layout:auto"}

### Atributos admitidos {#supported-attributes}

Puede asignar atributos de Experience Platform a cualquiera de los atributos a los que su organización tiene acceso en Marketo. En Marketo, puede usar [Describir solicitud de API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) para recuperar los campos de atributos a los que su organización tiene acceso.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia con los identificadores (correo electrónico, ECID) utilizados en el destino [!DNL Marketo Engage]. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configuración del destino y activación de audiencias {#set-up}

>[!IMPORTANT]
> 
>* Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions).
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para obtener instrucciones detalladas sobre cómo configurar el destino y activar audiencias, lee [Insertar una audiencia de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=es) en la documentación de Marketo.

El siguiente vídeo también muestra los pasos para configurar un destino de Marketo y activar audiencias.

>[!IMPORTANT]
>
>El vídeo no refleja completamente la capacidad actual. Para obtener la información más actualizada, consulte la guía vinculada anteriormente. Las siguientes partes del vídeo están obsoletas:
> 
>* La tarjeta de destino que debe usar en la interfaz de usuario de Experience Platform es **[!UICONTROL Marketo V2]**.
>* El vídeo no muestra el nuevo campo de selector **[!UICONTROL Person creation]** en el flujo de trabajo de conexión a destino. Para utilizar ese campo, debe asignar tanto el nombre como los apellidos durante el paso de asignación de atributos.
>* Las dos limitaciones indicadas en el vídeo ya no se aplican. Ahora puede asignar muchos otros campos de atributos de perfil además de la información de pertenencia a audiencias compatible en el momento de grabar el vídeo. También puede exportar a Marketo miembros de la audiencia que aún no existan en sus listas estáticas de Marketo y que se añadirán a las listas.
>* En el **[!UICONTROL Schedule audience step]** del flujo de trabajo de activación, en Marketo V1, necesitaba agregar manualmente un **[!UICONTROL Mapping ID]** para exportar correctamente los datos a Marketo. Este paso manual ya no es necesario en Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Supervisar destino {#monitor-destination}

Después de conectarse al destino y establecer un flujo de datos de destino, puede usar la [funcionalidad de supervisión](/help/dataflows/ui/monitor-destinations.md) en Real-Time CDP para obtener información detallada acerca de los registros de perfil activados en el destino en cada ejecución de flujo de datos.

La información de supervisión de la conexión [!DNL Marketo Engage] incluye información de nivel de audiencia relacionada con identidades activadas, excluidas y fallidas en cada flujo de datos y ejecución de flujo de datos. [Más información](/help/dataflows/ui/monitor-destinations.md#segment-level-view) sobre la nueva funcionalidad.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [descripción general del control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).
