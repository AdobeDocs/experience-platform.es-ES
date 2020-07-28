---
title: Espacio de trabajo Destinos
seo-title: Espacio de trabajo Destinos
description: En Adobe Real-time Customer Data Platform, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
seo-description: En Adobe Real-time Customer Data Platform, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 3%

---


# Espacio de trabajo Destinos {#destinations-workspace}

En Adobe Real-time Customer Data Platform, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Destinations] .

El espacio de trabajo [!UICONTROL Destinos] consta de cuatro secciones, **[!UICONTROL Catálogo]**, **[!UICONTROL Examinar]**, **[!UICONTROL Cuentas]** y Vista **[!UICONTROL del sistema]**, que se describen en las secciones siguientes.

![Destinos-información general](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La ficha **[!UICONTROL Catálogo]** muestra una lista de todos los destinos ofrecidos por Adobe a los que se pueden enviar datos.

Utilice la funcionalidad de búsqueda de la página para localizar un destino específico o destinos de filtro mediante el control de **[!UICONTROL Categorías]** .

Seleccione un destino en el catálogo para abrir el carril derecho. Aquí puede configurar una conexión con el destino (destino **[!UICONTROL de]** Connect), vista de las conexiones de destino existentes (destinos **[!UICONTROL de]** exploración) o obtener información más detallada sobre cada destino consultando la documentación (documentación **[!UICONTROL de]** Vista).

![Opciones de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obtener más información sobre las categorías de destino e información sobre cada destino, consulte Catálogo [de destino](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL Examinar] {#browse}

La ficha **[!UICONTROL Examinar]** muestra los destinos con los que ha establecido una conexión. Los destinos con la opción **[!UICONTROL habilitada]** activada establecen el destino en activo y viceversa. También puede realizar la vista de los destinos en los que tiene flujos de datos seleccionando **[!UICONTROL Segmentos > Examinar]** y seleccionando un segmento para inspeccionar. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la ficha Examinar:

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

## [!UICONTROL Cuentas] {#accounts}

En la ficha **[!UICONTROL Cuentas]** , puede obtener más información sobre las conexiones que ha establecido con varios destinos. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada destino:

![Ficha Cuentas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descripción |
---------|----------
| [!UICONTROL Plataforma] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li></ul> |
| [!UICONTROL Nombre de usuario] | Nombre de usuario seleccionado en el asistente [de](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexión de destino. |
| [!UICONTROL Flujos de datos] | Representa el número de flujos de destino exitosos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Con autorización] | La fecha en que se autorizó la conexión a este destino. |
| [!UICONTROL Estado] | `Active` O bien `Inactive`. Indica si los datos se están activando en este destino. Para editar el estado, consulte [Deshabilitar activación](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL Vista del sistema] {#system-view}

La ficha Vista **** del sistema muestra una representación gráfica de los flujos de activación que ha configurado en el Platform de datos del cliente en tiempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Seleccione cualquiera de los destinos que se muestran en la página y pulse los flujos **[!UICONTROL de]** Vista para ver la información sobre todas las conexiones configuradas para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)