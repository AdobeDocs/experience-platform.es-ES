---
title: Flujo de trabajo de los destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de los destinos de almacenamiento en la nube
description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en Adobe Real-time Customer Data Platform.

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione el destino de almacenamiento de nube preferido y, a continuación, seleccione Destino **[!UICONTROL de]** Connect.

   ![Conectar con destino de almacenamiento de nube](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. En el paso **[!UICONTROL Autenticación]** , si previamente ha configurado una conexión con el destino de almacenamiento de nube, seleccione Cuenta **** existente y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de almacenamiento de nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. <br> Consulte Destino, destino, destino [y destino de](/help/rtcdp/destinations/amazon-s3-destination.md) SFTP [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) de Amazon S3 [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) para obtener información detallada sobre las credenciales introducidas en el paso [Autenticación](/help/rtcdp/destinations/sftp-destination.md) **** .

   >[!NOTE]
   >
   >El CDP en tiempo real de Adobe admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si se introducen credenciales incorrectas en la ubicación del almacenamiento en la nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

   ![Conectar con destino de almacenamiento en la nube: paso de autenticación](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. En el paso **[!UICONTROL Configuración]** , introduzca un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación. <br>
También en este paso, puede seleccionar cualquier caso **[!UICONTROL de uso de]** Marketing que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos de uso de mercadotecnia definidos por Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos. <br>
Para los destinos de Amazon S3, inserte el nombre **[!UICONTROL del]** bucket y la ruta **[!UICONTROL de la]** carpeta en el destino de almacenamiento de nube donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

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