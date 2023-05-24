---
keywords: Experience Platform;inicio;temas populares;ingesta;ingesta por lotes de datos;tutorial;ingesta por lotes;tutorial;guía de iu;
solution: Experience Platform
title: Ingesta De Datos En El Experience Platform
type: Tutorial
description: Adobe Experience Platform permite importar fácilmente datos como archivos por lotes en forma de archivos de Parquet o datos que se ajusten a un esquema conocido de Experience Data Model (XDM).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# Introducción de datos en Adobe Experience Platform

Adobe Experience Platform permite importar fácilmente datos en [!DNL Platform] como archivos por lotes. Algunos ejemplos de datos que se van a introducir pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo de Parquet) o los datos que se ajustan a un [!DNL Experience Data Model] Esquema (XDM) en el Registro de esquemas.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Si prefiere introducir datos mediante las API de ingesta de datos, comience por leer la [Guía para desarrolladores de ingesta por lotes](../batch-ingestion/api-overview.md).

## Datasets Workspace

El espacio de trabajo Conjuntos de datos [!DNL Experience Platform] le permite ver y administrar todos los conjuntos de datos que ha creado su organización, así como crear otros nuevos.

Vea el espacio de trabajo Conjuntos de datos haciendo clic en **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo. El espacio de trabajo Conjuntos de datos contiene una lista de conjuntos de datos, incluidas columnas que muestran el nombre, el estado creado (fecha y hora), el origen, el esquema y el último lote, así como la fecha y la hora en que se actualizó el conjunto de datos por última vez.

>[!NOTE]
>
>Haga clic en el icono de filtro junto a la barra de búsqueda para utilizar las funcionalidades de filtrado y ver solo los conjuntos de datos habilitados para [!DNL Profile].

