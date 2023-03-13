---
keywords: Experience Platform;inicio;temas populares;Azure File Storage;Azure File Storage
solution: Experience Platform
title: Información general del conector de origen de Azure File Storage
description: Obtenga información sobre cómo conectar Azure File Storage a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Conector de Azure File Storage

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform], y [!DNL Azure], lo que le permite obtener los datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden incorporar sus propios datos en [!DNL Platform] sin necesidad de descargar, formatear ni cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes. [!DNL Platform] le permite introducir datos de [!DNL Azure File Storage] mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Connect [!DNL Azure File Storage] hasta [!DNL Platform]

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Azure File Storage] hasta [!DNL Platform] mediante las API de o la interfaz de usuario de:

### Uso de API

- [Crear una conexión base de Azure File Storage mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Crear una conexión de origen de Azure File Storage en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
