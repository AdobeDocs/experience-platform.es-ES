---
keywords: Experience Platform;home;popular topics;dataflow;Dataflow
solution: Experience Platform
title: Configuración de un flujo de datos para un conector por lotes de almacenamiento de nube en la interfaz de usuario
topic: overview
description: Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un conjunto de datos de la Plataforma. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.
translation-type: tm+mt
source-git-commit: 63eb8407617cda64f3f3b0cefd6bf427314e0216
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 0%

---


# Configuración de un flujo de datos para un conector por lotes de almacenamiento de nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un [!DNL Platform] conjunto de datos. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su cuenta de almacenamiento en la nube.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que tenga una cuenta de almacenamiento en la nube establecida. Encontrará una lista de tutoriales para crear distintas cuentas de almacenamiento en la nube en la interfaz de usuario en la descripción general [de los conectores](../../../../home.md)de origen.

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]:: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

## Seleccionar datos

Después de crear la cuenta de almacenamiento en la nube, aparece el paso **[!UICONTROL Seleccionar datos]** , que proporciona una interfaz interactiva para explorar la jerarquía de almacenamientos en la nube.

* La mitad izquierda de la interfaz es un navegador de directorios, que muestra los archivos y directorios del servidor.
* La mitad derecha de la interfaz permite la previsualización de hasta 100 filas de datos desde un archivo compatible.

La selección de una carpeta de la lista permite recorrer la jerarquía de carpetas en carpetas más profundas. Una vez seleccionado un archivo o carpeta compatible, aparece la lista desplegable **[!UICONTROL Seleccionar formato]** de datos, donde puede elegir un formato para mostrar los datos en la ventana previsualización.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Una vez que se complete la ventana de previsualización, puede seleccionar **[!UICONTROL Siguiente]** para cargar todos los archivos de la carpeta seleccionada. Si desea cargar en un archivo específico, seleccione ese archivo en el listado antes de seleccionar **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-preview.png)

### Ingesta de archivos de parqué o JSON

Los formatos de archivo admitidos para una cuenta de almacenamiento en la nube también incluyen JSON y Parquet. Los archivos JSON y Parquet deben ser compatibles con XDM. Para ingestar archivos JSON o Parquet, seleccione el formato de archivo adecuado en el navegador de directorios y aplique un formato de datos compatible desde la interfaz correcta. Seleccione **[!UICONTROL Siguiente]** para continuar.

>[!IMPORTANT]
>
>A diferencia de los tipos de archivo delimitados, los archivos con formato JSON y Parquet no están disponibles para la previsualización.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso **[!UICONTROL Asignación]** , que proporciona una interfaz interactiva para asignar los datos de origen a un [!DNL Platform] conjunto de datos. Los archivos de origen formateados en JSON o Parquet deben ser compatibles con XDM y no requieren la configuración manual de la asignación. Los archivos CSV, por el contrario, requieren que configure explícitamente la asignación, pero permiten elegir los campos de datos de origen que se asignarán.

Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede usar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para ingerir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos]** existente y, a continuación, seleccione el icono de conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Aparece el cuadro de diálogo **[!UICONTROL Seleccionar conjunto de datos]** . Busque el conjunto de datos que desee utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Usar un nuevo conjunto de datos**

Para ingestar datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto]** de datos e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Para agregar un esquema, puede introducir un nombre de esquema existente en el cuadro de diálogo **[!UICONTROL Seleccionar esquema]** . También puede seleccionar la búsqueda **[!UICONTROL avanzada de]** Esquema para buscar un esquema adecuado.

Durante este paso, puede habilitar el conjunto de datos [!DNL Real-time Customer Profile] y crear una vista holística de los atributos y comportamientos de una entidad. Se incluirán los datos de todos los conjuntos de datos habilitados [!DNL Profile] y se aplicarán los cambios al guardar el flujo de datos.

Alterne el botón **[!UICONTROL Perfil dataset]** para habilitar el conjunto de datos de destinatario para [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Seleccionar esquema]** . Seleccione el esquema que desea aplicar al nuevo conjunto de datos y, a continuación, seleccione **[!UICONTROL Listo]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

