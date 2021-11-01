---
keywords: Azure Blob;destino de Blob;s3;destino de azure blob
title: Conexión de Azure Blob
description: Cree una conexión saliente en directo al almacenamiento del blob de Azure para exportar periódicamente archivos de datos CSV de Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# [!DNL Azure Blob] connection

## Información general {#overview}

[!DNL Azure Blob] (en lo sucesivo denominados [!DNL Blob]) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona los pasos para crear un [!DNL Blob] destino usando la variable [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Blob] destino, puede omitir el resto de este documento y continuar con el tutorial en [activación de segmentos en el destino](../../ui/activate-batch-profile-destinations.md).

## Formatos de archivo compatibles {#file-formats}

[!DNL Experience Platform] admite el siguiente formato de archivo que se va a exportar a [!DNL Blob]:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. En el futuro se admitirán los archivos DSV generales.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Cadena de conexión]**: la cadena de conexión es necesaria para acceder a los datos del almacenamiento de blob. La variable [!DNL Blob] el patrón de cadena de conexión comienza por: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obtener más información sobre cómo configurar su [!DNL Blob] cadena de conexión, consulte [Configurar una cadena de conexión para una cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.

* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Contenedor]**: introduzca el nombre del [!DNL Azure Blob Storage] contenedor que utilizará este destino.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.
