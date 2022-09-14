---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Descripción general del conector de origen de Azure Data Lake Storage Gen2
topic-legacy: overview
description: Obtenga información sobre cómo conectar Azure Data Lake Storage Gen2 a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 72c3000022db68284836cc7f2248154493100913
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Conector de Azure Data Lake Storage Gen2

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform]y [!DNL Azure], lo que le permite obtener sus datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden incorporar sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos de [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>La variable [!DNL Azure Data Lake Storage Gen2] el origen no admite conectividad de la misma región con el Experience Platform. Si la instancia de Azure está usando la misma región de red que el Experience Platform, no se puede establecer una conexión con orígenes de Experience Platform. No use las regiones de Azure East US 2, Azure West Europe y Azure Australia East al configurar su [!DNL Azure Data Lake Storage Gen2] fuente. Actualmente, solo se admite la conectividad entre regiones.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones a las que debe tener en cuenta al asignar un nombre al archivo o directorio de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Puntos de código como `\uE000`, aunque válido en nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Connect [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

La siguiente documentación proporciona información sobre cómo conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión base de ADLS-Gen2 mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explorar la estructura de datos y el contenido de un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen ADLS-Gen2 en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
