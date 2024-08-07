---
title: Filtrado De Objetos De Origen En La IU
description: Obtenga información sobre cómo navegar por los objetos de origen, como cuentas y flujos de datos, en la interfaz de usuario de Experience Platform.
hide: true
hidefromtoc: true
exl-id: 59c200cc-1be7-45a8-9d7a-55e6f11dbcf2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# Filtrado de objetos de origen en la IU

Utilice las herramientas de filtrado, búsqueda y acciones en línea de la interfaz de usuario de Adobe Experience Platform para optimizar el flujo de trabajo en el espacio de trabajo de [!UICONTROL Sources]

* Utilice las capacidades de filtrado y búsqueda para navegar por las cuentas de origen y los flujos de datos de su organización.
* Utilice acciones en línea para modificar los ajustes de configuración aplicados a los flujos de datos y mejorar los flujos de trabajo de la organización. Puede utilizar acciones en línea para aplicar etiquetas, configurar alertas o crear trabajos de ingesta bajo demanda.

## Introducción 

Antes de trabajar con las herramientas de navegación de objetos en el espacio de trabajo de orígenes, resulta útil conocer las siguientes funciones y conceptos de Experience Platform:

* [Fuentes](../../home.md): Use fuentes en Experience Platform para introducir datos de una aplicación de Adobe o de una fuente de datos de terceros.
* [Etiquetas administrativas](../../../administrative-tags/overview.md): Use etiquetas administrativas para aplicar palabras clave de metadatos a los objetos y permitir la búsqueda para encontrar ese objeto dentro del ecosistema de Experience Platform.
* [Alertas](../../../observability/home.md): Use alertas para recibir notificaciones que proporcionen una actualización del estado de objetos como los flujos de datos de origen.
* [Flujos de datos](../../../dataflows/home.md): los flujos de datos son representaciones de trabajos de datos que mueven datos a través del Experience Platform. Puede utilizar el espacio de trabajo de fuentes para crear flujos de datos que introduzcan datos de una fuente determinada en el Experience Platform.
* [Conjuntos de datos](../../../catalog/datasets/user-guide.md): un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas).
* [Zonas protegidas](../../../sandboxes/home.md): utilice las zonas protegidas en Experience Platform para crear particiones virtuales entre las instancias de Experience Platform y crear entornos dedicados al desarrollo o la producción.

## Filtrar orígenes y flujos de datos {#filter-sources-dataflows}

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior.

![La página de flujos de datos en el área de trabajo de orígenes](../../images/tutorials/filter/dataflows-page.png)

De forma predeterminada, el menú de filtro se muestra a la izquierda de la interfaz. Para ocultar el menú, seleccione **[!UICONTROL Ocultar filtros]**.

![Se seleccionó la opción de ocultar filtro.](../../images/tutorials/filter/hide-filters.png)

Puede filtrar los flujos de datos de origen mediante los siguientes parámetros:

