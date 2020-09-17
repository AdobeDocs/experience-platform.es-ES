---
keywords: Experience Platform;home;popular topics;protocol connector
solution: Experience Platform
title: Configuración de un flujo de datos para un conector de protocolo en la interfaz de usuario
topic: overview
description: Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un conjunto de datos de Adobe Experience Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos mediante la cuenta de protocolos.
translation-type: tm+mt
source-git-commit: ad9b52e46d3eb4f6ed7774e4cbcb031a52801b49
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 0%

---


# Configuración de un flujo de datos para un conector de protocolo en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un conjunto de datos de Adobe Experience Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos mediante la cuenta de protocolos.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!Perfil del cliente en tiempo real de DNL]](../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado una cuenta de protocolos. Puede encontrar una lista de tutoriales para crear diferentes conectores de protocolo en la interfaz de usuario en la descripción general [de los conectores](../../../home.md)de origen.

## Seleccionar datos

Después de crear la cuenta de protocolos, aparece el paso **[!UICONTROL Seleccionar datos]** , que proporciona una interfaz interactiva para explorar la jerarquía de archivos.

- La mitad izquierda de la interfaz es un navegador de directorios, que muestra los archivos y directorios del servidor.
- La mitad derecha de la interfaz permite la previsualización de hasta 100 filas de datos desde un archivo compatible.

Puede utilizar la opción **[!UICONTROL Buscar]** en la parte superior de la página para identificar rápidamente los datos de origen que desee utilizar.

>[!NOTE]
>
>La opción de datos de origen de búsqueda está disponible para todos los conectores de origen basados en tabulaciones, excluyendo los conectores de Analytics, Clasificaciones, Eventos y Kinesis.

Una vez que encuentre los datos de origen, seleccione el directorio y haga clic en **[!UICONTROL Siguiente]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso **[!UICONTROL Asignación]** , que proporciona una interfaz interactiva para asignar los datos de origen a un [!DNL Platform] conjunto de datos.

Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede utilizar un conjunto de datos existente o crear un nuevo conjunto de datos.

### Usar un conjunto de datos existente

Para ingerir datos en un conjunto de datos existente, seleccione **[!UICONTROL Utilizar conjunto]** de datos existente y, a continuación, haga clic en el icono de conjunto de datos.

![use-existente-dataset](../../../images/tutorials/dataflow/protocols/use-existing-dataset.png)

Aparece el cuadro de diálogo **[!UICONTROL Seleccionar conjunto de datos]** . Busque el conjunto de datos que desee utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![select-existente-dataset](../../../images/tutorials/dataflow/protocols/select-existing-dataset.png)

### Usar un nuevo conjunto de datos

Para ingestar datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Crear nuevo conjunto]** de datos e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados.

Puede adjuntar un campo de esquema introduciendo un nombre de esquema en la barra de búsqueda **[!UICONTROL Seleccionar esquema]** . También puede seleccionar el icono desplegable para ver una lista de esquemas existentes. También puede seleccionar Búsqueda **** avanzada para acceder a la pantalla de esquemas existentes, incluidos sus respectivos detalles.

![create-new-dataset](../../../images/tutorials/dataflow/all-tabular/new-target-dataset.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Seleccionar esquema]** . Seleccione el esquema que desee aplicar al nuevo conjunto de datos y haga clic en **[!UICONTROL Finalizado]**.

![select-esquema](../../../images/tutorials/dataflow/protocols/select-existing-schema.png)

