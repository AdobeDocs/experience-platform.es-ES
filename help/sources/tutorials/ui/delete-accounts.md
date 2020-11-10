---
keywords: Experience Platform;home;popular topics; delete accounts
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del espacio de trabajo Fuentes.
solution: Experience Platform
title: Eliminar cuentas
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Eliminar cuentas

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del espacio de trabajo **[!UICONTROL Fuentes]** .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

## Eliminar cuentas mediante la interfaz de usuario

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes para los que puede crear cuentas y flujos de datos. Cada origen muestra el número de cuentas existentes y flujos de datos asociados a ellas.

Seleccione **[!UICONTROL Cuentas]** para acceder a la página **[!UICONTROL Cuentas]** .

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Aparece una lista de las cuentas existentes. En esta página hay una lista de información que se puede ordenar para cuentas existentes como, por ejemplo, origen, nombre de usuario, flujos de datos asociados y fecha de creación. Seleccione el icono **del** canal en la parte superior izquierda para ordenar.

![lista de flujos de datos](../../images/tutorials/delete-accounts/accounts.png)

El panel de ordenación aparece en el lado izquierdo de la pantalla, con una lista de los orígenes disponibles. Puede seleccionar más de un origen mediante la función de ordenación.

Seleccione la fuente a la que desea acceder y localice la cuenta que desea eliminar de la lista de cuentas en la interfaz principal. En el ejemplo, el origen seleccionado es **[!DNL Azure Blob Storage]** y el nombre de la cuenta es **[!UICONTROL blobTestConnector]**. Al seleccionar varios orígenes en el panel de ordenación, las cuentas creadas más recientemente aparecen primero porque la lista se ordena por fecha de creación.

Seleccione la cuenta que desee eliminar.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

El panel **[!UICONTROL Propiedades]** aparece en la parte derecha de la pantalla y contiene información sobre la cuenta seleccionada.

Seleccione las elipses (`...`) al lado del nombre de la cuenta que desea eliminar. Aparece un panel emergente con opciones para **[!UICONTROL Añadir datos]**, **[!UICONTROL editar detalles]** y **[!UICONTROL eliminar]**. Seleccione **[!UICONTROL Eliminar]** para eliminar la cuenta.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Aparecerá un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el espacio de trabajo **[!UICONTROL Fuentes]** para eliminar las cuentas existentes.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante la [!DNL Flow Service] API, consulte el tutorial sobre la [eliminación de conexiones mediante la API de servicio de flujo](../../tutorials/api/delete.md)