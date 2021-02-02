---
keywords: destino de almacenamiento de nube;almacenamiento de nube
title: Flujo de trabajo de los destinos de almacenamiento en la nube
seo-title: Flujo de trabajo de los destinos de almacenamiento en la nube
type: Tutorial
description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
seo-description: Instrucciones para conectarse a las ubicaciones de almacenamiento de la nube
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Flujo de trabajo para crear destinos de almacenamiento en la nube

## Información general

En esta página se explica cómo puede conectarse a ubicaciones de almacenamiento en la nube en Adobe Experience Platform.

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione el destino de almacenamiento en la nube que prefiera y, a continuación, seleccione **[!UICONTROL Configurar]**.

![Conectar con destino de almacenamiento de nube](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **[!UICONTROL Autenticación]**, si anteriormente había configurado una conexión con el destino del almacenamiento de nube, seleccione **[!UICONTROL Cuenta existente]** y seleccione la conexión existente. O bien, puede seleccionar **[!UICONTROL Nueva cuenta]** para configurar una nueva conexión con su destino de almacenamiento de nube. Rellene las credenciales de autenticación de cuenta y seleccione **[!UICONTROL Conectar con destino]**. Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar encriptación a sus archivos exportados. Tenga en cuenta que esta clave pública **debe** escribirse como una cadena con codificación Base64.

Consulte [Destino de Amazon S3](./amazon-s3.md), [[!DNL Amazon Kinesis]](./amazon-kinesis.md) destino, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) destino y [destino de SFTP](./sftp.md) para obtener detalles sobre las credenciales introducidas en el paso **Autenticación**.

>[!NOTE]
>
>La plataforma admite la validación de credenciales en el proceso de autenticación y muestra un mensaje de error si introduce credenciales incorrectas en la ubicación del almacenamiento de nube. Esto garantiza que no se complete el flujo de trabajo con credenciales incorrectas.

![Conectar con destino de almacenamiento en la nube: paso de autenticación](../../assets/catalog/cloud-storage/workflow/destination-account.png)

En el paso **[!UICONTROL Configuración]**, escriba un **[!UICONTROL Nombre]** y una **[!UICONTROL Descripción]** para el flujo de activación.

También en este paso, puede seleccionar cualquier **[!UICONTROL caso de uso de mercadotecnia]** que deba aplicarse a este destino. Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

Para los destinos de Amazon S3, inserte el **[!UICONTROL nombre del contenedor]** y la **[!UICONTROL ruta de carpeta]** en el destino de almacenamiento en la nube donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

![Conectar con destino de almacenamiento en la nube Amazon S3: paso de autenticación](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Para los destinos SFTP, inserte la **[!UICONTROL ruta de carpeta]** donde se enviarán los archivos. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

![Conectar con destino de almacenamiento de nube SFTP: paso de autenticación](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Para destinos [!DNL Amazon Kinesis], proporcione el nombre del flujo de datos existente en su cuenta [!DNL Amazon Kinesis]. La plataforma exportará datos a este flujo. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

![Conectar con destino de almacenamiento de nube de Kinesis: paso de autenticación](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Para destinos [!DNL Azure Event Hubs], proporcione el nombre del flujo de datos existente en su cuenta [!DNL Amazon Event Hubs]. La plataforma exportará datos a este flujo. Seleccione **[!UICONTROL Crear destino]** después de completar los campos anteriores.

![Conectar con destino de almacenamiento de nube de centros de Evento: paso de autenticación](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Se ha creado el destino. Puede seleccionar **[!UICONTROL Guardar y salir]** si desea activar segmentos más adelante o puede seleccionar **[!UICONTROL Siguiente]** para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para que el resto del flujo de trabajo exporte datos.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.