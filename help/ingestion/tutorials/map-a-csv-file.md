---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Asignación de un archivo CSV a un esquema XDM
topic: tutorial
type: Tutorial
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c19360450d7b1f11063683b796774a04f3dbe16c
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Asignación de un archivo CSV a un esquema XDM

Para poder ingerir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario [!DNL Platform] .

Además, en el apéndice de este tutorial se proporciona más información sobre el uso de funciones [de](#mapping-functions)asignación.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md):: El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md):: El método mediante el cual [!DNL Platform] ingesta datos de archivos de datos proporcionados por el usuario.

Este tutorial también requiere que ya haya creado un conjunto de datos para ingestar los datos de CSV. Para ver los pasos para crear un conjunto de datos en la interfaz de usuario, consulte el tutorial [de ingesta de](./ingest-batch-data.md)datos.

## Elegir un destino

Inicie sesión en [[!DNL Adobe Experience Platform]](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Flujos de trabajo]** en la barra de navegación izquierda para acceder al espacio de trabajo de **[!UICONTROL Flujos de trabajo]** .

En la pantalla **[!UICONTROL Flujos de trabajo]** , seleccione **[!UICONTROL Asignar CSV al esquema]** XDM en la sección **[!UICONTROL de ingesta]** de datos y, a continuación, seleccione **[!UICONTROL Iniciar]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Aparece el flujo de trabajo **[!UICONTROL Asignar CSV al esquema]** XDM, comenzando en el paso **[!UICONTROL Destino]** . Elija un conjunto de datos para los datos de entrada en los que se van a ingerir. Puede usar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para ingerir los datos CSV en un conjunto de datos existente, seleccione **[!UICONTROL Usar conjunto de datos]** existente. Puede recuperar un conjunto de datos existente mediante la función de búsqueda o desplazándose por la lista de conjuntos de datos existentes en el panel.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para ingestar los datos CSV en un nuevo conjunto de datos, seleccione **[!UICONTROL Crear nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Seleccione un esquema utilizando la función de búsqueda o desplazándose por la lista de esquemas proporcionada. Seleccione **[!UICONTROL Siguiente]** para continuar.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Añadir datos

Aparece el paso **[!UICONTROL Añadir datos]** . Arrastre y suelte el archivo CSV en el espacio proporcionado o seleccione **[!UICONTROL Elegir archivos]** para introducir manualmente el archivo CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La sección Datos **[!UICONTROL de]** ejemplo aparece una vez cargado el archivo, mostrando las primeras diez filas de datos. Una vez que confirme que los datos se han cargado según lo esperado, seleccione **[!UICONTROL Siguiente]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Asignar campos CSV a campos de esquema XDM

Aparece el paso **[!UICONTROL Asignación]** . Las columnas del archivo CSV se muestran en Campo **** de origen, con sus correspondientes campos de esquema XDM en Campo **[!UICONTROL de]** Destinatario.

[!DNL Platform] automáticamente proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema de destinatario o del conjunto de datos que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Para aceptar todos los valores de asignación que se generan automáticamente, seleccione la casilla de verificación rotulada &quot;[!UICONTROL Aceptar todos los campos]de destinatario&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A veces, hay más de una recomendación disponible para el esquema de origen. Cuando esto sucede, la tarjeta de asignación muestra la recomendación más prominente, seguida de un círculo azul que contiene el número de recomendaciones adicionales disponibles. Al seleccionar el icono de la bombilla se mostrará una lista de las recomendaciones adicionales. Para elegir una de las recomendaciones alternativas, seleccione la casilla de verificación situada junto a la recomendación a la que desee asignar.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Como alternativa, puede elegir asignar manualmente el esquema de origen a su esquema de destinatario. Pase el ratón sobre el esquema de origen que desee asignar y, a continuación, seleccione el icono de signo más.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Aparece la ventana emergente **[!UICONTROL Asignar origen a campo]** destinatario. Desde aquí, puede seleccionar qué campo desea asignar, seguido de **[!UICONTROL Guardar]** para agregar la nueva asignación.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Si desea eliminar una de las asignaciones, coloque el puntero sobre ella y, a continuación, seleccione el icono de menos.

### Añadir campo calculado

Los campos calculados permiten crear valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destinatario y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Seleccione el botón **[!UICONTROL Añadir campo]** calculado para continuar.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Aparece el panel **[!UICONTROL Crear campo]** calculado. El cuadro de diálogo izquierdo contiene los campos, las funciones y los operadores admitidos en los campos calculados. Seleccione una de las fichas para agregar funciones, campos o operadores al editor de expresiones en inicio.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulación | Descripción |
| --------- | ----------- |
| Campos | La ficha Campos lista campos y atributos disponibles en el esquema de origen. |
| Funciones | La ficha Funciones lista las funciones disponibles para transformar los datos. Para obtener más información sobre las funciones que puede utilizar en los campos calculados, lea la guía sobre el [uso de las funciones](../../data-prep/functions.md)de preparación de datos (Mapper). |
| Operadores | La ficha Operadores lista los operadores disponibles para transformar los datos. |

Puede agregar manualmente campos, funciones y operadores mediante el editor de expresiones del centro. Seleccione el editor para crear una expresión en inicio.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Seleccione **[!UICONTROL Guardar]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destinatario correspondiente y seleccione **[!UICONTROL Finalizar]** para completar la asignación.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitoreo de la ingesta de datos

Una vez asignado y creado el archivo CSV, puede supervisar los datos que se están ingeriendo a través de él. Para obtener más información sobre la supervisión de la ingestión de datos, consulte el tutorial sobre la [supervisión de la ingesta](../../ingestion/quality/monitor-data-ingestion.md)de datos.

## Pasos siguientes

Siguiendo este tutorial, ha asignado correctamente un archivo CSV plano a un esquema XDM y lo ha ingerido en [!DNL Platform]. Estos datos ahora pueden ser utilizados por servicios [!DNL Platform] de flujo descendente como [!DNL Real-time Customer Profile]. See the overview for [[!DNL Real-time Customer Profile]](../../profile/home.md) for more information.
