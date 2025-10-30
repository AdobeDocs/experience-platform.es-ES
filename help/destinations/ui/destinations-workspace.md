---
keywords: plataforma;destinos;espacio de trabajo de destinos;espacio de trabajo;iu;iu de destinos;catálogo;catálogo de destinos;
title: Espacio de trabajo Destinos
description: El espacio de trabajo Destinos consta de cinco secciones, Información general, Catálogo, Examinar, Cuentas y Vista de sistema. Se describen en las secciones siguientes.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Espacio de trabajo Destinos {#destinations-workspace}

En Adobe Experience Platform, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Destinations].

El área de trabajo [!UICONTROL Destinations] consta de cinco secciones, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] y [!UICONTROL System View], que se describen en las secciones siguientes.

![Panel de información general de destinos que muestra tres widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

La pestaña **[!UICONTROL Overview]** muestra el panel [!UICONTROL Destinations], que proporciona métricas clave relacionadas con los datos de destino de su organización. Para obtener más información, visite la [[!UICONTROL Destinations] guía de panel](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si su organización es nueva en Experience Platform y aún no tiene destinos activos, el panel [!UICONTROL Destinations] y la pestaña [!UICONTROL Overview] no son visibles. En su lugar, al seleccionar [!UICONTROL Destinations] en el panel de navegación izquierdo, se muestra la ficha [[!UICONTROL Catalog]](#catalog).

![Pestaña Información general del panel Destinos.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

La ficha **[!UICONTROL Catalog]** muestra una lista de todos los destinos disponibles en [!DNL Experience Platform] a los que puede enviar datos.

![Catálogo de destinos que muestra varios destinos.](../assets/ui/workspace/catalog.png)

La interfaz de usuario [!DNL Experience Platform] proporciona varias opciones de búsqueda y filtrado en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtrar destinos utilizando el control **[!UICONTROL Categories]**.
* Alternar entre **[!UICONTROL All destinations]** y **[!UICONTROL My destinations]**. Al seleccionar **[!UICONTROL All destinations]**, se muestran todos los destinos disponibles [!DNL Experience Platform]. Al seleccionar **[!UICONTROL My destinations]**, solo puede ver los destinos con los que ha establecido una conexión.
* Seleccione para ver los tipos **[!UICONTROL Connections]** y/o **[!UICONTROL Extensions]**. Para comprender la diferencia entre las dos categorías, lea [Tipos de destino y Categorías](../destination-types.md).
* Filtre los destinos disponibles según el [tipo de datos](/help/destinations/destination-sdk/functionality/destination-configuration/audience-data-type.md) admitido. Elija entre audiencias de personas, audiencias de cuenta, audiencias de clientes potenciales o exportaciones de conjuntos de datos.

Las tarjetas de destino contienen opciones de control principales y secundarias. Los controles principales incluyen [!UICONTROL Set up], [!UICONTROL Activate], [!UICONTROL Activate audiences] o [!UICONTROL Export datasets]. Los controles secundarios permiten ver las opciones. Estos controles se describen a continuación:

| Control | Descripción |
|---------|----------|
| [!UICONTROL Set up] | Permite crear una conexión con el destino. |
| [!UICONTROL Activate] | Una vez establecida una conexión con el destino, puede activar audiencias o exportar conjuntos de datos a este destino. |
| [!UICONTROL Activate audiences] | Una vez establecida una conexión con el destino, puede activar audiencias en este destino. |
| [!UICONTROL Export datasets] | Una vez establecida una conexión con el destino, puede exportar conjuntos de datos a este destino. |
| [!UICONTROL View account] | Ver las cuentas que ha conectado para un destino. |
| [!UICONTROL View dataflows] | Vea los flujos de activación de datos que existen para un destino. |
| [!UICONTROL View documentation] | Abre un vínculo a la página de documentación de ese destino específico, para obtener más información y para ayudarle a configurarlo. |

{style="table-layout:auto"}

![Controles en la tarjeta de destinos](../assets/ui/workspace/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril derecho. Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, incluida una descripción del destino e indicación de la categoría y el tipo de destino.

![Opciones del catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obtener más información sobre las categorías de destino e información sobre cada destino, consulte el [catálogo de destino](../catalog/overview.md) y [tipos y categorías de destino](../destination-types.md).

## [!UICONTROL Browse] {#browse}

>[!NOTE]
>
>Debido a las configuraciones de etiquetas de acceso, los flujos de datos de destino a los que un usuario no tiene acceso pueden aparecer en la interfaz de usuario en estado atenuado. Lea la documentación sobre [uso de etiquetas de acceso para administrar el acceso de los usuarios a los flujos de datos de destino](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know) para obtener más información.

La ficha **[!UICONTROL Browse]** muestra los destinos con los que ha establecido una conexión.

>[!TIP]
>
> Comience por [buscar en la barra](#search-browse) para encontrar flujos de datos específicos y, a continuación, utilice los [filtros de la barra lateral](#filter-options-browse) para reducir aún más los resultados.

Los destinos con la opción **[!UICONTROL Enabled/Disabled]** activada establecen el destino en **[!UICONTROL Enabled]** o **[!UICONTROL Disabled]**, respectivamente. También puede ver los destinos a los que le están fluyendo los datos seleccionando **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** y una audiencia que desee inspeccionar.

>[!TIP]
>
> ![Ficha Examinar](../assets/ui/workspace/browse-tab.png)
> 
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Activar control de audiencias](/help/images/icons/data-add.png) **[!UICONTROL Activate audiences]** para exportar audiencias o conjuntos de datos a ese destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Editar control de destino ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**para editar las conexiones de destino existentes. Lea el tutorial sobre [editar destinos](/help/destinations/ui/edit-destination.md) para obtener más información.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Editar control de acciones de marketing](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Edit marketing actions]** para [cambiar las acciones de marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) para el destino seleccionado.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Eliminar control](/help/images/icons/delete.png) **[!UICONTROL Delete]** para [quitar](delete-destinations.md) una conexión existente a un destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Ver en el control de supervisión](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]** para ver la información de activación de este destino en el [panel de supervisión](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Suscribirse a alertas](/help/images/icons/alert-add.png) **[!UICONTROL Subscribe to alerts]** para suscribirse a las alertas del flujo de datos de destino. Puede suscribirse a alertas para recibir mensajes sobre el estado, el éxito o el error de la ejecución del flujo. Consulte [Suscribirse a alertas de destino en contexto](alerts.md) para obtener información detallada sobre las alertas de flujo de datos de destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Name] y use el control ![Administrar etiquetas](/help/images/icons/manage-tags.png) **[!UICONTROL Manage tags]** para agregar o quitar etiquetas de un destino. Consulte la sección [Administrar etiquetas de destino](#manage-tags) para obtener información detallada sobre el uso de etiquetas.

Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la ficha [!UICONTROL Browse].

| Elemento | Descripción |
|---------|----------|
| Nombre | El nombre proporcionado para el flujo de activación a este destino. |
| Tipo de datos | Tipo de datos admitidos por la conexión de destino. Tipos de datos admitidos: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | El estado de la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Last Dataflow Run Date] | Fecha y hora en la que se produjo la última ejecución del flujo de datos. Seleccione el encabezado de columna para tener acceso a las opciones de ordenación (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]**). Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Destination] | La plataforma de destino seleccionada para el flujo de activación. |
| [!UICONTROL Account Expiration Date] | La fecha en la que caducará la autorización de conexión a este destino. <br> Aparece un icono de advertencia ![Advertencia: el icono de caducidad de la cuenta](/help/images/icons/alert-expiration.png) antes de la fecha de caducidad para avisarle de que la conexión caducará y puede que sea necesario renovarla. Los flujos de datos a conexiones caducadas se detienen y debe volver a autenticarse para reanudar los flujos de trabajo de activación. <br>**Importante**: Actualmente, esta columna solo está disponible para las conexiones de [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) y [Audiencias coincidentes de LinkedIn](../catalog/social/linkedin-b2b.md). <br> ![Ejemplo de advertencia de caducidad de la cuenta en la ficha Examinar](../assets/ui/workspace/account-expiration-browse.png){width="100" zoomable="yes" alt="Screenshot showing the account expiration warning icon and expiration date in the Browse tab."} |
| [!UICONTROL Username] | Las credenciales de cuenta seleccionadas para el flujo de destino. |
| [!UICONTROL Activation Data] | Indica la cantidad de audiencias que se están activando en este destino. Seleccione este control para obtener más información sobre las audiencias activadas. Consulte [Datos de activación](/help/destinations/ui/destination-details-page.md#activation-data) en la página de detalles de destino para obtener más información sobre las audiencias activadas. |
| [!UICONTROL Created] | La fecha y la hora en que se creó el flujo de activación al destino. Seleccione el símbolo de flecha arriba/abajo para ordenar los flujos de activación por el más reciente primero o el más antiguo primero. |
| [!UICONTROL Modified] | La fecha y la hora en que se modificó por última vez el flujo de activación al destino. |
| [!UICONTROL Status] | `Enabled` o `Disabled`. Indica si los datos se están activando en este destino. |
| [!UICONTROL Access labels] | Muestra cualquier etiqueta de acceso que se haya agregado a este flujo de datos de destino. Obtenga más información sobre [aplicar etiquetas de acceso a flujos de datos de destino](/help/access-control/abac/apply-access-labels-destinations.md). |
| [!UICONTROL Tags] | Muestra cualquier etiqueta añadida a este flujo de datos de destino. Utilice etiquetas para organizar y categorizar los flujos de datos para facilitar la administración. |

Haga clic en una fila de destino para que aparezca más información sobre el destino en el carril derecho, como el ID de destino, la descripción, el número de audiencias activadas, etc.

![Haga clic en la fila de destino](../assets/ui/workspace/click-destination-row.png)

Seleccione el nombre del destino para ver información sobre las audiencias activadas en este destino. Haga clic en **[!UICONTROL Edit destination]** para [modificar la configuración de destino](/help/destinations/ui/edit-destination.md) o **[!UICONTROL Activate audiences]** para agregar nuevas audiencias al flujo de datos.

### Filtrado de flujos de datos en la pestaña Browse {#filter-browse}

La pestaña **[!UICONTROL Browse]** incluye capacidades mejoradas de filtrado y búsqueda para ayudarle a encontrar y administrar rápidamente los flujos de datos de destino. Utilice la barra lateral izquierda para aplicar filtros y la barra de búsqueda para buscar flujos de datos específicos por nombre.

### Funcionalidad de búsqueda {#search-browse}

Utilice la barra de búsqueda situada en la parte superior de la tabla para buscar rápidamente flujos de datos por nombre. A medida que escribe, los resultados filtran automáticamente para mostrar solo los flujos de datos coincidentes.

![Demostración animada de la búsqueda de un flujo de datos de destino en la pestaña Examinar](../assets/ui/workspace/search.gif)

### Opciones de filtro {#filter-options-browse}

Utilice los filtros de la barra lateral izquierda para acotar la búsqueda.

![Filtros de destino en la ficha Examinar](../assets/ui/workspace/destination-filters.png)

* **[!UICONTROL Destination platform]**: filtre flujos de datos por plataformas de destino específicas (por ejemplo, [!DNL Amazon S3], [!DNL Facebook Custom Audience], [!DNL LinkedIn Matched Audience], etc.). Puede seleccionar varias plataformas simultáneamente.
* **[!UICONTROL Has any tag]**: filtre flujos de datos que tengan etiquetas específicas asignadas. Esto le ayuda a organizar y buscar flujos de datos en función del etiquetado personalizado.
* **[!UICONTROL Status]**: filtre los flujos de datos según su estado operativo:
   * **[!UICONTROL Enabled]**: solo muestra flujos de datos activos
   * **[!UICONTROL Disabled]**: solo muestra flujos de datos inactivos
* **[!UICONTROL Account name]**: filtre flujos de datos por el nombre de cuenta asociado. Esto le ayuda a encontrar todos los flujos de datos conectados a una cuenta de destino específica.
* **[!UICONTROL Created]**: filtre los flujos de datos por el usuario que los creó. Utilice este filtro para buscar flujos de datos creados por integrantes del equipo específicos.
* **[!UICONTROL Modified by]**: filtre los flujos de datos del usuario que los modificó por última vez. Utilice este filtro para identificar los cambios recientes realizados por usuarios específicos.
* **[!UICONTROL Creation date]**: filtre flujos de datos por su fecha de creación mediante un intervalo de fechas:
   * **[!UICONTROL Start date]**: establecer el comienzo del intervalo de fecha
   * **[!UICONTROL End date]**: establecer el final del intervalo de fecha
* **[!UICONTROL Modified date]**: filtre flujos de datos por su fecha de modificación mediante un intervalo de fechas:
   * **[!UICONTROL Start date]**: establecer el comienzo del intervalo de fecha
   * **[!UICONTROL End date]**: establecer el final del intervalo de fecha

### Filtros activos {#active-filters-browse}

Al aplicar filtros, aparecen como etiquetas debajo de la barra de búsqueda.

![Filtros activos mostrados como etiquetas debajo de la barra de búsqueda](../assets/ui/workspace/active-filters.png)

Aquí puede:

* Ver todos los filtros activos actualmente
* Elimine filtros individuales haciendo clic en el icono `X` de cada etiqueta de filtro
* Borrar todos los filtros a la vez utilizando la opción **[!UICONTROL Clear all]**

### Administrar etiquetas de destino {#manage-tags}

Las etiquetas ayudan a organizar y categorizar los flujos de datos de destino para facilitar la administración. Puede añadir y eliminar etiquetas de flujos de datos individuales para agruparlas según sus necesidades comerciales.

Para agregar una etiqueta a un flujo de datos, seleccione los puntos suspensivos (`...`) en la columna **[!UICONTROL Name]** y seleccione **[!UICONTROL Manage tags]** en el menú contextual.
Escriba el nombre de una etiqueta nueva en el campo **[!UICONTROL Tags]** y seleccione **[!UICONTROL Save]** para aplicar los cambios.

![Cuadro de diálogo Administrar etiquetas que muestra la selección de etiquetas y las opciones de creación](../assets/ui/workspace/tags.gif)

Para quitar una etiqueta de un flujo de datos, seleccione los puntos suspensivos (`...`) en la columna **[!UICONTROL Name]**, seleccione **[!UICONTROL Manage tags]** en el menú contextual y, a continuación, seleccione el icono `X` en la etiqueta que desee quitar.

### Prácticas recomendadas de etiquetado {#tag-best-practices}

Asegúrese de que los flujos de datos de destino permanezcan organizados, fáciles de encontrar y administrables siguiendo las directrices de etiquetado a continuación.

* **Use nombres descriptivos**: Cree etiquetas que indiquen claramente el propósito o la categoría del flujo de datos (por ejemplo, &quot;Campañas de marketing&quot;, &quot;Retención de clientes&quot;, &quot;Promociones de temporada&quot;)
* **Sea coherente**: Use una convención de nombres uniforme en toda la organización
* **Sea simple**: evite crear demasiadas etiquetas, ya que esto puede hacer que el filtrado sea menos efectivo
* **Usar etiquetas jerárquicas**: considere la posibilidad de usar prefijos para agrupar etiquetas relacionadas (por ejemplo, &quot;Campaign-Q4&quot;, &quot;Campaign-Q1&quot;)

## [!UICONTROL Accounts] {#accounts}

La ficha **[!UICONTROL Accounts]** muestra detalles acerca de las conexiones que ha establecido con varios destinos y le permite actualizar o eliminar detalles de cuenta existentes. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada cuenta de destino.

>[!TIP]
>
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Platform] y utilice el control ![Activate control ](/help/images/icons/data-add.png)**[!UICONTROL Activate]**/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**para exportar audiencias o conjuntos de datos a ese destino.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Platform] y use el control ![Editar detalles ](/help/images/icons/edit.png)**[!UICONTROL Edit details]**para [actualizar](update-accounts.md) los detalles de una cuenta de destino existente.
> * Seleccione los puntos suspensivos (`...`) en la columna [!UICONTROL Platform] y use el control ![Eliminar control ](/help/images/icons/delete.png)**[!UICONTROL Delete]**para [eliminar](delete-destination-account.md) una cuenta de destino existente.

