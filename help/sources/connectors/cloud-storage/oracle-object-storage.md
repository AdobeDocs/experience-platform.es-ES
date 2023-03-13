---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Información general sobre el conector de origen de almacenamiento de objetos oracle
description: Obtenga información sobre cómo conectar Almacenamiento de objetos de Oracle a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Conector de almacenamiento de objetos oracle

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform], lo que le permite introducir datos de estos sistemas en Platform para utilizarlos en servicios y destinos descendentes.

Las fuentes de almacenamiento en la nube pueden llevar los datos a Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. Platform le permite introducir datos de [!DNL Oracle Object Storage] mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode tampoco están permitidos, como los caracteres de control (0x00 a 0x1F, \u0081, etc.). Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Connect [!DNL Oracle Object Storage] a Platform

La siguiente documentación proporciona información sobre cómo conectar Oracle Object Storage a Adobe Experience Platform mediante API o la interfaz de usuario:

### Uso de API

- [Crear una conexión base de almacenamiento de objetos de Oracle mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Crear una conexión de origen de Almacenamiento de objetos de Oracle en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
