---
keywords: Experience Platform;inicio;temas populares;flujo de datos;Flujo de datos
title: Configure un flujo de datos para introducir datos por lotes desde una fuente de almacenamiento en la nube en la interfaz de usuario
description: Este tutorial proporciona pasos sobre cómo configurar un nuevo flujo de datos para la ingesta de datos por lotes desde una fuente de almacenamiento en la nube en la IU
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---

# Configure un flujo de datos para introducir datos por lotes desde una fuente de almacenamiento en la nube en la IU

Este tutorial proporciona pasos sobre cómo configurar un flujo de datos para traer datos por lotes de su fuente de almacenamiento en la nube a Adobe Experience Platform.

## Primeros pasos

>[!NOTE]
>
>Para crear un flujo de datos para traer datos por lotes desde un almacenamiento en la nube, ya debe tener acceso a una fuente de almacenamiento en la nube autenticada. Si no tiene acceso, vaya a la [información general de orígenes](../../../../home.md#cloud-storage) para obtener una lista de las fuentes de almacenamiento en la nube con las que puede crear una cuenta.

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Formatos de archivo compatibles

Las fuentes de almacenamiento en la nube para datos por lotes admiten los siguientes formatos de archivo para la ingesta:

* Valores separados por delimitadores (DSV): cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]: los archivos de datos con formato de parquet deben ser compatibles con XDM.
* Archivos comprimidos: los archivos JSON y delimitados se pueden comprimir como: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, y `tar`.

## Adición de datos

Después de crear la cuenta de almacenamiento en la nube, la variable **[!UICONTROL Añadir datos]** Este paso aparece y proporciona una interfaz para que explore la jerarquía de archivos del almacenamiento en la nube y seleccione la carpeta o el archivo específico que desea llevar a Platform.

* La parte izquierda de la interfaz es un explorador de directorios que muestra la jerarquía de archivos del almacenamiento en la nube.
* La parte derecha de la interfaz permite obtener una vista previa de hasta 100 filas de datos desde una carpeta o archivo compatible.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Seleccione la carpeta raíz para acceder a la jerarquía de carpetas. Desde aquí, puede seleccionar una sola carpeta para introducir todos los archivos de la carpeta de forma recursiva. Al ingerir una carpeta completa, debe asegurarse de que todos los archivos de esa carpeta compartan el mismo formato de datos y esquema.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Una vez seleccionada una carpeta, la interfaz correcta se actualiza a una vista previa del contenido y la estructura del primer archivo de la carpeta seleccionada.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Durante este paso, puede realizar varias configuraciones en los datos antes de continuar. Primero, seleccione **[!UICONTROL Formato de datos]** y, a continuación, seleccione el formato de datos adecuado para el archivo en el panel desplegable que aparece.

La siguiente tabla muestra los formatos de datos adecuados para los tipos de archivo admitidos:

| Tipo de archivo | Formato de datos |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Seleccionar un delimitador de columna

