---
title: Flujo de trabajo de destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de destinos de almacenamiento en la nube
description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

Esta página explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en la plataforma de datos del cliente en tiempo real de Adobe.

1. En **[!UICONTROL Connections > Destinations]**, seleccione su destino preferido de almacenamiento en la nube y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar con destino de almacenamiento en la nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de almacenamiento en la nube, seleccione **[!UICONTROL Existing Account]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión con su destino de almacenamiento en la nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Connect to destination]**.

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la ubicación de almacenamiento en la nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. En el **[!UICONTROL Setup]** paso, introduzca un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación.
   1. Para los destinos de Amazon S3, inserte el **[!UICONTROL Bucket name]** y el **[!UICONTROL Folder path]** en el destino de almacenamiento en la nube donde se entregarán los archivos. Seleccione **[!UICONTROL Create Destination]** una vez rellenados los campos anteriores.
   2. Para los destinos SFTP, inserte la variable **[!UICONTROL Folder path]**
   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para que el resto del flujo de trabajo exporte datos.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.