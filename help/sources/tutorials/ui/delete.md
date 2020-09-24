---
keywords: Experience Platform;home;popular topics; delete dataflows
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para eliminar flujos de datos del espacio de trabajo Fuentes.
solution: Experience Platform
title: Eliminar flujos de datos
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# Eliminar flujos de datos

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona pasos para eliminar flujos de datos del espacio de trabajo [!UICONTROL Fuentes] .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!Perfil del cliente en tiempo real de DNL]](../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Eliminar flujos de datos mediante la interfaz de usuario

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes para los que puede crear cuentas y flujos de datos. Cada origen muestra el número de cuentas existentes y flujos de datos asociados a ellas.

Seleccione **[!UICONTROL Flujos]** de datos para acceder a la página **[!UICONTROL Flujos]** de datos.

![dataset-flow-actividad](../../images/tutorials/delete/dataflows.png)

Aparece una lista de flujos de datos existentes. En esta página hay una lista de información que se puede ordenar para flujos de datos existentes como origen, nombre de usuario, estado de ejecución y fecha de la última ejecución. Seleccione el icono **del** canal en la parte superior izquierda para ordenar.

![lista de flujos de datos](../../images/tutorials/delete/dataflows-list.png)

El panel de ordenación aparece en el lado izquierdo de la pantalla, con una lista de los orígenes disponibles.
Puede seleccionar más de un origen mediante la función de ordenación.

Seleccione el origen al que desea acceder y localice el flujo de datos que desea eliminar de la lista de flujos de datos en la interfaz principal. En el ejemplo, el origen seleccionado es **[!DNL Azure Blob Storage]** y el nombre del flujo de datos es el flujo de datos de perfiles **[!UICONTROL del cliente]**. Al seleccionar varios orígenes en el panel de ordenación, los flujos de datos creados más recientemente aparecen primero porque la lista se ordena por fecha de creación.

Seleccione el flujo de datos que desea eliminar.

![dataflows-sort](../../images/tutorials/delete/dataflows-sort.png)

El panel **[!UICONTROL Propiedades]** aparece en la parte derecha de la pantalla y contiene información sobre el flujo de datos seleccionado, así como una opción para **[!UICONTROL editar la programación]**.

Para eliminar el flujo de datos, seleccione **[!UICONTROL Eliminar]**.

![dataflows-sort](../../images/tutorials/delete/dataflows-properties.png)

Aparecerá un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![delete](../../images/tutorials/delete/delete.png)

Después de unos momentos, aparece un cuadro de confirmación verde en la parte inferior de la pantalla para confirmar que la eliminación se ha realizado correctamente.

![confirmado](../../images/tutorials/delete/confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, se ha accedido correctamente a las cuentas y flujos de datos existentes desde el espacio de trabajo **[!UICONTROL Fuentes]** . Los datos entrantes ahora pueden ser utilizados por servicios [!DNL Platform] descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [[!DNL Real-time Customer Profile] sobre validación](../../../profile/home.md)
- [[!DNL Data Science Workspace] sobre validación](../../../data-science-workspace/home.md)