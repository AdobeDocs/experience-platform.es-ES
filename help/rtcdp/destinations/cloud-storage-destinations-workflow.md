---
title: Flujo de trabajo de los destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de los destinos de almacenamiento en la nube
description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en la plataforma de datos del cliente en tiempo real de Adobe.

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione el destino de almacenamiento de nube preferido y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar con destino de almacenamiento de nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. En el paso **[!UICONTROL Autenticación]** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de almacenamiento de nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. <br> Consulte Destino de [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , Destino de [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) , Destino de centros [de Evento de](/help/rtcdp/destinations/azure-event-hubs-destination.md) Azure y Destino de [SFTP](/help/rtcdp/destinations/sftp-destination.md) para obtener detalles sobre la introducción de credenciales en el paso **Autenticación** .

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la ubicación del almacenamiento en la nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. En el paso **[!UICONTROL Configuración]** , introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación. <br>
Para los destinos de Amazon S3, inserte el nombre **[!UICONTROL del]** bucket y la ruta **[!UICONTROL de la]** carpeta en el destino de almacenamiento de nube donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento en la nube Amazon S3: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Para los destinos SFTP, inserte la ruta **[!UICONTROL de]** carpeta donde se enviarán los archivos.

   ![Conectar con destino de almacenamiento de nube SFTP: paso de autenticación](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para que el resto del flujo de trabajo exporte datos.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.