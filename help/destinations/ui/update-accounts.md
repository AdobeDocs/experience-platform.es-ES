---
keywords: actualizar cuenta de destino;cuentas de destino;cómo actualizar cuentas
title: Actualizar cuentas de destino
type: Tutorial
description: Este tutorial enumera los pasos para actualizar las cuentas de destino en la interfaz de usuario de Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 6fd980b486c4a330f9188065bac55c624af584a1
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# Actualizar cuentas de destino

## Información general {#overview}

La pestaña **[!UICONTROL Accounts]** muestra detalles sobre las conexiones que ha establecido con varios destinos. Consulte la tabla siguiente para obtener toda la información sobre cada destino:

![Ficha Cuentas](../assets/ui/update-accounts/destination-accounts.png)

| Elemento | Descripción |
---------|----------
| [!UICONTROL Platform] | Destino para el que ha configurado la conexión. |
| [!UICONTROL Connection Type] | Representa el tipo de conexión con su espacio de almacenamiento o destino. <ul><li>Para destinos de marketing por correo electrónico: Puede ser S3 o FTP.</li><li>Para destinos de publicidad en tiempo real: Servidor a servidor</li><li>Para destinos de almacenamiento en la nube Amazon S3: Clave de acceso </li><li>Para destinos de almacenamiento en la nube SFTP: Autenticación básica para SFTP</li></ul> |
| [!UICONTROL Username] | El nombre de usuario seleccionado en el asistente de [conexión de destino](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Representa el número de flujos de destino correctos únicos conectados con la información básica creada para un destino. |
| [!UICONTROL Authorized] | La fecha en la que se autorizó la conexión a este destino. |

## Actualizar cuentas {#update}

Siga los pasos a continuación para actualizar los detalles de conexión a destinos existentes.

1. Inicie sesión en la [IU del Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda. Seleccione **[!UICONTROL Accounts]** en el encabezado superior para ver las cuentas existentes.

   ![Ficha Cuentas](../assets/ui/update-accounts/accounts-tab.png)

2. Seleccione el icono de filtro ![Filter-icon](../assets/ui/update-accounts/filter.png) en la parte superior izquierda para iniciar el panel de ordenación. El panel de ordenación proporciona una lista de todos sus destinos. Puede seleccionar más de un destino de la lista para ver una selección filtrada de cuentas asociadas con los destinos seleccionados.

   ![Filtrar destinos](../assets/ui/update-accounts/filter-accounts.png)

3. Seleccione el botón ![Edit account button](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** en la columna **[!UICONTROL Platform]** para editar la información de la cuenta.

   ![Ficha Cuentas](../assets/ui/update-accounts/accounts-edit.png)

4. Introduzca las credenciales de cuenta actualizadas.

   * Para las cuentas que utilizan un tipo de conexión `OAuth2`, seleccione **[!UICONTROL Reconnect OAuth]** para renovar las credenciales de la cuenta.

      ![Editar detalles OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * En el caso de las cuentas que utilizan un tipo de conexión `Access Key` o `ConnectionString`, puede editar la información de autenticación de la cuenta, incluida información como ID de acceso, claves secretas o cadenas de conexión.

      ![Editar detalles Clave de acceso](../assets/ui/update-accounts/edit-details-key.png)

5. Seleccione **[!UICONTROL Save]** para finalizar la actualización de credenciales.
