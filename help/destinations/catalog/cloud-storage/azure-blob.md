---
keywords: Azure Blob;destino de Blob;s3;destino de azure blob
title: Conexión de Azure Blob
description: Cree una conexión saliente en directo al almacenamiento del blob de Azure para exportar periódicamente archivos de datos de Adobe Experience Platform delimitados por tabulaciones o CSV.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# [!DNL Azure Blob] connection

## Información general {#overview}

[!DNL Azure Blob] (en lo sucesivo denominada  [!DNL Blob]) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona pasos para crear un destino [!DNL Blob] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene un destino [!DNL Blob] válido, puede omitir el resto de este documento y continuar con el tutorial sobre la [activación de segmentos en el destino](../../ui/activate-destinations.md).

## Formatos de archivo compatibles {#file-formats}

[!DNL Experience Platform] admite el siguiente formato de archivo para exportar a  [!DNL Blob]:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. En el futuro se admitirán los archivos DSV generales. Para obtener más información sobre los archivos compatibles, lea la sección almacenamiento en la nube en el tutorial sobre [activación de destinos](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Cadena]** de conexión: la cadena de conexión es necesaria para acceder a los datos del almacenamiento de blob. El patrón de la cadena de conexión [!DNL Blob] comienza por: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obtener más información sobre la configuración de la cadena de conexión [!DNL Blob], consulte [Configuración de una cadena de conexión para una cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.

* Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada [!DNL Base64].
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Ruta de acceso]** de la carpeta: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Contenedor]**: introduzca el nombre del  [!DNL Azure Blob Storage] contenedor que usará este destino.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada [!DNL Base64].

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.
