---
keywords: Experience Platform;inicio;temas populares;flujo de datos;flujo de datos
solution: Experience Platform
title: Configurar un flujo de datos para un conector por lotes de almacenamiento en la nube en la interfaz de usuario
topic: overview
type: Tutorial
description: Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.
translation-type: tm+mt
source-git-commit: 1fb4a272a914bf4ce7653f3f4f7fff63f36f9a48
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 0%

---


# Configurar un flujo de datos para una conexión por lotes de almacenamiento en la nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos [!DNL Platform]. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que tenga una cuenta de almacenamiento en la nube establecida. Puede encontrar una lista de tutoriales para crear distintas cuentas de almacenamiento en la nube en la interfaz de usuario en la [información general de conectores de origen](../../../../home.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

* Valores separados por delimitadores (DSV): Cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

## Seleccionar datos

Después de crear su cuenta de almacenamiento en la nube, aparece el paso **[!UICONTROL Select data]**, que proporciona una interfaz para explorar la jerarquía de archivos de almacenamiento en la nube.

* La parte izquierda de la interfaz es un explorador de directorios, que muestra sus archivos y directorios de almacenamiento en la nube.
* La parte derecha de la interfaz permite previsualizar hasta 100 filas de datos de un archivo compatible.

![interfaz](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

La selección de una carpeta de la lista permite recorrer la jerarquía de carpetas en carpetas más profundas. Puede seleccionar una sola carpeta para introducir todos los archivos de la carpeta de forma recursiva. Al ingerir una carpeta completa, debe asegurarse de que todos los archivos de la carpeta compartan el mismo esquema.

Una vez que haya seleccionado un archivo o carpeta compatible, seleccione el formato de datos correspondiente en el menú desplegable [!UICONTROL Select data format].

La tabla siguiente muestra el formato de datos adecuado para los tipos de archivo admitidos:

| Tipo de archivo | Formato de datos |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parqué | [!UICONTROL Parqué XDM] |

Seleccione **[!UICONTROL JSON]** y espere unos segundos para que se complete la interfaz de vista previa.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>A diferencia de los tipos de archivo delimitados y JSON, los archivos con formato de parquet no están disponibles para la vista previa.

La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. De forma predeterminada, la interfaz de vista previa muestra el primer archivo de la carpeta seleccionada.

Para obtener una vista previa de un archivo diferente, seleccione el icono de vista previa junto al nombre del archivo que desea inspeccionar.

![default-preview](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

Una vez que haya inspeccionado el contenido y la estructura de los archivos de la carpeta, seleccione **[!UICONTROL Next]** para introducir todos los archivos de la carpeta de forma recursiva.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Si prefiere seleccionar un archivo específico, seleccione el archivo que desea ingerir y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Definir un delimitador personalizado para archivos delimitados

Puede establecer un delimitador personalizado al introducir archivos delimitados. Seleccione la opción **[!UICONTROL Delimiter]** y, a continuación, seleccione un delimitador en el menú desplegable. El menú muestra las opciones más utilizadas para los delimitadores, como una coma (`,`), una pestaña (`\t`) y una barra vertical (`|`). Si prefiere usar un delimitador personalizado, seleccione **[!UICONTROL Personalizado]** e introduzca un delimitador de un solo carácter de su elección en la barra de entrada emergente.

Una vez que haya seleccionado el formato de los datos y establecido el delimitador, seleccione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso **[!UICONTROL Mapping]**, que proporciona una interfaz interactiva para asignar los datos de origen a un conjunto de datos [!DNL Platform]. Los archivos de origen formateados en Parquet deben ser compatibles con XDM y no requieren que configure manualmente la asignación, mientras que los archivos CSV requieren que configure explícitamente la asignación, pero permiten seleccionar qué campos de datos de origen asignar. Los archivos JSON, si se marcan como quejas de XDM, no requieren configuración manual. Sin embargo, si no está marcado como compatible con XDM, necesitará que configure explícitamente la asignación.

Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede utilizar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, seleccione el icono del conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Aparece el cuadro de diálogo **[!UICONTROL Seleccionar conjunto de datos]**. Busque el conjunto de datos que desea utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Usar un nuevo conjunto de datos**

Para introducir datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Para añadir un esquema, puede introducir un nombre de esquema existente en el cuadro de diálogo **[!UICONTROL Select schema]**. También puede seleccionar la **[!UICONTROL Búsqueda avanzada del esquema]** para buscar un esquema apropiado.

Durante este paso, puede habilitar su conjunto de datos para [!DNL Real-time Customer Profile] y crear una vista holística de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados se incluirán en [!DNL Profile] y los cambios se aplicarán cuando guarde el flujo de datos.

Alterne el botón **[!UICONTROL Profile dataset]** para habilitar el conjunto de datos de destinatario para [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

Aparece el cuadro de diálogo **[!UICONTROL Select schema]**. Seleccione el esquema que desea aplicar al nuevo conjunto de datos y, a continuación, seleccione **[!UICONTROL Listo]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de asignador para transformar los datos de origen a fin de derivar valores calculados o calculados. Para obtener más información sobre las funciones de asignación y asignación de datos, consulte el tutorial sobre [asignación de datos CSV a campos de esquema XDM](../../../../../ingestion/tutorials/map-a-csv-file.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

En el caso de los archivos JSON, además de asignar directamente los campos a otros campos, puede asignar directamente objetos a otros objetos y matrices a otras matrices. También puede obtener una vista previa y asignar tipos de datos complejos, como matrices en archivos JSON, mediante un conector de origen de almacenamiento en la nube.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Tenga en cuenta que no puede asignar entre distintos tipos. Por ejemplo, no se puede asignar un objeto a una matriz ni a un campo a un objeto.

>[!TIP]
>
>[!DNL Platform] proporciona recomendaciones inteligentes para campos asignados automáticamente basadas en el esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

Seleccione **[!UICONTROL Preview data]** para ver los resultados de asignación de hasta 100 filas de datos de ejemplo del conjunto de datos seleccionado.

Durante la vista previa, la columna de identidad se prioriza como el primer campo, ya que es la información clave necesaria al validar los resultados de la asignación.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Una vez asignados los datos de origen, seleccione **[!UICONTROL Close]**.

## Programar ejecuciones de ingesta

Aparece el paso **[!UICONTROL Scheduling]** , que le permite configurar una programación de ingesta para que ingrese automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day` y `Week`. |
| Intervalo | Un entero que define el intervalo para la frecuencia seleccionada. |
| Hora de inicio | Marca de tiempo UTC que indica cuándo se configura la primera ingesta. |
| Relleno | Un valor booleano que determina qué datos se introducen inicialmente. Si **[!UICONTROL Relleno de fondo]** está habilitado, todos los archivos actuales de la ruta especificada se incorporarán durante la primera ingesta programada. Si **[!UICONTROL Backfill]** está deshabilitado, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

Los flujos de datos están diseñados para introducir datos automáticamente y de forma programada. Comience por seleccionar la frecuencia de ingesta. A continuación, configure el intervalo para designar el periodo entre dos ejecuciones de flujo. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15.

Para definir la hora de inicio de la ingesta, ajuste la fecha y la hora que se muestran en el cuadro de hora de inicio. También puede seleccionar el icono de calendario para editar el valor de la hora de inicio. La hora de inicio debe ser buena o igual a la hora actual en UTC.

Proporcione valores para la programación y seleccione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configurar un flujo de datos de ingesta único

Para configurar la ingesta única, seleccione la flecha desplegable de frecuencia y seleccione **[!UICONTROL Once]**. Puede seguir realizando modificaciones en un conjunto de flujos de datos para una ingesta de frecuencia única, siempre y cuando la hora de inicio permanezca en el futuro. Una vez que ha pasado la hora de inicio, ya no se puede editar el valor de frecuencia de una sola vez. **** El  **** relleno de intervalación no es visible al configurar un flujo de datos de ingesta único.

>[!IMPORTANT]
>
>Se recomienda programar el flujo de datos para una ingesta única al utilizar el [conector FTP](../../../../connectors/cloud-storage/ftp.md).

Una vez que haya proporcionado los valores adecuados a la programación, seleccione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Proporcionar detalles de flujo de datos

Aparece el paso **[!UICONTROL Dataflow detail]**, que le permite dar un nombre y una breve descripción del nuevo flujo de datos.

Durante este proceso, también puede habilitar la **[!UICONTROL ingesta parcial]** y los **[!UICONTROL diagnósticos de error]**. Al habilitar la **[!UICONTROL ingesta parcial]** se puede ingerir datos que contengan errores, hasta un umbral determinado que se pueda establecer. Al habilitar **[!UICONTROL Error diagnostic]** se proporcionarán detalles sobre cualquier dato incorrecto que se haya enviado por lotes por separado. Para obtener más información, consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md).

Proporcione valores para el flujo de datos y seleccione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Revise el flujo de datos

Aparece el paso **[!UICONTROL Review]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos]** de conjunto de datos y asignación: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el período, la frecuencia y el intervalo activos del programa de ingesta.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finish]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se incorporan a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar el flujo de datos, consulte el tutorial sobre [monitorización de cuentas y flujos de datos en la interfaz de usuario](../../monitor.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente empleando la función **[!UICONTROL Delete]** disponible en el espacio de trabajo **[!UICONTROL Dataflows]**. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre la [eliminación de flujos de datos en la interfaz de usuario](../../delete.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para incorporar datos de un almacenamiento en la nube externo y ha obtenido información sobre la monitorización de conjuntos de datos. Para obtener más información sobre la creación de flujos de datos, puede complementar su aprendizaje viendo el siguiente vídeo. Además, los datos entrantes ahora se pueden usar en servicios descendentes [!DNL Platform] como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* Información general del [[!DNL Real-time Customer Profile] ](../../../../../profile/home.md)
* Información general del [[!DNL Data Science Workspace] ](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> La interfaz de usuario [!DNL Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Desactivación de un flujo de datos

Cuando se crea un flujo de datos, este se activa inmediatamente e ingresa los datos según la programación que se le haya dado. Puede deshabilitar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

Dentro del espacio de trabajo **[!UICONTROL Sources]** , haga clic en la pestaña **[!UICONTROL Browse]**. A continuación, haga clic en el nombre de la cuenta asociada al flujo de datos activo que desea desactivar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Aparece la página **[!UICONTROL Source activity]**. Seleccione el flujo de datos activo de la lista para abrir su columna **[!UICONTROL Properties]** en el lado derecho de la pantalla, que contiene un botón de alternancia **[!UICONTROL Enabled]**. Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos una vez desactivado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activar datos de entrada para la población [!DNL Profile]

Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar los datos [!DNL Real-time Customer Profile]. Para obtener más información sobre cómo rellenar los datos [!DNL Real-time Customer Profile], consulte el tutorial sobre [Población del perfil](../../profile.md).
