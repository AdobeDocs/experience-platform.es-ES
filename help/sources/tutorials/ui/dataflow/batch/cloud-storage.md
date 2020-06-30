---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuración de un flujo de datos para un conector por lotes de almacenamiento de nube en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 0%

---


# Configuración de un flujo de datos para un conector por lotes de almacenamiento de nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e ingiere datos de un origen a un [!DNL Platform] conjunto de datos. Este tutorial proporciona pasos para configurar un nuevo flujo de datos mediante el conector base del almacenamiento de nube.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado un conector de almacenamiento de nube. Encontrará una lista de tutoriales para crear diferentes conectores de almacenamiento en la interfaz de usuario en la descripción general [de los conectores](../../../../home.md)de origen.

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
* [!DNL JavaScript Object Notation] (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* [!DNL Apache Parquet]:: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

## Seleccionar datos

Después de crear el conector de almacenamiento de nube, aparece el paso *[!UICONTROL Seleccionar datos]* , que proporciona una interfaz interactiva para explorar la jerarquía de almacenamientos de nube.

* La mitad izquierda de la interfaz es un navegador de directorios, que muestra los archivos y directorios del servidor.
* La mitad derecha de la interfaz permite la previsualización de hasta 100 filas de datos desde un archivo compatible.

Si hace clic en una carpeta de la lista, podrá recorrer la jerarquía de carpetas para colocarla en carpetas más profundas. Una vez seleccionado un archivo o carpeta compatible, aparece la lista desplegable **[!UICONTROL Seleccionar formato]** de datos, donde puede elegir un formato para mostrar los datos en la ventana previsualización.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Una vez que se complete la ventana de previsualización, puede hacer clic en **[!UICONTROL Siguiente]** para cargar todos los archivos de la carpeta seleccionada. Si desea cargar en un archivo específico, selecciónelo en el listado antes de hacer clic en **[!UICONTROL Siguiente]**.

>[!NOTE] Los formatos de archivo admitidos son CSV, JSON y Parquet. Los archivos JSON y Parquet deben ser compatibles con XDM.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-next.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso *[!UICONTROL Asignación]* , que proporciona una interfaz interactiva para asignar los datos de origen a un [!DNL Platform] conjunto de datos. Los archivos de origen formateados en JSON o Parquet deben ser compatibles con XDM y no requieren la configuración manual de la asignación. Los archivos CSV, por el contrario, requieren que configure explícitamente la asignación, pero permiten elegir los campos de datos de origen que se asignarán.

Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede usar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para ingerir datos en un conjunto de datos existente, seleccione **[!UICONTROL Utilizar conjunto]** de datos existente y, a continuación, haga clic en el icono de conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Aparece el cuadro de diálogo _Seleccionar conjunto de datos_ . Busque el conjunto de datos que desee utilizar, selecciónelo y haga clic en **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-data.png)

**Usar un nuevo conjunto de datos**

Para ingestar datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Crear nuevo conjunto]** de datos e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. A continuación, haga clic en el icono de esquema.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-schema.png)

Aparecerá el cuadro de diálogo _Seleccionar esquema_ . Seleccione el esquema que desee aplicar al nuevo conjunto de datos y haga clic en **[!UICONTROL Finalizado]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

En función de sus necesidades, puede elegir asignar los campos directamente o utilizar funciones de asignador para transformar los datos de origen para derivar valores calculados o calculados. Para obtener más información sobre la asignación de datos y las funciones del asignador, consulte el tutorial sobre la [asignación de datos CSV a campos](../../../../../ingestion/tutorials/map-a-csv-file.md)de esquema XDM.

Una vez asignados los datos de origen, haga clic en **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

## Programar ejecuciones de ingestión

Aparece el paso *[!UICONTROL Programación]* , que le permite configurar una programación de ingestión para ingestar automáticamente los datos de origen seleccionados mediante las asignaciones configuradas. La siguiente tabla describe los diferentes campos configurables para la programación:

| Campo | Descripción |
| --- | --- |
| Frecuencia | Las frecuencias seleccionables incluyen Minuto, Hora, Día y Semana. |
| Intervalo | Un entero que establece el intervalo para la frecuencia seleccionada. |
| Tiempo de Inicio | Marca de hora UTC para la que se producirá la primera ingestión. |
| Rellenar | Un valor booleano que determina qué datos se ingieren inicialmente. Si *[!UICONTROL Rellenar]* está activado, todos los archivos actuales de la ruta especificada se ingerirán durante la primera ingestión programada. Si *[!UICONTROL Rellenar]* está desactivado, solo se ingerirán los archivos que se carguen entre la primera ejecución de la ingesta y el tiempo *[!UICONTROL de]* Inicio. Los archivos cargados antes de la hora *[!UICONTROL de]* Inicio no se ingieren. |

Los flujos de datos están diseñados para transferir datos automáticamente en forma programada. Si solo desea realizar una ingesta una vez a través de este flujo de trabajo, puede hacerlo configurando la **[!UICONTROL Frecuencia]** en &quot;Día&quot; y aplicando un número muy grande para el **[!UICONTROL intervalo]**, como 10000 o similar.

Proporcione valores para la programación y haga clic en **Siguiente**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling.png)

## Asigne un nombre al flujo de datos

Aparece el paso de flujo ** Nombre, que le permite asignar un nombre y una breve descripción al nuevo flujo de datos.

Proporcione valores para el flujo de datos y haga clic en **[!UICONTROL Siguiente]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/name-your-dataflow.png)

### Revise el flujo de datos

Aparece el paso *[!UICONTROL Revisar]* , que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* *[!UICONTROL Detalles]* de la fuente: Muestra el tipo de origen, la ruta de acceso relevante del archivo de origen seleccionado y la cantidad de columnas dentro de ese archivo de origen.
* *[!UICONTROL Detalles]* del Destinatario: Muestra en qué conjunto de datos se están ingeriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* *[!UICONTROL Detalles]* de programación: Muestra el período activo, la frecuencia y el intervalo del programa de ingestión.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitorear el flujo de datos

Una vez creado el flujo de datos del almacenamiento de nube, puede supervisar los datos que se están ingeriendo a través de él. Para obtener más información sobre la supervisión de conjuntos de datos, consulte el tutorial sobre la [supervisión de flujos de datos](../../../../../ingestion/quality/monitor-data-flows.md)de flujo continuo.

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para traer datos de un almacenamiento de nube externo y ha adquirido una perspectiva sobre la supervisión de conjuntos de datos. Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general sobre el Perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Información general sobre el área de trabajo de ciencias de datos](../../../../../data-science-workspace/home.md)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Deshabilitar un flujo de datos

Cuando se crea un flujo de datos, se activa inmediatamente y se ingieren datos según la programación que se le haya dado. Puede desactivar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

En el espacio de trabajo *[!UICONTROL Fuentes]* , haga clic en la ficha **[!UICONTROL Examinar]** . A continuación, haga clic en el nombre de la cuenta asociada al flujo de datos activo que desea deshabilitar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Aparece la página actividad ** de origen. Seleccione el flujo de datos activo de la lista para abrir su columna *[!UICONTROL Propiedades]* en el lado derecho de la pantalla, que contiene un botón de alternancia **[!UICONTROL Habilitado]** . Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos después de desactivarlo.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activar datos de entrada para [!DNL Profile] población

Los datos entrantes del conector de origen se pueden utilizar para enriquecer y rellenar [!DNL Real-time Customer Profile] los datos. Para obtener más información sobre cómo rellenar los datos de clientes reales [!DNL Profile] , consulte el tutorial sobre población [de](../../profile.md)Perfiles.