![Ver todos los conjuntos de datos](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha del espacio de trabajo Conjuntos de datos.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

En el **[!UICONTROL Crear conjunto de datos]** , seleccione si desea &quot;[!UICONTROL Crear conjunto de datos a partir de esquema]&quot; o &quot;[!UICONTROL Crear conjunto de datos a partir de archivo CSV]&quot;.

Para este tutorial, se utilizará un esquema para crear el conjunto de datos. Clic **[!UICONTROL Crear conjunto de datos a partir de esquema]** para continuar.

![Seleccionar fuente de datos](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleccionar esquema del conjunto de datos

En el **[!UICONTROL Seleccionar esquema]** , seleccione un esquema haciendo clic en el botón de opción situado junto al esquema que desea utilizar. Para este tutorial, el conjunto de datos se realizará mediante el esquema Miembros socio. El uso de la barra de búsqueda para filtrar esquemas es una forma útil de encontrar el esquema exacto que está buscando.

Una vez seleccionado el botón de opción situado junto al esquema que desea utilizar, haga clic en **[!UICONTROL Siguiente]**.

![Seleccionar esquema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar el conjunto de datos

En el **[!UICONTROL Configurar conjunto de datos]** , deberá asignar un nombre al conjunto de datos y también puede proporcionar una descripción del conjunto de datos.

**Notas sobre los nombres de conjuntos de datos:**

- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que se puedan encontrar fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos para que no se reutilicen en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que puede ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Cuando el conjunto de datos tenga un nombre y una descripción, haga clic en **[!UICONTROL Finalizar]**.

![Configurar el conjunto de datos](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Actividad de conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto al **[!UICONTROL Actividad de conjunto de datos]** en el espacio de trabajo Conjuntos de datos. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación que indique que no se han agregado lotes. Esto es lo que cabe esperar, ya que todavía no ha añadido ningún lote a este conjunto de datos.

En el lado derecho del espacio de trabajo Conjuntos de datos verá el **[!UICONTROL Información]** pestaña que contiene información relacionada con el nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, nombre de tabla, esquema, flujo y origen. La pestaña Información también incluye información sobre cuándo se creó el conjunto de datos y su última fecha de modificación.

También se encuentra en la pestaña Información un  **[!UICONTROL Perfil]** que se utiliza para habilitar el conjunto de datos para utilizarlo con [!DNL Real-Time Customer Profile]. Uso de esta opción y [!DNL Real-Time Customer Profile], se explicarán con más detalle en la sección siguiente.

![Actividad de conjunto de datos](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Habilitar conjunto de datos para [!DNL Real-Time Customer Profile]

Los conjuntos de datos se utilizan para introducir datos en [!DNL Experience Platform]y que, en última instancia, los datos se utilizan para identificar a las personas y unir información proveniente de múltiples fuentes. Esa información unida se denomina [!DNL Real-Time Customer Profile]. Para que [!DNL Platform] para saber qué información debe incluirse en la [!DNL Real-Time Profile], los conjuntos de datos se pueden marcar para su inclusión mediante el **[!UICONTROL Perfil]** alternar.

De forma predeterminada, esta opción está desactivada. Si decide activar la opción [!DNL Profile], todos los datos introducidos en el conjunto de datos se utilizarán para ayudar a identificar a un individuo y unir sus datos [!DNL Real-Time Profile].

Para obtener más información acerca de [!DNL Real-Time Customer Profile] y trabajar con identidades, revise las [Servicio de identidad](../../identity-service/home.md) documentación.

Para habilitar el conjunto de datos para [!DNL Real-Time Customer Profile], haga clic en **[!UICONTROL Perfil]** alternar en **[!UICONTROL Información]** pestaña.

![Alternar perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Aparecerá un cuadro de diálogo pidiéndole que confirme que desea habilitar el conjunto de datos para [!DNL Real-Time Customer Profile].

![Cuadro de diálogo Habilitar perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Clic **[!UICONTROL Activar]** y la opción se pondrá azul, indicando que está activada.

![Habilitado para el perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Añadir datos al conjunto de datos

Los datos se pueden agregar a un conjunto de datos de varias formas diferentes. Puede elegir usar [!DNL Data Ingestion] API o un socio de ETL como [!DNL Unifi] o [!DNL Informatica]. Para este tutorial, los datos se agregarán al conjunto de datos utilizando **[!UICONTROL Añadir datos]** dentro de la interfaz de usuario.

Para empezar a agregar datos al conjunto de datos, haga clic en **[!UICONTROL Añadir datos]** pestaña. Ahora puede arrastrar y soltar archivos o examinar el equipo en busca de los archivos que desea agregar.

>[!NOTE]
>
>Platform admite dos tipos de archivos para la ingesta de datos: Parquet o JSON. Puede agregar hasta cinco archivos a la vez, con un tamaño máximo de archivo de 1 GB.

![Pestaña Añadir datos](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Cargar un archivo

Una vez que arrastre y suelte (o examine y seleccione) un archivo Parquet o JSON que desee cargar, [!DNL Platform] comenzará inmediatamente a procesar el archivo y una **[!UICONTROL Cargando]** El cuadro de diálogo aparecerá en **[!UICONTROL Añadir datos]** pestaña que muestra el progreso de la carga del archivo.

![Cuadro de diálogo Cargar](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas de conjunto de datos

Una vez que el archivo haya terminado de cargarse, la variable **[!UICONTROL Actividad de conjunto de datos]** ya no muestra que &quot;No se han agregado lotes&quot;. En su lugar, la variable **[!UICONTROL Actividad de conjunto de datos]** ahora muestra las métricas del conjunto de datos. En esta fase, todas las métricas mostrarán &quot;0&quot;, ya que el lote aún no se ha cargado.

En la parte inferior de la pestaña hay una lista que muestra el **[!UICONTROL ID de lote]** de los datos que se acaban de ingerir a través de [&quot;Añadir datos al conjunto de datos&quot;](#add-data-to-dataset) proceso. También se incluye información relacionada con el lote, incluida la fecha de ingesta, el número de registros ingeridos y el estado actual del lote.

![Métricas de conjunto de datos](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalles del lote

Haga clic en **[!UICONTROL ID de lote]** para ver una **[!UICONTROL Introducción a lotes]**, mostrando detalles adicionales sobre el lote. Una vez que el lote haya terminado de cargarse, la información sobre el lote se actualizará para mostrar el número de registros introducidos y el tamaño del archivo. El estado también cambiará a &quot;Correcto&quot; o &quot;Fallido&quot;. Si el lote no supera el **[!UICONTROL Código de error]** contendrá detalles sobre cualquier error durante la ingesta.

Para obtener más información y las preguntas más frecuentes sobre la ingesta por lotes, consulte la [Guía de solución de problemas de ingesta por lotes](../batch-ingestion/troubleshooting.md).

Para volver a la **[!UICONTROL Actividad de conjunto de datos]** , haga clic en el nombre del conjunto de datos (**[!UICONTROL Detalles de fidelización]**) en la ruta de exploración.

![Introducción a lotes](../images/tutorials/ingest-batch-data/batch-details.png)

## Previsualizar conjunto de datos

Una vez que el conjunto de datos esté listo, una opción para lo siguiente **[!UICONTROL Previsualizar conjunto de datos]** aparece en la parte superior de la **[!UICONTROL Actividad de conjunto de datos]** pestaña.

Clic **[!UICONTROL Previsualizar conjunto de datos]** para abrir un cuadro de diálogo que muestre datos de ejemplo desde el conjunto de datos. Si el conjunto de datos se creó con un esquema, los detalles del esquema del conjunto de datos aparecerán en el lado izquierdo de la vista previa. Puede expandir el esquema mediante las flechas para ver la estructura del esquema. Cada encabezado de columna de los datos de vista previa representa un campo del conjunto de datos.

![Detalles del conjunto de datos](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Pasos siguientes y recursos adicionales

Ahora que ha creado un conjunto de datos y ha introducido correctamente los datos en [!DNL Experience Platform]Además, puede repetir estos pasos para crear un nuevo conjunto de datos o introducir más datos en el conjunto de datos existente.

Para obtener más información sobre la ingesta por lotes, lea la [Resumen de ingesta por lotes](../batch-ingestion/overview.md) y complemente su aprendizaje viendo el siguiente vídeo.

>[!WARNING]
>
>El [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