![Pestaña Cuentas](../assets/ui/workspace/accounts-tab.png)

| Elemento | Descripción |
|---|---|
| [!UICONTROL Name] | El nombre que asignó a la cuenta de destino al [configurar](connect-destination.md#authenticate) el destino. Seleccione el encabezado de columna para tener acceso a las opciones de ordenación (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]**). |
| [!UICONTROL Destination] | El conector de destino para el que ha configurado la conexión. |
| [!UICONTROL Connection Type] | Representa el tipo de conexión de cuenta al espacio de almacenamiento o destino. Según el destino, las opciones de autenticación son: <ul><li>Para destinos de marketing por correo electrónico: puede ser S3, FTP o Azure Blob.</li><li>Para destinos de publicidad en tiempo real: de servidor a servidor</li><li>Para destinos de almacenamiento en la nube de Amazon S3: clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: autenticación básica para SFTP.</li><li>Autenticación OAuth 1 u OAuth 2</li><li>Autenticación de token de portador</li></ul> |
| [!UICONTROL Username] | El nombre de usuario que seleccionó en [conectar flujo de trabajo de destino](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Representa el número de flujos de datos de destino únicos correctos conectados con información básica creada para un destino. |
| [!UICONTROL Authorization date] | La fecha en la que se autorizó la conexión con este destino. |
| [!UICONTROL Expiration date] | La fecha en la que caducará la autorización de conexión a este destino. <br> Un icono de advertencia ![La cuenta caducó el icono de advertencia.](/help/images/icons/alert-expiration.png) aparece antes de la fecha de caducidad para avisarle de que la conexión caducará y podría requerir renovación. Los flujos de datos a conexiones caducadas se detienen y debe volver a autenticarse para reanudar los flujos de trabajo de activación. <br>**Importante**: Actualmente esta columna solo está disponible para las conexiones de [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) y [Audiencias coincidentes de LinkedIn](../catalog/social/linkedin-b2b.md). <br> ![](../assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Filtrado de cuentas {#filter-accounts}

La pestaña **[!UICONTROL Accounts]** incluye capacidades mejoradas de filtrado y búsqueda para ayudarle a encontrar y administrar rápidamente sus cuentas de destino. Utilice la barra lateral izquierda para aplicar filtros y la barra de búsqueda para buscar cuentas específicas por nombre.

#### Búsqueda de cuentas {#search-accounts}

Utilice la barra de búsqueda situada en la parte superior de la tabla para buscar rápidamente cuentas por nombre. A medida que escribe, los resultados filtran automáticamente para mostrar solo las cuentas coincidentes.

![Barra de búsqueda en la ficha Cuentas.](../assets/ui/workspace/accounts-search.gif)

#### Opciones de filtro {#filter-options-accounts}

Utilice los filtros de la barra lateral izquierda para acotar la búsqueda.

![Filtros de cuenta en la ficha Cuentas](../assets/ui/workspace/account-filters.png)

* **[!UICONTROL Destination platform]**: filtre las cuentas por plataformas de destino específicas (por ejemplo: [!DNL Microsoft Bing], [!DNL Amazon S3], [!DNL Facebook Custom Audiences], [!DNL LinkedIn Matched Audiences], etc.). Puede seleccionar varias plataformas simultáneamente.
* **[!UICONTROL Created by]**: filtre las cuentas según el usuario que las creó. Utilice este filtro para buscar cuentas creadas por integrantes específicos del equipo.

#### Filtros activos {#active-filters-accounts}

Al aplicar filtros, aparecen como etiquetas debajo de la barra de búsqueda.

![Filtros activos mostrados como etiquetas en la ficha Cuentas](../assets/ui/workspace/accounts-active-filters.png)

Aquí puede:

* Ver todos los filtros activos actualmente
* Elimine filtros individuales haciendo clic en el icono `X` de cada etiqueta de filtro
* Borrar todos los filtros a la vez utilizando la opción **[!UICONTROL Clear all]**

## [!UICONTROL System View] {#system-view}

La pestaña **[!UICONTROL System View]** muestra una representación gráfica de los flujos de activación que ha configurado en Adobe Experience Platform.

![Flujos de datos1](../assets/ui/workspace/system-view-dataflows.png)

Seleccione cualquiera de los destinos mostrados en la página y haga clic en **[!UICONTROL View dataflows]** para ver información sobre todas las conexiones configuradas para cada destino.

![Flujos de datos2](../assets/ui/workspace/system-view-dataflows-2.png)
