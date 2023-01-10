---
keywords: Experience Platform;inicio;temas populares; eliminar cuentas
description: Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del espacio de trabajo de fuentes.
solution: Experience Platform
title: Eliminar cuentas de conexión de origen en la interfaz de usuario
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Eliminar cuentas de conexión de origen

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del **[!UICONTROL Fuentes]** espacio de trabajo.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición del esquema](../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Eliminar cuentas mediante la interfaz de usuario

>[!TIP]
>
>Antes de eliminar la cuenta de origen, debe eliminar los flujos de datos existentes asociados a la cuenta de origen. Para eliminar flujos de datos existentes, consulte el tutorial sobre [eliminación de flujos de datos de origen en la interfaz de usuario](./delete.md).

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear cuentas y flujos de datos. Cada origen muestra la cantidad de cuentas existentes y flujos de datos asociados a ellas.

Select **[!UICONTROL Cuentas]** para acceder a la **[!UICONTROL Cuentas]** página.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Aparecerá una lista de cuentas existentes. En esta página hay una lista de información que se puede ordenar para cuentas existentes como fuente, nombre de usuario, flujos de datos asociados y fecha de creación. Seleccione el **icono de canal** en la parte superior izquierda para ordenar.

![lista de flujos de datos](../../images/tutorials/delete-accounts/accounts.png)

El panel de ordenación aparece en la parte izquierda de la pantalla y contiene una lista de los orígenes disponibles. Puede seleccionar más de un origen utilizando la función de ordenación.

Seleccione la fuente a la que desea acceder y busque la cuenta que desea eliminar de la lista de cuentas de la interfaz principal. En el ejemplo, el origen seleccionado es **[!DNL Azure Blob Storage]** y el nombre de la cuenta es **[!UICONTROL blobTestConnector]**. Al seleccionar varios orígenes en el panel de ordenación, las cuentas creadas más recientemente aparecen primero porque la lista se ordena por fecha de creación.

Seleccione la cuenta que desee eliminar.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

La variable **[!UICONTROL Propiedades]** aparece a la derecha de la pantalla, con información sobre la cuenta seleccionada.

Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea eliminar. Aparece un panel emergente que proporciona las opciones para **[!UICONTROL Añadir datos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]**. Select **[!UICONTROL Eliminar]** para eliminar la cuenta.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Aparece un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![eliminar](../../images/tutorials/delete-accounts/confirm.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable **[!UICONTROL Fuentes]** espacio de trabajo para eliminar cuentas existentes.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación usando la variable [!DNL Flow Service] API, consulte el tutorial sobre [eliminación de conexiones mediante la API de servicio de flujo](../../tutorials/api/delete.md)
