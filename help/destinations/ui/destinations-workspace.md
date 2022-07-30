---
keywords: plataforma;destinos;espacio de trabajo de destinos;espacio de trabajo;iu;iu de destinos;catálogo;catálogo de destinos
title: Espacio de trabajo de destinos
description: El espacio de trabajo Destinos consta de cinco secciones, Información general, Catálogo, Examinar, Cuentas y Vista del sistema. Se describen en las secciones siguientes.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 802a15212f51db2c616860ed0fd2c3f1cf2d3777
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 2%

---

# Espacio de trabajo de destinos {#destinations-workspace}

En Adobe Experience Platform, seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda para acceder a la [!UICONTROL Destinos] espacio de trabajo.

La variable [!UICONTROL Destinos] workspace consta de cinco secciones, [!UICONTROL Información general], [!UICONTROL Catálogo], [!UICONTROL Examinar], [!UICONTROL Cuentas]y [!UICONTROL Vista del sistema], descrito en las secciones siguientes.

![Información general sobre destinos](../assets/ui/workspace/destinations-overview.png)

## Información general de  {#overview}

La variable **[!UICONTROL Información general]** muestra la [!UICONTROL Destinos] tablero, que proporciona métricas clave relacionadas con los datos de destino de su organización. Para obtener más información, visite [[!UICONTROL Destinos] guía del tablero](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si su organización es nueva en Experience Platform y aún no tiene destinos activos, la variable [!UICONTROL Destinos] tablero y [!UICONTROL Información general] no están visibles. En su lugar, seleccione [!UICONTROL Destinos] en la navegación izquierda, se muestra la variable [[!UICONTROL Catálogo] ficha](#catalog).

![La pestaña Información general del panel Destinos .](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La variable **[!UICONTROL Catálogo]** muestra una lista de todos los destinos disponibles en [!DNL Platform], a la que puede enviar datos.

La variable [!DNL Platform] la interfaz de usuario de proporciona varias opciones de búsqueda y filtro en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtre los destinos usando la variable [!UICONTROL Categorías] control.
* Alternar entre [!UICONTROL Todos los destinos] y [!UICONTROL Mis destinos]. Al seleccionar **[!UICONTROL Todos los destinos]**, todo disponible [!DNL Platform] se muestran los destinos de . Al seleccionar **[!UICONTROL Mis destinos]**, solo puede ver los destinos con los que ha establecido una conexión.
* Seleccione para ver **[!UICONTROL Conexiones]** y/o **[!UICONTROL Extensiones]**. Para comprender la diferencia entre las dos categorías, consulte [Tipos y categorías de destino](../destination-types.md).

![Catálogo](../assets/ui/workspace/catalog.png)

Las tarjetas de destino contienen un **[!UICONTROL Configuración]** o **[!UICONTROL Activar segmentos]** y un control secundario que muestra más opciones. Estos controles se describen a continuación:

| Control | Descripción |
|---------|----------|
| [!UICONTROL Configuración] | Permite crear una conexión con el destino. |
| [!UICONTROL Activar segmentos] | Una vez que haya establecido una conexión con el destino, puede activar segmentos. |
| [!UICONTROL Ver cuenta] | Ver las cuentas que se han conectado para un destino. |
| [!UICONTROL Ver flujos de datos] | Ver los flujos de activación de datos que existen para un destino. |
| [!UICONTROL Ver documentación] | Abre un vínculo a la página de documentación para ese destino específico, para obtener más información y para ayudarle a configurarla. |

{style=&quot;table-layout:auto&quot;}

![Controles en la tarjeta de destino](../assets/ui/workspace/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril derecho. Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, incluida una descripción del destino y una indicación de la categoría y el tipo de destino.

![Opciones de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obtener más información sobre las categorías de destino y sobre cada destino, consulte la [Catálogo de destino](../catalog/overview.md) y [Tipos y categorías de destino](../destination-types.md).

## [!UICONTROL Cuentas] {#accounts}

La variable **[!UICONTROL Cuentas]** muestra detalles sobre las conexiones establecidas con varios destinos y permite actualizar o eliminar detalles de cuentas existentes. Consulte la siguiente tabla para obtener toda la información que puede obtener en cada cuenta de destino.

>[!TIP]
>
> * Seleccione los tres puntos del [!UICONTROL Plataforma] y utilice la variable ![Botón Activar segmentos](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activar segmentos ]**para enviar segmentos a ese destino.
> * Seleccione los tres puntos del [!UICONTROL Plataforma] y utilice la variable ![Botón Editar detalles](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Editar detalles ]**botón para [actualizar](update-accounts.md) los detalles de una cuenta de destino existente.
> * Seleccione los tres puntos del [!UICONTROL Plataforma] y utilice la variable ![Botón Eliminar](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Eliminar ]**botón para [delete](delete-destination-account.md) una cuenta de destino existente.


![Ficha Cuentas](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descripción |
|---|---|
| [!UICONTROL Plataforma] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión de la cuenta a su espacio de almacenamiento o destino. Según el destino, las opciones de autenticación son: <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3, FTP o Azure Blob.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li><li>Autenticación OAuth 1 u OAuth 2</li><li>Autenticación de token del portador</li></ul> |
| [!UICONTROL Nombre de usuario] | El nombre de usuario seleccionado en la variable [asistente de conexión de destino](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa el número de flujos de datos de destino correctos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Con autorización] | La fecha en la que se autorizó la conexión a este destino. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Examinar] {#browse}

La variable **[!UICONTROL Examinar]** muestra los destinos con los que ha establecido una conexión. Destinos con la variable **[!UICONTROL Habilitado/Deshabilitado]** active establecer el destino en activo o inactivo, respectivamente. También puede ver los destinos en los que tiene datos fluyendo seleccionando **[!UICONTROL Segmentos]** > **[!UICONTROL Examinar]** y seleccionar un segmento para inspeccionarlo. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la variable [!UICONTROL Examinar] pestaña:

>[!TIP]
>
> * Seleccione los tres puntos del [!UICONTROL Nombre] y utilice la variable ![Botón Activar segmentos](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activar segmentos ]**para enviar segmentos a ese destino.
> * Seleccione los tres puntos del [!UICONTROL Nombre] y utilice la variable ![Botón Eliminar](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Eliminar ]**botón para [remove](delete-destinations.md) una conexión existente a un destino.
> * Seleccione los tres puntos del [!UICONTROL Nombre] y utilice la variable ![Ver en el botón de monitorización](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Ver en monitorización ]**para ver la información de activación de este destino en el [panel de monitorización](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Seleccione los tres puntos del [!UICONTROL Nombre] y utilice la variable ![Suscripción a alertas ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Suscripción a alertas ]**para suscribirse a las alertas de flujo de datos de destino. Puede suscribirse a alertas para recibir mensajes sobre el estado, el éxito o el error de la ejecución del flujo. Consulte [Suscripción a alertas de destino en contexto](alerts.md) para obtener información detallada sobre las alertas de flujo de datos de destino.


![Ficha Examinar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descripción |
|---------|----------|
| Nombre | Nombre que ha proporcionado para el flujo de activación a este destino. La misma columna incluye dos controles: [!UICONTROL Activar ] y [!UICONTROL Eliminar destino]. |
| [!UICONTROL Estado de ejecución del último flujo] | Estado de la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Fecha de ejecución del último flujo] | Hora y fecha en que se produjo la última ejecución del flujo de datos. Consulte [Ver detalles de destino](destination-details-page.md) para obtener más información sobre las ejecuciones de flujo de datos. |
| [!UICONTROL Destino] | La plataforma de destino que seleccionó para el flujo de activación. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con su espacio de almacenamiento o destino. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3, FTP o [!DNL Azure Blob].</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor.</li><li>Para destinos de flujo continuo: Puede [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nombre de usuario] | Credenciales de cuenta que ha seleccionado para el flujo de destino. |
| [!UICONTROL Datos de activación] | Indica el número de segmentos que se están activando en este destino. Seleccione este control para obtener más información sobre los segmentos activados. Consulte [Datos de activación](/help/destinations/ui/destination-details-page.md#activation-data) en la página de detalles de destino para obtener más información sobre los segmentos activados. |
| [!UICONTROL Creado] | La fecha y la hora UTC en que se creó el flujo de activación al destino. Seleccione el símbolo de flecha hacia arriba o hacia abajo para ordenar los flujos de activación por primero más reciente o más antiguo. |
| [!UICONTROL Estado] | `Enabled` o `Disabled`. Indica si se están activando datos en este destino. |

Haga clic en una fila de destino para que aparezca más información sobre el destino en el carril derecho.

![Haga clic en la fila de destino](../assets/ui/workspace/click-destination-row.png)

Seleccione el nombre del destino para ver información sobre los segmentos activados en este destino. Haga clic en **[!UICONTROL Editar activación]** para modificar o añadir a los segmentos que se envían a este destino.

## [!UICONTROL Vista del sistema] {#system-view}

La variable **[!UICONTROL Vista del sistema]** muestra una representación gráfica de los flujos de activación que ha configurado en Adobe Experience Platform.

![Flujos de datos1](../assets/ui/workspace/data-flows1.png)

Seleccione cualquiera de los destinos mostrados en la página y haga clic en **[!UICONTROL Ver flujos de datos]** para ver información sobre todas las conexiones configuradas para cada destino.

![Flujos de datos2](../assets/ui/workspace/data-flows2.png)