Después de configurar el formato de datos, puede establecer un delimitador de columna al ingerir archivos delimitados. Seleccione el **[!UICONTROL Delimitador]** y, a continuación, seleccione un delimitador en el menú desplegable. El menú muestra las opciones utilizadas con más frecuencia para delimitadores, incluida una coma (`,`), una pestaña (`\t`) y una barra vertical (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Si prefiere utilizar un delimitador personalizado, seleccione **[!UICONTROL Personalizado]** e introduzca un delimitador de un solo carácter de su elección en la barra de entrada emergente.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Ingesta de archivos comprimidos

También puede introducir archivos JSON comprimidos o delimitados especificando su tipo de compresión.

En el [!UICONTROL Seleccionar datos] , seleccione un archivo comprimido para su ingesta y, a continuación, seleccione su tipo de archivo adecuado y si es compatible con XDM o no. A continuación, seleccione **[!UICONTROL Tipo de compresión]** y, a continuación, seleccione el tipo de archivo comprimido adecuado para los datos de origen.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Para llevar un archivo específico a Platform, seleccione una carpeta y, a continuación, el archivo que desea introducir. Durante este paso, también puede obtener una vista previa del contenido de otros archivos de una carpeta determinada mediante el icono de vista previa junto a un nombre de archivo.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Proporcionar detalles del flujo de datos

El [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o uno nuevo. Durante este proceso, también puede configurar los datos para que se introduzcan en el perfil y habilitar ajustes como [!UICONTROL Diagnósticos de error], [!UICONTROL Ingesta parcial], y [!UICONTROL Alertas].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Usar un conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable. Una vez seleccionado un conjunto de datos, proporcione un nombre y una descripción para el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Usar un nuevo conjunto de datos

Para introducir en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre del conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Habilitar diagnósticos de perfil y error

A continuación, seleccione la **[!UICONTROL Conjunto de datos de perfil]** para habilitar el conjunto de datos para el perfil. Esto le permite crear una vista integral de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados para perfiles se incluirán en el perfil y los cambios se aplicarán al guardar el flujo de datos.

[!UICONTROL Diagnósticos de error] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] permite la ingesta de datos que contienen errores, hasta un determinado umbral que se define manualmente. Consulte la [resumen de ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Habilitar alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la IU](../../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Asignación de campos de datos a un esquema XDM

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez que los datos de origen se hayan asignado correctamente, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Programar ejecuciones de ingesta

>[!IMPORTANT]
>
>Se recomienda programar el flujo de datos para una ingesta única al utilizar [Origen de FTP](../../../../connectors/cloud-storage/ftp.md).

El [!UICONTROL Programación] Este paso aparece, lo que le permite configurar una programación de ingesta para introducir automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. De forma predeterminada, la programación está configurada en `Once`. Para ajustar la frecuencia de ingesta, seleccione **[!UICONTROL Frecuencia]** y, a continuación, seleccione una opción en el menú desplegable.

>[!TIP]
>
>El intervalo y el relleno no son visibles durante una ingesta única.

![programación](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Si establece la frecuencia de ingesta en `Minute`, `Hour`, `Day`, o `Week`, debe establecer un intervalo para establecer un intervalo de tiempo establecido entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para introducir datos cada 15 días.

Durante este paso, también puede activar **relleno** y defina una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar los nuevos datos de los datos existentes.

Consulte la tabla siguiente para obtener más información sobre las configuraciones de programación.

| Campo | Descripción |
| --- | --- |
| Frecuencia | La frecuencia con la que se produce una ingesta. Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`, y `Week`. |
| Intervalo | Un entero que define el intervalo para la frecuencia seleccionada. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15. |
| Hora de inicio | Una marca de tiempo UTC que indica cuándo se configurará para que se produzca la primera ingesta. La hora de inicio debe ser buena o igual a la hora UTC actual. |
| Relleno | Un valor booleano que determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si se desactiva el relleno, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

>[!NOTE]
>
>Para la ingesta por lotes, cada flujo de datos posterior selecciona los archivos que se van a ingerir desde el origen en función de su **última modificación** marca de tiempo. Esto significa que los flujos de datos por lotes seleccionan archivos del origen que son nuevos o que se han modificado desde la última ejecución del flujo. Además, debe asegurarse de que haya un lapso de tiempo suficiente entre la carga del archivo y una ejecución de flujo programada, ya que es posible que los archivos que no se han cargado completamente en su cuenta de almacenamiento en la nube antes del tiempo de ejecución del flujo programado no se recojan para su ingesta.

Cuando termine de configurar la programación de ingesta, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Revisión del flujo de datos

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el periodo activo, la frecuencia y el intervalo de la programación de ingesta.

Una vez revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para introducir datos de un almacenamiento de nube externo y ha obtenido información sobre la monitorización de conjuntos de datos. Para obtener más información sobre la creación de flujos de datos, puede complementar su aprendizaje viendo el vídeo siguiente. Además, ahora los datos entrantes pueden utilizarse en el flujo descendente [!DNL Platform] servicios como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> El [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar el flujo de datos, visite el tutorial sobre [monitorización de cuentas y flujos de datos en la IU](../../monitor.md).

## Actualizar el flujo de datos

Para actualizar las configuraciones de la programación, la asignación y la información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la IU](../../update-dataflows.md)

## Eliminar el flujo de datos

Puede eliminar los flujos de datos que ya no son necesarios o que se crearon incorrectamente utilizando **[!UICONTROL Eliminar]** función disponible en el **[!UICONTROL Flujos de datos]** workspace. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminación de flujos de datos en la IU](../../delete.md).