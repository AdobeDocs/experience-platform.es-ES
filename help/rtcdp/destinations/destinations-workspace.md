---
keywords: RTCDP;rtcdp
title: Espacio de trabajo Destinos
seo-title: Espacio de trabajo Destinos
description: El espacio de trabajo Destinos consta de cuatro secciones, Catálogo, Examinar, Cuentas y Vista del sistema, que se describen en las secciones siguientes.
seo-description: En la plataforma de datos del cliente en tiempo real de Adobe, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 2%

---


# Espacio de trabajo Destinos {#destinations-workspace}

En la plataforma de datos del cliente en tiempo real de Adobe, seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Destinos] .

El espacio de trabajo [!UICONTROL Destinos] consta de cuatro secciones, [!UICONTROL Catálogo], [!UICONTROL Examinar], [!UICONTROL Cuentas]y Vista [!UICONTROL del sistema], que se describen en las secciones siguientes.

![Destinos-información general](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La ficha **[!UICONTROL Catálogo]** muestra una lista de todos los destinos disponibles en Adobe Real-time CDP, a los que puede enviar datos.

La interfaz de usuario CDP en tiempo real de Adobe proporciona una serie de opciones de búsqueda y filtro en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtre los destinos mediante el control de [!UICONTROL Categorías] .
* Alternar entre [!UICONTROL Todos los destinos] y [!UICONTROL Mis destinos]. Cuando se selecciona **[!UICONTROL Todos los destinos]** , se muestran todos los destinos CDP en tiempo real de Adobe disponibles. Cuando se selecciona **[!UICONTROL Mis destinos]** , solo puede ver los destinos con los que ha establecido una conexión.
* Seleccione para **[!UICONTROL Conexiones]** de vista y/o **[!UICONTROL Extensiones]**. Para comprender la diferencia entre las dos categorías, consulte Tipos [de destino y Categorías](/help/rtcdp/destinations/destination-types.md).

![filtros de destinos y demostración de búsqueda](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

Las tarjetas de destino contienen un control **[!UICONTROL Configurar]** o **[!UICONTROL Activar]** y un control secundario que muestra más opciones. Todos ellos se describen a continuación:

| Control | Descripción |
---------|----------
| [!UICONTROL Configurar] | Permite crear una conexión con el destino. |
| [!UICONTROL Activar] | Una vez que haya establecido una conexión con el destino, puede activar segmentos. |
| [!UICONTROL Cuenta de vista] | Vista las cuentas que ha conectado para un destino. |
| [!UICONTROL Flujos de datos de vista] | Vista los flujos de activación de datos que existen para un destino. |
| [!UICONTROL Documentación de vista] | Abre un vínculo a la página de documentación de ese destino específico, para obtener más información y ayudarle a configurarla. |

![Controles en la tarjeta de destinos](/help/rtcdp/destinations/assets/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril correcto.  Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, así como una descripción del destino y una indicación de la categoría y el tipo de destino.

![Opciones de catálogo de destino](/help/rtcdp/destinations/assets/destination-right-rail.png)

Para obtener más información sobre las categorías de destino e información sobre cada destino, consulte el Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destino y Tipos y Categorías [de](/help/rtcdp/destinations/destination-types.md)destino.

## [!UICONTROL Cuentas] {#accounts}

En la ficha **[!UICONTROL Cuentas]** , puede obtener más información sobre las conexiones que ha establecido con varios destinos. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada destino:

>[!TIP]
>
>Utilice el botón ![](/help/rtcdp/destinations/assets/add-data-symbol.png) Añadir datos de la columna **[!UICONTROL Plataforma]** para crear una nueva conexión de destino para esa cuenta.

![Ficha Cuentas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descripción |
---------|----------
| [!UICONTROL Plataforma] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li></ul> |
| [!UICONTROL Nombre de usuario] | Nombre de usuario seleccionado en el asistente [de](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexión de destino. |
| [!UICONTROL Destinos] | Representa el número de flujos de destino exitosos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Con autorización] | La fecha en que se autorizó la conexión a este destino. |

## [!UICONTROL Examinar] {#browse}

La ficha **[!UICONTROL Examinar]** muestra los destinos con los que ha establecido una conexión. Los destinos con la opción **[!UICONTROL Habilitado]** activada establecen el destino en activo y viceversa. También puede realizar la vista de los destinos en los que fluyen los datos seleccionando **[!UICONTROL Segmentos]** > **[!UICONTROL Examinar]** y un segmento para inspeccionar. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la ficha Examinar:

>[!TIP]
>
>Utilice el botón ![](/help/rtcdp/destinations/assets/add-data-symbol.png) Añadir datos de la columna **[!UICONTROL Nombre]** para activar segmentos adicionales en ese destino.

![Ficha Examinar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descripción |
---------|----------
| Nombre | Nombre proporcionado para el flujo de activación a este destino. |
| [!UICONTROL Destino] | La plataforma de destino seleccionada para el flujo de activación. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li></ul> |
| [!UICONTROL Nombre de usuario] | Las credenciales de cuenta que ha seleccionado para el flujo de destino. |
| [!UICONTROL Segmentos] | Número de segmentos que se están activando en este destino. |
| [!UICONTROL Creado] | Fecha y hora UTC en que se creó el flujo de activación al destino. |
| [!UICONTROL Estado] | `Active` O bien `Inactive`. Indica si los datos se están activando en este destino. Para editar el estado, consulte [Deshabilitar activación](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Haga clic en una fila de destino para ver más información sobre el destino en el carril derecho.

![Haga clic en la fila de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Seleccione el nombre del destino para ver la información sobre los segmentos activados en este destino. Haga clic en **[!UICONTROL Editar activación]** para modificar o agregar los segmentos que se están enviando a este destino.

## [!UICONTROL Vista del sistema] {#system-view}

La ficha Vista **** del sistema muestra una representación gráfica de los flujos de activación que ha configurado en la plataforma de datos del cliente en tiempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Seleccione cualquiera de los destinos que se muestran en la página y pulse los flujos **[!UICONTROL de]** Vista para ver la información sobre todas las conexiones configuradas para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)