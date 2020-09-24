---
keywords: cloud storage destination;cloud storage
title: Flujo de trabajo de los destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de los destinos de almacenamiento en la nube
type: Tutorial
description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en la plataforma de datos del cliente en tiempo real de Adobe.

1. En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione el destino de almacenamiento en la nube preferido y, a continuación, seleccione **[!UICONTROL Configurar]**.

   ![Conectar con destino de almacenamiento de nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

   >[!NOTE]
   >
   >Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

2. En el paso **[!UICONTROL Autenticación]** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de almacenamiento de nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. <br> Consulte Destino de [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , destino [[!DNL Amazon Kinesis]](/help/rtcdp/destinations/amazon-kinesis-destination.md) , destino [[!DNL Azure Evento Hubs]](/help/rtcdp/destinations/azure-event-hubs-destination.md) y destino [SFTP](/help/rtcdp/destinations/sftp-destination.md) para obtener detalles sobre la introducción de credenciales en el paso **Autenticación** .

   >[!NOTE]
   >
   >CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en la ubicación del almacenamiento de nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. En el paso **[!UICONTROL Configuración]** , introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación. <br>
También en este paso, puede seleccionar cualquier caso **[!UICONTROL de uso de]** Marketing que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos. <br>
Para los destinos de Amazon S3, inserte el nombre **[!UICONTROL del]** depósito y la ruta **[!UICONTROL de]** carpeta en el destino de almacenamiento de nube donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento en la nube Amazon S3: paso de autenticación](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Para los destinos SFTP, inserte la ruta **[!UICONTROL de]** carpeta donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento de nube SFTP: paso de autenticación](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Para [!DNL Amazon Kinesis] los destinos, especifique el nombre del flujo de datos existente en la [!DNL Amazon Kinesis] cuenta. CDP en tiempo real de Adobe exportará datos a este flujo. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento de nube de Kinesis: paso de autenticación](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Para [!DNL Azure Event Hubs] los destinos, especifique el nombre del flujo de datos existente en la [!DNL Amazon Kinesis] cuenta. CDP en tiempo real de Adobe exportará datos a este flujo. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

   ![Conectar con destino de almacenamiento de nube de Kinesis: paso de autenticación](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para que el resto del flujo de trabajo exporte datos.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.