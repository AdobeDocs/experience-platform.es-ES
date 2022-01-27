---
keywords: Experience Platform;inicio;temas populares;flujo de datos;flujo de datos
solution: Experience Platform
title: Configurar un flujo de datos para un conector por lotes de almacenamiento en la nube en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 86d8313d7acea41e7b3bcea6554e91ea2190ae69
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# Configurar un flujo de datos para una conexión por lotes de almacenamiento en la nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un [!DNL Platform] conjunto de datos. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que tenga una cuenta de almacenamiento en la nube establecida. Puede encontrar una lista de tutoriales para crear distintas cuentas de almacenamiento en la nube en la interfaz de usuario de [información general sobre conectores de origen](../../../../home.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

* Valores separados por delimitadores (DSV): Cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]: Los archivos de datos con formato de parqué deben ser compatibles con XDM.
* Archivos comprimidos: Los archivos JSON y delimitados se pueden comprimir como: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`y `tar`.

## Seleccionar datos

Después de crear su cuenta de almacenamiento en la nube, la variable **[!UICONTROL Seleccionar datos]** aparece, proporcionando una interfaz para explorar la jerarquía de archivos de almacenamiento en la nube.

* La parte izquierda de la interfaz es un explorador de directorios, que muestra sus archivos y directorios de almacenamiento en la nube.
* La parte derecha de la interfaz permite previsualizar hasta 100 filas de datos de un archivo compatible.

![interfaz](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

La selección de una carpeta de la lista permite recorrer la jerarquía de carpetas en carpetas más profundas. Puede seleccionar una sola carpeta para introducir todos los archivos de la carpeta de forma recursiva. Al ingerir una carpeta completa, debe asegurarse de que todos los archivos de la carpeta compartan el mismo esquema.

Una vez que haya seleccionado un archivo o carpeta compatible, seleccione el formato de datos correspondiente en la [!UICONTROL Seleccionar formato de datos] menú desplegable.

La tabla siguiente muestra el formato de datos adecuado para los tipos de archivo admitidos:

| Tipo de archivo | Formato de datos |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parqué | [!UICONTROL Parqué XDM] |

Select **[!UICONTROL JSON]** y espere unos segundos para que se complete la interfaz de vista previa.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>A diferencia de los tipos de archivo delimitados y JSON, los archivos con formato de parquet no están disponibles para la vista previa.

La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. De forma predeterminada, la interfaz de vista previa muestra el primer archivo de la carpeta seleccionada.

Para obtener una vista previa de un archivo diferente, seleccione el icono de vista previa junto al nombre del archivo que desea inspeccionar.

![default-preview](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

Una vez que haya inspeccionado el contenido y la estructura de los archivos de la carpeta, seleccione **[!UICONTROL Siguiente]** para introducir todos los archivos de la carpeta de forma recursiva.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Si prefiere seleccionar un archivo específico, seleccione el archivo que desea ingerir y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Definir un delimitador personalizado para archivos delimitados

Puede establecer un delimitador personalizado al introducir archivos delimitados. Seleccione el **[!UICONTROL Delimitador]** y, a continuación, seleccione un delimitador en el menú desplegable. El menú muestra las opciones más utilizadas para los delimitadores, incluida una coma (`,`), una pestaña (`\t`) y una barra vertical (`|`). Si prefiere usar un delimitador personalizado, seleccione **[!UICONTROL Personalizado]** e introduzca un delimitador de un solo carácter de su elección en la barra de entrada emergente.

Una vez que haya seleccionado el formato de datos y haya definido el delimitador, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Ingesta de archivos comprimidos

Puede introducir archivos JSON comprimidos o delimitados especificando su tipo de compresión.

En el [!UICONTROL Seleccionar datos] , seleccione un archivo comprimido para la ingesta y, a continuación, seleccione su tipo de archivo adecuado y si es compatible con XDM o no. A continuación, seleccione **[!UICONTROL Tipo de compresión]** y, a continuación, seleccione el tipo de archivo comprimido apropiado para los datos de origen.

Con un tipo de archivo comprimido identificado, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## Asignación de campos de datos a un esquema XDM

La variable **[!UICONTROL Asignación]** aparece, proporcionando una interfaz interactiva para asignar los datos de origen a un [!DNL Platform] conjunto de datos. Los archivos de origen formateados en Parquet deben ser compatibles con XDM y no requieren que configure manualmente la asignación, mientras que los archivos CSV requieren que configure explícitamente la asignación, pero permiten seleccionar qué campos de datos de origen asignar. Los archivos JSON, si se marcan como quejas de XDM, no requieren configuración manual. Sin embargo, si no está marcado como compatible con XDM, necesitará que configure explícitamente la asignación.

Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede utilizar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, seleccione el icono del conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

La variable **[!UICONTROL Seleccionar conjunto de datos]** se abre. Busque el conjunto de datos que desea utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Usar un nuevo conjunto de datos**

Para introducir datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Para añadir un esquema, puede introducir un nombre de esquema existente en la **[!UICONTROL Seleccionar esquema]** para abrir el Navegador. También puede seleccionar el **[!UICONTROL Búsqueda avanzada de esquema]** para buscar un esquema adecuado.

Durante este paso, puede habilitar su conjunto de datos para [!DNL Real-time Customer Profile] y crear una vista holística de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados se incluirán en [!DNL Profile] Los cambios y se aplican cuando guarda el flujo de datos.

Alternar el **[!UICONTROL Conjunto de datos del perfil]** para habilitar el conjunto de datos de target [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

La variable **[!UICONTROL Seleccionar esquema]** se abre. Seleccione el esquema que desee aplicar al nuevo conjunto de datos y, a continuación, seleccione **[!UICONTROL Listo]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](../../../../../data-prep/ui/mapping.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

En el caso de los archivos JSON, además de asignar directamente los campos a otros campos, puede asignar directamente objetos a otros objetos y matrices a otras matrices. También puede obtener una vista previa y asignar tipos de datos complejos, como matrices en archivos JSON, mediante un conector de origen de almacenamiento en la nube.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Tenga en cuenta que no puede asignar entre distintos tipos. Por ejemplo, no se puede asignar un objeto a una matriz ni a un campo a un objeto.

>[!TIP]
>
>Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

Select **[!UICONTROL Vista previa de datos]** para ver los resultados de asignación de hasta 100 filas de datos de ejemplo del conjunto de datos seleccionado.

Durante la vista previa, la columna de identidad se prioriza como el primer campo, ya que es la información clave necesaria al validar los resultados de la asignación.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Una vez asignados los datos de origen, seleccione **[!UICONTROL Cerrar]**.

## Programar ejecuciones de ingesta

La variable **[!UICONTROL Programación]** , lo que le permite configurar una programación de ingesta para que ingrese automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`y `Week`. |
| Intervalo | Un entero que define el intervalo para la frecuencia seleccionada. |
| Hora de inicio | Marca de tiempo UTC que indica cuándo se configura la primera ingesta. |
| Relleno | Un valor booleano que determina qué datos se introducen inicialmente. If **[!UICONTROL Relleno]** está activada, todos los archivos actuales de la ruta especificada se incorporarán durante la primera ingesta programada. If **[!UICONTROL Relleno]** está desactivado, solo se introducen los archivos que se cargan entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

