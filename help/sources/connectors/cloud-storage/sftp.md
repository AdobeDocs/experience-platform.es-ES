---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp
solution: Experience Platform
title: Información general del conector de origen SFTP
topic: sobre validación
description: Obtenga información sobre cómo conectar un servidor SFTP a Adobe Experience Platform mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Conector SFTP

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure], lo que le permite obtener sus datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos de un servidor FTP o SFTP por lotes.

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

## Conectar SFTP a [!DNL Platform]

>[!IMPORTANT]
>
>Los usuarios deben deshabilitar la autenticación interactiva por teclado en la configuración del servidor SFTP antes de conectarse. Al desactivar la configuración, las contraseñas se pueden introducir manualmente, en lugar de hacerlo a través de un servicio o programa. Consulte el [documento Component Pro](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) para obtener más información sobre la autenticación interactiva por teclado.

La documentación siguiente proporciona información sobre cómo conectar un servidor SFTP a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de las API

- [Creación de una conexión de origen SFTP mediante la API del servicio de flujo](../../tutorials/api/create/cloud-storage/sftp.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen SFTP en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Configurar un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)