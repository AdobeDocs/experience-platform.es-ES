---
keywords: Experience Platform;inicio;temas populares; eliminar cuentas
description: Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del espacio de trabajo de orígenes.
solution: Experience Platform
title: Eliminar cuentas de conexión de origen en la IU
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Eliminar cuentas de conexión de origen

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas de la **[!UICONTROL Fuentes]** workspace.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Conceptos básicos de composición de esquemas](../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Eliminación de cuentas mediante la IU

>[!TIP]
>
>Antes de eliminar la cuenta de origen, primero debe eliminar cualquier flujo de datos existente asociado a la cuenta de origen. Para eliminar flujos de datos existentes, consulte el tutorial sobre [Eliminar flujos de datos de origen en la IU](./delete.md).

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear cuentas y flujos de datos con. Cada fuente muestra el número de cuentas y flujos de datos existentes asociados a ellas.

Seleccionar **[!UICONTROL Cuentas]** para acceder a **[!UICONTROL Cuentas]** página.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Aparecerá una lista de cuentas existentes. En esta página hay una lista de información que se puede ordenar para cuentas existentes como origen, nombre de usuario, flujos de datos asociados y fecha de creación. Seleccione el **icono de canal** en la parte superior izquierda para ordenar.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

El panel de ordenación aparece en la parte izquierda de la pantalla y contiene una lista de orígenes disponibles. Puede seleccionar más de un origen mediante la función de ordenación.

Seleccione el origen al que desea acceder y busque la cuenta que desea eliminar de la lista de cuentas de la interfaz principal. En el ejemplo, la fuente seleccionada es **[!DNL Azure Blob Storage]** y el nombre de la cuenta es **[!UICONTROL blobTestConnector]**. Al seleccionar varios orígenes en el panel de ordenación, las cuentas creadas más recientemente aparecen primero porque la lista se ordena por fecha de creación.

Seleccione la cuenta que desea eliminar.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

El **[!UICONTROL Propiedades]** el panel aparece a la derecha de la pantalla y contiene información sobre la cuenta seleccionada.

Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea eliminar. Aparecerá un panel emergente con las opciones siguientes **[!UICONTROL Añadir datos]**, **[!UICONTROL Editar detalles]**, y **[!UICONTROL Eliminar]**. Seleccionar **[!UICONTROL Eliminar]** para eliminar la cuenta.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Aparece un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable **[!UICONTROL Fuentes]** espacio de trabajo para eliminar cuentas existentes.

Para obtener información sobre los pasos para realizar estas operaciones mediante programación usando [!DNL Flow Service] API, consulte el tutorial sobre [eliminación de conexiones mediante la API de Flow Service](../../tutorials/api/delete.md)
