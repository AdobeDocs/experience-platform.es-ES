---
keywords: eliminar cuenta de destino, cuentas de destino, cómo eliminar cuentas
title: Eliminar cuentas de destino
type: Tutorial
description: Este tutorial enumera los pasos para eliminar cuentas de destino en la interfaz de usuario de Adobe Experience Platform
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Eliminar cuentas de destino

## Información general {#overview}

La variable **[!UICONTROL Cuentas]** muestra los detalles sobre las conexiones que ha establecido con varios destinos. Consulte la [Información general sobre cuentas](../ui/destinations-workspace.md#accounts) para toda la información que pueda obtener en cada cuenta de destino.

Este tutorial trata los pasos para eliminar cuentas de destino que ya no se necesitan mediante la interfaz de usuario del Experience Platform.

![Ficha Cuentas](../assets/ui/update-accounts/destination-accounts.png)

## Eliminar cuentas {#delete}

>[!TIP]
>
>Antes de eliminar la cuenta de destino, debe eliminar los flujos de datos existentes asociados a la cuenta de destino. Para eliminar flujos de datos de destino existentes, consulte el tutorial sobre [eliminación de flujos de datos de destino en la interfaz de usuario](./delete-destinations.md).

Siga los pasos a continuación para eliminar las cuentas de destino existentes.

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Select **[!UICONTROL Cuentas]** en el encabezado superior para ver sus cuentas existentes.

   ![Ficha Cuentas](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/update-accounts/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de cuentas asociadas con los destinos seleccionados.

   ![Filtrar destinos](../assets/ui/delete-accounts/filter-accounts.png)

3. Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea eliminar. Aparece un panel emergente que proporciona las opciones para **[!UICONTROL Activar segmentos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]** la cuenta. Seleccione el ![Botón Eliminar](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Eliminar]** para eliminar la cuenta que desee.

   ![Eliminar cuenta de destino](../assets/ui/delete-accounts/delete-accounts.png)

4. Aparece un cuadro de diálogo de confirmación final, seleccione **[!UICONTROL Eliminar]** para completar el proceso.

![Confirmar eliminación de cuenta](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente el espacio de trabajo de destinos para eliminar cuentas existentes.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación usando la variable [!DNL Flow Service] API, consulte el tutorial sobre [eliminación de conexiones mediante la API de servicio de flujo](../api/delete-destination-account.md)
