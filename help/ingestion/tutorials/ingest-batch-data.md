---
keywords: Experience Platform;inicio;temas populares;ingesta;ingesta por lotes de datos;tutorial;ingesta por lotes;tutorial;tutorial;guía de iu;
solution: Experience Platform
title: Ingesta De Datos En Experience Platform
type: Tutorial
description: Adobe Experience Platform permite importar fácilmente datos como archivos por lotes en forma de archivos de Parquet o datos que se ajusten a un esquema conocido de Experience Data Model (XDM).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 31631b03b6ff1e50e55c01e948fae5c29fd618dd
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# Ingesta de datos en Adobe Experience Platform

Adobe Experience Platform permite importar fácilmente datos en [!DNL Experience Platform] como archivos por lotes. Algunos ejemplos de datos que se van a ingerir son los datos de perfil de un archivo plano de un sistema CRM (como un archivo de Parquet) o los datos que se ajustan a un esquema conocido de [!DNL Experience Data Model] (XDM) en el Registro de esquemas.

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Si prefiere introducir datos mediante las API de ingesta de datos, comience por leer la [Guía para desarrolladores de ingesta por lotes](../batch-ingestion/api-overview.md).

## Datasets Workspace

El área de trabajo Conjuntos de datos de [!DNL Experience Platform] le permite ver y administrar todos los conjuntos de datos que ha creado su organización, así como crear nuevos conjuntos de datos.

Vea el área de trabajo Conjuntos de datos haciendo clic en **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo. El espacio de trabajo Conjuntos de datos contiene una lista de conjuntos de datos, incluidas columnas que muestran el nombre, el estado creado (fecha y hora), el origen, el esquema y el último lote, así como la fecha y la hora en que se actualizó el conjunto de datos por última vez.

>[!NOTE]
>
>Haga clic en el icono de filtro junto a la barra de búsqueda para utilizar las capacidades de filtrado y ver solo los conjuntos de datos habilitados para [!DNL Profile].

