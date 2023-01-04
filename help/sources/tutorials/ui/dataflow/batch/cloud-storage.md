---
keywords: Experience Platform;inicio;temas populares;flujo de datos;flujo de datos
title: Configurar un flujo de datos para introducir datos por lotes desde una fuente de almacenamiento en la nube en la interfaz de usuario
description: Este tutorial proporciona pasos sobre cómo configurar un nuevo flujo de datos para la ingesta de datos por lotes desde un origen de almacenamiento en la nube en la interfaz de usuario
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---

# Configure un flujo de datos para introducir datos por lotes desde un origen de almacenamiento en la nube en la interfaz de usuario

Este tutorial proporciona pasos sobre cómo configurar un flujo de datos para traer datos por lotes desde el origen de almacenamiento en la nube a Adobe Experience Platform.

## Primeros pasos

>[!NOTE]
>
>Para crear un flujo de datos con el fin de obtener datos por lotes de un almacenamiento en la nube, ya debe tener acceso a un origen de almacenamiento en la nube autenticado. Si no tiene acceso, vaya a la [información general sobre fuentes](../../../../home.md#cloud-storage) para obtener una lista de los orígenes de almacenamiento en la nube con los que puede crear una cuenta.

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

### Formatos de archivo compatibles

Los orígenes de almacenamiento en la nube para datos por lotes admiten los siguientes formatos de archivo para la ingesta:

* Valores separados por delimitadores (DSV): Cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]: Los archivos de datos con formato de parqué deben ser compatibles con XDM.
* Archivos comprimidos: Los archivos JSON y delimitados se pueden comprimir como: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`y `tar`.

## Adición de datos

Después de crear su cuenta de almacenamiento en la nube, la variable **[!UICONTROL Añadir datos]** aparece, proporcionando una interfaz para explorar la jerarquía de archivos de almacenamiento en la nube y seleccionar la carpeta o el archivo específico que desea traer a Platform.

* La parte izquierda de la interfaz es un explorador de directorios, que muestra la jerarquía de archivos de almacenamiento en la nube.
* La parte derecha de la interfaz permite previsualizar hasta 100 filas de datos de una carpeta o archivo compatible.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Seleccione la carpeta raíz para acceder a la jerarquía de carpetas. Desde aquí, puede seleccionar una sola carpeta para introducir todos los archivos de la carpeta de forma recursiva. Al ingerir una carpeta completa, debe asegurarse de que todos los archivos de esa carpeta compartan el mismo formato de datos y esquema.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Una vez seleccionada una carpeta, la interfaz correcta se actualiza a una previsualización del contenido y la estructura del primer archivo de la carpeta seleccionada.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Durante este paso, puede realizar varias configuraciones en los datos antes de continuar. Primero, seleccione **[!UICONTROL Formato de datos]** y, a continuación, seleccione el formato de datos adecuado para el archivo en el panel desplegable que aparece.

La tabla siguiente muestra los formatos de datos adecuados para los tipos de archivo admitidos:

| Tipo de archivo | Formato de datos |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parqué | [!UICONTROL Parqué XDM] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Seleccionar un delimitador de columna

Después de configurar el formato de datos, puede establecer un delimitador de columna al introducir archivos delimitados. Seleccione el **[!UICONTROL Delimitador]** y, a continuación, seleccione un delimitador en el menú desplegable. El menú muestra las opciones más utilizadas para los delimitadores, incluida una coma (`,`), una pestaña (`\t`) y una barra vertical (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Si prefiere usar un delimitador personalizado, seleccione **[!UICONTROL Personalizado]** e introduzca un delimitador de un solo carácter de su elección en la barra de entrada emergente.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Ingesta de archivos comprimidos

También puede introducir archivos JSON comprimidos o delimitados especificando su tipo de compresión.

En el [!UICONTROL Seleccionar datos] , seleccione un archivo comprimido para la ingesta y, a continuación, seleccione su tipo de archivo adecuado y si es compatible con XDM o no. A continuación, seleccione **[!UICONTROL Tipo de compresión]** y, a continuación, seleccione el tipo de archivo comprimido apropiado para los datos de origen.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Para traer un archivo específico a Platform, seleccione una carpeta y, a continuación, seleccione el archivo que desea ingerir. Durante este paso, también puede obtener una vista previa del contenido de otros archivos de una carpeta determinada mediante el icono de vista previa situado junto al nombre de un archivo.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Proporcionar detalles de flujo de datos

La variable [!UICONTROL Detalles de flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o un nuevo conjunto de datos. Durante este proceso, también puede configurar los datos para que se introduzcan en Perfil y habilitar opciones como [!UICONTROL Diagnóstico de errores], [!UICONTROL Ingesta parcial]y [!UICONTROL Alertas].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Usar un conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable. Una vez que haya seleccionado un conjunto de datos, proporcione un nombre y una descripción para el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Usar un nuevo conjunto de datos

Para introducir en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre de conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema para asignarlo mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez que haya seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Habilitar el diagnóstico de perfiles y errores

A continuación, seleccione la **[!UICONTROL Conjunto de datos del perfil]** para habilitar el conjunto de datos para Perfil. Esto le permite crear una vista holística de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados para perfil se incluirán en Perfil y se aplicarán cambios cuando guarde el flujo de datos.

[!UICONTROL Diagnóstico de errores] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] le permite introducir datos que contengan errores, hasta un umbral determinado que defina manualmente. Consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Habilitar alertas

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la interfaz de usuario](../../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Asignación de campos de datos a un esquema XDM

La variable [!UICONTROL Asignación] aparece, proporcionando una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez asignados correctamente los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Programar ejecuciones de ingesta

>[!IMPORTANT]
>
>Se recomienda programar el flujo de datos para una ingesta única al usar la variable [Fuente de FTP](../../../../connectors/cloud-storage/ftp.md).

La variable [!UICONTROL Programación] , lo que le permite configurar una programación de ingesta para que ingrese automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. De forma predeterminada, la programación está configurada en `Once`. Para ajustar la frecuencia de ingesta, seleccione **[!UICONTROL Frecuencia]** y, a continuación, seleccione una opción en el menú desplegable.

>[!TIP]
>
>El intervalo y el relleno no son visibles durante una ingesta única.

![programación](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Si establece la frecuencia de ingesta en `Minute`, `Hour`, `Day`o `Week`, debe configurar un intervalo para establecer un intervalo de tiempo definido entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para la ingesta de datos cada 15 días.

Durante este paso, también puede activar **relleno** y defina una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar nuevos datos de los datos existentes.

Consulte la siguiente tabla para obtener más información sobre las configuraciones de programación.

| Campo | Descripción |
| --- | --- |
| Frecuencia | Frecuencia con la que se produce una ingesta. Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`y `Week`. |
| Intervalo | Un entero que define el intervalo para la frecuencia seleccionada. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15. |
| Hora de inicio | Marca de tiempo UTC que indica cuándo se configura la primera ingesta. La hora de inicio debe ser buena o igual a la hora UTC actual. |
| Relleno | Un valor booleano que determina qué datos se introducen inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se incorporarán durante la primera ingesta programada. Si el relleno está desactivado, solo se incorporarán los archivos que se cargan entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

