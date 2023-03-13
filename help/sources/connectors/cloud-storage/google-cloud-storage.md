---
keywords: Experience Platform;inicio;temas populares;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Información general sobre el conector de origen de Google Cloud Storage
description: Obtenga información sobre cómo conectar Google Cloud Storage a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Conector de Google Cloud Storage

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform], y [!DNL Azure], lo que le permite obtener los datos de estos sistemas.

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato JSON o Parquet compatible con el modelo de datos de experiencia (XDM) o un formato delimitado. Cada paso del proceso se integra en el flujo de trabajo de fuentes. Platform le permite introducir datos de [!DNL Google Cloud Storage] mediante lotes.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Configuración previa necesaria para conectar su [!DNL Google Cloud Storage] account

Para conectarse a Platform, primero debe habilitar la interoperabilidad para sus [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** desde el **[!UICONTROL Almacenamiento en la nube]** en el panel de navegación.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

El **[!UICONTROL Configuración]** página. A partir de aquí, puede ver información sobre su [!DNL Google] ID de proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperación]** desde el encabezado superior.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

El **[!UICONTROL Interoperación]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Creación de una clave para una cuenta de servicio]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Puede utilizar el ID de clave de acceso y la clave de acceso secreta generados recientemente para conectar su [!DNL Google Cloud Storage] a Platform.

Para obtener más información, lea la guía de [crear y administrar claves de cuenta de servicio](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) desde el [!DNL Google Cloud] documentación.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Connect [!DNL Google Cloud Storage] a Platform

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Google Cloud Storage] Vaya a Platform mediante las API o la interfaz de usuario de:

### Uso de API

- [Crear una conexión base de Google Cloud Storage mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/google.md)
- [Explore la estructura de datos y el contenido de una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Cree una conexión de origen de Google Cloud Storage en la interfaz de usuario de](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)
