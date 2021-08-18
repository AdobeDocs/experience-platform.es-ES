---
keywords: plataforma;destinos;espacio de trabajo de destinos;espacio de trabajo;iu;iu de destinos;catálogo;catálogo de destinos
title: Espacio de trabajo de destinos
description: El espacio de trabajo Destinos consta de cuatro secciones, Catálogo, Examinar, Cuentas y Vista del sistema. Se describen en las secciones siguientes.
seo-description: En Adobe Experience Platform, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a97b235e2d8834f6be002923be9cdbca5f08495b
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---

# Espacio de trabajo de destinos {#destinations-workspace}

En Adobe Experience Platform, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Destinations].

El espacio de trabajo [!UICONTROL Destinations] consta de cinco secciones, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] y [!UICONTROL System View], que se describen en las secciones siguientes.

![Información general sobre destinos](../assets/ui/workspace/destinations-overview.png)

## Información general de  {#overview}

La pestaña **[!UICONTROL Overview]** muestra el panel [!UICONTROL Destinations], que proporciona métricas clave relacionadas con los datos de destino de la organización. Para obtener más información, consulte la [[!UICONTROL Destinations] guía del tablero](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si su organización es nueva para Experience Platform y aún no tiene destinos activos, el panel [!UICONTROL Destinations] y la pestaña [!UICONTROL Overview] no están visibles. En su lugar, al seleccionar [!UICONTROL Destinations] en el panel de navegación izquierdo, se muestra la pestaña [[!UICONTROL Catalog]](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La pestaña **[!UICONTROL Catalog]** muestra una lista de todos los destinos disponibles en [!DNL Platform] a los que puede enviar datos.

La interfaz de usuario [!DNL Platform] proporciona varias opciones de búsqueda y filtro en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtre los destinos mediante el control [!UICONTROL Categories].
* Alternar entre [!UICONTROL Todos los destinos] y [!UICONTROL Mis destinos]. Cuando selecciona **[!UICONTROL Todos los destinos]**, se muestran todos los destinos [!DNL Platform] disponibles. Al seleccionar **[!UICONTROL Mis destinos]**, solo puede ver los destinos con los que ha establecido una conexión.
* Seleccione para ver **[!UICONTROL Conexiones]** o **[!UICONTROL Extensiones]**. Para comprender la diferencia entre las dos categorías, consulte [Tipos de destino y Categorías](../destination-types.md).

![filtrado de destinos y demostración de búsqueda](../assets/ui/workspace/destinations-search-and-filter.gif)

Las tarjetas de destino contienen un control **[!UICONTROL Configure]** o **[!UICONTROL Activate]** y un control secundario que muestra más opciones. Estos controles se describen a continuación:

| Control | Descripción |
|---------|----------|
| [!UICONTROL Configurar] | Permite crear una conexión con el destino. |
| [!UICONTROL Activar] | Una vez que haya establecido una conexión con el destino, puede activar segmentos. |
| [!UICONTROL Ver cuenta] | Ver las cuentas que se han conectado para un destino. |
| [!UICONTROL Ver flujos de datos] | Ver los flujos de activación de datos que existen para un destino. |
| [!UICONTROL Ver documentación] | Abre un vínculo a la página de documentación para ese destino específico, para obtener más información y para ayudarle a configurarla. |

{style=&quot;table-layout:auto&quot;}

![Controles en la tarjeta de destino](../assets/ui/workspace/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril derecho. Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, incluida una descripción del destino y una indicación de la categoría y el tipo de destino.

![Opciones de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obtener más información sobre las categorías de destino y la información sobre cada destino, consulte [Destination catalog](../catalog/overview.md) y [Destination types and categories](../destination-types.md).

## [!UICONTROL Cuentas] {#accounts}

La pestaña **[!UICONTROL Accounts]** le muestra detalles sobre las conexiones que ha establecido con varios destinos y le permite actualizar los detalles de conexión existentes. Consulte [Actualizar cuentas](update-accounts.md) para obtener instrucciones detalladas.

## [!UICONTROL Examinar] {#browse}

La pestaña **[!UICONTROL Browse]** muestra los destinos con los que ha establecido una conexión. Los destinos con la opción **[!UICONTROL Enabled/Disabled]** activada establecen el destino como activo o inactivo, respectivamente. También puede ver los destinos en los que tiene datos fluyendo seleccionando **[!UICONTROL Segments]** > **[!UICONTROL Browse]** y un segmento para inspeccionar. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la pestaña Examinar:

>[!TIP]
>
> * Seleccione los tres puntos de la columna [!UICONTROL Name] y utilice el botón ![Add segments button](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate ]**para enviar segmentos a ese destino.
> * Seleccione los tres puntos de la columna [!UICONTROL Name] y utilice el botón ![Delete destinos button](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete ]**para [eliminar](delete-destinations.md) una conexión existente a un destino.


![Ficha Examinar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descripción |
|---------|----------|
| Nombre | Nombre que ha proporcionado para el flujo de activación a este destino. La misma columna incluye dos controles: [!UICONTROL Activar ] y [!UICONTROL Eliminar destino]. |
| [!UICONTROL Estado de ejecución del último flujo] | Estado de la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Fecha de ejecución del último flujo] | Hora y fecha en que se produjo la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Destino] | La plataforma de destino que seleccionó para el flujo de activación. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con su espacio de almacenamiento o destino. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3, FTP o [!DNL Azure Blob].</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor.</li><li>Para destinos de flujo continuo: Puede ser [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nombre de usuario] | Credenciales de cuenta que ha seleccionado para el flujo de destino. |
| [!UICONTROL Datos de activación] | Indica el número de segmentos que se están activando en este destino. Seleccione este control para obtener más información sobre los segmentos activados. Consulte [Datos de activación](/help/destinations/ui/destination-details-page.md#activation-data) en la página de detalles de destino para obtener más información sobre los segmentos activados. |
| [!UICONTROL Creado] | La fecha y la hora UTC en que se creó el flujo de activación al destino. |
| [!UICONTROL Estado] | `Active` o `Inactive`. Indica si se están activando datos en este destino. |

Haga clic en una fila de destino para que aparezca más información sobre el destino en el carril derecho.

![Haga clic en la fila de destino](../assets/ui/workspace/click-destination-row.png)

Seleccione el nombre del destino para ver información sobre los segmentos activados en este destino. Haga clic en **[!UICONTROL Editar activación]** para modificar o agregar a los segmentos que se envían a este destino.

## [!UICONTROL Vista del sistema] {#system-view}

La pestaña **[!UICONTROL System View]** muestra una representación gráfica de los flujos de activación que ha configurado en Adobe Experience Platform.

![Flujos de datos1](../assets/ui/workspace/data-flows1.png)

Seleccione cualquiera de los destinos mostrados en la página y haga clic en **[!UICONTROL Ver flujos de datos]** para ver información sobre todas las conexiones configuradas para cada destino.

![Flujos de datos2](../assets/ui/workspace/data-flows2.png)