| Filtro | Descripción |
| --- | --- |
| [Plataforma Source](#filter-dataflows-by-source-platform) | Filtre los flujos de datos en función de la fuente con la que se crearon. |
| [Etiquetas](#filter-dataflows-by-tags) | Filtre los flujos de datos en función de las etiquetas aplicadas a ellos. |
| [Estado](#filter-dataflows-by-status) | Filtre los flujos de datos según su estado actual. |
| [Conjunto de datos de destino](#filter-dataflows-by-target-dataset) | Filtre los flujos de datos en función del conjunto de datos de destinatario con el que se crearon. |
| [Nombre de cuenta](#filter-dataflows-by-account-name) | Filtre los flujos de datos en función del nombre de la cuenta con la que se corresponden. |
| [Creado por](#filter-dataflows-by-user) | Filtre los flujos de datos en función de quién los creó. |
| [Fecha de creación](#filter-dataflows-by-creation-date) | Filtre los flujos de datos en función de la fecha de creación. |
| [Fecha de modificación](#filter-dataflows-by-modification-date) | Filtre los flujos de datos en función de la fecha en la que se actualizaron por última vez. |

### Filtrado de flujos de datos por plataforma de origen {#filter-dataflows-by-source-platform}

Utilice el panel [!UICONTROL Plataforma Source] para filtrar los flujos de datos por tipo de origen. Puede escribir un origen determinado o utilizar el menú desplegable para ver una lista de orígenes en el catálogo. También puede filtrar por varios orígenes diferentes para una consulta determinada. Por ejemplo, puede seleccionar [!DNL Amazon S3], [!DNL Azure Data Lake Storage Gen2] y [!DNL Google Cloud Storage] para actualizar el catálogo y mostrar solo los flujos de datos creados con los orígenes seleccionados.

### Filtrado de flujos de datos por etiquetas {#filter-dataflows-by-tags}

Utilice el panel Etiquetas para filtrar los flujos de datos por sus respectivas etiquetas.

Seleccione **[!UICONTROL Tiene cualquier etiqueta]** y, a continuación, seleccione las etiquetas que desee filtrar mediante el menú desplegable. Utilice esta configuración para filtrar flujos de datos que tengan cualquiera de las etiquetas seleccionadas.

![Consulta para filtrar flujos de datos por cualquier etiqueta.](../../images/tutorials/filter/has-any-tag.png)

Seleccione **[!UICONTROL Tiene todas las etiquetas]** y, a continuación, seleccione las etiquetas que desee filtrar mediante el menú desplegable. Utilice esta configuración para filtrar flujos de datos que tengan todas las etiquetas seleccionadas.

![Consulta para filtrar flujos de datos por todas las etiquetas.](../../images/tutorials/filter/has-all-tags.png)

### Filtrado de flujos de datos por estado {#filter-dataflows-by-status}

Puede filtrar por estado usando el panel [!UICONTROL Estado].

| Estado | Descripción |
| --- | --- |
| Habilitado | Seleccione **[!UICONTROL Habilitado]** para filtrar la vista y mostrar solo los flujos de datos activos. |
| Desactivado | Seleccione **[!UICONTROL Deshabilitado]** para filtrar la vista y mostrar solo los flujos de datos desactivados. |
| Borrador | Seleccione **[!UICONTROL Borrador]** para filtrar la vista y mostrar solo los flujos de datos que están en modo de borrador. |

### Filtrado de flujos de datos por conjunto de datos de destino {#filter-dataflows-by-target-dataset}

Seleccione **[!UICONTROL Conjunto de datos de destino]** para acceder al menú desplegable de todos los conjuntos de datos de destino. A continuación, seleccione un conjunto de datos de destino para filtrar la vista y mostrar solo los flujos de datos creados con los conjuntos de datos de destino especificados.

### Filtrar flujos de datos por nombre de cuenta {#filter-dataflows-by-account-name}

Seleccione **[!UICONTROL Nombre de cuenta]** para acceder al menú desplegable de todas las cuentas. A continuación, seleccione una cuenta para filtrar la vista y mostrar los flujos de datos creados por la cuenta seleccionada.

### Filtrado de flujos de datos por usuario {#filter-dataflows-by-user}

Utilice el panel [!UICONTROL Creado por] para filtrar los flujos de datos por el usuario que los creó o actualizó por última vez. Seleccione el menú desplegable y, a continuación, el nombre de usuario por el que filtrar los flujos de datos.

### Filtrado de flujos de datos por fecha de creación {#filter-dataflows-by-creation-date}

Puede filtrar los flujos de datos por sus fechas de creación. En el panel [!UICONTROL Fecha de creación], configure una fecha de inicio y una fecha de finalización para crear una ventana de lapso de tiempo y filtre la vista para mostrar solo los flujos de datos creados dentro de esa ventana.

Puede configurar el lapso de tiempo introduciendo la fecha de inicio y la de finalización. También puede seleccionar el icono de calendario y utilizar el calendario para configurar las fechas.

También puede seguir los mismos pasos, pero filtrar los flujos de datos por su fecha de última modificación, a diferencia de su fecha de creación.

### Filtrado de flujos de datos por fecha de modificación {#filter-dataflows-by-modification-date}

Del mismo modo, puede aplicar los mismos principios y filtrar el flujo de datos por sus fechas de modificación. Use **[!UICONTROL Fecha de modificación]** para configurar un intervalo de tiempo determinado y filtrar la vista para mostrar solo los flujos de datos que se han modificado durante ese período.

### Combinación de filtros {#combine-filters}

Puede combinar distintos filtros para ampliar o reducir la búsqueda. En el ejemplo siguiente, se aplica un filtro para buscar:

* Flujos de datos creados con el origen [!DNL Amazon S3].
* Flujos de datos que contienen la etiqueta **[!DNL ACME]**.
* Flujos de datos habilitados actualmente.
* Flujos de datos creados con el conjunto de datos [!DNL Loyalty Dataset B2C].
* Flujos de datos creados entre el 1/4/2024 y el 19/4/2024.

![Ventana desplegable que muestra todos los filtros aplicados.](../../images/tutorials/filter/combine-filters.png)

Para quitar todos los filtros, seleccione **[!UICONTROL Borrar todo]**.

![Opción seleccionada para borrar todo.](../../images/tutorials/filter/clear-all.png)

## Filtrar cuentas de origen {#filter-sources-accounts}

En la interfaz de usuario del Experience Platform, seleccione [!UICONTROL Orígenes] en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Cuentas]** en el encabezado superior. Puede filtrar las cuentas de origen en función del origen con el que se crearon o del usuario que las creó.

![La página de cuentas en el área de trabajo de orígenes](../../images/tutorials/filter/accounts.png)

## Buscar cuentas y flujos de datos {#search-for-accounts-and-dataflows}

Puede acelerar la eficacia utilizando la barra de búsqueda para navegar inmediatamente a una cuenta o flujo de datos determinado.

>[!BEGINTABS]

>[!TAB Buscar flujos de datos]

Utilice la barra de búsqueda de la página [!UICONTROL Flujos de datos] para encontrar un flujo de datos específico. Puede buscar un flujo de datos utilizando su nombre o descripción.

![Una consulta de búsqueda para un flujo de datos ACME](../../images/tutorials/filter/search-dataflow.png)

>[!TAB Buscar cuentas]

Utilice la barra de búsqueda de la página [!UICONTROL Cuentas] para encontrar una cuenta específica. Puede buscar una cuenta utilizando su nombre o descripción.

![Consulta de búsqueda para una cuenta de abril](../../images/tutorials/filter/search-account.png)

>[!ENDTABS]

## Acciones en línea para flujos de datos de origen {#inline-actions-for-sources-dataflows}

Seleccione los puntos suspensivos (`...`) junto al nombre de un flujo de datos para obtener una lista de acciones en línea que puede utilizar para realizar modificaciones en el flujo de datos.

![Selección de acciones en línea entre las que puede elegir para un flujo de datos determinado.](../../images/tutorials/filter/inline-actions.png)

| Acciones en línea | Descripción |
| --- | --- |
| [!UICONTROL Editar programación] | Seleccione **[!UICONTROL Editar programación]** para actualizar la programación de ingesta del flujo de datos. Un flujo de datos que se ha establecido en ingesta única no se puede editar. |
| [!UICONTROL Deshabilitar flujo de datos] | Seleccione **[!UICONTROL Deshabilitar flujo de datos]** para desactivar la ejecución de un flujo de datos. Esta opción no elimina el flujo de datos. |
| [!UICONTROL Ver en supervisión] | Seleccione **[!UICONTROL Ver en supervisión]** para ver las métricas y el estado del flujo de datos en el panel de supervisión. Para obtener más información, lea la guía sobre [fuentes de supervisión y flujos de datos](../../../dataflows/ui/monitor-sources.md). |
| [!UICONTROL Eliminar] | Seleccione **[!UICONTROL Delete]** para eliminar el flujo de datos. |
| [!UICONTROL Ejecutar bajo demanda] | Seleccione **[!UICONTROL Ejecutar bajo demanda]** para almacenar en déclencheur una sola iteración de una ejecución de flujo de datos. Para obtener más información, lea la guía sobre [creación de una ejecución de flujo de datos bajo demanda](../ui/on-demand-ingestion.md). |
| [!UICONTROL Suscribirse a alertas] | Seleccione **[!UICONTROL Suscribirse a alertas]** para ver una ventana emergente de alertas a las que puede suscribirse: <ul><li>Inicio de la ejecución del flujo de datos de origen: seleccione esta alerta para recibir una notificación cuando comience la ejecución del flujo de datos bajo demanda.</li><li>Ejecución correcta del flujo de datos de origen: seleccione esta alerta para recibir una notificación cuando la ejecución del flujo de datos bajo demanda finalice correctamente.</li><li>Error al ejecutar el flujo de datos de origen: seleccione esta alerta cuando la ejecución del flujo de datos bajo demanda falle debido a errores.</li></ul> Para obtener más información, lea la guía sobre [suscripción a alertas para flujos de datos de origen](../ui/alerts.md). |
| [!UICONTROL Agregar al paquete] | Seleccione **[!UICONTROL Agregar al paquete]** para agregar el flujo de datos a un paquete y exportarlo para utilizarlo en una zona protegida diferente. Durante este paso, puede crear un nuevo paquete o agregar el flujo de datos a un paquete existente. Para obtener más información, lea la guía sobre [herramientas de espacio aislado](../../../sandboxes/ui/sandbox-tooling.md). |
| [!UICONTROL Administrar etiquetas] | Seleccione **[!UICONTROL Administrar etiquetas]** para agregar o quitar etiquetas de su flujo de datos. Utilice etiquetas para administrar taxonomías de metadatos y clasificar objetos empresariales para facilitar la detección y la categorización. Para obtener más información, lea la guía sobre [administración de etiquetas](../../../administrative-tags/ui/managing-tags.md). |

## Pasos siguientes

Al leer este documento, ha aprendido a navegar por las páginas de cuentas de origen y flujos de datos. Para obtener más información sobre las fuentes, lea [descripción general de las fuentes](../../home.md).
