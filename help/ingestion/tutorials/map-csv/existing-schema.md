---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de iu;
solution: Experience Platform
title: Asignar un archivo CSV a un esquema XDM existente
type: Tutorial
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM existente mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# Asignar un archivo CSV a un esquema XDM existente

>[!NOTE]
>
>Este documento explica cómo asignar un archivo CSV a un esquema XDM existente. Para obtener información sobre cómo utilizar la herramienta de recomendación de esquemas generados por IA (actualmente en fase beta), consulte el documento sobre [asignación de un archivo CSV mediante recomendaciones de aprendizaje automático](./recommendations.md).

Para ingerir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario [!DNL Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.
- [Ingesta por lotes](../../batch-ingestion/overview.md): Método mediante el cual [!DNL Platform] ingiere datos de archivos de datos proporcionados por el usuario.
- [Preparación de datos de Adobe Experience Platform](../../batch-ingestion/overview.md): Un conjunto de funcionalidades que le permiten asignar y transformar datos ingeridos para que se ajusten a esquemas XDM. La documentación de [funciones de preparación de datos](../../../data-prep/functions.md) es especialmente relevante para la asignación de esquemas.

Este tutorial también requiere que ya haya creado un conjunto de datos para introducir los datos CSV en. Para ver los pasos para crear un conjunto de datos en la interfaz de usuario, consulte el [tutorial de ingesta de datos](../ingest-batch-data.md).

## Elija un destino

Inicie sesión en [[!DNL Adobe Experience Platform]](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Flujos de trabajo]** en la barra de navegación izquierda para acceder al área de trabajo **[!UICONTROL Flujos de trabajo]**.

En la pantalla **[!UICONTROL Flujos de trabajo]**, seleccione **[!UICONTROL Asignar CSV al esquema XDM]** en la sección **[!UICONTROL Ingesta de datos]** y, a continuación, seleccione **[!UICONTROL Iniciar]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

Aparece el flujo de trabajo **[!UICONTROL Asignar CSV al esquema XDM]**, a partir del paso **[!UICONTROL Destino]**. Elija un conjunto de datos para los datos de entrada que se van a introducir en. Puede utilizar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para introducir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Usar conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la función de búsqueda o desplazándose por la lista de conjuntos de datos existentes en el panel.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para introducir los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Crear nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Seleccione un esquema mediante la función de búsqueda o desplazándose por la lista de esquemas proporcionados. Seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Adición de datos

Aparecerá el paso **[!UICONTROL Agregar datos]**. Arrastre y suelte el archivo CSV en el espacio proporcionado o seleccione **[!UICONTROL Elegir archivos]** para introducir manualmente el archivo CSV.

![](../../images/tutorials/map-a-csv-file/add-data.png)

La sección **[!UICONTROL Datos de ejemplo]** aparece una vez cargado el archivo y muestra las primeras diez filas de datos. Una vez que confirme que los datos se han cargado según lo esperado, seleccione **[!UICONTROL Siguiente]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## Asignar campos CSV a campos de esquema XDM

Aparecerá el paso **[!UICONTROL Mapping]**. Las columnas del archivo CSV se enumeran en **[!UICONTROL Campo de Source]**, con sus campos de esquema XDM correspondientes en **[!UICONTROL Campo de destino]**.

[!DNL Platform] proporciona automáticamente recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Para aceptar todos los valores de asignación generados automáticamente, active la casilla de verificación con la etiqueta &quot;[!UICONTROL Aceptar todos los campos de destino]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A veces, hay más de una recomendación disponible para el esquema de origen. Cuando esto sucede, la tarjeta de asignación muestra la recomendación más destacada, seguida de un círculo azul que contiene el número de recomendaciones adicionales disponibles. Al seleccionar el icono de la bombilla, se mostrará una lista de las recomendaciones adicionales. Puede elegir una de las recomendaciones alternativas seleccionando la casilla de verificación situada junto a la recomendación a la que desee asignar en su lugar.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Como alternativa, puede elegir asignar manualmente el esquema de origen al esquema de destino. Pase el ratón sobre el esquema de origen que desee asignar y, a continuación, seleccione el icono de signo +.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Aparece la ventana emergente **[!UICONTROL Asignar origen a campo de destino]**. Desde aquí, puede seleccionar qué campo desea asignar, seguido de **[!UICONTROL Guardar]** para agregar su nueva asignación.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Si desea eliminar una de las asignaciones, pase el ratón sobre esa asignación y, a continuación, seleccione el icono menos.

### Añadir campo calculado {#add-calculated-field}

Los campos calculados permiten crear valores basados en los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Seleccione el botón **[!UICONTROL Agregar campo calculado]** para continuar.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

Aparecerá el panel **[!UICONTROL Crear campo calculado]**. El cuadro de diálogo de la izquierda contiene los campos, funciones y operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulación | Descripción |
| --------- | ----------- |
| Campos | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| Funciones | La pestaña functions enumera las funciones disponibles para transformar los datos. Para obtener más información acerca de las funciones que puede usar en los campos calculados, lea la guía de [uso de las funciones de preparación de datos (asignador)](../../../data-prep/functions.md). |
| Operadores | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

Puede añadir manualmente campos, funciones y operadores utilizando el editor de expresiones en el centro. Seleccione el editor para empezar a crear una expresión.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Seleccione **[!UICONTROL Guardar]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destino correspondiente y seleccione **[!UICONTROL Finalizar]** para completar la asignación.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorización de la ingesta de datos

Una vez asignado y creado el archivo CSV, puede monitorizar los datos que se están introduciendo a través de él. Para obtener más información sobre la supervisión de la ingesta de datos, consulte el tutorial sobre [supervisión de la ingesta de datos](../../../ingestion/quality/monitor-data-ingestion.md).

## Pasos siguientes

Al seguir este tutorial, ha asignado correctamente un archivo CSV sin formato a un esquema XDM y lo ha introducido en [!DNL Platform]. Estos datos ahora pueden ser utilizados por servicios de flujo descendente [!DNL Platform] como [!DNL Real-Time Customer Profile]. Vea la descripción general de [[!DNL Real-Time Customer Profile]](../../../profile/home.md) para obtener más información.

>[!TIP]
>
>También puede usar algoritmos de aprendizaje automático (ML) para **generar un esquema a partir de datos de ejemplo** del espacio de trabajo de esquemas. Este flujo de trabajo crea automáticamente un nuevo esquema basado en la estructura y el contenido del archivo, lo que garantiza que el esquema coincida con el formato de los datos. Esto le ahorra tiempo y aumenta la precisión al definir la estructura, los campos y los tipos de datos para conjuntos de datos grandes y complejos. Consulte la [guía de creación de esquemas asistidos por ML](../../../xdm/ui/ml-assisted-schema-creation.md) para obtener más información sobre este flujo de trabajo.