Los flujos de datos están diseñados para introducir datos automáticamente y de forma programada. Comience por seleccionar la frecuencia de ingesta. A continuación, configure el intervalo para designar el periodo entre dos ejecuciones de flujo. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15.

Para definir la hora de inicio de la ingesta, ajuste la fecha y la hora que se muestran en el cuadro de hora de inicio. También puede seleccionar el icono de calendario para editar el valor de la hora de inicio. La hora de inicio debe ser buena o igual a la hora actual en UTC.

Proporcione valores para la programación y seleccione **[!UICONTROL Siguiente]**.

>[!NOTE]
>
>Para la ingesta por lotes, cada flujo de datos resultante selecciona los archivos que se van a ingerir de su origen en función de sus **última modificación** marca de tiempo. Esto significa que los flujos de datos por lotes seleccionan los archivos del origen que son nuevos o que se han modificado desde la última ejecución del flujo. Además, debe asegurarse de que haya un lapso de tiempo suficiente entre la carga de archivos y la ejecución de un flujo programado, ya que es posible que los archivos que no se carguen completamente en la cuenta de almacenamiento en la nube antes del tiempo de ejecución del flujo programado no se recojan para su incorporación.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configurar un flujo de datos de ingesta único

Para configurar la ingesta única, seleccione la flecha desplegable de frecuencia y seleccione **[!UICONTROL Una vez]**. Puede seguir realizando modificaciones en un conjunto de flujos de datos para una ingesta de frecuencia única, siempre y cuando la hora de inicio permanezca en el futuro. Una vez que ha pasado la hora de inicio, ya no se puede editar el valor de frecuencia de una sola vez. **[!UICONTROL Intervalo]** y **[!UICONTROL Relleno]** no están visibles al configurar un flujo de datos de ingesta único.

