---
keywords: Experience Platform;inicio;temas populares;ingesta;ingesta de datos por lotes;tutorial;ingesta por lotes;tutorial;guía de interfaz de usuario;
solution: Experience Platform
title: Ingesta de datos en el Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform permite importar fácilmente datos como archivos por lotes en forma de archivos de parquet o datos que se ajustan a un esquema conocido del Modelo de datos de experiencia (XDM).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Ingesta de datos en Adobe Experience Platform

Adobe Experience Platform permite importar fácilmente datos en [!DNL Platform] como archivos por lotes. Algunos ejemplos de datos que se van a introducir pueden ser los datos de perfil de un archivo plano en un sistema CRM (como un archivo Parquet) o los datos que se ajustan a un esquema conocido [!DNL Experience Data Model] (XDM) en el Registro de esquemas.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Si prefiere ingerir datos mediante las API de ingesta de datos, comience leyendo la [Guía para desarrolladores de ingesta de lotes](../batch-ingestion/api-overview.md).

## Espacio de trabajo de conjuntos de datos

El espacio de trabajo Conjuntos de datos en [!DNL Experience Platform] le permite ver y administrar todos los conjuntos de datos que ha realizado su organización de IMS, así como crear nuevos.

Para ver el espacio de trabajo Conjuntos de datos, haga clic en **[!UICONTROL Datasets]** en el panel de navegación izquierdo. El espacio de trabajo de conjuntos de datos contiene una lista de conjuntos de datos, que incluye columnas que muestran el nombre, la fecha y la hora creadas, el origen, el esquema y el estado del último lote, así como la fecha y la hora de la última actualización del conjunto de datos.

>[!NOTE]
>
>Haga clic en el icono de filtro junto a la barra de búsqueda para utilizar las funcionalidades de filtrado para ver solo los conjuntos de datos habilitados para [!DNL Profile].

