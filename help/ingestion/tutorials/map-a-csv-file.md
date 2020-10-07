---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Asignación de un archivo CSV a un esquema XDM
topic: tutorial
type: Tutorial
description: Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# Asignación de un archivo CSV a un esquema XDM

Para poder ingerir datos CSV en [!DNL Adobe Experience Platform], los datos deben asignarse a un esquema [!DNL Experience Data Model] (XDM). Este tutorial explica cómo asignar un archivo CSV a un esquema XDM mediante la interfaz de usuario [!DNL Platform] .

Además, en el apéndice de este tutorial se proporciona más información sobre el uso de funciones [de](#mapping-functions)asignación.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de [!DNL Platform]:

- [[!Modelo de datos de experiencia DNL (sistema XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
- [[!DNL Ingesta por lotes]](../batch-ingestion/overview.md): El método mediante el cual [!DNL Platform] ingesta datos de archivos de datos proporcionados por el usuario.

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

Aparece el paso **[!UICONTROL Asignación]** . Las columnas del archivo CSV se muestran en Campo **** de origen, con sus correspondientes campos de esquema XDM en Campo **[!UICONTROL de]** Destinatario. Los campos de destinatario no seleccionados están delineados en rojo. Puede utilizar la opción de campos de filtro para reducir la lista de los campos de origen disponibles.

>[!TIP]
>
>[!DNL Platform] proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema de destinatario o del conjunto de datos que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

Para asignar una columna CSV a un campo XDM, seleccione el icono de esquema junto al campo de destinatario correspondiente de la columna.

![](../images/tutorials/map-a-csv-file/mapping.png)

Aparece la ventana **[!UICONTROL Seleccionar esquema]** . Aquí puede desplazarse por la estructura del esquema XDM y localizar el campo al que desea asignar la columna CSV. Haga clic en un campo XDM para seleccionarlo y, a continuación, haga clic en **[!UICONTROL Seleccionar]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Después de completar los pasos para los campos de origen sin asignar restantes, la pantalla **[!UICONTROL Asignación]** vuelve a aparecer con el campo XDM seleccionado que aparece ahora en Campo **[!UICONTROL de]** Destinatario.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Al asignar campos, también puede incluir funciones para calcular valores en función de los campos de origen de entrada. Consulte la sección de funciones [de](#mapping-functions) asignación del apéndice para obtener más información.

### Añadir campo calculado

Los campos calculados permiten crear valores en función de los atributos del esquema de entrada. Estos valores se pueden asignar a atributos en el esquema de destinatario y se les puede proporcionar un nombre y una descripción para facilitar la referencia.

Seleccione el botón **[!UICONTROL Añadir campo]** calculado para continuar.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

Aparece el panel **[!UICONTROL Crear campo]** calculado. El cuadro de diálogo izquierdo contiene los campos, las funciones y los operadores admitidos en los campos calculados. Seleccione una de las fichas para agregar funciones, campos o operadores al editor de expresiones en inicio.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulación | Descripción |
| --------- | ----------- |
| Campos | La ficha Campos lista campos y atributos disponibles en el esquema de origen. |
| Funciones | La ficha Funciones lista las funciones disponibles para transformar los datos. |
| Operadores | La ficha Operadores lista los operadores disponibles para transformar los datos. |

Puede agregar manualmente campos, funciones y operadores mediante el editor de expresiones del centro. Seleccione el editor para crear una expresión en inicio.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Seleccione **[!UICONTROL Guardar]** para continuar.

La pantalla de asignación vuelve a aparecer con el campo de origen recién creado. Aplique el campo de destinatario correspondiente y seleccione **[!UICONTROL Finalizar]** para completar la asignación.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Monitorear el flujo de datos

Una vez asignado y creado el archivo CSV, puede supervisar los datos que se están ingeriendo a través de él. Para obtener más información sobre la supervisión de flujos de datos, consulte el tutorial sobre la [supervisión de flujos de datos](../../ingestion/quality/monitor-data-flows.md)de flujo continuo.

## Uso de funciones de asignación

Para utilizar una función, escríbala en Campo **** de origen con la sintaxis y las entradas adecuadas.

Por ejemplo, para concatenar campos CSV de ciudad y país y asignarlos al campo XDM de ciudad, establezca el campo de origen como `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Para obtener más información sobre la asignación de columnas a campos XDM, lea la guía sobre el [uso de funciones](../../data-prep/functions.md)de preparación de datos (Mapper).

## Pasos siguientes

Siguiendo este tutorial, ha asignado correctamente un archivo CSV plano a un esquema XDM y lo ha ingerido en [!DNL Platform]. Estos datos ahora pueden ser utilizados por servicios [!DNL Platform] de flujo descendente como [!DNL Real-time Customer Profile]. Consulte la descripción general de [[!DNL Perfil del cliente en tiempo real]](../../profile/home.md) para obtener más información.
