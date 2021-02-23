---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos Oracle;almacenamiento de objetos oracle
solution: Experience Platform
title: Introducción al conector de origen de Almacenamiento de objetos Oracle
topic: sobre validación
description: Obtenga información sobre cómo conectar el Almacenamiento de objetos Oracle a Adobe Experience Platform mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Conector del Almacenamiento de objetos Oracle

Adobe Experience Platform proporciona conectividad nativa para proveedores de cloud como AWS, [!DNL Google Cloud Platform], lo que le permite llevar datos de estos sistemas a la plataforma para su uso en servicios y destinos de flujo continuo.

Las fuentes de almacenamiento de nube pueden llevar sus datos a la plataforma sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, Parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de las fuentes. Platform le permite traer datos de [!DNL Oracle Object Storage] por lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes. Consulte el documento [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nombres para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al asignar un nombre al archivo o directorio de almacenamiento de nube:

- Los nombres de los componentes de directorio y archivo no pueden exceder los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode tampoco están permitidos, como los caracteres de control (0x00 a 0x1F, \u0081, etc.). Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Conectar [!DNL Oracle Object Storage] a la plataforma

La siguiente documentación proporciona información sobre cómo conectar el Almacenamiento de objetos Oracle a Adobe Experience Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de Almacenamiento de objetos Oracle mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen de Almacenamiento de objetos Oracle en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Configuración de un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)