En función de sus necesidades, puede elegir asignar los campos directamente o utilizar funciones de asignador para transformar los datos de origen para derivar valores calculados o calculados. Para obtener más información sobre la asignación de datos y las funciones del asignador, consulte el tutorial sobre la [asignación de datos CSV a campos](../../../../../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

>[!TIP]
>
>[!DNL Platform] proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema de destinatario o del conjunto de datos que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Seleccione los datos **[!UICONTROL de]** Previsualización para ver los resultados de asignación de hasta 100 filas de datos de muestra del conjunto de datos seleccionado.

Durante la previsualización, se da prioridad a la columna de identidad como primer campo, ya que es la información clave necesaria para validar los resultados de la asignación.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Una vez asignados los datos de origen, seleccione **[!UICONTROL Cerrar]**.

## Programar ejecuciones de ingestión

Aparece el paso **[!UICONTROL Programación]** , que le permite configurar una programación de ingestión para ingestar automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`y `Week`. |
| Intervalo | Un entero que establece el intervalo para la frecuencia seleccionada. |
| Tiempo de inicio | Marca de hora UTC que indica cuándo se produce la primera ingestión. |
| Rellenar | Un valor booleano que determina qué datos se ingieren inicialmente. Si **[!UICONTROL Rellenar]** está activado, todos los archivos actuales de la ruta especificada se ingerirán durante la primera ingestión programada. Si **[!UICONTROL Rellenar]** está desactivado, solo se ingerirán los archivos que se carguen entre la primera ejecución de la ingesta y el tiempo **[!UICONTROL de]** Inicio. Los archivos cargados antes de la hora **[!UICONTROL de]** Inicio no se ingieren. |

Los flujos de datos están diseñados para transferir datos automáticamente en forma programada. Inicio seleccionando la frecuencia de ingestión. A continuación, configure el intervalo para designar el período entre dos ejecuciones de flujo. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15.

Para establecer la hora de inicio para la ingestión, ajuste la fecha y la hora que se muestran en el cuadro de hora del inicio. También puede seleccionar el icono de calendario para editar el valor de tiempo del inicio. La hora de inicio debe ser buena o igual a la hora actual en UTC.

Proporcione valores para la programación y seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configurar un flujo de datos de ingestión único

Para configurar la ingestión de una sola vez, seleccione la flecha desplegable de frecuencia y seleccione **[!UICONTROL Una vez]**. Puede seguir editando en un conjunto de flujos de datos para una ingestión de frecuencia única, siempre y cuando el tiempo de inicio permanezca en el futuro. Una vez transcurrido el tiempo de inicio, ya no se puede editar el valor de frecuencia de una sola vez.

>[!TIP]
>
>**[!UICONTROL El intervalo]** y el **[!UICONTROL relleno]** no son visibles durante una ingestión única.

Una vez que haya proporcionado los valores adecuados a la programación, seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Proporcionar detalles de flujo de datos

Aparece el paso de detalles **** de flujo de datos, que le permite asignar un nombre y una breve descripción del nuevo flujo de datos.

Durante este proceso, también puede activar los diagnósticos **[!UICONTROL de ingestión]** parcial y de **[!UICONTROL error]**. La activación de la ingestión **** parcial permite ingestar datos que contengan errores, hasta un umbral determinado que se pueda establecer. Al habilitar los diagnósticos **[!UICONTROL de]** error se proporcionarán detalles sobre los datos incorrectos que se agrupan por lotes por separado. Para obtener más información, consulte la información general sobre la ingestión [parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md).

Proporcione valores para el flujo de datos y seleccione **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Revise el flujo de datos

Aparece el paso **[!UICONTROL Revisar]** , que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta de acceso relevante del archivo de origen seleccionado y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos]** de conjunto de datos y mapa: Muestra en qué conjunto de datos se están ingeriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **[!UICONTROL Programación]**: Muestra el período activo, la frecuencia y el intervalo del programa de ingestión.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitorear el flujo de datos

Una vez creado el flujo de datos, puede monitorear los datos que se están ingeriendo a través de él para ver información sobre tasas de ingestión, éxito y errores. Para obtener más información sobre cómo supervisar el flujo de datos, consulte el tutorial sobre la [supervisión de cuentas y flujos de datos en la interfaz de usuario](../../monitor.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Eliminar]** disponible en el espacio de trabajo **[!UICONTROL Flujos]** de datos. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre la [eliminación de flujos de datos en la interfaz de usuario](../../delete.md).

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para traer datos de un almacenamiento de nube externo y ha adquirido una perspectiva sobre la supervisión de conjuntos de datos. Para obtener más información sobre la creación de flujos de datos, puede complementar su aprendizaje viendo el siguiente vídeo. Además, los datos entrantes ahora pueden ser utilizados por servicios de flujo [!DNL Platform] descendente como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [[!DNL Real-time Customer Profile] sobre validación](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] sobre validación](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> La interfaz de usuario que [!DNL Platform] se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Deshabilitar un flujo de datos

Cuando se crea un flujo de datos, se activa inmediatamente y se ingieren datos según la programación que se le haya dado. Puede desactivar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

En el espacio de trabajo **[!UICONTROL Fuentes]** , haga clic en la ficha **[!UICONTROL Examinar]** . A continuación, haga clic en el nombre de la cuenta asociada al flujo de datos activo que desea deshabilitar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Aparece la página actividad **** de origen. Seleccione el flujo de datos activo de la lista para abrir su columna **[!UICONTROL Propiedades]** en el lado derecho de la pantalla, que contiene un botón de alternancia **[!UICONTROL Habilitado]** . Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos después de desactivarlo.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activar datos de entrada para [!DNL Profile] población

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar [!DNL Real-time Customer Profile] los datos. Para obtener más información sobre cómo rellenar [!DNL Real-time Customer Profile] los datos, consulte el tutorial sobre población [de](../../profile.md)Perfiles.
