---
keywords: Experience Platform;inicio;temas populares;Google Cloud Storage;almacenamiento en la nube de google
solution: Experience Platform
title: Descripción general del conector de origen de almacenamiento de Google Cloud
description: Obtenga información sobre cómo conectar el almacenamiento en la nube de Google a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Conector de almacenamiento de Google Cloud

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform]y [!DNL Azure], lo que le permite obtener sus datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a Platform sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato JSON o Parquet compatible con el Modelo de datos de experiencia (XDM) o en un formato delimitado. Cada paso del proceso se integra en el flujo de trabajo de fuentes. Platform le permite introducir datos de [!DNL Google Cloud Storage] mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Configuración de requisitos previos para conectar su [!DNL Google Cloud Storage] account

Para conectarse a Platform, primero debe habilitar la interoperabilidad para su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** de la variable **[!UICONTROL Almacenamiento en la nube]** en el panel de navegación.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

La variable **[!UICONTROL Configuración]** se abre. Desde aquí puede ver información sobre su [!DNL Google] ID del proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

La variable **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Crear una clave para una cuenta de servicio]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Puede utilizar el ID de clave de acceso y la clave de acceso secreta que acaba de generar para conectar su [!DNL Google Cloud Storage] a Platform.

Para obtener más información, consulte la guía de [creación y administración de claves de cuenta de servicio](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) de la variable [!DNL Google Cloud] documentación.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones a las que debe tener en cuenta al asignar un nombre al archivo o directorio de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Puntos de código como `\uE000`, aunque válido en nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Connect [!DNL Google Cloud Storage] a Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Google Cloud Storage] a Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de base de almacenamiento en la nube de Google mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/google.md)
- [Explorar la estructura de datos y el contenido de un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen de Google Cloud Storage en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
