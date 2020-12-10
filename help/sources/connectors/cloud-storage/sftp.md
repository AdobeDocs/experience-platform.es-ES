---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Conector SFTP
topic: overview
description: La siguiente documentación proporciona información sobre cómo conectar un servidor SFTP a la plataforma mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Conector SFTP (Beta)

>[!NOTE]
>
>El conector SFTP está en versión beta. Consulte la descripción general [de](../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS [!DNL Google Cloud Platform], y [!DNL Azure], lo que le permite traer sus datos de estos sistemas.

Las fuentes de almacenamiento de nube pueden incorporar sus propios datos [!DNL Platform] sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] permite introducir datos desde un servidor FTP o SFTP por lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes. Consulte la página de lista de permitidos [de direcciones](../../ip-address-allow-list.md) IP para obtener más información.

## Restricciones de nombres para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento de nube.

- Los nombres de los componentes de directorio y archivo no pueden exceder los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas](https://www.ietf.org/rfc/rfc2616.txt) básicas y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Conectar SFTP a [!DNL Platform]

>[!IMPORTANT]
>
>Los usuarios deben desactivar la autenticación interactiva por teclado en la configuración del servidor SFTP antes de conectarse. Al deshabilitar la configuración, las contraseñas se pueden introducir manualmente, en lugar de hacerlo a través de un servicio o un programa. Consulte el documento [](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) Componente Pro para obtener más información sobre la autenticación interactiva por teclado.

La siguiente documentación proporciona información sobre cómo conectar un servidor SFTP a [!DNL Platform] través de API o de la interfaz de usuario:

### Uso de las API

- [Creación de un conector SFTP mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/sftp.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen SFTP en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)