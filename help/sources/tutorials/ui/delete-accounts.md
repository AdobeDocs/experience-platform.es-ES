---
keywords: Experience Platform;inicio;temas populares; eliminar cuentas
description: Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del espacio de trabajo de orígenes.
solution: Experience Platform
title: Eliminar cuentas de conexión de Source en la IU
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Eliminar cuentas de conexión de origen

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para eliminar cuentas del área de trabajo **[!UICONTROL Sources]**.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   - [Aspectos básicos de la composición de esquemas](../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

## Eliminación de cuentas mediante la IU

>[!TIP]
>
>Antes de eliminar la cuenta de origen, primero debe eliminar cualquier flujo de datos existente asociado a la cuenta de origen. Para eliminar flujos de datos existentes, consulte el tutorial sobre [eliminar flujos de datos de origen en la interfaz de usuario](./delete.md).

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear cuentas y flujos de datos. Cada fuente muestra el número de cuentas y flujos de datos existentes asociados a ellas.

Seleccione **[!UICONTROL Cuentas]** para acceder a la página **[!UICONTROL Cuentas]**.

![cuentas de catálogo](../../images/tutorials/delete-accounts/catalog.png)

Aparecerá una lista de cuentas existentes. En esta página hay una lista de información que se puede ordenar para cuentas existentes como origen, nombre de usuario, flujos de datos asociados y fecha de creación. Seleccione el **icono de embudo** en la parte superior izquierda para ordenar.

![lista de flujos de datos](../../images/tutorials/delete-accounts/accounts.png)

El panel de ordenación aparece en la parte izquierda de la pantalla y contiene una lista de orígenes disponibles. Puede seleccionar más de un origen mediante la función de ordenación.

Seleccione el origen al que desea acceder y busque la cuenta que desea eliminar de la lista de cuentas de la interfaz principal. En el ejemplo, el origen seleccionado es **[!DNL Azure Blob Storage]** y el nombre de cuenta es **[!UICONTROL blobTestConnector]**. Al seleccionar varios orígenes en el panel de ordenación, las cuentas creadas más recientemente aparecen primero porque la lista se ordena por fecha de creación.

Seleccione la cuenta que desea eliminar.

![flujos de datos-sort](../../images/tutorials/delete-accounts/sort.png)

El panel **[!UICONTROL Propiedades]** aparece a la derecha de la pantalla y contiene información sobre la cuenta seleccionada.

Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea eliminar. Aparece un panel emergente que proporciona opciones para **[!UICONTROL Agregar datos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]**. Seleccione **[!UICONTROL Eliminar]** para eliminar la cuenta.

![flujos de datos-sort](../../images/tutorials/delete-accounts/delete.png)

Aparece un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![eliminar](../../images/tutorials/delete-accounts/confirm.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el área de trabajo **[!UICONTROL Sources]** para eliminar cuentas existentes.

Para obtener información sobre cómo realizar estas operaciones mediante programación usando la API [!DNL Flow Service], consulte el tutorial sobre [eliminación de conexiones mediante la API de Flow Service](../../tutorials/api/delete.md)
