---
keywords: personalización de target; destino; destino de experience platform target;destino de adobe target;
title: Conexión Adobe Target
description: Adobe Target es una aplicación que proporciona funciones de personalización y experimentación en tiempo real y con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 2dbc449d6074c5bbfc44f92de59dd8acc3bf275d
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 1%

---

# Conexión Adobe Target {#adobe-target-connection}

## Registro de cambios del destino {#changelog}

>[!IMPORTANT]
>
>Con la versión beta del conector de destino Adobe Target V2 mejorado, es posible que vea dos tarjetas Adobe Target en el catálogo de destinos.
>El conector de destino Adobe Target V2 está actualmente en fase beta y solo está disponible para un número determinado de clientes. Además de la funcionalidad proporcionada por la tarjeta Adobe V1, el conector Target V2 agrega una [paso de asignación](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) al flujo de trabajo de activación, que le permite asignar atributos de perfil a Adobe Target, habilitando la personalización de la misma página y de la página siguiente basada en atributos.

![Imagen de las dos tarjetas de destino de Adobe Target en una vista en paralelo.](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## Información general {#overview}

Adobe Target es una aplicación que proporciona funciones de personalización y experimentación en tiempo real y con tecnología de IA en todas las interacciones de clientes entrantes entre sitios web, aplicaciones móviles y mucho más.

Adobe Target es una conexión personalizada en el catálogo de destinos de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

### ID de almacén de datos {#datastream-id}

Al configurar la conexión de Adobe Target a [usar un ID de conjunto de datos](#parameters), debe tener la variable [SDK web de Adobe Experience Platform](../../../edge/home.md) implementado.

La configuración de la conexión de Adobe Target sin utilizar un ID de conjunto de datos no requiere que implemente el SDK web.

>[!IMPORTANT]
>
>Antes de crear una [!DNL Adobe Target] conexión, lea la guía sobre cómo [configurar destinos de personalización para la personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md). Esta guía le guía a través de los pasos de configuración necesarios para casos de uso de personalización de la misma página y de la siguiente página, en varios componentes de Experience Platform. La personalización de la misma página y de la página siguiente requiere que utilice un ID de conjunto de datos al configurar la conexión de Adobe Target.

### Requisitos previos en Adobe Target {#prerequisites-in-adobe-target}

En Adobe Target, asegúrese de que su usuario tenga:

* Acceso a [espacio de trabajo predeterminado](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* La variable **Aprobador** [función](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

Obtenga más información sobre la concesión de permisos para [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) y para [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!DNL Profile request]** | Está solicitando todos los segmentos asignados en el destino de Adobe Target para un solo perfil. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

**Personalización de un banner de página principal**

Una empresa de ventas y alquiler de casa quiere personalizar su página principal con un banner, según las clasificaciones de segmentos del cliente en Adobe Experience Platform. La empresa puede seleccionar qué audiencias deben obtener una experiencia personalizada y enviarlas a Adobe Target como criterios de objetivo para su oferta de Target.

## Conectarse al destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Acerca de los ID de conjunto de datos"
>abstract="Esta opción determina en qué almacén de datos de recopilación de datos se incluirán los segmentos. El menú desplegable muestra solo los conjuntos de datos que tienen habilitada la configuración de Target. Para utilizar la segmentación perimetral, debe seleccionar un ID de conjunto de datos. Al seleccionar Ninguno se desactivan todos los casos de uso que utilizan segmentación perimetral."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Obtenga más información sobre la selección de conjuntos de datos"

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

Adobe Experience Platform se conecta automáticamente a la instancia de Adobe Target de su empresa. No se requiere autenticación.

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **Nombre**: Rellene el nombre preferido para este destino.
* **Descripción**: Escriba una descripción para el destino. Por ejemplo, puede mencionar para qué campaña utiliza este destino. Este campo es opcional.
* **ID de almacén de datos**: Esto determina en qué almacén de datos de recopilación de datos se incluyen los segmentos. El menú desplegable muestra solo los conjuntos de datos que tienen habilitado el destino de Target. Consulte [configuración de un conjunto de datos](../../../edge/datastreams/overview.md#target) para obtener información detallada sobre cómo configurar un conjunto de datos para Adobe Target.
   * **[!UICONTROL Ninguna]**: Seleccione esta opción si necesita configurar la personalización de Adobe Target pero no puede implementar la variable [SDK web de Experience Platform](../../../edge/home.md). Al utilizar esta opción, los segmentos exportados de Experience Platform a Target solo admiten la personalización de la siguiente sesión, y la segmentación perimetral está deshabilitada. Consulte la siguiente tabla para obtener más información.

| No se ha seleccionado ningún conjunto de datos | Almacén de datos seleccionado |
|---|---|
| <ul><li>[Segmentación de Edge](../../../segmentation/ui/edge-segmentation.md) no es compatible.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md) no son compatibles.</li><li>Puede compartir segmentos con la conexión de Adobe Target solo para el *entorno limitado de producción predeterminado*.</li><li>Para configurar la personalización de la siguiente sesión sin utilizar un ID de flujo de datos, utilice [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>La segmentación de Edge funciona según lo esperado.</li><li>[Personalización de la misma página y de la página siguiente](../../ui/configure-personalization-destinations.md) son compatibles.</li><li>El uso compartido de segmentos es compatible con otros entornos limitados.</li></ul> |

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar perfiles y segmentos en destinos de solicitud de perfil](../../ui/activate-profile-request-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Adobe Target lee datos de perfil de Adobe Experience Platform Edge Network, por lo que no se exportan datos.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=es).
