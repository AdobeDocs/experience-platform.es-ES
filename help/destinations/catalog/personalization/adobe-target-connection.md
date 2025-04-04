---
keywords: personalización de target; destino; destino de experience platform target; destino de adobe target;
title: Conexión de Adobe Target
description: Adobe Target es una aplicación que proporciona capacidades de personalización y experimentación en tiempo real impulsadas por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 10%

---

# Conexión de Adobe Target {#adobe-target-connection}

## Registro de cambios de destino {#changelog}

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Abril de 2024 | Actualización de funcionalidad y documentación | Al conectarse al destino de Target y usar un ID de flujo de datos, ahora *no necesita* para habilitar necesariamente el flujo de datos para la segmentación de Edge. Esto significa que el destino de Target funcionará con audiencias por lotes y de flujo continuo, aunque los casos de uso que puede realizar difieren. Vea la tabla en la sección [parámetros de conexión](#parameters) para obtener más información. |
| Enero de 2024 | Actualización de funcionalidad y documentación | Ahora puede compartir audiencias y atributos de perfil con la conexión de Adobe Target para la zona protegida de producción predeterminada y otras zonas protegidas no predeterminadas. |
| Junio de 2023 | Actualización de funcionalidad y documentación | A partir de junio de 2023, puede seleccionar el espacio de trabajo de Adobe Target con el que desea compartir audiencias al configurar una nueva conexión de destino de Adobe Target. Consulte la sección [parámetros de conexión](#parameters) para obtener más información. Además, consulte el tutorial sobre [configuración de espacios de trabajo](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es) en Adobe Target para obtener más información acerca de los espacios de trabajo. |
| Mayo de 2023 | Actualización de funcionalidad y documentación | A partir de mayo de 2023, la conexión de **[!UICONTROL Adobe Target]** admite la [personalización basada en atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) y, por lo general, está disponible para todos los clientes. |

{style="table-layout:auto"}

## Información general {#overview}

Adobe Target es una aplicación que proporciona capacidades de personalización y experimentación en tiempo real impulsadas por IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.

Adobe Target es una conexión de personalización del catálogo de destinos de Adobe Experience Platform.

## Vídeo introductorio {#video-overview}

Vea el siguiente vídeo para obtener una breve descripción general sobre cómo configurar la conexión de Adobe Target en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Casos de uso admitidos basados en el tipo de implementación {#supported-use-cases}

La tabla siguiente muestra los casos de uso admitidos para el destino de Adobe Target, según el tipo de implementación, con o sin [Web SDK](/help/web-sdk/home.md) y con o sin [segmentación de Edge](/help/segmentation/home.md#edge) habilitada.

| Implementación de Adobe Target *sin* Web SDK | Implementación de Adobe Target *con* Web SDK | Implementación de Adobe Target *con* Web SDK *y* segmentación de Edge desactivada |
|---|---|---|
| <ul><li>No se requiere una secuencia de datos. Adobe Target se puede implementar mediante los métodos de implementación [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [del lado del servidor](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) o [híbrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation).</li><li>[No se admite la segmentación de Edge](../../../segmentation/methods/edge-segmentation.md).</li><li>[No se admite la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md).</li><li>Puede compartir audiencias y atributos de perfil con la conexión de Adobe Target para la *zona protegida de producción predeterminada* y las zonas protegidas no predeterminadas.</li><li>Para configurar la personalización de la sesión siguiente sin usar un ID de flujo de datos, usa [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Se requiere un flujo de datos con Adobe Target y Experience Platform configurados como servicios.</li><li>La segmentación de Edge funciona según lo esperado.</li><li>[Se admite la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md#use-cases).</li><li>Se admite el uso compartido de audiencias y atributos de perfil desde otras zonas protegidas.</li></ul> | <ul><li>Se requiere un flujo de datos con Adobe Target y Experience Platform configurados como servicios.</li><li>Al [configurar la secuencia de datos](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), no active la casilla de verificación **Segmentación de Edge**.</li><li>[Se admite la personalización para la próxima sesión](../../ui/activate-edge-personalization-destinations.md#next-session).</li><li>Se admite el uso compartido de audiencias y atributos de perfil desde otras zonas protegidas.</li></ul> |


## Requisitos previos {#prerequisites}

### ID de la secuencia de datos {#datastream-id}

Al configurar la conexión de Adobe Target para [usar un ID de secuencia de datos](#parameters), debe tener implementado [Adobe Experience Platform Web SDK](/help/web-sdk/home.md).

La configuración de la conexión de Adobe Target sin utilizar un ID de conjunto de datos no requiere la implementación de Web SDK.

>[!IMPORTANT]
>
>Antes de crear una conexión de [!DNL Adobe Target], lea la guía sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md). Esta guía le explica los pasos de configuración necesarios para los casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform. Para conseguir casos de uso de personalización de la misma página y de la siguiente, debe utilizar un ID de flujo de datos al configurar la conexión de Adobe Target.

### Requisitos previos en Adobe Target {#prerequisites-in-adobe-target}

En Adobe Target, asegúrese de que el usuario tenga:

* Acceso al [espacio de trabajo predeterminado](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* El **aprobador** [rol](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Obtenga más información sobre la concesión de permisos para [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) y para [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

>[!IMPORTANT]
>
>Al activar *audiencias de Edge para casos de uso de personalización de la misma página y de la siguiente página*, las audiencias *deben* usar una [política de combinación activa en Edge](../../../segmentation/ui/segment-builder.md#merge-policies). La política de combinación [!DNL active-on-edge] garantiza que las audiencias se evalúen constantemente [en el perímetro](../../../segmentation/methods/edge-segmentation.md) y que estén disponibles para casos de uso de personalización en tiempo real y de la página siguiente.  Obtenga información sobre [todos los casos de uso disponibles](#parameter), según el tipo de implementación.
>Si asigna audiencias perimetrales que utilizan una política de combinación diferente a destinos de Adobe Target, esas audiencias no se evalúan para casos de uso en tiempo real y de la página siguiente.
>Siga las instrucciones de [creación de una política de combinación](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy) y asegúrese de habilitar la opción **[!UICONTROL Política de combinación activa en Edge]**.


| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todas las audiencias asignadas en el destino de Adobe Target para un solo perfil. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Acerca de los ID de secuencia de datos"
>abstract="Esta opción determina en qué secuencia de datos de recopilación de datos se incluirán los públicos. El menú desplegable muestra solo las secuencias de datos que tienen habilitada la configuración de destino. Para utilizar la segmentación de Edge, debe seleccionar un ID de la secuencia de datos. Al seleccionar Ninguno, se desactivan todos los casos de uso que utilizan segmentación de Edge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=es#parameters" text="Obtenga más información sobre la selección de secuencias de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Acerca de Adobe Target Workspaces"
>abstract="Seleccione el espacio de trabajo de Adobe Target que se compartirá al público. Puede seleccionar un único espacio de trabajo para cada conexión de Adobe Target. Tras la activación, el público se dirige al espacio de trabajo seleccionado siguiendo las etiquetas de uso de datos del Experience Platform aplicables."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es" text="Más información acerca de los espacios de trabajo de Adobe Target"

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **Nombre**: rellene el nombre preferido para este destino.
* **Descripción**: escribe una descripción para el destino. Por ejemplo, puede mencionar para qué campaña está usando este destino. Este campo es opcional.
* **ID de secuencia de datos**: Esto determina en qué secuencia de datos de recopilación de datos se incluirán las audiencias. El menú desplegable solo muestra las secuencias de datos que tienen habilitados los servicios de Target y Adobe Experience Platform. Consulte [configuración de un conjunto de datos](../../../datastreams/configure.md#aep) para obtener información detallada sobre cómo configurar un conjunto de datos para Adobe Experience Platform y Adobe Target.

  >[!IMPORTANT]
  >
  >El ID de la secuencia de datos es único para cada conexión de destino de Adobe Target. No se puede usar el mismo ID de flujo de datos para varias conexiones de destino de Adobe Target.
  >Si necesita asignar las mismas audiencias a varios flujos de datos, debe [crear una nueva conexión de destino](../../ui/connect-destination.md) para cada ID de flujo de datos y pasar por el [flujo de activación de audiencia](#activate).

   * **[!UICONTROL Ninguno]**: seleccione esta opción si necesita configurar la personalización de Adobe Target pero no puede implementar [Experience Platform Web SDK](/help/web-sdk/home.md). Con esta opción, las audiencias exportadas de Experience Platform a Target solo admiten la personalización de la sesión siguiente y la segmentación de Edge está desactivada. Consulte la tabla en la sección [casos de uso admitidos](#supported-use-cases) para ver una comparación de los casos de uso disponibles por tipo de implementación.

  | Implementación de Adobe Target *sin* Web SDK | Implementación de Adobe Target *con* Web SDK | Implementación de Adobe Target *con* Web SDK *y* segmentación de Edge desactivada |
  |---|---|---|
  | <ul><li>No se requiere una secuencia de datos. Adobe Target se puede implementar mediante los métodos de implementación [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [del lado del servidor](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) o [híbrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation).</li><li>[No se admite la segmentación de Edge](../../../segmentation/methods/edge-segmentation.md).</li><li>[No se admite la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md).</li><li>Puede compartir audiencias y atributos de perfil con la conexión de Adobe Target para la *zona protegida de producción predeterminada* y las zonas protegidas no predeterminadas.</li><li>Para configurar la personalización de la sesión siguiente sin usar un ID de flujo de datos, usa [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Se requiere un flujo de datos con Adobe Target y Experience Platform configurados como servicios.</li><li>La segmentación de Edge funciona según lo esperado.</li><li>[Se admite la personalización de la misma página y de la página siguiente](../../ui/activate-edge-personalization-destinations.md#use-cases).</li><li>Se admite el uso compartido de audiencias y atributos de perfil desde otras zonas protegidas.</li></ul> | <ul><li>Se requiere un flujo de datos con Adobe Target y Experience Platform configurados como servicios.</li><li>Al [configurar la secuencia de datos](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), no active la casilla de verificación **Segmentación de Edge**.</li><li>[Se admite la personalización para la próxima sesión](../../ui/activate-edge-personalization-destinations.md#next-session).</li><li>Se admite el uso compartido de audiencias y atributos de perfil desde otras zonas protegidas.</li></ul> |

* **Workspace**: seleccione el [espacio de trabajo](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=es) de Adobe Target en el que se compartirán las audiencias. Puede seleccionar un único espacio de trabajo para cada conexión de Adobe Target. Tras la activación, las audiencias se enrutan al espacio de trabajo seleccionado siguiendo las [etiquetas de uso de datos de Experience Platform](../../../data-governance/labels/overview.md) aplicables.

>[!NOTE]
>
>Cuando se usa un área de trabajo de Target personalizada para la personalización de la misma página y de la página siguiente de [con atributos](../../ui/activate-edge-personalization-destinations.md), solo se envían las [audiencias seleccionadas](../../ui/activate-edge-personalization-destinations.md#select-audiences) al área de trabajo de Target seleccionada. Los [atributos asignados](../../ui/activate-edge-personalization-destinations.md#mapping) se envían al espacio de trabajo de Target predeterminado.
><br>
>Este comportamiento cambiará en una actualización futura.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lea [Activar audiencias en destinos de personalización Edge](../../ui/activate-edge-personalization-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Eliminación de audiencias de un destino de Target {#remove}

Se requieren pasos adicionales para quitar una audiencia de una conexión de Adobe Target existente cuando esa audiencia ya se está usando en una [actividad](https://experienceleague.adobe.com/en/docs/target/using/activities/activities) de Adobe Target. Si se intenta eliminar una audiencia de una conexión de Adobe Target, se produce un error si una actividad de Adobe Target utiliza la audiencia.

![Imagen de la interfaz de usuario de Experience Platform que muestra un error provocado al intentar quitar una audiencia que usa una actividad de Target.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Para quitar una audiencia de un destino de Target cuando la audiencia se está usando en una actividad, primero debe quitar la audiencia de la actividad de Target que la está usando o eliminar por completo la actividad. A continuación, puede quitar la audiencia de la conexión de Target.

Si la audiencia no se está usando en una actividad, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** > **[!UICONTROL Seleccionar flujo de datos de destino]** > **[!UICONTROL Datos de activación]**, seleccione las audiencias que desee eliminar y, a continuación, seleccione **[!UICONTROL Quitar audiencias]**.

## Datos exportados {#exported-data}

Adobe Target *lee* datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).
