---
title: Espacio de trabajo Destinos
seo-title: Espacio de trabajo Destinos
description: En la plataforma de datos del cliente en tiempo real de Adobe, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
seo-description: En la plataforma de datos del cliente en tiempo real de Adobe, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Espacio de trabajo Destinos {#destinations-workspace}

En la plataforma de datos del cliente en tiempo real de Adobe, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al [!UICONTROL Destinations] espacio de trabajo.

El espacio de trabajo [!UICONTROL Destinations] consta de cuatro secciones **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** y **[!UICONTROL System View]**, que se describen en las secciones siguientes.

![Destinos-información general](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

La **[!UICONTROL Catalog]** ficha muestra una lista de todos los destinos ofrecidos por Adobe a los que se pueden enviar datos.

Utilice la funcionalidad de búsqueda de la página para localizar un destino específico o para filtrar destinos mediante el **[!UICONTROL Categories]** control.

Seleccione un destino en el catálogo para abrir el carril derecho. Aquí puede configurar una conexión con el destino (**[!UICONTROL Connect destination]**), vista de conexiones de destino existentes (**[!UICONTROL Browse destinations]**) o obtener información más detallada sobre cada destino consultando la documentación (**[!UICONTROL View documentation]**).

![Opciones de catálogo de destino](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Para obtener más información sobre las categorías de destino e información sobre cada destino, consulte Catálogo [de destino](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL Browse] {#browse}

La **[!UICONTROL Browse]** ficha muestra los destinos con los que ha establecido una conexión. Los destinos con la **[!UICONTROL enabled]** opción activada establecen el destino en activo y viceversa. También puede realizar la vista de los destinos en los que fluyen los datos seleccionando **[!UICONTROL Segments > Browse]** y seleccionando un segmento para inspeccionar. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la ficha Examinar:

![Ficha Examinar](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descripción |
---------|----------
| Nombre | Nombre proporcionado para el flujo de activación a este destino. |
| [!UICONTROL Destination] | La plataforma de destino seleccionada para el flujo de activación. |
| [!UICONTROL Connection Type] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li></ul> |
| [!UICONTROL Username] | Las credenciales de cuenta que ha seleccionado para el flujo de destino. |
| [!UICONTROL Segments] | Número de segmentos que se están activando en este destino. |
| [!UICONTROL Created] | Fecha y hora UTC en que se creó el flujo de activación al destino. |
| [!UICONTROL Status] | `Active` O bien `Inactive`. Indica si los datos se están activando en este destino. Para editar el estado, consulte [Deshabilitar activación](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Haga clic en una fila de destino para ver más información sobre el destino en el carril derecho.

![Haga clic en la fila de destino](/help/rtcdp/destinations/assets/click-destination-row.png)

Seleccione el nombre del destino para ver la información sobre los segmentos activados en este destino. Haga clic en **[!UICONTROL Edit activation]** para modificar o agregar los segmentos que se están enviando a este destino.

## [!UICONTROL Accounts] {#accounts}

En la **[!UICONTROL Accounts]** ficha, puede obtener más información sobre las conexiones establecidas con varios destinos. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada destino:

![Ficha Cuentas](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descripción |
---------|----------
| [!UICONTROL Platform] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Connection Type] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube de Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li></ul> |
| [!UICONTROL Username] | Nombre de usuario seleccionado en el asistente [de](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)conexión de destino. |
| [!UICONTROL Data Flows] | Representa el número de flujos de destino exitosos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Authorized] | La fecha en que se autorizó la conexión a este destino. |
| [!UICONTROL Status] | `Active` O bien `Inactive`. Indica si los datos se están activando en este destino. Para editar el estado, consulte [Deshabilitar activación](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL System View] {#system-view}

La **[!UICONTROL System View]** ficha muestra una representación gráfica de los flujos de activación que ha configurado en la plataforma de datos del cliente en tiempo real.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Seleccione cualquiera de los destinos que se muestran en la página y pulse **[!UICONTROL View flows]** para ver la información sobre todas las conexiones que ha configurado para cada destino.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)