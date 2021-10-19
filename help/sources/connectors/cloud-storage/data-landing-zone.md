---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Fuente de la zona de aterrizaje de datos
topic-legacy: overview
description: Obtenga información sobre cómo conectar la zona de aterrizaje de datos a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento de información aprovisionada por Adobe Experience Platform, lo que le permite acceder a un servicio de almacenamiento de archivos seguro y basado en la nube para introducir archivos en Platform. Tiene acceso a uno [!DNL Data Landing Zone] contenedores por entorno limitado, y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con la licencia de productos y servicios de Platform. Todos los clientes de Platform y sus servicios de aplicación, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]y [!DNL Real-time Customer Data Platform] se aprovisionan con uno [!DNL Data Landing Zone] contenedor por simulador de pruebas. Puede leer y escribir archivos en el contenedor a través de [!DNL Azure Storage Explorer] o su interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con [!DNL Azure Blob] mecanismos de seguridad del almacenamiento en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para acceder a su [!DNL Data Landing Zone] contenedor, lo que significa que no necesita configurar ninguna lista de permitidos o configuración entre regiones para su red. Platform exige un tiempo de vida estricto de siete días (TTL) en todos los archivos cargados en un [!DNL Data Landing Zone] contenedor. Todos los archivos se eliminan al cabo de siete días.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar los archivos o directorios de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Puntos de código como `\uE000`, aunque válido en nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (como `0x00` a `0x1F`, `\u0081`, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Connect [!DNL Data Landing Zone] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo obtener datos de su [!DNL Data Landing Zone] contenedor para Adobe Experience Platform mediante API o la interfaz de usuario.

### Uso de API

- [Cree un [!DNL Data Landing Zone] conexión de origen mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Connect [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
