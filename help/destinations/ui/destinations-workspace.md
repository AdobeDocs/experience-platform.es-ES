---
keywords: plataforma;destinos;espacio de trabajo de destinos;espacio de trabajo;iu;iu de destinos;catálogo;catálogo de destinos;
title: Espacio de trabajo Destinos
description: El espacio de trabajo Destinos consta de cinco secciones, Información general, Catálogo, Examinar, Cuentas y Vista de sistema. Se describen en las secciones siguientes.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# Espacio de trabajo Destinos {#destinations-workspace}

En Adobe Experience Platform, seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Destinos].

El área de trabajo [!UICONTROL Destinos] consta de cinco secciones, [!UICONTROL Información general], [!UICONTROL Catálogo], [!UICONTROL Examinar], [!UICONTROL Cuentas] y [!UICONTROL Vista del sistema], que se describen en las secciones siguientes.

![Panel de información general de destinos que muestra tres widgets.](../assets/ui/workspace/destinations-overview.png)

## Información general de  {#overview}

La pestaña **[!UICONTROL Información general]** muestra el panel [!UICONTROL Destinos], que proporciona métricas clave relacionadas con los datos de destino de su organización. Para obtener más información, visita la guía de panel [[!UICONTROL Destinos]](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si su organización es nueva en Experience Platform y aún no tiene destinos activos, el panel [!UICONTROL Destinos] y la pestaña [!UICONTROL Información general] no están visibles. En su lugar, al seleccionar [!UICONTROL Destinos] en el panel de navegación izquierdo, se muestra la ficha [[!UICONTROL Catálogo]](#catalog).

![Pestaña Información general del panel Destinos.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La ficha **[!UICONTROL Catálogo]** muestra una lista de todos los destinos disponibles en [!DNL Experience Platform] a los que puede enviar datos.

La interfaz de usuario [!DNL Experience Platform] proporciona varias opciones de búsqueda y filtrado en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtrar destinos utilizando el control [!UICONTROL Categories].
* Alternar entre [!UICONTROL Todos los destinos] y [!UICONTROL Mis destinos]. Al seleccionar **[!UICONTROL Todos los destinos]**, se muestran todos los destinos disponibles [!DNL Experience Platform]. Al seleccionar **[!UICONTROL Mis destinos]**, solo podrá ver los destinos con los que estableció una conexión.
* Seleccione para ver los tipos de **[!UICONTROL Conexiones]** y/o **[!UICONTROL Extensiones]**. Para comprender la diferencia entre las dos categorías, lea [Tipos de destino y Categorías](../destination-types.md).

![Catálogo de destinos que muestra algunos destinos de almacenamiento en la nube y publicidad.](../assets/ui/workspace/catalog.png)

Las tarjetas de destino contienen opciones de control principales y secundarias. Los controles principales incluyen [!UICONTROL Configurar], [!UICONTROL Activar], [!UICONTROL Activar audiencias] o [!UICONTROL Exportar conjuntos de datos]. Los controles secundarios permiten ver las opciones. Estos controles se describen a continuación:

| Control | Descripción |
|---------|----------|
| [!UICONTROL Configurar] | Permite crear una conexión con el destino. |
| [!UICONTROL Activar] | Una vez establecida una conexión con el destino, puede activar audiencias o exportar conjuntos de datos a este destino. |
| [!UICONTROL Activar audiencias] | Una vez establecida una conexión con el destino, puede activar audiencias en este destino. |
| [!UICONTROL Exportar conjuntos de datos] | Una vez establecida una conexión con el destino, puede exportar conjuntos de datos a este destino. |
| [!UICONTROL Ver cuenta] | Ver las cuentas que ha conectado para un destino. |
| [!UICONTROL Ver flujos de datos] | Vea los flujos de activación de datos que existen para un destino. |
| [!UICONTROL Ver documentación] | Abre un vínculo a la página de documentación de ese destino específico, para obtener más información y para ayudarle a configurarlo. |

{style="table-layout:auto"}

![Controles en la tarjeta de destinos](../assets/ui/workspace/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril derecho. Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, incluida una descripción del destino e indicación de la categoría y el tipo de destino.

![Opciones del catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obtener más información sobre las categorías de destino e información sobre cada destino, consulte el [catálogo de destino](../catalog/overview.md) y [tipos y categorías de destino](../destination-types.md).

## [!UICONTROL Cuentas] {#accounts}

La ficha **[!UICONTROL Cuentas]** muestra detalles acerca de las conexiones que ha establecido con varios destinos y le permite actualizar o eliminar los detalles de cuenta existentes. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada cuenta de destino.

>[!TIP]
>
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Plataforma] y use el control ![Activar control](/help/images/icons/data-add.png)**[!UICONTROL Activar &#x200B;]**/**[!UICONTROL &#x200B; Activar audiencias &#x200B;]**/**[!UICONTROL &#x200B; Exportar conjuntos de datos &#x200B;]**&#x200B;para exportar audiencias o conjuntos de datos a ese destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Plataforma] y use el control ![Editar detalles](/help/images/icons/edit.png)**[!UICONTROL Editar detalles &#x200B;]**&#x200B;para [actualizar](update-accounts.md) los detalles de una cuenta de destino existente.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Plataforma] y use el control ![Eliminar control](/help/images/icons/delete.png)**[!UICONTROL Eliminar &#x200B;]**&#x200B;para [eliminar](delete-destination-account.md) una cuenta de destino existente.

![Pestaña Cuentas](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descripción |
|---|---|
| [!UICONTROL Destino] | El conector de destino para el que ha configurado la conexión. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión de cuenta al espacio de almacenamiento o destino. Según el destino, las opciones de autenticación son: <ul><li>Para destinos de marketing por correo electrónico: puede ser S3, FTP o Azure Blob.</li><li>Para destinos de publicidad en tiempo real: de servidor a servidor</li><li>Para destinos de almacenamiento en la nube de Amazon S3: clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: autenticación básica para SFTP.</li><li>Autenticación OAuth 1 u OAuth 2</li><li>Autenticación de token de portador</li></ul> |
| [!UICONTROL Nombre de usuario] | El nombre de usuario que seleccionó en [conectar flujo de trabajo de destino](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Conexiones] | Representa el número de flujos de datos de destino únicos correctos conectados con información básica creada para un destino. |
| [!UICONTROL Fecha de autorización] | La fecha en la que se autorizó la conexión con este destino. |

{style="table-layout:auto"}

## [!UICONTROL Examinar] {#browse}

La ficha **[!UICONTROL Examinar]** muestra los destinos con los que ha establecido una conexión. Los destinos con la opción **[!UICONTROL Habilitado/Deshabilitado]** activada establecen el destino como activo o inactivo, respectivamente. También puede ver los destinos a los que le están fluyendo los datos seleccionando **[!UICONTROL Audiencias]** > **[!UICONTROL Examinar]** y una audiencia para inspeccionar. Consulte la tabla siguiente para obtener toda la información que se proporciona para cada destino en la ficha [!UICONTROL Examinar]:

>[!TIP]
>
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Activar control de audiencias](/help/images/icons/data-add.png)**[!UICONTROL Activar &#x200B;]**&#x200B;para exportar audiencias o conjuntos de datos a ese destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Eliminar control](/help/images/icons/delete.png)**[!UICONTROL Eliminar &#x200B;]**&#x200B;para [quitar](delete-destinations.md) una conexión existente a un destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Ver en control de supervisión](/help/images/icons/monitoring.png)**[!UICONTROL Ver en control de supervisión &#x200B;]**&#x200B;para ver la información de activación de este destino en el [panel de supervisión](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Nombre] y use el control ![Suscribirse a alertas ](/help/images/icons/alert-add.png)**[!UICONTROL Suscribirse a alertas &#x200B;]**&#x200B;para suscribirse a alertas de flujo de datos de destino. Puede suscribirse a alertas para recibir mensajes sobre el estado, el éxito o el error de la ejecución del flujo. Consulte [Suscribirse a alertas de destino en contexto](alerts.md) para obtener información detallada sobre las alertas de flujo de datos de destino.

![Ficha Examinar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descripción |
|---------|----------|
| Nombre | El nombre proporcionado para el flujo de activación a este destino. La misma columna incluye dos controles: [!UICONTROL Activar] y [!UICONTROL Eliminar destino]. |
| [!UICONTROL Último estado de ejecución de flujo] | El estado de la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Última fecha de ejecución de flujo] | Fecha y hora en la que se produjo la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Destino] | La plataforma de destino seleccionada para el flujo de activación. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión a su espacio de almacenamiento o destino. <ul><li>Para destinos de marketing por correo electrónico: puede ser S3, FTP o [!DNL Azure Blob].</li><li>Para destinos de publicidad en tiempo real: de servidor a servidor.</li><li>Para destinos de flujo continuo: puede ser [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nombre de usuario] | Las credenciales de cuenta seleccionadas para el flujo de destino. |
| [!UICONTROL Datos de activación] | Indica la cantidad de audiencias que se están activando en este destino. Seleccione este control para obtener más información sobre las audiencias activadas. Consulte [Datos de activación](/help/destinations/ui/destination-details-page.md#activation-data) en la página de detalles de destino para obtener más información sobre las audiencias activadas. |
| [!UICONTROL Creado] | La fecha y la hora en formato UTC en que se creó el flujo de activación al destino. Seleccione el símbolo de flecha arriba/abajo para ordenar los flujos de activación por el más reciente primero o el más antiguo primero. |
| [!UICONTROL Estado] | `Enabled` o `Disabled`. Indica si los datos se están activando en este destino. |

Haga clic en una fila de destino para que aparezca más información sobre el destino en el carril derecho, como el ID de destino, la descripción, el número de audiencias activadas, etc.

![Haga clic en la fila de destino](../assets/ui/workspace/click-destination-row.png)

Seleccione el nombre del destino para ver información sobre las audiencias activadas en este destino. Haga clic en **[!UICONTROL Editar activación]** para modificar o agregar audiencias que se envíen a este destino.

## [!UICONTROL Vista de sistema] {#system-view}

La ficha **[!UICONTROL Vista de sistema]** muestra una representación gráfica de los flujos de activación que ha configurado en Adobe Experience Platform.

![Flujos de datos1](../assets/ui/workspace/data-flows1.png)

Seleccione cualquiera de los destinos mostrados en la página y haga clic en **[!UICONTROL Ver flujos de datos]** para ver información sobre todas las conexiones configuradas para cada destino.

![Flujos de datos2](../assets/ui/workspace/data-flows2.png)