>[!IMPORTANT]
>
>Se recomienda programar el flujo de datos para una ingesta única al usar la variable [Conector FTP](../../../../connectors/cloud-storage/ftp.md).

Una vez que haya proporcionado los valores adecuados a la programación, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Proporcionar detalles de flujo de datos

La variable **[!UICONTROL Detalles de flujo de datos]** aparece, lo que le permite asignar un nombre y describir brevemente el nuevo flujo de datos.

Durante este proceso, también puede habilitar **[!UICONTROL Ingesta parcial]** y **[!UICONTROL Diagnóstico de errores]**. Habilitación **[!UICONTROL Ingesta parcial]** proporciona la capacidad de ingerir datos que contengan errores, hasta un umbral determinado que se pueda definir. Habilitación **[!UICONTROL Diagnóstico de errores]** proporcionará detalles sobre cualquier dato incorrecto que se haya enviado por lotes por separado. Para obtener más información, consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md).

Proporcione valores para el flujo de datos y seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Revise el flujo de datos

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el período, la frecuencia y el intervalo activos del programa de ingesta.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se incorporan a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar el flujo de datos, consulte el tutorial en [supervisión de cuentas y flujos de datos en la interfaz de usuario](../../monitor.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente empleando la función **[!UICONTROL Eliminar]** en la función **[!UICONTROL Flujos de datos]** espacio de trabajo. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminación de flujos de datos en la interfaz de usuario](../../delete.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para incorporar datos de un almacenamiento en la nube externo y ha obtenido información sobre la monitorización de conjuntos de datos. Para obtener más información sobre la creación de flujos de datos, puede complementar su aprendizaje viendo el siguiente vídeo. Además, los datos entrantes ahora se pueden utilizar en el flujo descendente [!DNL Platform] servicios como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> La variable [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Desactivación de un flujo de datos

Cuando se crea un flujo de datos, este se activa inmediatamente e ingresa los datos según la programación que se le haya dado. Puede deshabilitar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

Dentro de **[!UICONTROL Fuentes]** espacio de trabajo, haga clic en **[!UICONTROL Examinar]** pestaña . A continuación, haga clic en el nombre de la cuenta asociada al flujo de datos activo que desea desactivar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La variable **[!UICONTROL Actividad de origen]** se abre. Seleccione el flujo de datos activo de la lista para abrir su **[!UICONTROL Propiedades]** a la derecha de la pantalla, que contiene un **[!UICONTROL Habilitado]** botón de alternancia. Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos una vez desactivado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activar datos de entrada para [!DNL Profile] población

Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar el [!DNL Real-time Customer Profile] datos. Para obtener más información sobre cómo rellenar la variable [!DNL Real-time Customer Profile] datos, consulte el tutorial en [Población del perfil](../../profile.md).
