---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Fuente de la zona de aterrizaje de datos
topic-legacy: overview
description: Obtenga información sobre cómo conectar la zona de aterrizaje de datos a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] es una interfaz de  [!DNL Azure Blob] almacenamiento de información aprovisionada por Adobe Experience Platform, lo que le permite acceder a una instalación de almacenamiento de archivos segura y basada en la nube para introducir y extraer archivos de Platform a través de fuentes y destinos. Tiene acceso a un contenedor [!DNL Data Landing Zone] por simulador de pruebas y el volumen total de datos en todos los contenedores está limitado a los datos totales proporcionados con su licencia de Platform Produces and Services. Todos los clientes de Platform y sus servicios de aplicación como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] y [!DNL Real-time Customer Data Platform] están aprovisionados con un contenedor [!DNL Data Landing Zone] por simulador de pruebas. Puede leer y escribir archivos en su contenedor a través de [!DNL Azure Storage Explorer] o su interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con mecanismos de seguridad de  [!DNL Azure Blob] almacenamiento estándar en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su contenedor [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para acceder al contenedor [!DNL Data Landing Zone], lo que significa que no es necesario configurar ninguna lista de permitidos o configuración entre regiones para la red. Platform exige un tiempo de vida estricto de siete días (TTL) en todos los archivos cargados en un contenedor [!DNL Data Landing Zone]. Todos los archivos se eliminan al cabo de siete días.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar los archivos o directorios de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (como `0x00` a `0x1F`, `\u0081`, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Conectar [!DNL Data Landing Zone] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo traer datos de su contenedor [!DNL Data Landing Zone] a Adobe Experience Platform mediante API o la interfaz de usuario.

### Uso de API

- [Crear una conexión de origen [!DNL Data Landing Zone] mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Conectarse [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
