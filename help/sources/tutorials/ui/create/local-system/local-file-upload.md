---
keywords: Experience Platform;inicio;temas populares;sistema local;carga de archivos;asignación de csv;asignación de archivo csv;asignación de archivo csv a xdm;asignación de csv a xdm;guía de interfaz de usuario;
solution: Experience Platform
title: Crear un conector de origen de carga de archivos local en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen para que el sistema local traiga archivos locales a Platform
source-git-commit: 1bf112db27b534e2ec977be7b47e3becf75ee066
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 1%

---

# Creación de un conector de origen de carga de archivos local en la interfaz de usuario

Este tutorial proporciona los pasos para crear un conector de origen de carga de archivos local para la ingesta de archivos locales en Platform mediante la interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Cargar archivos locales a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría [!UICONTROL Local system], seleccione **[!UICONTROL Local file upload]** y, a continuación, seleccione **[!UICONTROL Configure]**.

![catálogo](../../../../images/tutorials/create/local/catalog.png)

### Usar un conjunto de datos existente

La página [!UICONTROL Detalles del flujo de datos] permite seleccionar si desea introducir los datos CSV en un conjunto de datos existente o un nuevo conjunto de datos.

Para introducir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la opción [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable.

![select-existing-dataset](../../../../images/tutorials/create/local/select-existing-dataset.png)

Con un conjunto de datos seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional.

Durante este proceso, también puede habilitar [!UICONTROL Diagnósticos de error] y [!UICONTROL Ingesta parcial]. [!UICONTROL El ] diagnóstico de error permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que el  [!UICONTROL cuestionario ] parcial permite introducir datos que contengan errores, hasta un determinado umbral que se defina manualmente. Consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

![dataflow-detail-existing](../../../../images/tutorials/create/local/dataflow-detail-existing.png)

### Usar un nuevo conjunto de datos

Para introducir los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre de conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema para asignar con la opción [!UICONTROL Advanced search] o desplácese por la lista de esquemas existentes en el menú desplegable.

![select-new-dataset](../../../../images/tutorials/create/local/select-new-dataset.png)

Con un esquema seleccionado, proporcione un nombre para el flujo de datos y una descripción opcional y, a continuación, aplique la configuración [!UICONTROL Error diagnostic] y [!UICONTROL Partial ingestion] que desee para el flujo de datos. Cuando termine, seleccione **[!UICONTROL Next]**.

### Seleccionar datos

Aparece el paso [!UICONTROL Select data], que proporciona una interfaz para cargar los archivos locales y previsualizar su estructura y contenido. Seleccione **[!UICONTROL Elegir archivos]** para cargar un archivo CSV desde el sistema local. También puede arrastrar y soltar el archivo CSV que desea cargar en el panel [!UICONTROL Arrastrar y soltar archivos].

>[!TIP]
>
>Actualmente, la carga de archivos locales solo admite los archivos CSV. El tamaño máximo de archivo para cada archivo es de 1 GB.

![elegir-archivos](../../../../images/tutorials/create/local/choose-files.png)

Una vez cargado el archivo, la interfaz de vista previa se actualiza para mostrar el contenido y la estructura del archivo.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Según el archivo, puede seleccionar un delimitador de columna, como tabulaciones, comas, barras verticales o un delimitador de columna personalizado para los datos de origen. Seleccione la flecha desplegable **[!UICONTROL Delimiter]** y, a continuación, seleccione el delimitador adecuado en el menú.

Cuando termine, seleccione **[!UICONTROL Next]**.

![delimiter](../../../../images/tutorials/create/local/delimiter.png)

### Asignación

Aparece el paso [!UICONTROL Mapping], que le proporciona una interfaz para asignar los campos de origen del esquema de origen a los campos XDM de destino adecuados en el esquema de destino.

![mapping-interface](../../../../images/tutorials/create/local/mapping-interface.png)

#### Previsualización de datos

Seleccione **[!UICONTROL Preview data]** para ver los resultados de asignación de hasta 100 filas de datos de ejemplo del conjunto de datos seleccionado.

![previsualización-asignación](../../../../images/tutorials/create/local/preview-mapping.png)

Durante la vista previa, la columna de identidad se prioriza como el primer campo, ya que es la información clave necesaria al validar los resultados de la asignación. Cuando termine, seleccione **[!UICONTROL Cerrar]**.

![vista previa-panel](../../../../images/tutorials/create/local/preview-panel.png)

#### Añadir campo calculado

Los campos calculados permiten que se creen valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Seleccione el botón **[!UICONTROL Add calculated field]** para continuar.

![add-calculated-field](../../../../images/tutorials/create/local/add-calculated-field.png)

Aparece el panel [!UICONTROL Crear campo calculado]. El cuadro de diálogo izquierdo contiene los campos, las funciones y los operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

![create-calculated-field](../../../../images/tutorials/create/local/create-calculated-field.png)

| Tabulación | Descripción |
| --------- | ----------- |
| Función | La pestaña funciones enumera las funciones disponibles para transformar los datos. Para obtener más información sobre las funciones que puede utilizar en los campos calculados, lea la guía sobre el uso de las funciones [de preparación de datos (Mapper)](../../../../../data-prep/functions.md). |
| Campo | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| Operador | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

Seleccione el editor de expresiones para añadir manualmente campos, funciones y operadores. Una vez creado un campo calculado, seleccione **[!UICONTROL Save]** para continuar.

![expression-editor](../../../../images/tutorials/create/local/expression-editor.png)

#### Filtrar el árbol de asignación de esquema de origen

Para filtrar por el esquema de origen, seleccione **[!UICONTROL All source fields]** y, a continuación, seleccione el campo específico que desea asignar en el menú desplegable.

La tabla siguiente muestra las opciones de clasificación del árbol de esquema de origen:

| Campos de origen | Descripción |
| --- | --- |
| [!UICONTROL Todos los campos de origen] | Esta opción muestra todos los campos de origen del esquema de origen. Esta opción se muestra de forma predeterminada. |
| [!UICONTROL Campos requeridos] | Esta opción filtra el esquema de origen para mostrar solo los campos necesarios para completar la asignación. |
| [!UICONTROL Campos de identidad] | Esta opción filtra el esquema de origen para mostrar solo los campos marcados para Identity. |
| [!UICONTROL Campos asignados] | Esta opción filtra el esquema de origen para mostrar solo los campos que ya se han asignado. |
| [!UICONTROL Campos sin asignar] | Esta opción filtra el esquema de origen para mostrar solo los campos que aún no se han asignado. |
| [!UICONTROL Campos con recomendación] | Esta opción filtra el esquema de origen para mostrar solo los campos que contienen recomendaciones de asignación. |

![todos los campos de origen](../../../../images/tutorials/create/local/all-source-fields.png)

#### Recomendaciones inteligentes

Platform proporciona automáticamente recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![source-schema-tree](../../../../images/tutorials/create/local/source-schema-tree.png)

Para aceptar todos los valores de asignación de generación automática, seleccione **[!UICONTROL Accept all target fields]**.

![todos los campos de destino](../../../../images/tutorials/create/local/all-target-fields.png)

A veces, hay más de una recomendación disponible para el esquema de origen. Cuando esto sucede, la tarjeta de asignación muestra la recomendación más destacada, seguida de un círculo azul que contiene el número de recomendaciones adicionales disponibles. Al seleccionar el icono de la bombilla se mostrará una lista de las recomendaciones adicionales. Para elegir una de las recomendaciones alternativas, seleccione la casilla que hay junto a la recomendación a la que desea asignar.

![asignación manual](../../../../images/tutorials/create/local/manual-mapping.png)

Como alternativa, puede elegir asignar manualmente el esquema de origen al esquema de destino. Para ello, pase el ratón sobre el esquema de origen que desea asignar y, a continuación, seleccione el icono de signo más (`+`).

![select-plus-icon](../../../../images/tutorials/create/local/select-plus-icon.png)

Aparece la ventana **[!UICONTROL Map source to target field]**. Desde aquí, puede seleccionar qué campo desea asignar, seguido de **[!UICONTROL Save]** para agregar la nueva asignación.

![map-source-to-target-field](../../../../images/tutorials/create/local/map-source-to-target-field.png)

Cuando termine, seleccione **[!UICONTROL Finalizado]**.

![finalizar](../../../../images/tutorials/create/local/finish.png)

## Monitorización de la ingesta de datos

Una vez asignado y creado el archivo CSV, puede monitorizar los datos que se están incorporando a través de él mediante el panel de monitorización. Para obtener más información, consulte el tutorial sobre flujos de datos de [fuentes de monitorización en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

## Pasos siguientes

Al seguir este tutorial, ha asignado correctamente un archivo CSV plano a un esquema XDM y lo ha introducido en Platform. Ahora, estos datos los pueden utilizar servicios descendentes [!DNL Platform] como [!DNL Real-time Customer Profile]. Consulte la descripción general de [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) para obtener más información.
