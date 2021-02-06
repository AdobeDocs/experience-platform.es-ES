---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de Google Cloud;almacenamiento de Google Cloud
solution: Experience Platform
title: Información general sobre el conector de origen de Almacenamiento de Google Cloud
topic: overview
description: Obtenga información sobre cómo conectar Google Cloud Almacenamiento a Adobe Experience Platform mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Conector de Almacenamiento de Google Cloud

Adobe Experience Platform proporciona conectividad nativa para proveedores de cloud como AWS, [!DNL Google Cloud Platform] y [!DNL Azure], lo que le permite traer sus datos de estos sistemas.

Las fuentes de almacenamiento de nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, Parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] permite traer datos de  [!DNL Google Cloud Storage] lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Configuración de requisitos previos para conectar su cuenta [!DNL Google Cloud Storage]

Para conectarse a [!DNL Platform], primero debe habilitar la interoperabilidad para su cuenta [!DNL Google Cloud Storage]. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** en la opción **[!UICONTROL Almacenamiento]** del panel de navegación.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Aparece la página **[!UICONTROL Configuración]**. Desde aquí puede ver información relacionada con su [!DNL Google] ID de proyecto y detalles sobre su cuenta [!DNL Google Cloud Storage]. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La página **[!UICONTROL Interoperabilidad]** contiene información sobre autenticación, claves de acceso y el proyecto predeterminado asociado con su cuenta de usuario. Si aún no ha establecido un proyecto predeterminado para el acceso interoperable, puede configurarlo desde la sección **[!UICONTROL Proyecto predeterminado para el acceso interoperable]**. Si ya se ha establecido un proyecto predeterminado, la sección mostrará una confirmación de que se ha establecido un proyecto como predeterminado.

Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de usuario, seleccione **[!UICONTROL Crear una clave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreto recién generados para conectar su cuenta [!DNL Google Cloud Storage] a [!DNL Platform].

## Restricciones de nombres para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento de nube.

- Los nombres de los componentes de directorio y archivo no pueden exceder los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, aunque válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Conectar [!DNL Google Cloud Storage] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Google Cloud Storage] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de Almacenamiento de Google Cloud mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/google.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen de Almacenamiento de Google Cloud en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuración de un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)