---
keywords: destino de almacenamiento en la nube;almacenamiento en la nube
title: Crear un destino de almacenamiento en la nube
type: Tutorial
description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento en la nube
exl-id: 58003c1e-2f70-4e28-8a38-3be00da7cc3c
translation-type: tm+mt
source-git-commit: 7bb862c4c6c52c42e45d5e736fa6d239e812ac2c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Crear un destino de almacenamiento en la nube

## Información general {#overview}

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en Adobe Experience Platform.

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione su destino preferido de almacenamiento en la nube y, a continuación, seleccione **[!UICONTROL Configure]**.

![Conectarse al destino de almacenamiento en la nube](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

## Paso de cuenta {#account}

En el paso **[!UICONTROL Account]**, si ha configurado anteriormente una conexión con su destino de almacenamiento en la nube, seleccione **[!UICONTROL Existing Account]** y la conexión existente. O bien, puede seleccionar **[!UICONTROL New Account]** para configurar una nueva conexión con su destino de almacenamiento en la nube. Complete las credenciales de autenticación de la cuenta y seleccione **[!UICONTROL Connect to destination]**. Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada [!DNL Base64].

Consulte [Destino de Amazon S3](./amazon-s3.md), destino [[!DNL Amazon Kinesis]](./amazon-kinesis.md), destino [[!DNL Azure Event Hubs]](./azure-event-hubs.md) y destino [SFTP](./sftp.md) para obtener información específica sobre las credenciales introducidas en el paso **Autenticación**.

>[!NOTE]
>
>Platform admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en la ubicación de almacenamiento en la nube. Esto garantiza que no complete el flujo de trabajo con credenciales incorrectas.

![Conectarse al destino de almacenamiento en la nube: paso de la cuenta](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## Paso de autenticación {#authentication}

En el paso **[!UICONTROL Authentication]**, introduzca un **[!UICONTROL Name]** y un **[!UICONTROL Description]** para el flujo de activación.

En este paso, también puede seleccionar cualquier **[!UICONTROL Marketing action]** que deba aplicarse a este destino. Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

Para destinos de Amazon S3, inserte **[!UICONTROL Bucket name]** y **[!UICONTROL Folder path]** en el destino de almacenamiento en la nube donde se enviarán los archivos. Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectarse al destino de almacenamiento en la nube Amazon S3: paso de autenticación](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Para los destinos SFTP, inserte el **[!UICONTROL Folder path]** donde se enviarán los archivos. Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectarse al destino de almacenamiento en la nube SFTP: paso de autenticación](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Para destinos [!DNL Amazon Kinesis], proporcione el nombre del flujo de datos existente en su cuenta [!DNL Amazon Kinesis]. Platform exportará datos a este flujo. Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectarse al destino de almacenamiento en la nube de Kinesis: paso de autenticación](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Para destinos [!DNL Azure Event Hubs], proporcione el nombre del flujo de datos existente en su cuenta [!DNL Amazon Event Hubs]. Platform exportará datos a este flujo. Seleccione **[!UICONTROL Create Destination]** después de rellenar los campos anteriores.

![Conectarse al destino de almacenamiento en la nube de los centros de eventos: paso de autenticación](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Save & Exit]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Next]** para continuar con el flujo de trabajo y seleccionar segmentos para activarlos. Lea la sección [Activar segmentos](#activate-segments) para que el resto del flujo de trabajo exporte datos.

## Utilice macros para crear una carpeta en su ubicación de almacenamiento{#use-macros}

Para crear una carpeta personalizada por archivo de segmento en su ubicación de almacenamiento, puede utilizar macros en el campo de entrada de ruta de carpeta. Inserte las macros al final del campo de entrada, como se muestra a continuación.

![Cómo usar macros para crear una carpeta en el almacenamiento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Los ejemplos siguientes hacen referencia a un segmento de muestra `Luxury Audience` con ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_ID%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`



## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.
