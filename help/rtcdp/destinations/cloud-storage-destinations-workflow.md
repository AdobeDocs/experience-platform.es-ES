---
title: Flujo de trabajo de los destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de los destinos de almacenamiento en la nube
description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
translation-type: tm+mt
source-git-commit: 60b10aa823af55d6f38651308dc93eeb57a7fee6

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en la plataforma de datos del cliente en tiempo real de Adobe.

1. En **[!UICONTROL Connections > Destinations]**, seleccione su destino de almacenamiento de nube preferido y, a continuación, seleccione **[!UICONTROL Connect destination]**.

   ![Conectar con destino de almacenamiento de nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. En el paso **Autenticación** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione **[!UICONTROL Existing Account]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** configurar una nueva conexión con su destino de almacenamiento de nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Connect to destination]**. Consulte Destino [](/help/rtcdp/destinations/amazon-s3-destination.md) de Amazon S3 y destino [](/help/rtcdp/destinations/sftp-destination.md) SFTP para obtener detalles sobre las credenciales introducidas en el paso **Autenticación** .

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la ubicación del almacenamiento en la nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. En el **[!UICONTROL Setup]** paso, introduzca un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación. <br>
Para los destinos de Amazon S3, inserte el **[!UICONTROL Bucket name]** y el **[!UICONTROL Folder path]** en el destino de almacenamiento de nube donde se enviarán los archivos. Seleccione **[!UICONTROL Create Destination]** una vez rellenados los campos anteriores.

   ![Conectar con destino de almacenamiento en la nube Amazon S3: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Para los destinos SFTP, inserte el **[!UICONTROL Folder path]** lugar donde se enviarán los archivos.

   ![Conectar con destino de almacenamiento de nube SFTP: paso de autenticación](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para que el resto del flujo de trabajo exporte datos.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.