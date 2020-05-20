---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Almacenamiento de Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 256a193e56e69078d1c01c622656f0b1a18e73ff
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Conector de Almacenamiento de Google Cloud

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, Google Cloud Platform y Azure. Puede llevar los datos de estos sistemas a la plataforma.

Las fuentes de almacenamiento de nube pueden llevar sus propios datos a la plataforma sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. Platform le permite traer datos desde Google Cloud Almacenamiento por lotes.

## Configuración de requisitos previos para la conexión de la cuenta de Almacenamiento de Google Cloud

Para conectarse a Platform, primero debe habilitar la interoperabilidad para su cuenta de Almacenamiento de Google Cloud. Para acceder a la configuración de interoperabilidad, abra la plataforma de Google Cloud y seleccione **[!UICONTROL Configuración]** en la opción de **[!UICONTROL Almacenamiento]** del panel de navegación.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Aparece la página **[!UICONTROL Configuración]** . Desde aquí puede ver información sobre su ID de proyecto de Google y detalles sobre su cuenta de Almacenamiento de Google Cloud. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La página **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de usuario. Si todavía no ha establecido un proyecto predeterminado para el acceso interoperable, puede configurarlo desde la sección Proyecto *[!UICONTROL predeterminado para el acceso]* interoperable. Si ya se ha establecido un proyecto predeterminado, la sección mostrará una confirmación de que se ha establecido un proyecto como predeterminado.

Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de usuario, seleccione **[!UICONTROL Crear una clave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreto recién generados para conectar su cuenta de Almacenamiento de Google Cloud a Platform.

La siguiente documentación proporciona información sobre cómo conectar el Almacenamiento de Google Cloud a la plataforma mediante API o la interfaz de usuario:

## Conectar el Almacenamiento a la plataforma de Google Cloud

La siguiente documentación proporciona información sobre cómo conectar el Almacenamiento de Google Cloud a la plataforma mediante API o la interfaz de usuario:

### Uso de API

- [Creación de un conector de Almacenamiento de Google Cloud mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/google.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen de Almacenamiento de Google Cloud en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)