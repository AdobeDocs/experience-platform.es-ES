---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitorear cuentas y flujos de conjuntos de datos
topic: overview
translation-type: tm+mt
source-git-commit: fc0a406bdea7b31e046d02427805a9deba557e93

---


# Monitorear cuentas y flujos de conjuntos de datos

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para ver las cuentas existentes y los flujos de conjuntos de datos desde el espacio de trabajo *Fuentes* .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Supervisión de cuentas

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de fuentes para las que puede crear flujos de conjuntos de datos de cuentas. Cada fuente muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Seleccione *Cuentas* del encabezado superior para vista de cuentas existentes.

![catálogo](../../images/tutorials/monitor/catalog.png)

Se abre la página *Cuentas* . En esta página hay una lista de cuentas visualizables, que incluye información sobre su origen, nombre de usuario, número de flujos de conjuntos de datos y fecha de creación.

Seleccione el icono en la parte superior izquierda para iniciar la ventana de ordenación.

![cuentas](../../images/tutorials/monitor/accounts-list.png)

El panel de ordenación permite acceder a las cuentas desde un origen específico. Seleccione el origen con el que desea trabajar y seleccione la cuenta en la lista de la derecha.

![accounts-select](../../images/tutorials/monitor/accounts-sort.png)

Desde la página *Cuentas* , puede realizar una vista de una lista de los flujos de conjuntos de datos existentes asociados con la cuenta a la que accedió. Seleccione el flujo del conjunto de datos que desee vista.

![accounts-page](../../images/tutorials/monitor/dataset-flows.png)

Aparece la pantalla de actividad *de flujo de* datos. Esta página muestra la velocidad de los mensajes que se consumen en forma de gráfico.

![dataset-flow-actividad](../../images/tutorials/monitor/dataset-flows-activity.png)

## Monitorear flujos de conjuntos de datos

Se puede acceder a los flujos de conjuntos de datos directamente desde la página *Catálogo* sin ver *las cuentas*. Seleccione los flujos *de* conjuntos de datos desde el encabezado superior para la vista de una lista de los flujos de conjuntos de datos existentes.

![dataset-flows](../../images/tutorials/monitor/dataset-flows-list.png)

De forma similar a las cuentas, puede ordenar la lista de los flujos de conjuntos de datos mediante el icono de ordenación en la parte superior izquierda. Seleccione el origen que desee vista y seleccione el flujo del conjunto de datos en la lista de la derecha.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

Aparece la pantalla de actividad *de flujo de* datos. Esta página muestra la velocidad de los mensajes que se consumen en forma de gráfico.

![dataset-flow-actividad](../../images/tutorials/monitor/dataset-flows-activity.png)

Para obtener más información sobre la supervisión de conjuntos de datos y la ingestión, consulte el tutorial sobre la [supervisión de flujos de datos](../../../ingestion/quality/monitor-data-flows.md)de flujo continuo.

## Pasos siguientes

Siguiendo este tutorial, ha accedido correctamente a las cuentas existentes y a los flujos de conjuntos de datos desde el espacio de trabajo *Fuentes* . Los datos entrantes ahora se pueden utilizar en los servicios de plataforma descendente, como Perfil del cliente en tiempo real y Área de trabajo de ciencias de datos. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../profile/home.md)
- [Información general sobre el área de trabajo de ciencias de datos](../../../data-science-workspace/home.md)