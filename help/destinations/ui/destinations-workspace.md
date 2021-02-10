---
keywords: plataforma;destinos;área de trabajo de destinos;espacio de trabajo;ui;destinos ui;catálogo;destinos de catálogo;
title: Descripción general del espacio de trabajo Destinations
description: El espacio de trabajo Destinos consta de cuatro secciones, Catálogo, Examinar, Cuentas y Vista del sistema, que se describen en las secciones siguientes.
seo-description: En Adobe Experience Platform, seleccione Destinos en la barra de navegación izquierda para acceder al espacio de trabajo de destinos.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---


# Visión general del espacio de trabajo Destinations {#destinations-workspace}

En Adobe Experience Platform, seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Destinations].

El espacio de trabajo [!UICONTROL Destinations] consta de cuatro secciones, [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] y [!UICONTROL System Vista], que se describen en las secciones siguientes.

![Destinos-información general](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catálogo] {#catalog}

La ficha **[!UICONTROL Catalog]** muestra una lista de todos los destinos disponibles en Platform a los que puede enviar datos.

La interfaz de usuario de la plataforma proporciona una serie de opciones de búsqueda y filtro en la página del catálogo de destinos:

* Utilice la funcionalidad de búsqueda de la página para localizar un destino específico.
* Filtre los destinos mediante el control [!UICONTROL Categorías].
* Alternar entre [!UICONTROL Todos los destinos] y [!UICONTROL Mis destinos]. Cuando se selecciona **[!UICONTROL Todos los destinos]**, se muestran todos los destinos de plataforma disponibles. Cuando **[!UICONTROL Mis destinos]** está seleccionado, solo puede ver los destinos con los que ha establecido una conexión.
* Seleccione la vista **[!UICONTROL Conexiones]** y/o **[!UICONTROL Extensiones]**. Para comprender la diferencia entre las dos categorías, consulte [Tipos de destino y Categorías](../destination-types.md).

![filtros de destinos y demostración de búsqueda](../assets/ui/workspace/destinations-search-and-filter.gif)

Las tarjetas de destino contienen un control **[!UICONTROL Configurar]** o **[!UICONTROL Activar]** y un control secundario que muestra más opciones. Todos ellos se describen a continuación:

| Control | Descripción |
---------|----------
| [!UICONTROL Configurar] | Permite crear una conexión con el destino. |
| [!UICONTROL Activar] | Una vez que haya establecido una conexión con el destino, puede activar segmentos. |
| [!UICONTROL Cuenta de vista] | Vista las cuentas que ha conectado para un destino. |
| [!UICONTROL Flujos de datos de vista] | Vista los flujos de activación de datos que existen para un destino. |
| [!UICONTROL Documentación de vista] | Abre un vínculo a la página de documentación de ese destino específico, para obtener más información y ayudarle a configurarla. |

![Controles en la tarjeta de destinos](../assets/ui/workspace/destination-card-options.png)

Seleccione una tarjeta de destino en el catálogo para abrir el carril correcto.  Aquí puede ver una descripción del destino. El carril derecho proporciona los mismos controles descritos en la tabla anterior, así como una descripción del destino y una indicación de la categoría y el tipo de destino.

![Opciones de catálogo de destino](../assets/ui/workspace/destination-right-rail.png)

Para obtener más información sobre categorías de destino e información sobre cada destino, consulte el [Catálogo de destino](../catalog/overview.md) y [Tipos y Categorías de destino](../destination-types.md).

## [!UICONTROL Cuentas] {#accounts}

En la ficha **[!UICONTROL Cuentas]** puede obtener más información sobre las conexiones que ha establecido con varios destinos. Consulte la tabla siguiente para obtener toda la información que puede obtener sobre cada destino:

>[!TIP]
>
>Utilice el botón ![Añadir datos](../assets/ui/workspace/add-data-symbol.png) de la columna **[!UICONTROL Plataforma]** para crear una nueva conexión de destino para esa cuenta.

![Ficha Cuentas](../assets/ui/workspace/edit-account-destinations.png)

| Elemento | Descripción |
---------|----------
| [!UICONTROL Plataforma] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li></ul> |
| [!UICONTROL Nombre de usuario] | El nombre de usuario seleccionado en el [asistente de destino de conexión](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinos] | Representa el número de flujos de destino exitosos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Con autorización] | La fecha en que se autorizó la conexión a este destino. |

