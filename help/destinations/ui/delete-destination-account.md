---
keywords: eliminar cuenta de destino, cuentas de destino, cómo eliminar cuentas
title: Eliminar cuentas de destino
type: Tutorial
description: Este tutorial enumera los pasos para eliminar cuentas de destino en la interfaz de usuario de Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Eliminar cuentas de destino

## Información general {#overview}

El **[!UICONTROL Cuentas]** La pestaña muestra detalles sobre las conexiones que ha establecido con varios destinos. Consulte la [Resumen de cuentas](../ui/destinations-workspace.md#accounts) para toda la información que puede obtener en cada cuenta de destino.

Este tutorial trata los pasos para eliminar cuentas de destino que ya no se necesitan mediante la interfaz de usuario de Experience Platform.

![Pestaña Cuentas](../assets/ui/update-accounts/destination-accounts.png)

## Eliminar cuentas {#delete}

>[!TIP]
>
>Antes de eliminar la cuenta de destino, primero debe eliminar cualquier flujo de datos existente asociado a la cuenta de destino. Para eliminar flujos de datos de destino existentes, consulte el tutorial sobre [eliminación de flujos de datos de destino en la IU](./delete-destinations.md).

Siga los pasos a continuación para eliminar las cuentas de destino existentes.

1. Inicie sesión en [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Seleccionar **[!UICONTROL Cuentas]** desde el encabezado superior para ver sus cuentas existentes.

   ![Pestaña Cuentas](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/update-accounts/filter.png) en la parte superior izquierda para iniciar el panel ordenar. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de cuentas asociadas con los destinos seleccionados.

   ![Filtrar destinos](../assets/ui/delete-accounts/filter-accounts.png)

3. Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea eliminar. Aparecerá un panel emergente con las opciones siguientes **[!UICONTROL Activar audiencias]**, **[!UICONTROL Editar detalles]**, y **[!UICONTROL Eliminar]** la cuenta. Seleccione el ![Botón Eliminar](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Eliminar]** para eliminar la cuenta deseada.

   ![Eliminar cuenta de destino](../assets/ui/delete-accounts/delete-accounts.png)

4. Aparece un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![Confirmar eliminación de cuenta](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo de destinos para eliminar cuentas existentes.

Para obtener información sobre los pasos para realizar estas operaciones mediante programación usando [!DNL Flow Service] API, consulte el tutorial sobre [eliminación de conexiones mediante la API de Flow Service](../api/delete-destination-account.md)