![Ver todos los conjuntos de datos](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **[!UICONTROL Create Dataset]** en la esquina superior derecha del espacio de trabajo de conjuntos de datos.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

En la pantalla **[!UICONTROL Create Dataset]**, seleccione si desea &quot;[!UICONTROL Create Dataset from Schema]&quot; o &quot;[!UICONTROL Create Dataset from CSV File]&quot;.

Para este tutorial, se utilizará un esquema para crear el conjunto de datos. Haga clic en **[!UICONTROL Create Dataset from Schema]** para continuar.

![Seleccionar fuente de datos](../images/tutorials/ingest-batch-data/create-dataset.png)

## Seleccionar esquema del conjunto de datos

En la pantalla **[!UICONTROL Select Schema]** , elija un esquema haciendo clic en el botón de opción situado junto al esquema que desea utilizar. Para este tutorial, el conjunto de datos se realiza con el esquema miembros de lealtad . Usar la barra de búsqueda para filtrar esquemas es una forma útil de encontrar el esquema exacto que está buscando.

Una vez que haya seleccionado el botón de opción situado junto al esquema que desea utilizar, haga clic en **[!UICONTROL Next]**.

![Seleccionar esquema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar el conjunto de datos

En la pantalla **[!UICONTROL Configure Dataset]**, se le pedirá que proporcione un nombre al conjunto de datos y que también proporcione una descripción del conjunto de datos.

**Notas sobre los nombres de conjuntos de datos:**

- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos se pueda encontrar fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que podría ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tiene un nombre y una descripción, haga clic en **[!UICONTROL Finish]**.

![Configurar el conjunto de datos](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Actividad del conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto a la pestaña **[!UICONTROL Dataset Activity]** en el espacio de trabajo de conjuntos de datos. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que aún no ha agregado ningún lote a este conjunto de datos.

A la derecha del espacio de trabajo de conjuntos de datos , verá la pestaña **[!UICONTROL Info]** que contiene información relacionada con el nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, nombre de tabla, esquema, flujo continuo y origen. La pestaña Información también incluye información sobre cuándo se creó el conjunto de datos y su fecha de última modificación.

También en la ficha Información hay una **[!UICONTROL Profile]** opción que se utiliza para habilitar su conjunto de datos para su uso con [!DNL Real-time Customer Profile]. El uso de esta opción, y [!DNL Real-time Customer Profile], se explicarán con más detalle en la sección siguiente.

![Actividad del conjunto de datos](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Habilitar conjunto de datos para [!DNL Real-time Customer Profile]

Los conjuntos de datos se utilizan para la ingesta de datos en [!DNL Experience Platform] y esos datos se utilizan finalmente para identificar individuos y unir información proveniente de múltiples fuentes. Esa información unida se denomina [!DNL Real-Time Customer Profile]. Para que [!DNL Platform] sepa qué información debe incluirse en [!DNL Real-Time Profile], los conjuntos de datos se pueden marcar para su inclusión mediante la opción **[!UICONTROL Profile]**.

De forma predeterminada, esta opción está desactivada. Si decide activar [!DNL Profile], todos los datos introducidos en el conjunto de datos se utilizarán para ayudar a identificar a un individuo y unir su [!DNL Real-Time Profile].

Para obtener más información sobre [!DNL Real-time Customer Profile] y trabajar con identidades, consulte la documentación de [Identity Service](../../identity-service/home.md).

Para habilitar el conjunto de datos para [!DNL Real-time Customer Profile], haga clic en el botón **[!UICONTROL Profile]** en la pestaña **[!UICONTROL Info]**.

![Alternar perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Aparecerá un cuadro de diálogo que le pedirá que confirme que desea habilitar el conjunto de datos para [!DNL Real-time Customer Profile].

![Cuadro de diálogo Activar perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Haga clic en **[!UICONTROL Enable]** y la opción cambiará a azul, indicando que está activada.

![Habilitado para perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Añadir datos al conjunto de datos

Los datos se pueden agregar a un conjunto de datos de varias formas diferentes. Puede elegir utilizar las API [!DNL Data Ingestion] o un socio de ETL como [!DNL Unifi] o [!DNL Informatica]. Para este tutorial, se agregarán datos al conjunto de datos mediante la pestaña **[!UICONTROL Add Data]** de la interfaz de usuario.

Para empezar a agregar datos al conjunto de datos, haga clic en la pestaña **[!UICONTROL Add Data]** . Ahora puede arrastrar y soltar archivos o buscar en el equipo los archivos que desee agregar.

>[!NOTE]
>
>Platform admite dos tipos de archivos para la ingesta de datos, Parquet o JSON. Puede agregar hasta cinco archivos a la vez, con un tamaño máximo de 10 GB para cada archivo.

![Ficha Agregar datos](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Cargar un archivo

Una vez que arrastre y suelte (o examine y seleccione) un archivo Parquet o JSON que desee cargar, [!DNL Platform] empezará inmediatamente a procesar el archivo y aparecerá un cuadro de diálogo **[!UICONTROL Uploading]** en la pestaña **[!UICONTROL Add Data]** que mostrará el progreso de la carga del archivo.

![Cuadro de diálogo de carga](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas de conjunto de datos

Una vez que el archivo ha terminado de cargarse, la pestaña **[!UICONTROL Dataset Activity]** ya no muestra que &quot;No se han agregado lotes&quot;. Ahora, la pestaña **[!UICONTROL Dataset Activity]** muestra las métricas del conjunto de datos. Todas las métricas mostrarán &quot;0&quot; en esta fase, ya que el lote aún no se ha cargado.

En la parte inferior de la pestaña hay una lista que muestra el **[!UICONTROL Batch ID]** de los datos que se acaban de introducir a través del proceso [&quot;Add data to dataset&quot;](#add-data-to-dataset). También se incluye información relacionada con el lote, incluida la fecha de ingesta, el número de registros ingeridos y el estado actual del lote.

![Métricas de conjunto de datos](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalles de lotes

Haga clic en **[!UICONTROL Batch ID]** para ver un **[!UICONTROL Batch Overview]**, mostrando detalles adicionales sobre el lote. Una vez que el lote haya terminado de cargarse, la información sobre el lote se actualizará para mostrar el número de registros introducidos y el tamaño del archivo. El estado también cambiará a &quot;Correcto&quot; o &quot;Fallido&quot;. Si el lote falla, la sección **[!UICONTROL Error Code]** contendrá detalles sobre cualquier error durante la ingesta.

Para obtener más información y las preguntas más frecuentes sobre la ingesta de lotes, consulte la [Guía de solución de problemas de ingesta de lotes](../batch-ingestion/troubleshooting.md).

Para volver a la pantalla **[!UICONTROL Dataset Activity]** , haga clic en el nombre del conjunto de datos (**[!UICONTROL Loyalty Details]**) en la ruta de exploración.

![Información general de lotes](../images/tutorials/ingest-batch-data/batch-details.png)

## Vista previa del conjunto de datos

Una vez que el conjunto de datos está listo, aparece una opción **[!UICONTROL Preview Dataset]** en la parte superior de la pestaña **[!UICONTROL Dataset Activity]**.

Haga clic en **[!UICONTROL Preview Dataset]** para abrir un cuadro de diálogo que muestre datos de ejemplo desde el conjunto de datos. Si el conjunto de datos se creó con un esquema, los detalles del esquema del conjunto de datos aparecerán en el lado izquierdo de la vista previa. Puede expandir el esquema con las flechas para ver la estructura del esquema. Cada encabezado de columna en los datos de vista previa representa un campo en el conjunto de datos.

![Detalles del conjunto de datos](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Pasos siguientes y recursos adicionales

Ahora que ha creado un conjunto de datos y ha introducido correctamente los datos en [!DNL Experience Platform], puede repetir estos pasos para crear un nuevo conjunto de datos o introducir más datos en el conjunto de datos existente.

Para obtener más información sobre la ingesta por lotes, lea la [información general sobre la ingesta por lotes](../batch-ingestion/overview.md) y complemente su aprendizaje viendo el siguiente vídeo.

>[!WARNING]
>
>La interfaz de usuario [!DNL Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