En función de sus necesidades, puede elegir asignar los campos directamente o utilizar funciones de asignador para transformar los datos de origen para derivar valores calculados o calculados. Para obtener más información sobre la asignación de datos y las funciones del asignador, consulte el tutorial sobre la [asignación de datos CSV a campos](../../../../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

>[!TIP]
>
>[!DNL Platform] proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema de destinatario o del conjunto de datos que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Seleccione los datos **[!UICONTROL de]** Previsualización para ver los resultados de asignación de hasta 100 filas de datos de muestra del conjunto de datos seleccionado.

Durante la previsualización, se da prioridad a la columna de identidad como primer campo, ya que es la información clave necesaria para validar los resultados de la asignación.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Una vez asignados los datos de origen, seleccione **[!UICONTROL Cerrar]**.

## Programar ejecuciones de ingestión

Aparece el paso **[!UICONTROL Programación]** , que le permite configurar una programación de ingestión para ingestar automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen `Once`, `Minute`, `Hour`, `Day`y `Week`. |
| Intervalo | Un entero que establece el intervalo para la frecuencia seleccionada. |
| Tiempo de inicio | Marca de hora UTC que indica cuándo se produce la primera ingestión. |
| Rellenar | Un valor booleano que determina qué datos se ingieren inicialmente. Si **[!UICONTROL Rellenar]** está activado, todos los archivos actuales de la ruta especificada se ingerirán durante la primera ingestión programada. Si **[!UICONTROL Rellenar]** está desactivado, solo se ingerirán los archivos que se carguen entre la primera ejecución de la ingesta y el tiempo **[!UICONTROL de]** Inicio. Los archivos cargados antes de la hora **[!UICONTROL de]** Inicio no se ingieren. |
| Columna delta | Una opción con un conjunto filtrado de campos de esquema de origen de tipo, fecha u hora. Este campo se utiliza para diferenciar entre datos nuevos y existentes. Los datos incrementales se ingieren según la marca de tiempo de la columna seleccionada. |

Los flujos de datos están diseñados para transferir datos automáticamente en forma programada. Inicio seleccionando la frecuencia de ingestión. A continuación, configure el intervalo para designar el período entre dos ejecuciones de flujo. El valor del intervalo debe ser un entero distinto de cero y debe establecerse en bueno o igual a 15.

Para establecer la hora de inicio para la ingestión, ajuste la fecha y la hora que se muestran en el cuadro de hora del inicio. También puede seleccionar el icono de calendario para editar el valor de tiempo del inicio. La hora de inicio debe ser buena o igual a la hora UTC actual.

Seleccione **[!UICONTROL Cargar datos incrementales por]** para asignar la columna delta. Este campo ofrece una distinción entre los datos nuevos y los existentes.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Configurar un flujo de datos de ingestión único

Para configurar la ingestión de una sola vez, seleccione la flecha desplegable de frecuencia y seleccione **[!UICONTROL Una vez]**.

>[!TIP]
>
>**[!UICONTROL El intervalo]** y el **[!UICONTROL relleno]** no son visibles durante una ingestión única.

Una vez que haya proporcionado los valores adecuados a la programación, seleccione **[!UICONTROL Siguiente]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Proporcionar detalles de flujo de datos

Aparece el paso de detalles **** de flujo de datos, que le permite asignar un nombre al nuevo flujo de datos y proporcionarle una breve descripción.

Durante este proceso, también puede activar los diagnósticos **[!UICONTROL de ingestión]** parcial y de **[!UICONTROL error]**. La activación de la ingestión **** parcial permite ingestar datos que contengan errores hasta un determinado umbral. Una vez habilitada la inserción **[!UICONTROL parcial]** , arrastre el **[!UICONTROL dial de umbral de error %]** para ajustar el umbral de error del lote. Como alternativa, puede ajustar manualmente el umbral seleccionando el cuadro de entrada. Para obtener más información, consulte la información general sobre la ingestión [parcial de lotes](../../../../ingestion/batch-ingestion/partial.md).

Proporcione valores para el flujo de datos y seleccione **[!UICONTROL Siguiente]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Revise el flujo de datos

Aparece el paso **[!UICONTROL Revisar]** , que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta de acceso relevante del archivo de origen seleccionado y la cantidad de columnas dentro de ese archivo de origen.
- **[!UICONTROL Asignar campos]** de conjunto de datos y mapa: Muestra en qué conjunto de datos se están ingeriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
- **[!UICONTROL Programación]**: Muestra el período activo, la frecuencia y el intervalo del programa de ingestión.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

![revisión](../../../images/tutorials/dataflow/protocols/review.png)

## Monitorear el flujo de datos

Una vez creado el flujo de datos, puede monitorear los datos que se están ingeriendo a través de él para ver información sobre tasas de ingestión, éxito y errores. Para obtener más información sobre cómo supervisar el flujo de datos, consulte el tutorial sobre la [supervisión de cuentas y flujos de datos en la interfaz de usuario](../monitor.md).

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Eliminar]** disponible en el espacio de trabajo **[!UICONTROL Flujos]** de datos. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre la [eliminación de flujos de datos en la interfaz de usuario](../delete.md).

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para incorporar datos de un sistema de automatización de marketing y ha adquirido una perspectiva sobre la supervisión de conjuntos de datos. Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [[!DNL Real-time Customer Profile] sobre validación](../../../../profile/home.md)
- [[!DNL Data Science Workspace] sobre validación](../../../../data-science-workspace/home.md)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Deshabilitar un flujo de datos

Cuando se crea un flujo de datos, se activa inmediatamente y se ingieren datos según la programación que se le haya dado. Puede desactivar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

En la pantalla **[!UICONTROL Flujos]** de datos, seleccione el nombre del flujo de datos que desea deshabilitar.

![browse-dataset-flow](../../../images/tutorials/dataflow/protocols/view-dataset-flows.png)

La columna **[!UICONTROL Propiedades]** aparece en la parte derecha de la pantalla. Este panel contiene un botón de alternancia **[!UICONTROL activado]** . Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos después de desactivarlo.

![disable](../../../images/tutorials/dataflow/protocols/disable.png)

### Activar datos de entrada para [!DNL Profile] población

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar [!DNL Real-time Customer Profile] los datos. Para obtener más información sobre cómo rellenar [!DNL Real-time Customer Profile] los datos, consulte el tutorial sobre población [de](../profile.md)Perfiles.