![Ver todos los conjuntos de datos](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha del área de trabajo Conjuntos de datos.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

En la pantalla **[!UICONTROL Crear conjunto de datos]**, seleccione si desea &quot;[!UICONTROL Crear conjunto de datos a partir del esquema]&quot; o &quot;[!UICONTROL Crear conjunto de datos a partir del archivo CSV]&quot;.

Para este tutorial, se utilizará un esquema para crear el conjunto de datos. Haga clic en **[!UICONTROL Crear conjunto de datos a partir del esquema]** para continuar.

![Seleccionar origen de datos](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleccionar esquema del conjunto de datos

En la pantalla **[!UICONTROL Seleccionar esquema]**, elija un esquema haciendo clic en el botón de opción situado junto al esquema que desee utilizar. Para este tutorial, el conjunto de datos se realizará mediante el esquema Miembros socio. El uso de la barra de búsqueda para filtrar esquemas es una forma útil de encontrar el esquema exacto que está buscando.

Una vez que haya seleccionado el botón de opción situado junto al esquema que desea utilizar, haga clic en **[!UICONTROL Siguiente]**.

![Seleccionar esquema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar conjunto de datos

En la pantalla **[!UICONTROL Configurar conjunto de datos]**, se le pedirá que indique un nombre y que proporcione también una descripción del conjunto de datos.

**Notas sobre nombres de conjuntos de datos:**

- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que se puedan encontrar fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos para que no se reutilicen en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que puede ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tenga un nombre y una descripción, haga clic en **[!UICONTROL Finalizar]**.

![Configurar conjunto de datos](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Actividad del conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto a la ficha **[!UICONTROL Actividad de conjunto de datos]** en el área de trabajo Conjuntos de datos. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación que indique que no se han agregado lotes. Esto es lo que cabe esperar, ya que todavía no ha añadido ningún lote a este conjunto de datos.

En el lado derecho del área de trabajo Conjuntos de datos verá la pestaña **[!UICONTROL Información]** que contiene información relacionada con el nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, nombre de tabla, esquema, flujo y origen. La pestaña Información también incluye información sobre cuándo se creó el conjunto de datos y su última fecha de modificación.

En la ficha Información también se encuentra la opción **[!UICONTROL Perfil]** que se usa para habilitar el conjunto de datos para su uso con [!DNL Real-Time Customer Profile]. El uso de esta opción, y [!DNL Real-Time Customer Profile], se explicará con más detalle en la sección siguiente.

![Actividad del conjunto de datos](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Habilitar conjunto de datos para [!DNL Real-Time Customer Profile] {#enable-for-profile}

Los conjuntos de datos se utilizan para la ingesta de datos en [!DNL Experience Platform], y en última instancia esos datos se utilizan para identificar a las personas y unir información proveniente de múltiples fuentes. Esa información unida se denomina [!DNL Real-Time Customer Profile]. Para que [!DNL Experience Platform] sepa qué información debe incluirse en [!DNL Real-Time Profile], los conjuntos de datos se pueden marcar para su inclusión mediante la opción **[!UICONTROL Perfil]**.

De forma predeterminada, esta opción está desactivada. Si elige activar [!DNL Profile], todos los datos introducidos en el conjunto de datos se utilizarán para ayudar a identificar a un individuo y unir sus [!DNL Real-Time Profile].

Para obtener más información acerca de [!DNL Real-Time Customer Profile] y cómo trabajar con identidades, consulte la documentación de [Servicio de identidad](../../identity-service/home.md).

Para habilitar el conjunto de datos de [!DNL Real-Time Customer Profile], haga clic en el botón de alternancia **[!UICONTROL Perfil]** en la ficha **[!UICONTROL Información]**.

![Alternar perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Aparecerá un cuadro de diálogo pidiéndole que confirme que desea habilitar el conjunto de datos para [!DNL Real-Time Customer Profile].

![Activar cuadro de diálogo de perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Haga clic en **[!UICONTROL Habilitar]** y el conmutador se pondrá azul, lo que indica que está activado.

![Habilitado para el perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Añadir datos al conjunto de datos

Los datos se pueden agregar a un conjunto de datos de varias formas diferentes. Puede elegir usar las API [!DNL Data Ingestion] o un socio de ETL como [!DNL Unifi] o [!DNL Informatica]. Para este tutorial, los datos se agregarán al conjunto de datos mediante la ficha **[!UICONTROL Agregar datos]** dentro de la interfaz de usuario.

Para empezar a agregar datos al conjunto de datos, haga clic en la ficha **[!UICONTROL Agregar datos]**. Ahora puede arrastrar y soltar archivos o examinar el equipo en busca de los archivos que desea agregar.

>[!NOTE]
>
>Experience Platform admite dos tipos de archivo para la ingesta de datos: Parquet o JSON. Puede agregar hasta cinco archivos a la vez, con un tamaño máximo de archivo de 1 GB.

![Agregar ficha de datos](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Cargar un archivo {#upload-file}

Una vez que arrastre y suelte (o examine y seleccione) un archivo Parquet o JSON que desee cargar, [!DNL Experience Platform] comenzará a procesar el archivo inmediatamente y aparecerá un cuadro de diálogo **[!UICONTROL Cargando]** en la ficha **[!UICONTROL Agregar datos]** que mostrará el progreso de la carga del archivo.

![Cuadro de diálogo de carga](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas de conjunto de datos

Una vez que el archivo haya terminado de cargarse, la ficha **[!UICONTROL Actividad de conjuntos de datos]** ya no muestra que &quot;No se han agregado lotes&quot;. En su lugar, la pestaña **[!UICONTROL Actividad de conjuntos de datos]** ahora muestra métricas de conjuntos de datos. En esta fase, todas las métricas mostrarán &quot;0&quot;, ya que el lote aún no se ha cargado.

En la parte inferior de la pestaña hay una lista que muestra el **[!UICONTROL ID de lote]** de los datos que se acaban de introducir a través del proceso [&quot;Agregar datos al conjunto de datos&quot;](#add-data-to-dataset). También se incluye información relacionada con el lote, incluida la fecha de ingesta, el número de registros ingeridos y el estado actual del lote.

![Métricas de conjuntos de datos](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalles del lote

Haga clic en **[!UICONTROL ID de lote]** para ver una **[!UICONTROL descripción general de lote]** que muestra detalles adicionales sobre el lote. Una vez que el lote haya terminado de cargarse, la información sobre el lote se actualizará para mostrar el número de registros introducidos y el tamaño del archivo. El estado también cambiará a &quot;Correcto&quot; o &quot;Fallido&quot;. Si el lote falla, la sección **[!UICONTROL Código de error]** contendrá detalles con respecto a cualquier error durante la ingesta.

Para obtener más información y las preguntas más frecuentes sobre la ingesta por lotes, consulte la [Guía de solución de problemas de ingesta por lotes](../batch-ingestion/troubleshooting.md).

Para volver a la pantalla **[!UICONTROL Actividad del conjunto de datos]**, haga clic en el nombre del conjunto de datos (**[!UICONTROL Detalles de fidelidad]**) en la ruta de exploración.

![Información general por lotes](../images/tutorials/ingest-batch-data/batch-details.png)

## Previsualizar conjunto de datos

Una vez que el conjunto de datos está listo, aparece una opción para **[!UICONTROL Previsualizar conjunto de datos]** en la parte superior de la pestaña **[!UICONTROL Actividad del conjunto de datos]**.

Haga clic en **[!UICONTROL Vista previa del conjunto de datos]** para abrir un cuadro de diálogo que muestre datos de ejemplo desde el conjunto de datos. Si el conjunto de datos se creó con un esquema, los detalles del esquema del conjunto de datos aparecerán en el lado izquierdo de la vista previa. Puede expandir el esquema mediante las flechas para ver la estructura del esquema. Cada encabezado de columna de los datos de vista previa representa un campo del conjunto de datos.

![Detalles del conjunto de datos](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Pasos siguientes y recursos adicionales

Ahora que ha creado un conjunto de datos y ha ingerido datos correctamente en [!DNL Experience Platform], puede repetir estos pasos para crear un nuevo conjunto de datos o ingerir más datos en el conjunto de datos existente.

Para obtener más información sobre la ingesta por lotes, lea la [descripción general de la ingesta por lotes](../batch-ingestion/overview.md) y complemente su aprendizaje viendo el siguiente vídeo.

>[!WARNING]
>
>La interfaz de usuario [!DNL Experience Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/34380?quality=12&learn=on&captions=spa)
