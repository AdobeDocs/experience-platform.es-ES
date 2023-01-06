---
keywords: Experience Platform;inicio;temas populares;asignar csv;asignar archivo csv;asignar archivo csv a xdm;asignar csv a xdm;guía de ui;
solution: Experience Platform
title: Asignación de un archivo CSV a un esquema XDM existente
type: Tutorial
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM existente mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# Asignación de un archivo CSV a un esquema XDM existente

>[!NOTE]
>
>Este documento explica cómo asignar un archivo CSV a un esquema XDM existente. Para obtener información sobre cómo utilizar la herramienta de recomendación de esquema generada por AI (actualmente en versión beta), consulte el documento sobre [asignación de un archivo CSV mediante recomendaciones de aprendizaje automático](./recommendations.md).

Para introducir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a un [!DNL Experience Data Model] (XDM). Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante el [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
- [Ingesta por lotes](../../batch-ingestion/overview.md): El método mediante el cual [!DNL Platform] Ingesta datos de archivos de datos suministrados por el usuario.
- [Preparación de datos de Adobe Experience Platform](../../batch-ingestion/overview.md): Conjunto de funciones que le permiten asignar y transformar datos ingestados para ajustarse a esquemas XDM. La documentación de [Funciones de preparación de datos](../../../data-prep/functions.md) es especialmente relevante para la asignación de esquemas.

Este tutorial también requiere que ya haya creado un conjunto de datos para introducir los datos CSV en. Para ver los pasos sobre la creación de un conjunto de datos en la interfaz de usuario, consulte la [tutorial de ingesta de datos](../ingest-batch-data.md).

## Elegir un destino

Iniciar sesión en [[!DNL Adobe Experience Platform]](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Flujos de trabajo]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Flujos de trabajo]** espacio de trabajo.

En el **[!UICONTROL Flujos de trabajo]** pantalla, seleccionar **[!UICONTROL Asignación de CSV al esquema XDM]** en el **[!UICONTROL Ingesta de datos]** y, a continuación, seleccione **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

La variable **[!UICONTROL Asignación de CSV al esquema XDM]** aparece el flujo de trabajo, empezando por el **[!UICONTROL Destino]** paso a paso. Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede utilizar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para introducir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Usar conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la función de búsqueda o desplazándose por la lista de conjuntos de datos existentes en el panel.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para introducir los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Crear nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Seleccione un esquema utilizando la función de búsqueda o desplazándose por la lista de esquemas proporcionados. Select **[!UICONTROL Siguiente]** para continuar.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Adición de datos

La variable **[!UICONTROL Añadir datos]** aparece. Arrastre y suelte el archivo CSV en el espacio proporcionado o seleccione **[!UICONTROL Elegir archivos]** para introducir manualmente el archivo CSV.

![](../../images/tutorials/map-a-csv-file/add-data.png)

La variable **[!UICONTROL Datos de muestra]** aparece una vez cargado el archivo y muestra las primeras diez filas de datos. Una vez que haya confirmado que los datos se han cargado según lo esperado, seleccione **[!UICONTROL Siguiente]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## Asignación de campos CSV a campos de esquema XDM

La variable **[!UICONTROL Asignación]** aparece. Las columnas del archivo CSV se enumeran en **[!UICONTROL Campo de origen]**, con sus correspondientes campos de esquema XDM enumerados en **[!UICONTROL Campo de destino]**.

[!DNL Platform] proporciona automáticamente recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Para aceptar todos los valores de asignación de generación automática, seleccione la casilla de verificación denominada &quot;[!UICONTROL Aceptar todos los campos de destino]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A veces, hay más de una recomendación disponible para el esquema de origen. Cuando esto sucede, la tarjeta de asignación muestra la recomendación más destacada, seguida de un círculo azul que contiene el número de recomendaciones adicionales disponibles. Al seleccionar el icono de la bombilla se mostrará una lista de las recomendaciones adicionales. Para elegir una de las recomendaciones alternativas, seleccione la casilla que hay junto a la recomendación a la que desea asignar.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Como alternativa, puede elegir asignar manualmente el esquema de origen al esquema de destino. Pase el ratón sobre el esquema de origen que desee asignar y, a continuación, seleccione el icono de signo más.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

La variable **[!UICONTROL Asignar origen al campo de destino]** se abre. Desde aquí, puede seleccionar qué campo desea asignar, seguido de **[!UICONTROL Guardar]** para añadir la nueva asignación.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Si desea eliminar una de las asignaciones, pase el ratón sobre esa asignación y, a continuación, seleccione el icono menos.

### Añadir campo calculado {#add-calculated-field}

Los campos calculados permiten que se creen valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destino y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Seleccione el **[!UICONTROL Añadir campo calculado]** para continuar.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

La variable **[!UICONTROL Crear campo calculado]** aparece. El cuadro de diálogo izquierdo contiene los campos, las funciones y los operadores admitidos en los campos calculados. Seleccione una de las pestañas para empezar a añadir funciones, campos u operadores al editor de expresiones.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulación | Descripción |
| --------- | ----------- |
| Campos | La pestaña fields enumera los campos y atributos disponibles en el esquema de origen. |
| Funciones | La pestaña funciones enumera las funciones disponibles para transformar los datos. Para obtener más información sobre las funciones que puede utilizar en los campos calculados, consulte la guía de [uso de las funciones de preparación de datos (Mapper)](../../../data-prep/functions.md). |
| Operadores | La pestaña operadores enumera los operadores disponibles para transformar los datos. |

Puede añadir manualmente campos, funciones y operadores con el editor de expresiones del centro. Seleccione el editor para comenzar a crear una expresión.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Select **[!UICONTROL Guardar]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destino correspondiente correspondiente y seleccione **[!UICONTROL Finalizar]** para completar la asignación.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorización de la ingesta de datos

Una vez asignado y creado el archivo CSV, puede supervisar los datos que se están incorporando a través de él. Para obtener más información sobre la monitorización de la ingesta de datos, consulte el tutorial sobre [monitorización de la ingesta de datos](../../../ingestion/quality/monitor-data-ingestion.md).

## Pasos siguientes

Siguiendo este tutorial, ha asignado correctamente un archivo CSV plano a un esquema XDM y lo ha introducido en [!DNL Platform]. Ahora, estos datos los puede utilizar el flujo descendente [!DNL Platform] servicios como [!DNL Real-Time Customer Profile]. Consulte la descripción general para [[!DNL Real-Time Customer Profile]](../../../profile/home.md) para obtener más información.