Además, puede editar o actualizar la información de su cuenta. Seleccione el ![botón Editar cuenta](../assets/ui/workspace/pencil-icon.png) en la columna **[!UICONTROL Plataforma]** para editar la información de la cuenta.

Para las cuentas que utilizan un tipo de conexión `OAuth2`, puede seleccionar **[!UICONTROL Volver a conectar OAuth]** para renovar sus credenciales de cuenta.

![Imagen de Oauth](../assets/ui/workspace/reconnect-oauth.png)

Para las cuentas que utilizan un tipo de conexión `Access Key` o `ConnectionString`, puede editar la información de autenticación de la cuenta, incluida información como ID de acceso, claves secretas o cadenas de conexión.

![Imagen de información de la cuenta](../assets/ui/workspace/edit-account-details.png)

Una vez que haya terminado de editar los detalles de la cuenta, seleccione **[!UICONTROL Guardar]** para completar la actualización.

## [!UICONTROL Examinar] {#browse}

La ficha **[!UICONTROL Examinar]** muestra los destinos con los que ha establecido una conexión. Los destinos con la opción **[!UICONTROL Habilitado]** activada establecen el destino en activo y viceversa. También puede realizar la vista de los destinos en los que tiene flujos de datos seleccionando **[!UICONTROL Segmentos]** > **[!UICONTROL Examinar]** y seleccionando un segmento para inspeccionar. Consulte la tabla siguiente para obtener toda la información proporcionada para cada destino en la ficha Examinar:

>[!TIP]
>
>Utilice el botón ![Añadir datos](../assets/ui/workspace/add-data-symbol.png) de la columna **[!UICONTROL Nombre]** para activar segmentos adicionales en ese destino.

![Ficha Examinar](../assets/ui/workspace/browse-tab.png)

| Elemento | Descripción |
---------|----------
| Nombre | Nombre proporcionado para el flujo de activación a este destino. |
| [!UICONTROL Destino] | La plataforma de destino seleccionada para el flujo de activación. |
| [!UICONTROL Tipo de conexión] | Representa el tipo de conexión con el contenedor o destino de almacenamiento. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li></ul> |
| [!UICONTROL Nombre de usuario] | Las credenciales de cuenta que ha seleccionado para el flujo de destino. |
| [!UICONTROL Segmentos] | Número de segmentos que se están activando en este destino. |
| [!UICONTROL Creado] | Fecha y hora UTC en que se creó el flujo de activación al destino. |
| [!UICONTROL Estado] | `Active` O bien `Inactive`. Indica si los datos se están activando en este destino. Para editar el estado, consulte [Deshabilitar activación](./activate-destinations.md#disable-activation). |

Haga clic en una fila de destino para ver más información sobre el destino en el carril derecho.

![Haga clic en la fila de destino](../assets/ui/workspace/click-destination-row.png)

Seleccione el nombre del destino para ver la información sobre los segmentos activados en este destino. Haga clic en **[!UICONTROL Editar activación]** para modificar o agregar los segmentos que se están enviando a este destino.

## [!UICONTROL Vista del sistema] {#system-view}

La ficha **[!UICONTROL Vista del sistema]** muestra una representación gráfica de los flujos de activación que ha configurado en el Adobe Experience Platform.

![Flujos de datos1](../assets/ui/workspace/data-flows1.png)

Seleccione cualquiera de los destinos que se muestran en la página y presione **[!UICONTROL Flujos de Vista]** para ver información sobre todas las conexiones que ha configurado para cada destino.

![Flujos de datos2](../assets/ui/workspace/data-flows2.png)