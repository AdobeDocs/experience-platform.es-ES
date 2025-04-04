---
keywords: Experience Platform;inicio;temas populares;Google Cloud Storage;almacenamiento en la nube de Google
solution: Experience Platform
title: Información general sobre el conector Source de Google Cloud Storage
description: Obtenga información sobre cómo conectar Google Cloud Storage a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Conector de Google Cloud Storage

>[!IMPORTANT]
>
>Ahora puede usar el origen [!DNL Google Cloud Storage] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure], lo que le permite obtener los datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Experience Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato JSON o Parquet compatible con el modelo de datos de experiencia (XDM) o un formato delimitado. Cada paso del proceso se integra en el flujo de trabajo de fuentes. Experience Platform le permite traer datos de [!DNL Google Cloud Storage] por lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Configuración de requisitos previos para conectar su cuenta de [!DNL Google Cloud Storage]

Para conectarse a Experience Platform, primero debe habilitar la interoperabilidad para su cuenta de [!DNL Google Cloud Storage]. Para obtener acceso a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** en la opción **[!UICONTROL Almacenamiento en la nube]** del panel de navegación.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

Aparecerá la página **[!UICONTROL Configuración]**. Desde aquí puede ver información sobre el identificador de proyecto [!DNL Google] y detalles sobre la cuenta [!DNL Google Cloud Storage]. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

La página **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo identificador de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Crear una clave para una cuenta de servicio]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Puede usar el identificador de clave de acceso y la clave de acceso secreta generados recientemente para conectar su cuenta de [!DNL Google Cloud Storage] a Experience Platform.

Para obtener más información, lea la guía sobre [creación y administración de claves de cuenta de servicio](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) de la documentación de [!DNL Google Cloud].

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Conectar [!DNL Google Cloud Storage] a Experience Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Google Cloud Storage] a Experience Platform mediante API o la interfaz de usuario:

### Uso de API

- [Crear una conexión base de Google Cloud Storage mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/google.md)
- [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Cree una conexión de origen de Google Cloud Storage en la interfaz de usuario de](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
