---
keywords: Experience Platform;inicio;temas populares;Azure File Storage;almacenamiento de archivos azure
solution: Experience Platform
title: Descripción general del conector de origen de almacenamiento de archivos de Azure
topic-legacy: overview
description: Obtenga información sobre cómo conectar el almacenamiento de archivos de Azure a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: 446436346e3368d98eb990dba1000ac0974b84dc
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Conector de almacenamiento de archivos de Azure

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure], lo que le permite obtener sus datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos de  [!DNL Azure File Storage] mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones a las que debe tener en cuenta al asignar un nombre al archivo o directorio de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Conectar [!DNL Azure File Storage] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure File Storage] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión base de almacenamiento de archivos de Azure mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explorar la estructura de datos y el contenido de un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Crear una conexión de origen de almacenamiento de archivos de Azure en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
