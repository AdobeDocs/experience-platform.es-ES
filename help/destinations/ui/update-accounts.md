---
keywords: actualizar cuenta de destino, cuentas de destino, cómo actualizar cuentas, actualizar destino
title: Actualizar cuentas de destino
type: Tutorial
description: Este tutorial enumera los pasos para actualizar las cuentas de destino en la interfaz de usuario de Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Actualizar cuentas de destino

## Información general {#overview}

La variable **[!UICONTROL Cuentas]** muestra los detalles sobre las conexiones que ha establecido con varios destinos. Consulte la [Información general sobre cuentas](../ui/destinations-workspace.md#accounts) para toda la información que pueda obtener en cada cuenta de destino.

Este tutorial trata los pasos para actualizar los detalles de la cuenta de destino mediante la interfaz de usuario del Experience Platform.

Puede actualizar los detalles de la cuenta de destino para actualizar y volver a autenticar las credenciales de las cuentas actuales o caducadas de los destinos que esté utilizando en ese momento. Normalmente, OAuth y los tokens de portador tienen una duración limitada, según la plataforma de destino. Cuando estos tokens caducan, puede actualizarlos en el flujo de trabajo que se describe a continuación. Este flujo de trabajo le indica que vaya a través del flujo de trabajo de OAuth o que vuelva a insertar un token. Del mismo modo, si ha cambiado una contraseña o acceso de usuario en la plataforma descendente, puede actualizar las credenciales.

Para los destinos por lotes, puede actualizar la clave secreta o de acceso si cualquiera de ellas ha cambiado. Además, si desea cifrar los archivos que se van a avanzar, puede insertar una clave pública RSA y los archivos exportados se cifrarán a partir de ahora.

![Ficha Cuentas](../assets/ui/update-accounts/destination-accounts.png)

## Actualizar cuentas {#update}

Siga los pasos a continuación para actualizar los detalles de conexión a destinos existentes.

1. Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda. Select **[!UICONTROL Cuentas]** en el encabezado superior para ver sus cuentas existentes.

   ![Ficha Cuentas](../assets/ui/update-accounts/accounts-tab.png)

2. Seleccione el icono de filtro ![Icono de filtro](../assets/ui/update-accounts/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de cuentas asociadas con los destinos seleccionados.

   ![Filtrar cuentas de destino](../assets/ui/update-accounts/filter-accounts.png)

3. Seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta que desea actualizar. Aparece un panel emergente que proporciona las opciones para **[!UICONTROL Activar segmentos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]** la cuenta. Seleccione el ![Botón Editar detalles](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Editar detalles]** para editar la información de la cuenta.

   ![Editar cuenta](../assets/ui/update-accounts/accounts-edit.png)

4. Introduzca las credenciales de cuenta actualizadas.

   * Para cuentas que usan un `OAuth1` o `OAuth2` tipo de conexión, seleccione **[!UICONTROL Vuelva a conectar OAuth]** para renovar las credenciales de su cuenta. También puede actualizar el nombre y la descripción de su cuenta.

   ![Editar detalles OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * Para cuentas que usan un `Access Key` o `ConnectionString` tipo de conexión, puede editar la información de autenticación de su cuenta, incluida información como el ID de acceso, las claves secretas o las cadenas de conexión. También puede actualizar el nombre y la descripción de su cuenta.

   ![Editar detalles Clave de acceso](../assets/ui/update-accounts/edit-details-key.png)

   * Para cuentas que usan un `Bearer token` tipo de conexión, puede introducir un nuevo token al portador, si es necesario. También puede actualizar el nombre y la descripción de su cuenta.

   ![Editar detalles Token de portador](../assets/ui/update-accounts/edit-details-bearer.png)

   * Para cuentas que usan un `Server to server` tipo de conexión, puede actualizar el nombre y la descripción de su cuenta.

   ![Editar detalles de servidor a servidor](../assets/ui/update-accounts/edit-details-s2s.png)

5. Select **[!UICONTROL Guardar]** para finalizar la actualización de los detalles de la cuenta.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable **[!UICONTROL destinos]** espacio de trabajo para actualizar cuentas existentes.

Para obtener más información sobre los destinos, consulte [información general sobre destinos](../catalog/overview.md).