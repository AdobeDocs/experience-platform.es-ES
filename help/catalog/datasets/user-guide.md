---
keywords: Experience Platform;inicio;temas populares;habilitar conjunto de datos;Conjunto de datos;conjunto de datos
solution: Experience Platform
title: Guía de IU de conjuntos de datos
description: Obtenga información sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: aee82356f1f519398f381e161be14789532561f1
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 3%

---

# Guía de IU de conjuntos de datos

Esta guía del usuario proporciona instrucciones sobre cómo realizar acciones comunes al trabajar con conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## Introducción

Esta guía del usuario requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Conjuntos de datos](overview.md): la construcción de almacenamiento y administración para la persistencia de datos en [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Aprenda a crear sus propios esquemas XDM personalizados con el [!DNL Schema Editor] dentro de [!DNL Platform] interfaz de usuario.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garantice el cumplimiento de las regulaciones, restricciones y políticas relativas al uso de los datos del cliente.

## Ver conjuntos de datos {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos en la actividad del conjunto de datos"
>abstract="Los números negativos de los registros ingeridos implican que un usuario ha eliminado determinados lotes en un intervalo de tiempo seleccionado."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Caducidad del conjunto de datos"
>abstract="Esta columna indica el número de días que le quedan al conjunto de datos de destinatario antes de que caduque automáticamente."

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para abrir **[!UICONTROL Conjuntos de datos]** panel. El panel enumera todos los conjuntos de datos disponibles para su organización. Se muestran los detalles de cada conjunto de datos enumerado, incluido su nombre, el esquema al que se adhiere el conjunto de datos y el estado de la ejecución de ingesta más reciente.

![La interfaz de usuario de Platform con el elemento Conjuntos de datos resaltado en la barra de navegación izquierda.](../images/datasets/user-guide/browse-datasets.png)

Seleccione el nombre de un conjunto de datos en la [!UICONTROL Examinar] para acceder a su **[!UICONTROL Actividad de conjunto de datos]** y ver los detalles del conjunto de datos seleccionado. La pestaña actividad incluye un gráfico que visualiza la tasa de consumo de los mensajes, así como una lista de lotes correctos y fallidos.

![Se resaltan las métricas y visualizaciones del conjunto de datos seleccionado.](../images/datasets/user-guide/dataset-activity-1.png)
![Se resaltan los lotes de muestra relacionados con el conjunto de datos seleccionado.](../images/datasets/user-guide/dataset-activity-2.png)

## Más acciones {#more-actions}

Puede [!UICONTROL Eliminar] o [!UICONTROL Habilitar un conjunto de datos para el perfil] desde el [!UICONTROL Conjunto de datos] vista de detalles. Para ver las acciones disponibles, seleccione **[!UICONTROL ... Más]** en la parte superior derecha de la interfaz de usuario. Aparecerá el menú desplegable.

![El espacio de trabajo Conjuntos de datos con [!UICONTROL ... Más] menú desplegable resaltado.](../images/datasets/user-guide/more-actions.png)

Si selecciona **[!UICONTROL Habilitar un conjunto de datos para el perfil]**, aparece un cuadro de diálogo de confirmación. Seleccionar **[!UICONTROL Activar]** para confirmar su elección.

>[!NOTE]
>
>Para habilitar un conjunto de datos para el perfil, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en el perfil del cliente en tiempo real. Consulte la [Habilitar un conjunto de datos para el perfil](#enable-profile) para obtener más información.

![Cuadro de diálogo de confirmación Habilitar conjunto de datos.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Si selecciona **[!UICONTROL Eliminar]**, el [!UICONTROL Eliminar conjunto de datos] Aparecerá el cuadro de diálogo de confirmación. Seleccionar **[!UICONTROL Eliminar]** para confirmar su elección.

>[!NOTE]
>
>No puede eliminar conjuntos de datos del sistema.

También puede eliminar un conjunto de datos o agregar uno para utilizarlo con el perfil del cliente en tiempo real desde las acciones en línea que se encuentran en [!UICONTROL Examinar] pestaña. Consulte la [sección de acciones en línea](#inline-actions) para obtener más información.

![Cuadro de diálogo de confirmación Eliminar conjunto de datos.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Acciones de conjuntos de datos en línea {#inline-actions}

La IU de conjuntos de datos ahora ofrece colecciones de acciones en línea para cada conjunto de datos disponible. Seleccione los puntos suspensivos (...) de un conjunto de datos que desee administrar para ver las opciones disponibles en un menú emergente. Las acciones disponibles incluyen: [[!UICONTROL Previsualizar conjunto de datos]](#preview), [[!UICONTROL Administración de datos y etiquetas de acceso]](#manage-and-enforce-data-governance), [[!UICONTROL Habilitar perfil unificado]](#enable-profile), [[!UICONTROL Administración de etiquetas]](#add-tags), [[!UICONTROL Mover a carpetas]](#move-to-folders), y [[!UICONTROL Eliminar]](#delete). Puede encontrar más información sobre estas acciones disponibles en sus secciones respectivas.

### Añadir etiquetas de conjuntos de datos {#add-tags}

Añada etiquetas personalizadas creadas para organizar conjuntos de datos y mejorar las capacidades de búsqueda, filtrado y ordenación. Desde el [!UICONTROL Examinar] de la pestaña [!UICONTROL Conjuntos de datos] espacio de trabajo, seleccione los puntos suspensivos de un conjunto de datos que desee administrar seguido de **[!UICONTROL Administración de etiquetas]** en el menú desplegable.

![La pestaña Examinar del espacio de trabajo Conjuntos de datos con la opción de puntos suspensivos y Administrar etiquetas resaltada para el conjunto de datos elegido.](../images/datasets/user-guide/manage-tags.png)

El [!UICONTROL Administración de etiquetas] aparece el cuadro de diálogo. Escriba una breve descripción para crear una etiqueta personalizada o elija una etiqueta preexistente para etiquetar el conjunto de datos. Seleccionar **[!UICONTROL Guardar]** para confirmar la configuración.

![Cuadro de diálogo Administrar etiquetas con etiquetas personalizadas resaltadas.](../images/datasets/user-guide/manage-tags-dialog.png)

El [!UICONTROL Administración de etiquetas] El cuadro de diálogo también puede eliminar las etiquetas existentes de un conjunto de datos. Simplemente, seleccione la &quot;x&quot; junto a la etiqueta que desee eliminar y seleccione **[!UICONTROL Guardar]**.

Una vez que se ha añadido una etiqueta a un conjunto de datos, los conjuntos de datos se pueden filtrar según la etiqueta correspondiente. Consulte la sección sobre cómo [filtrar conjuntos de datos por etiquetas](#enable-profile) para obtener más información.

Para obtener más información sobre cómo clasificar objetos empresariales para facilitar su detección y categorización, consulte la guía sobre [administración de taxonomías de metadatos](../../administrative-tags/ui/managing-tags.md). Esta guía detalla cómo un usuario con los permisos adecuados puede crear etiquetas predefinidas, asignar categorías a las etiquetas y realizar todas las operaciones de CRUD relacionadas en etiquetas y categorías de etiquetas en la IU de Platform.

## Buscar y filtrar conjuntos de datos {#search-and-filter}

Para buscar o filtrar la lista de conjuntos de datos disponibles, seleccione el icono de filtro (![El icono de filtro.](../images/datasets/user-guide/icon.png)), en la parte superior izquierda del espacio de trabajo. Aparecerá un conjunto de opciones de filtro en el carril izquierdo. Existen varios métodos para filtrar los conjuntos de datos disponibles. Estos incluyen: [[!UICONTROL Mostrar conjuntos de datos del sistema]](#show-system-datasets), [[!UICONTROL Incluido en el perfil]](#filter-profile-enabled-datasets), [[!UICONTROL Etiquetas]](#filter-by-tag), [[!UICONTROL Fecha de creación]](#filter-by-creation-date), [[!UICONTROL Fecha de modificación], [!UICONTROL Creado por]](#filter-by-creation-date), y [[!UICONTROL Esquema]](#filter-by-schema).

La lista de filtros aplicados se muestra encima de los resultados filtrados.

![La pestaña Examinar del espacio de trabajo Conjuntos de datos con la lista de filtros aplicados resaltada.](../images/datasets/user-guide/applied-filters.png)

### Mostrar conjuntos de datos del sistema {#show-system-datasets}

De forma predeterminada, solo se muestran los conjuntos de datos en los que ha introducido datos. Si desea ver los conjuntos de datos generados por el sistema, seleccione la **[!UICONTROL Sí]** casilla de verificación en la [!UICONTROL Mostrar conjuntos de datos del sistema] sección. Los conjuntos de datos generados por el sistema solo se utilizan para procesar otros componentes. Por ejemplo, el conjunto de datos de exportación de perfiles generado por el sistema se utiliza para procesar el panel de perfiles.

![Las opciones de filtro del espacio de trabajo Conjuntos de datos con [!UICONTROL Mostrar conjuntos de datos del sistema] sección resaltada.](../images/datasets/user-guide/show-system-datasets.png)

### Filtrar conjuntos de datos habilitados para perfil {#filter-profile-enabled-datasets}

Los conjuntos de datos que se han habilitado para los datos de perfil se utilizan para rellenar perfiles de clientes después de introducir los datos. Consulte la sección sobre [habilitar conjuntos de datos para el perfil](#enable-profile) para obtener más información.

Para filtrar el conjunto de datos en función de si se han habilitado para el perfil, seleccione la variable [!UICONTROL Sí] de las opciones de filtro.

![Las opciones de filtro del espacio de trabajo Conjuntos de datos con [!UICONTROL Incluido en el perfil] sección resaltada.](../images/datasets/user-guide/included-in-profile.png)

### Filtrar conjuntos de datos por etiqueta {#filter-by-tag}

Introduzca el nombre de la etiqueta personalizada en [!UICONTROL Etiquetas] introduzca y, a continuación, seleccione la etiqueta de la lista de opciones disponibles para buscar y filtrar conjuntos de datos que correspondan a esa etiqueta.

![Las opciones de filtro del espacio de trabajo Conjuntos de datos con [!UICONTROL Etiquetas] icono de entrada y filtro resaltado.](../images/datasets/user-guide/filter-tags.png)

### Filtrar conjuntos de datos por fecha de creación {#filter-by-creation-date}

Los conjuntos de datos se pueden filtrar por fecha de creación durante un período de tiempo personalizado. Esto se puede utilizar para excluir datos históricos o para generar perspectivas e informes de datos cronológicos específicos. Elija una [!UICONTROL Fecha de inicio] y un [!UICONTROL Fecha de finalización] seleccionando el icono de calendario de cada campo. Después de lo cual, solo los conjuntos de datos que se ajusten a ese criterio aparecerán en la pestaña Examinar.

### Filtrar conjuntos de datos por fecha de modificación {#filter-by-modified-date}

De forma similar al filtro para la fecha de creación, puede filtrar los conjuntos de datos en función de la fecha en la que se modificaron por última vez. En el [!UICONTROL Fecha de modificación] , Elegir una [!UICONTROL Fecha de inicio] y un [!UICONTROL Fecha de finalización] seleccionando el icono de calendario de cada campo. Después de lo cual, solo los conjuntos de datos modificados durante ese período aparecerán en la pestaña Examinar.

### Filtrar por esquema {#filter-by-schema}

Puede filtrar conjuntos de datos en función del esquema que define su estructura. Seleccione el icono desplegable o introduzca el nombre del esquema en el campo de texto. Aparecerá una lista de posibles coincidencias. Seleccione el esquema adecuado de la lista.

## Ordenar conjuntos de datos por fecha de creación {#sort}

Conjuntos de datos en [!UICONTROL Examinar] La pestaña se puede ordenar por fechas en orden ascendente o descendente. Seleccione el [!UICONTROL Creado] o [!UICONTROL Última actualización] encabezados de columna para alternar entre ascendente y descendente. Una vez seleccionada, la columna lo indica con una flecha hacia arriba o hacia abajo a un lado del encabezado de la columna.

![La pestaña Examinar del área de trabajo Conjuntos de datos con la columna Creado y Última actualización resaltada.](../images/datasets/user-guide/ascending-descending-columns.png)

## Previsualización de un conjunto de datos {#preview}

Puede obtener una vista previa de los datos de ejemplo del conjunto de datos desde las opciones en línea del [!UICONTROL Examinar] y también la pestaña [!UICONTROL Actividad de conjunto de datos] vista. Desde el [!UICONTROL Examinar] , seleccione los puntos suspensivos (...) junto al nombre del conjunto de datos que desea previsualizar. Aparecerá una lista de opciones de menú. A continuación, seleccione **[!UICONTROL Previsualizar conjunto de datos]** de la lista de opciones disponibles. Si el conjunto de datos está vacío, el vínculo de vista previa se desactivará y, en su lugar, indicará que la vista previa no está disponible.

![La pestaña Examinar del espacio de trabajo de conjuntos de datos con la opción de puntos suspensivos y Vista previa del conjunto de datos resaltada para el conjunto de datos elegido.](../images/datasets/user-guide/preview-dataset-option.png)

Esto abre la ventana de vista previa, donde la vista jerárquica del esquema para el conjunto de datos se muestra a la derecha.

![Se muestra el cuadro de diálogo de vista previa del conjunto de datos con información sobre la estructura y los valores de muestra del conjunto de datos.](../images/datasets/user-guide/preview-dataset.png)

Alternativamente, desde el **[!UICONTROL Actividad de conjunto de datos]** pantalla, seleccione **[!UICONTROL Previsualizar conjunto de datos]** cerca de la esquina superior derecha de la pantalla para obtener una vista previa de hasta 100 filas de datos.

![Se resaltará el botón Vista previa del conjunto de datos.](../images/datasets/user-guide/select-preview.png)

Para obtener métodos más sólidos para acceder a los datos, [!DNL Experience Platform] proporciona servicios descendentes como [!DNL Query Service] y [!DNL JupyterLab] para explorar y analizar datos. Consulte los siguientes documentos para obtener más información:

* [Introducción al servicio de consultas](../../query-service/home.md)
* [Guía del usuario de JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Crear un conjunto de datos {#create}

Para crear un nuevo conjunto de datos, comience seleccionando **[!UICONTROL Crear conjunto de datos]** en el **[!UICONTROL Conjuntos de datos]** panel.

![El botón Crear conjunto de datos está resaltado.](../images/datasets/user-guide/select-create.png)

En la siguiente pantalla, se le presentan las dos opciones siguientes para crear un nuevo conjunto de datos:

* [Crear conjunto de datos a partir de esquema](#schema)
* [Crear conjunto de datos a partir de archivo CSV](#csv)

### Crear un conjunto de datos con un esquema existente {#schema}

En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccione **[!UICONTROL Crear conjunto de datos a partir de esquema]** para crear un nuevo conjunto de datos vacío.

![El botón Crear conjunto de datos a partir de esquema está resaltado.](../images/datasets/user-guide/create-dataset-schema.png)

El **[!UICONTROL Seleccionar esquema]** aparece el paso. Examine la lista de esquemas y seleccione el esquema al que se adherirá el conjunto de datos antes de seleccionar **[!UICONTROL Siguiente]**.

![Se muestra una lista de esquemas. Se resalta el esquema que se utilizará para crear el conjunto de datos.](../images/datasets/user-guide/select-schema.png)

El **[!UICONTROL Configurar conjunto de datos]** aparece el paso. Proporcione al conjunto de datos un nombre y una descripción opcional y, a continuación, seleccione **[!UICONTROL Finalizar]** para crear el conjunto de datos.

![Se insertan los detalles de configuración del conjunto de datos. Esto incluye detalles como el nombre y la descripción del conjunto de datos.](../images/datasets/user-guide/configure-dataset-schema.png)

Los conjuntos de datos se pueden filtrar desde la lista de conjuntos de datos disponibles en la interfaz de usuario con el filtro de esquema. Consulte la sección sobre cómo [filtrar conjuntos de datos por esquema](#filter-by-schema) para obtener más información.

### Creación de un conjunto de datos con un archivo CSV {#csv}

Cuando se crea un conjunto de datos con un archivo CSV, se crea un esquema ad hoc para proporcionar al conjunto de datos una estructura que coincida con el archivo CSV proporcionado. En el **[!UICONTROL Crear conjunto de datos]** pantalla, seleccione **[!UICONTROL Crear conjunto de datos a partir de archivo CSV]**.

![El botón Crear conjunto de datos a partir de archivo CSV está resaltado.](../images/datasets/user-guide/create-dataset-csv.png)

El **[!UICONTROL Configurar]** aparece el paso. Proporcione al conjunto de datos un nombre y una descripción opcional y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Se insertan los detalles de configuración del conjunto de datos. Esto incluye detalles como el nombre y la descripción del conjunto de datos.](../images/datasets/user-guide/configure-dataset-csv.png)

El **[!UICONTROL Añadir datos]** aparece el paso. Cargue el archivo CSV arrastrándolo y soltándolo en el centro de la pantalla, o seleccione **[!UICONTROL Examinar]** para explorar el directorio de archivos. El archivo puede tener un tamaño de hasta diez gigabytes. Una vez cargado el archivo CSV, seleccione **[!UICONTROL Guardar]** para crear el conjunto de datos.

>[!NOTE]
>
>Los nombres de las columnas CSV deben comenzar con caracteres alfanuméricos y solo pueden contener letras, números y guiones bajos.

![Se muestra la pantalla Añadir datos. Se resaltará la ubicación donde puede cargar el archivo CSV para el conjunto de datos.](../images/datasets/user-guide/add-csv-data.png)

## Habilitar un conjunto de datos para el perfil del cliente en tiempo real {#enable-profile}

Cada conjunto de datos tiene la capacidad de enriquecer los perfiles de los clientes con los datos introducidos. Para ello, el esquema al que se adhiere el conjunto de datos debe ser compatible para su uso en [!DNL Real-Time Customer Profile]. Un esquema compatible cumple los siguientes requisitos:

* El esquema tiene al menos un atributo especificado como propiedad de identidad.
* El esquema tiene una propiedad de identidad definida como la identidad principal.

Para obtener más información sobre la activación de un esquema para [!DNL Profile], consulte la [Guía del usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

Puede habilitar un conjunto de datos para el perfil desde las opciones en línea del [!UICONTROL Examinar] y también la pestaña [!UICONTROL Actividad de conjunto de datos] vista. Desde el [!UICONTROL Examinar] de la pestaña [!UICONTROL Conjuntos de datos] , seleccione los puntos suspensivos de un conjunto de datos que desee habilitar para el perfil. Aparecerá una lista de opciones de menú. A continuación, seleccione **[!UICONTROL Habilitar perfil unificado]** de la lista de opciones disponibles.

![La pestaña Examinar del espacio de trabajo Conjuntos de datos con los puntos suspensivos y Habilitar perfil unificado resaltados.](../images/datasets/user-guide/enable-for-profile.png)

Alternativamente, desde el **[!UICONTROL Actividad de conjunto de datos]** , seleccione la **[!UICONTROL Perfil]** alternar dentro de **[!UICONTROL Propiedades]** columna. Una vez habilitados, los datos que se incorporen al conjunto de datos también se utilizarán para rellenar perfiles de clientes.

>[!NOTE]
>
>Si un conjunto de datos ya contiene datos y, a continuación, está habilitado para [!DNL Profile], los datos existentes no se consumen automáticamente por [!DNL Profile]. Después de habilitar un conjunto de datos para [!DNL Profile]Sin embargo, se recomienda volver a introducir los datos existentes para que contribuyan a los perfiles de los clientes.

![La opción Perfil se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/enable-dataset-profiles.png)

Los conjuntos de datos que se han habilitado para el perfil también se pueden filtrar según este criterio. Consulte la sección sobre cómo [filtrar conjuntos de datos habilitados para perfil](#filter-profile-enabled-datasets) para obtener más información.

## Administración y aplicación del control de datos en un conjunto de datos {#manage-and-enforce-data-governance}

Puede administrar las etiquetas de control de datos de un conjunto de datos seleccionando las opciones en línea del [!UICONTROL Examinar] pestaña. Seleccione los puntos suspensivos (...) junto al nombre del conjunto de datos que desea administrar, seguido de **[!UICONTROL Administración de datos y etiquetas de acceso]** en el menú desplegable.

Las etiquetas de uso de datos, aplicadas en el nivel de esquema, le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información sobre las etiquetas, o consulte la [guía del usuario sobre etiquetas de uso de datos](../../data-governance/labels/overview.md) para obtener instrucciones sobre cómo aplicar etiquetas a esquemas para su propagación a conjuntos de datos.

## Mover a carpetas {#move-to-folders}

Puede colocar conjuntos de datos en carpetas para administrar mejor los conjuntos de datos. Para mover un conjunto de datos a una carpeta, seleccione los puntos suspensivos (...) junto al nombre del conjunto de datos que desea administrar, seguido de **[!UICONTROL Mover a carpeta]** en el menú desplegable.

![El [!UICONTROL Conjuntos de datos] panel con los puntos suspensivos y [!UICONTROL Mover a carpeta] resaltado.](../images/datasets/user-guide/move-to-folder.png)

El [!UICONTROL Mover] aparece el cuadro de diálogo conjunto de datos a carpeta. Seleccione la carpeta a la que desee mover la audiencia y, a continuación, seleccione **[!UICONTROL Mover]**. Una notificación emergente le informa de que el movimiento del conjunto de datos se ha realizado correctamente.

![El [!UICONTROL Mover] diálogo de conjunto de datos con [!UICONTROL Mover] resaltado.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>También puede crear carpetas directamente desde el cuadro de diálogo Mover conjunto de datos. Para crear una carpeta, seleccione el icono Crear carpeta (![Icono Crear carpeta.](../images/datasets/user-guide/create-folder-icon.png)), en la parte superior derecha del cuadro de diálogo.
>
>![El [!UICONTROL Mover] cuadro de diálogo conjunto de datos con el icono crear carpeta resaltado.](/help/catalog/images/datasets/user-guide/create-folder.png)

Una vez que el conjunto de datos esté en una carpeta, puede elegir mostrar solo los conjuntos de datos que pertenecen a una carpeta específica. Para abrir la estructura de carpetas, seleccione el icono mostrar carpetas (![Icono de mostrar carpetas](../images/datasets/user-guide/show-folders-icon.png)). A continuación, seleccione la carpeta elegida para ver todos los conjuntos de datos asociados.

![El [!UICONTROL Conjuntos de datos] paneles con la estructura de carpetas de conjuntos de datos mostrada, el icono mostrar carpetas y una carpeta seleccionada resaltada.](../images/datasets/user-guide/folder-structure.png)

## Eliminar un conjunto de datos {#delete}

Puede eliminar un conjunto de datos de las acciones en línea del conjunto de datos en [!UICONTROL Examinar] o en la parte superior derecha de la pestaña [!UICONTROL Actividad de conjunto de datos] vista. Desde el [!UICONTROL Examinar] , seleccione los puntos suspensivos (...) junto al nombre del conjunto de datos que desea eliminar. Aparecerá una lista de opciones de menú. A continuación, seleccione **[!UICONTROL Eliminar]** en el menú desplegable.

![La pestaña Examinar del espacio de trabajo Conjuntos de datos con los puntos suspensivos y la opción Eliminar resaltada para el conjunto de datos elegido.](../images/datasets/user-guide/inline-delete-dataset.png)

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Eliminar]** para confirmar.

Como alternativa, seleccione **[!UICONTROL Eliminar conjunto de datos]** desde el **[!UICONTROL Actividad de conjunto de datos]** pantalla.

>[!NOTE]
>
>Conjuntos de datos creados y utilizados por aplicaciones y servicios de Adobe (como Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) no se puede eliminar.

![El botón Eliminar conjunto de datos se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/delete-dataset.png)

Aparecerá un cuadro de confirmación. Seleccionar **[!UICONTROL Eliminar]** para confirmar la eliminación del conjunto de datos.

![Se muestra el modal de confirmación para la eliminación, con el botón Eliminar resaltado.](../images/datasets/user-guide/confirm-delete.png)

## Eliminar un conjunto de datos con perfil habilitado

Si un conjunto de datos está habilitado para Perfil, al eliminar ese conjunto de datos a través de la interfaz de usuario, se eliminará del lago de datos, el servicio de identidad y el almacén de perfiles en Platform.

Puede eliminar un conjunto de datos del [!DNL Profile] Almacenar solo (dejando los datos en el lago de datos) mediante la API de Perfil del cliente en tiempo real. Para obtener más información, consulte la [guía de extremo de API de trabajos del sistema de perfiles](../../profile/api/profile-system-jobs.md).

## Monitorización de la ingesta de datos

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Monitorización]** en el panel de navegación izquierdo. El **[!UICONTROL Monitorización]** El panel de control de Campaign le permite ver los estados de los datos de entrada procedentes de la ingesta por lotes o de la transmisión. Para ver los estados de los lotes individuales, seleccione **[!UICONTROL Lote de extremo a extremo]** o **[!UICONTROL Transmisión de extremo a extremo]**. Los paneles enumeran todas las ejecuciones de ingesta por lotes o de flujo continuo, incluidas las que se realizan correctamente, las que fallaron o las que aún están en curso. Cada lista proporciona detalles del lote, incluido el ID de lote, el nombre del conjunto de datos de destinatario y el número de registros introducidos. Si el conjunto de datos de destinatario está habilitado para [!DNL Profile], también se muestra el número de registros de identidad y perfil ingeridos.

![Se muestra la pantalla de monitorización de un lote completo. Se resaltan tanto la monitorización como el lote a lote.](../images/datasets/user-guide/batch-listing.png)

Puede seleccionar un individuo **[!UICONTROL ID de lote]** para acceder a **[!UICONTROL Introducción a lotes]** y ver los detalles del lote, incluidos los registros de errores en caso de que el lote no se pueda ingerir.

![Se muestran los detalles del lote seleccionado. Esto incluye el número de registros introducidos, el número de registros fallidos, el estado del lote, el tamaño del archivo, las horas de inicio y finalización de la ingesta, los ID de conjunto de datos y lote, el ID de organización, el nombre del conjunto de datos y la información de acceso.](../images/datasets/user-guide/batch-overview.png)

Si desea eliminar el lote, seleccione **[!UICONTROL Eliminar lote]** cerca de la parte superior derecha del panel. Al eliminar un lote también se eliminan sus registros del conjunto de datos en el que se ingirió originalmente el lote.

>[!NOTE]
>
>Si los datos ingeridos se han habilitado para el perfil y se han procesado, al eliminar un lote no se eliminan esos datos del almacén de perfiles.

![El botón Eliminar lote se resalta en la página de detalles del conjunto de datos.](../images/datasets/user-guide/delete-batch.png)

## Pasos siguientes

Esta guía del usuario proporciona instrucciones para realizar acciones comunes al trabajar con conjuntos de datos en [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre la realización de [!DNL Platform] flujos de trabajo que implican conjuntos de datos, consulte los siguientes tutoriales:

* [Creación de un conjunto de datos mediante API](create.md)
* [Consulta de datos de conjuntos de datos mediante la API de acceso a datos](../../data-access/home.md)
* [Configuración de un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad mediante API](../../profile/tutorials/dataset-configuration.md)
