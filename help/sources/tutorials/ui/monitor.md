---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitorear cuentas y flujos de conjuntos de datos
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Monitorear cuentas y flujos de conjuntos de datos

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para ver las cuentas existentes y los flujos de conjuntos de datos desde el espacio de trabajo *[!UICONTROL Fuentes]* .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)de modelo de datos de experiencia (XDM): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Supervisión de cuentas

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo *[!UICONTROL Fuentes]* . La pantalla *[!UICONTROL Catálogo]* muestra una serie de fuentes para las que puede crear flujos de conjuntos de datos de cuentas. Cada fuente muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Seleccione *[!UICONTROL Cuentas]* del encabezado superior para vista de cuentas existentes.

![catálogo](../../images/tutorials/monitor/catalog.png)

Se abre la página *[!UICONTROL Cuentas]* . En esta página hay una lista de cuentas visualizables, que incluye información sobre su origen, nombre de usuario, número de flujos de conjuntos de datos y fecha de creación.

Seleccione el icono en la parte superior izquierda para iniciar la ventana de ordenación.

![cuentas](../../images/tutorials/monitor/accounts-list.png)

El panel de ordenación permite acceder a las cuentas desde un origen específico. Seleccione el origen con el que desea trabajar y seleccione la cuenta en la lista de la derecha.

![accounts-select](../../images/tutorials/monitor/accounts-sort.png)

Desde la página *[!UICONTROL Cuentas]* , puede realizar una vista de una lista de los flujos de conjuntos de datos existentes asociados con la cuenta a la que accedió. Seleccione el flujo del conjunto de datos que desee vista.

![accounts-page](../../images/tutorials/monitor/dataset-flows.png)

Aparece la pantalla de actividad *[!UICONTROL de flujo de]* datos. Esta página muestra la velocidad de los mensajes que se consumen en forma de gráfico.

![dataset-flow-actividad](../../images/tutorials/monitor/dataset-flows-activity.png)

## Monitorear flujos de conjuntos de datos

Se puede acceder a los flujos de conjuntos de datos directamente desde la página *[!UICONTROL Catálogo]* sin ver *[!UICONTROL las cuentas]*. Seleccione los flujos *[!UICONTROL de]* conjuntos de datos desde el encabezado superior para la vista de una lista de los flujos de conjuntos de datos existentes.

![dataset-flows](../../images/tutorials/monitor/dataset-flows-list.png)

De forma similar a las cuentas, puede ordenar la lista de los flujos de conjuntos de datos mediante el icono de ordenación en la parte superior izquierda. Seleccione el origen que desee vista y seleccione el flujo del conjunto de datos en la lista de la derecha.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

Aparece la pantalla de actividad *[!UICONTROL de flujo de]* datos. Esta página muestra la velocidad de los mensajes que se consumen en forma de gráfico.

![dataset-flow-actividad](../../images/tutorials/monitor/dataset-flows-activity.png)

Para obtener más información sobre la supervisión de conjuntos de datos y la ingestión, consulte el tutorial sobre la [supervisión de flujos de datos](../../../ingestion/quality/monitor-data-flows.md)de flujo continuo.

## Pasos siguientes

Siguiendo este tutorial, ha accedido correctamente a las cuentas existentes y a los flujos de conjuntos de datos desde el espacio de trabajo *[!UICONTROL Fuentes]* . Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../data-science-workspace/home.md)