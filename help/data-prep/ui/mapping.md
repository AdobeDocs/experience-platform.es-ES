---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;asignador;asignación;preparación de datos;preparación de datos;
title: Guía de IU de preparación de datos
description: Este documento proporciona instrucciones sobre cómo utilizar las funciones de preparación de datos en la interfaz de usuario de Platform para asignar archivos CSV a un esquema XDM.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 1%

---

# Guía de IU de preparación de datos

Este documento proporciona instrucciones sobre cómo utilizar las funciones de preparación de datos en la interfaz de usuario de Adobe Experience Platform para asignar archivos CSV a un esquema XDM.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [Servicio de identidad](../../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Fuentes](../../sources/home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.

## Detalles del flujo de datos

>[!TIP]
>
>Puede acceder a los detalles del flujo de datos seleccionando cualquier fuente del catálogo de fuentes. Para obtener más información, consulte [descripción general de orígenes](../../sources/home.md).

Antes de poder asignar los datos CSV a un esquema XDM, primero debe establecer los detalles del flujo de datos.

La página [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea introducir los datos CSV en un conjunto de datos de destino existente o en un nuevo conjunto de datos de destino. Un conjunto de datos existente viene con un esquema de destino generado previamente al que asignar los datos, mientras que un nuevo conjunto de datos requiere que seleccione un esquema existente o cree un nuevo esquema para asignar los datos.

### Usar un conjunto de datos de destinatario existente

Para introducir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable.

Con un conjunto de datos seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional.

Durante este proceso, también puede habilitar [!UICONTROL diagnósticos de error] e [!UICONTROL ingesta parcial]. [!UICONTROL Diagnósticos de error] permite la generación detallada de mensajes de error para cualquier registro erróneo que ocurra en su flujo de datos, mientras que [!UICONTROL Ingesta parcial] le permite ingerir datos que contengan errores, hasta un determinado umbral que usted defina manualmente. Consulte la [descripción general de la ingesta parcial por lotes](../../ingestion/batch-ingestion/partial.md) para obtener más información.

![conjunto de datos existente](../images/ui/mapping/existing-dataset.png)

### Usar un nuevo conjunto de datos de destinatario

Para introducir los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre de conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar con la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable.

Con un esquema seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional y, a continuación, aplique la configuración de [!UICONTROL diagnósticos de error] e [!UICONTROL ingesta parcial] que desee para el flujo de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![nuevo conjunto de datos](../images/ui/mapping/new-dataset.png)

## Seleccionar datos

Aparecerá el paso [!UICONTROL Seleccionar datos], que le proporcionará una interfaz para cargar los archivos locales y obtener una vista previa de su estructura y contenido. Seleccione **[!UICONTROL Elegir archivos]** para cargar un archivo CSV desde el sistema local. También puede arrastrar y soltar el archivo CSV que desee cargar en el panel [!UICONTROL Arrastrar y soltar archivos].

>[!TIP]
>
>Actualmente solo se admiten archivos CSV en la carga de archivos locales. El tamaño máximo de archivo para cada archivo es 1 GB.

![elegir-archivos](../images/ui/mapping/choose-files.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar el contenido y la estructura del archivo.

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

Según el archivo, puede seleccionar un delimitador de columna como tabulaciones, comas, barras verticales o un delimitador de columna personalizado para los datos de origen. Seleccione la flecha desplegable **[!UICONTROL Delimitador]** y, a continuación, seleccione el delimitador apropiado en el menú.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![delimitador](../images/ui/mapping/delimiter.png)

## Asignación

La interfaz **[!UICONTROL mapping]** proporciona una completa herramienta para asignar campos de origen desde el esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### Explicación de la interfaz de asignación {#mapping-interface}

La interfaz de asignación incluye un panel que proporciona información sobre el estado de los campos de asignación en el contexto del flujo de trabajo de ingesta. El panel muestra los siguientes detalles sobre los campos de asignación:

| Propiedad | Descripción |
| --- | --- |
| [!UICONTROL Campos asignados] | Muestra el número total de campos de origen que se han asignado a un campo XDM de destino, independientemente de los errores. |
| [!UICONTROL Campos obligatorios] | Muestra el número de campos de asignación requeridos. |
| [!UICONTROL Campos de identidad] | Muestra el número total de campos de asignación definidos como identidad. Estos campos de asignación se representan mediante un icono de huella digital. |
| [!UICONTROL Errores] | Muestra el número de campos de asignación erróneos. |

![panel superior](../images/ui/mapping/top-panel.png)

La interfaz de asignación también proporciona un panel de opciones entre las que puede elegir para interactuar mejor o filtrar por los campos de asignación.

![segundo panel](../images/ui/mapping/second-panel.png)

Para buscar un conjunto de asignaciones concreto, seleccione **[!UICONTROL Buscar campos de origen]** e introduzca el nombre de los datos de origen que desea aislar.

![búsqueda](../images/ui/mapping/search.png)

Seleccione **[!UICONTROL Todos los campos de origen]** para ver un menú desplegable de opciones de filtrado y así reducir la vista de la interfaz de asignación.

Las opciones de filtrado son:

| Campos de Source | Descripción |
| --- | --- |
| [!UICONTROL Todos los campos de origen] | Esta opción muestra todos los campos de origen del esquema de origen. Esta opción se muestra de forma predeterminada. |
| [!UICONTROL Campos obligatorios] | Esta opción filtra el esquema de origen para mostrar solo los campos necesarios para completar la asignación. |
| [!UICONTROL Campos de identidad] | Esta opción filtra el esquema de origen para mostrar solo los campos marcados para Identidad. |
| [!UICONTROL Campos asignados] | Esta opción filtra el esquema de origen para mostrar solo los campos que ya se han asignado. |
| [!UICONTROL Campos sin asignar] | Esta opción filtra el esquema de origen para mostrar solo los campos que aún no se han asignado. |
| [!UICONTROL Campos con recomendación] | Esta opción filtra el esquema de origen para mostrar solo los campos que contienen recomendaciones de asignación. |

Seleccione **[!UICONTROL Campos con errores]** para ver todos los campos de asignación con errores.

![filtro](../images/ui/mapping/filter.png)

Aparece una vista aislada de los campos de asignación erróneos, que le permite solucionar errores mediante recomendaciones de asignación inteligente o a través del árbol de asignación manual.

![campos con errores](../images/ui/mapping/fields-with-errors.png)

### Añadir un nuevo tipo de campo

Puede agregar un nuevo campo de asignación o un campo calculado seleccionando **[!UICONTROL Nuevo tipo de campo]**.

#### Nuevo campo de asignación

Para agregar un nuevo campo de asignación, seleccione **[!UICONTROL Nuevo tipo de campo]** y, a continuación, seleccione **[!UICONTROL Agregar nuevo campo]** en el menú desplegable que aparece.

![agregar-nuevo-campo](../images/ui/mapping/add-new-field.png)

A continuación, seleccione el campo de origen que desee agregar desde el árbol de esquema de origen que aparece y, a continuación, seleccione **[!UICONTROL Seleccionar]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

La interfaz de asignación se actualiza con el campo de origen seleccionado y un campo de destino vacío. Seleccione **[!UICONTROL Asignar campo de destino]** para comenzar a asignar el nuevo campo de origen a su campo XDM de destino apropiado.

![map-target-field](../images/ui/mapping/map-target-field.png)

Aparece un árbol de esquema de destino interactivo, que le permite atravesar manualmente el esquema de destino y encontrar el campo XDM de destino adecuado para el campo de origen.

![asignación manual](../images/ui/mapping/manual-mapping.png)

Cuando termine, seleccione el icono de esquema para cerrar la interfaz de esquema de destinatario.

![árbol de esquemas](../images/ui/mapping/schema-tree.png)

#### Campos calculados {#calculated-fields}

Los campos calculados permiten crear valores basados en los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia. Los campos calculados tienen una longitud máxima de 4096 caracteres.

Para crear un campo calculado, seleccione **[!UICONTROL Nuevo tipo de campo]** y luego seleccione **[!UICONTROL Agregar campo calculado]**

![add-calculated-field](../images/ui/mapping/add-calculated-field.png)

Aparecerá el panel **[!UICONTROL Crear campo calculado]**. El cuadro de diálogo de la izquierda contiene los campos, funciones y operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

| Tabulación | Descripción |
| --- | ----------- |
| [!UICONTROL Función] | La pestaña functions enumera las funciones disponibles para transformar los datos. Para obtener más información acerca de las funciones que puede usar en los campos calculados, lea la guía de [uso de las funciones de preparación de datos (asignador)](../functions.md). |
| [!UICONTROL Campo] | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| [!UICONTROL Operador] | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

![tabulaciones](../images/ui/mapping/tabs.png)

Puede añadir manualmente campos, funciones y operadores utilizando el editor de expresiones en el centro. Seleccione el editor para empezar a crear una expresión. Una vez que haya terminado, seleccione **[!UICONTROL Guardar]** para continuar.

![create-calculated-field](../images/ui/mapping/create-calculated-field.png)

### Importar asignación {#import}

Puede reutilizar la asignación de un flujo de datos existente para reducir el tiempo de configuración manual de la ingesta de datos y limitar los errores. Seleccione **[!UICONTROL Importar asignación]** para reutilizar una asignación existente.

![import-mapping](../images/ui/mapping/import-mapping.png)

Aparecerá la ventana [!UICONTROL Importar asignación], que le proporcionará una lista de flujos de datos para elegir.

Seleccione el icono de previsualización para previsualizar la asignación del flujo de datos seleccionado.

![asignación de lista](../images/ui/mapping/list-mapping.png)

La ventana de vista previa permite inspeccionar la asignación existente antes de importarla al flujo de datos. Una vez verificada la asignación, puede seleccionar **[!UICONTROL Atrás]** para regresar a la lista de flujos de datos e inspeccionar otro conjunto de asignaciones, o bien puede seleccionar **[!UICONTROL Seleccionar]** para continuar.

![asignación de vista previa](../images/ui/mapping/preview-mapping.png)

También puede seleccionar la asignación que desee importar desde la ventana list of data fllows. Seleccione el flujo de datos que contiene la asignación que desea importar y, a continuación, seleccione **[!UICONTROL Seleccionar]** para continuar.

![select-mapping](../images/ui/mapping/select-mapping.png)

La interfaz se actualiza con la asignación importada.

>[!NOTE]
>
>Los conjuntos de asignaciones existentes que establezca o las recomendaciones de asignación XML se sustituirán por la asignación importada desde un flujo de datos existente.

![asignación importada](../images/ui/mapping/mapping-imported.png)

Seleccione **[!UICONTROL Vista previa de datos]** para ver los resultados de asignación de hasta 100 filas de datos de ejemplo del conjunto de datos seleccionado.

![datos de vista previa](../images/ui/mapping/preview-data.png)

Durante la vista previa, la columna de identidad se prioriza como el primer campo, ya que es la información clave necesaria para validar los resultados de la asignación. Cuando termine, seleccione **[!UICONTROL Cerrar]**.

![pantalla de vista previa](../images/ui/mapping/preview-screen.png)

Para quitar todos los campos de asignación, seleccione **[!UICONTROL Borrar todas las asignaciones]**.

![borrar todo](../images/ui/mapping/clear-all.png)

### Uso de la interfaz de asignación

Platform proporciona automáticamente recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso o corregir cualquier campo de asignación duplicado para borrar cualquier error.

![interfaz de asignación](../images/ui/mapping/mapping-interface.png)

Seleccione el icono de bombilla en el campo de destino que desee ajustar.

![mapping-recc](../images/ui/mapping/mapping-recc.png)

Aparecerá el panel emergente [!UICONTROL Recomendaciones de asignación], que muestra una lista de los campos de destino recomendados que se pueden asignar a un campo de origen determinado. De forma predeterminada, la primera recomendación se aplica automáticamente.

A veces, hay más de una recomendación disponible para el esquema de origen. Cuando esto sucede, la tarjeta de asignación muestra la recomendación más destacada, seguida de un icono que contiene la cantidad de recomendaciones adicionales disponibles. Al seleccionar el icono de la bombilla, se mostrará una lista de las recomendaciones adicionales. Puede elegir una de las recomendaciones alternativas seleccionando la casilla de verificación situada junto a la recomendación a la que desee asignar en su lugar.

Desde aquí, puede cambiar el campo de destino seleccionado para corregir un error o hacer coincidir el caso de uso.

También puede seleccionar **[!UICONTROL Seleccionar manualmente]** para usar manualmente el árbol de asignación de esquema de destino interactivo.

![recc-panel](../images/ui/mapping/recc-panel.png)

La interfaz de asignación de esquema de destino aparece en la misma vista que los campos de asignación, lo que le permite modificar los pares de asignación dentro de la misma pantalla. Seleccione el campo de destino que se adapte a su caso de uso o corrija sus errores.

![select-target-field](../images/ui/mapping/select-target-field.png)

Cuando termine, seleccione **[!UICONTROL Finalizar]** para continuar.

![finalizar](../images/ui/mapping/finish.png)

## Pasos siguientes

Al leer este documento, ha asignado correctamente un archivo CSV a un esquema XDM de destino mediante la interfaz de asignación en la interfaz de usuario de Platform. Consulte los siguientes documentos para obtener más información:

* [Resumen de preparación de datos](../home.md)
* [Información general de fuentes](../../sources/home.md)
* [Monitorización de orígenes y flujos de datos en la IU](../../dataflows/ui/monitor-sources.md)