>[!NOTE]
>
>Para la ingesta por lotes, cada flujo de datos resultante selecciona los archivos que se van a ingerir de su origen en función de sus **última modificación** marca de tiempo. Esto significa que los flujos de datos por lotes seleccionan los archivos del origen que son nuevos o que se han modificado desde la última ejecución del flujo. Además, debe asegurarse de que haya un lapso de tiempo suficiente entre la carga de archivos y la ejecución de un flujo programado, ya que es posible que los archivos que no se carguen completamente en la cuenta de almacenamiento en la nube antes del tiempo de ejecución del flujo programado no se recojan para su incorporación.

Cuando termine de configurar la programación de ingesta, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Revise el flujo de datos

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el período, la frecuencia y el intervalo activos del programa de ingesta.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para incorporar datos de un almacenamiento en la nube externo y ha obtenido información sobre la monitorización de conjuntos de datos. Para obtener más información sobre la creación de flujos de datos, puede complementar su aprendizaje viendo el siguiente vídeo. Además, los datos entrantes ahora se pueden utilizar en el flujo descendente [!DNL Platform] servicios como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> La variable [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se incorporan a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar el flujo de datos, visite el tutorial en [supervisión de cuentas y flujos de datos en la interfaz de usuario](../../monitor.md).

## Actualizar el flujo de datos

Para actualizar las configuraciones de los flujos de datos, programar, asignar e información general, visite el tutorial en [actualización de flujos de datos de fuentes en la interfaz de usuario](../../update-dataflows.md)

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente empleando la función **[!UICONTROL Eliminar]** en la función **[!UICONTROL Flujos de datos]** espacio de trabajo. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial en [eliminación de flujos de datos en la interfaz de usuario](../../delete.md).