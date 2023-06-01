---
keywords: personalización de target; destino; destino de experience platform target; destino de adobe target;
title: Conexión de Adobe Target
description: Adobe Target es una aplicación que proporciona capacidades de personalización y experimentación en tiempo real impulsadas por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 6ac48762dc9ea1cb77b04651275a3846411449ea
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 8%

---

# Conexión de Adobe Target {#adobe-target-connection}

## Registro de cambios de destino {#changelog}

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Mayo de 2023 | Actualización de funcionalidad y documentación | A partir de mayo de 2023, la **[!UICONTROL Adobe Target]** compatibilidad de conexión [personalización basada en atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) y está disponible para todos los clientes. |

{style="table-layout:auto"}

## Información general {#overview}

Adobe Target es una aplicación que proporciona capacidades de personalización y experimentación en tiempo real impulsadas por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.

Adobe Target es una conexión de personalización del catálogo de destinos de Adobe Experience Platform.

Vea el siguiente vídeo para obtener una breve descripción general sobre cómo configurar la conexión de Adobe Target en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Requisitos previos {#prerequisites}

### ID de flujo de datos {#datastream-id}

Al configurar la conexión de Adobe Target a [usar un ID de secuencia de datos](#parameters), debe tener el [SDK web de Adobe Experience Platform](../../../edge/home.md) implementado.

La configuración de la conexión de Adobe Target sin utilizar un ID de conjunto de datos no requiere la implementación del SDK web.

>[!IMPORTANT]
>
>Antes de crear un [!DNL Adobe Target] conexión, lea la guía sobre cómo [configuración de destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la página siguiente, en varios componentes de Experience Platform. La personalización de la misma página y de la página siguiente requiere que utilice un ID de flujo de datos al configurar la conexión de Adobe Target.

### Requisitos previos en Adobe Target {#prerequisites-in-adobe-target}

En Adobe Target, asegúrese de que el usuario tenga:

* Acceso a la [workspace predeterminado](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* El **Aprobador** [función](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

Más información sobre la concesión de permisos para [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) y para [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todos los segmentos asignados en el destino de Adobe Target para un solo perfil. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Acerca de los ID de secuencia de datos"
>abstract="Esta opción determina en qué secuencia de datos de recopilación de datos se incluirán los segmentos. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Para utilizar la segmentación de Edge, debe seleccionar un ID de la secuencia de datos. Al seleccionar Ninguno, se desactivan todos los casos de uso que utilizan segmentación de Edge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es#parameters" text="Obtenga más información sobre la selección de secuencias de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **Nombre**: complete el nombre preferido para este destino.
* **Descripción**: introduzca una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **ID de flujo de datos**: Determina en qué flujo de datos de recopilación de datos se incluirán los segmentos. El menú desplegable solo muestra las secuencias de datos que tienen habilitados los servicios de Target y Adobe Experience Platform. Consulte [configuración de una secuencia de datos](../../../edge/datastreams/configure.md#aep) para obtener información detallada sobre cómo configurar un conjunto de datos para Adobe Experience Platform y Adobe Target.
   * **[!UICONTROL Ninguno]**: Seleccione esta opción si necesita configurar la personalización de Adobe Target pero no puede implementar la variable [SDK web de Experience Platform](../../../edge/home.md). Con esta opción, los segmentos exportados de Experience Platform a Target solo admiten la personalización de la sesión siguiente y la segmentación de Edge está desactivada. Consulte la tabla siguiente para obtener más información.

| No se han seleccionado flujos de datos | Flujo de datos seleccionado |
|---|---|
| <ul><li>[Segmentación de Edge](../../../segmentation/ui/edge-segmentation.md) no es compatible.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md) no son compatibles.</li><li>Solo puede compartir segmentos con la conexión de Adobe Target para *zona protegida de producción predeterminada*.</li><li>Para configurar la personalización de la sesión siguiente sin utilizar un ID de conjunto de datos, utilice [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>La segmentación de Edge funciona según lo esperado.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md) son compatibles.</li><li>El uso compartido de segmentos es compatible con otras zonas protegidas.</li></ul> |

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Adobe Target lee datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).
