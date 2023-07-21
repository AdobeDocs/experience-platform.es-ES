---
keywords: personalización de target; destino; destino de experience platform target; destino de adobe target;
title: Conexión de Adobe Target
description: Adobe Target es una aplicación que proporciona capacidades de personalización y experimentación en tiempo real impulsadas por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: c111b712e24dd9e4280abfe882e6d7f5eb8493d1
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 15%

---

# Conexión de Adobe Target {#adobe-target-connection}

## Registro de cambios de destino {#changelog}

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Junio de 2023 | Actualización de funcionalidad y documentación | A partir de junio de 2023, puede seleccionar el espacio de trabajo de Adobe Target con el que desea compartir audiencias al configurar una nueva conexión de destino de Adobe Target. Consulte la sección [parámetros de conexión](#parameters) para obtener más información. Además, consulte el tutorial sobre [configuración de espacios de trabajo](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es) en Adobe Target para obtener más información acerca de los espacios de trabajo. |
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
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todas las audiencias asignadas en el destino de Adobe Target para un solo perfil. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar con el destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Acerca de los ID de secuencia de datos"
>abstract="Esta opción determina en qué flujo de datos de recopilación de datos se incluirán las audiencias. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Para utilizar la segmentación de Edge, debe seleccionar un ID de la secuencia de datos. Al seleccionar Ninguno, se desactivan todos los casos de uso que utilizan segmentación de Edge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es#parameters" text="Obtenga más información sobre la selección de secuencias de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Acerca de Adobe Target Workspaces"
>abstract="Seleccione el espacio de trabajo de Adobe Target que se compartirá al público. Puede seleccionar un único espacio de trabajo para cada conexión de Adobe Target. Tras la activación, el público se dirige al espacio de trabajo seleccionado siguiendo las etiquetas de uso de datos del Experience Platform aplicables."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es" text="Más información acerca de los espacios de trabajo de Adobe Target"

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **Nombre**: complete el nombre preferido para este destino.
* **Descripción**: introduzca una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **ID de flujo de datos**: Determina en qué flujo de datos de recopilación de datos se incluirán las audiencias. El menú desplegable solo muestra las secuencias de datos que tienen habilitados los servicios de Target y Adobe Experience Platform. Consulte [configuración de una secuencia de datos](../../../edge/datastreams/configure.md#aep) para obtener información detallada sobre cómo configurar un conjunto de datos para Adobe Experience Platform y Adobe Target.
   * **[!UICONTROL Ninguno]**: Seleccione esta opción si necesita configurar la personalización de Adobe Target pero no puede implementar la variable [SDK web de Experience Platform](../../../edge/home.md). Con esta opción, las audiencias exportadas de Experience Platform a Target solo admiten la personalización de la sesión siguiente y la segmentación de Edge está desactivada. Consulte la tabla siguiente para obtener más información.

  | Implementación de Adobe Target (sin SDK web) | Implementación del SDK web |
  |---|---|
  | <ul><li>No se requiere una secuencia de datos. Adobe Target se puede implementar mediante [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=es), [del lado del servidor](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=en#server-side-implementation), o [híbrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=en#hybrid-implementation) métodos de implementación.</li><li>[Segmentación de Edge](../../../segmentation/ui/edge-segmentation.md) no es compatible.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md) no son compatibles.</li><li>Solo puede compartir audiencias y atributos de perfil con la conexión de Adobe Target para *zona protegida de producción predeterminada*.</li><li>Para configurar la personalización de la sesión siguiente sin utilizar un ID de conjunto de datos, utilice [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>Se requiere un conjunto de datos con Adobe Target y Experience Platform configurados como servicios.</li><li>La segmentación de Edge funciona según lo esperado.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md) son compatibles.</li><li>Se admite el uso compartido de audiencias y atributos de perfil desde otras zonas protegidas.</li></ul> |

* **Workspace**: seleccione el Adobe Target [workspace](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es) a qué audiencias se compartirán. Puede seleccionar un único espacio de trabajo para cada conexión de Adobe Target. Tras la activación, las audiencias se dirigen al espacio de trabajo seleccionado siguiendo el [Experience Platform etiquetas de uso de datos](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Al utilizar un espacio de trabajo de Target personalizado para [personalización de la misma página y de la página siguiente con atributos](../../ui/activate-edge-personalization-destinations.md), solo el [audiencias seleccionadas](../../ui/activate-edge-personalization-destinations.md#select-audiences) se envían al espacio de trabajo de Target seleccionado. El [atributos asignados](../../ui/activate-edge-personalization-destinations.md#mapping) se envían al espacio de trabajo de Target predeterminado.
><br>
>Este comportamiento cambiará en una actualización futura.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activación de audiencias en destinos de personalización de Edge](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Adobe Target lee datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).
