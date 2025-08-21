---
title: Información general sobre el conector Source de Azure Blob
description: Obtenga información sobre cómo conectar su cuenta de Azure Blob a Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# Fuente de [!DNL Azure Blob Storage] 

[!DNL Azure Blob Storage] es un servicio de almacenamiento de objetos basado en la nube proporcionado por [!DNL Microsoft Azure]. Está diseñado para almacenar grandes cantidades de datos no estructurados, como texto, imágenes, vídeos, copias de seguridad y registros. Puede usar [!DNL Azure Blob Storage] para almacenar y administrar grandes cantidades de datos no estructurados, como documentos, imágenes, vídeos y archivos de audio. Es ideal para realizar backups y archivar datos, admitir la recuperación ante desastres y gestionar grandes cargas de trabajo de datos para análisis.

Use el origen [!DNL Azure Blob Storage] para conectar su cuenta e ingerir datos de [!DNL Azure Blob Storage] a Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El origen [!DNL Azure Blob] no admite la conectividad de la misma región con Experience Platform. Si la instancia de [!DNL Azure] utiliza la misma región de red que Experience Platform, no se puede establecer una conexión con orígenes de Experience Platform. Actualmente, solo se admite la conectividad entre regiones.

### Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

### Autenticar [!DNL Azure Blob Storage] en Experience Platform {#authentication}

Puede conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform mediante los siguientes tipos de autenticación:

- **Autenticación de clave de cuenta**: Utiliza la clave de acceso de la cuenta de almacenamiento para autenticarse y conectarse a su cuenta de [!DNL Azure Blob Storage].
- **Firma de acceso compartido (SAS)**: Utiliza un URI de SAS para proporcionar acceso delegado y limitado en el tiempo a los recursos de su cuenta de [!DNL Azure Blob Storage].
- **Autenticación basada en entidad de seguridad de servicio**: Utiliza una entidad de seguridad de servicio de Azure Active Directory (AAD) (ID de cliente y secreto) para autenticarse de forma segura en su cuenta de Azure Blob Storage.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Proporcione valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform mediante la autenticación de clave de cuenta.

| Credencial | Descripción |
| --- | --- |
| `connectionString` | La cadena de conexión [!DNL Azure Blob Storage] de su cuenta de almacenamiento. Esta cadena contiene la información necesaria para autenticarse y conectarse a la instancia de [!DNL Azure Blob Storage]. Formato de ejemplo: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | Nombre del contenedor [!DNL Azure Blob Storage] donde se almacenan los archivos de datos. Un contenedor organiza un conjunto de blobs, similar a un directorio de un sistema de archivos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. Es una ruta de subdirectorio opcional (carpeta virtual) dentro del contenedor. Si se deja en blanco, se utiliza la raíz del contenedor. |
| `connectionSpec.id` | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL Azure Blob Storage] es `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información acerca de cómo usar la autenticación de clave de cuenta con [!DNL Azure Blob Storage], lea la [guía de autenticación de Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB Firma de acceso compartido]

Proporcione valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform mediante la firma de acceso compartido.

| Credencial | Descripción |
| --- | --- |
| `SasURI` | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su cuenta. El patrón de URI de SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Para obtener más información, consulte este documento de [!DNL Azure] sobre [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Nombre del contenedor [!DNL Azure Blob Storage] donde se almacenan los archivos de datos. Un contenedor organiza un conjunto de blobs, similar a un directorio de un sistema de archivos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. Es una ruta de subdirectorio opcional (carpeta virtual) dentro del contenedor. Si se deja en blanco, se utiliza la raíz del contenedor. |
| `connectionSpec.id` | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL Azure Blob Storage] es `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información acerca de cómo usar la firma de acceso compartido con [!DNL Azure Blob Storage], lea la [guía de autenticación de Microsoft Azure](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB Autenticación basada en entidad de seguridad de servicio]

Proporcione valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform mediante la autenticación basada en la entidad de seguridad de servicio.

| Credencial | Descripción |
| --- | --- |
| `serviceEndpoint` | La dirección URL de extremo de su cuenta de [!DNL Azure Blob Storage]. Normalmente en el formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | El tipo de su cuenta de [!DNL Azure Blob Storage]. Los valores comunes incluyen `Storage` (propósito general V1), `StorageV2` (propósito general V2), `BlobStorage` y `BlockBlobStorage`. |
| `servicePrincipalId` | Identificador de cliente/aplicación de la entidad de seguridad del servicio de Azure Active Directory (AAD) que se usa para la autenticación. |
| `servicePrincipalKey` | El secreto de cliente o la contraseña asociados con la entidad de seguridad del servicio de Azure. |
| `tenant` | Identificador de inquilino de Azure Active Directory (AAD) donde está registrada la entidad de seguridad de servicio. |
| `container` | Nombre del contenedor de almacenamiento del blob de Azure donde se almacenan los archivos de datos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. Es una ruta de subdirectorio opcional (carpeta virtual) dentro del contenedor. Si se deja en blanco, se utiliza la raíz del contenedor. |
| `connectionSpec.id` | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para Azure Blob Storage es `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información sobre cómo usar la autenticación basada en la entidad de seguridad de servicio con [!DNL Azure Blob Storage], lea la [guía de autenticación de Microsoft Azure](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## Conectar [!DNL Azure Blob Storage] a [!DNL Experience Platform]

La siguiente documentación proporciona información sobre cómo conectar Azure Blob a Adobe Experience Platform mediante API o la interfaz de usuario de:

### Uso de API

- [Conectar [!DNL Azure Blob Storage] a Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Conectar [!DNL Azure Blob Storage] a Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
