---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Almacenamiento Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Conector Gen2 de Azure Data Lake Almacenamiento
topic: overview
description: La siguiente documentación proporciona información sobre cómo conectar Azure Data Lake Almacenamiento Gen2 a la plataforma mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Conector Gen2 de Azure Data Lake Almacenamiento

Adobe Experience Platform proporciona conectividad nativa para proveedores de cloud como AWS, [!DNL Google Cloud Platform] y [!DNL Azure], lo que le permite traer sus datos de estos sistemas.

Las fuentes de almacenamiento de nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, Parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] le permite introducir datos desde  [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) a través de lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nombres para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento de nube.

- Los nombres de los componentes de directorio y archivo no pueden exceder los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de un conector ADLS-Gen2 mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

## Uso de la interfaz de usuario

- [Creación de un conector de origen ADLS-Gen2 en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)