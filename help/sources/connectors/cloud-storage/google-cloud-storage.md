---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Almacenamiento de Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Conector de Almacenamiento de Google Cloud

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS [!DNL Google Cloud Platform], y [!DNL Azure], lo que le permite traer sus datos de estos sistemas.

Las fuentes de almacenamiento de nube pueden incorporar sus propios datos [!DNL Platform] sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] le permite traer datos desde [!DNL Google Cloud Storage] lotes.

## Configuración de requisitos previos para conectar su [!DNL Google Cloud Storage] cuenta

Para conectarse a [!DNL Platform], primero debe habilitar la interoperabilidad para su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** en la opción **[!UICONTROL Almacenamiento]** del panel de navegación.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Aparece la página **[!UICONTROL Configuración]** . Desde aquí puede ver información sobre su ID [!DNL Google] de proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La página **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de usuario. Si todavía no ha establecido un proyecto predeterminado para el acceso interoperable, puede configurarlo desde la sección Proyecto *[!UICONTROL predeterminado para el acceso]* interoperable. Si ya se ha establecido un proyecto predeterminado, la sección mostrará una confirmación de que se ha establecido un proyecto como predeterminado.

Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de usuario, seleccione **[!UICONTROL Crear una clave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreto recién generados para conectar su [!DNL Google Cloud Storage] cuenta a [!DNL Platform].

La documentación siguiente proporciona información sobre cómo conectarse [!DNL Google Cloud Storage] a [!DNL Platform] través de API o de la interfaz de usuario:

## Conectar [!DNL Google Cloud Storage] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectarse [!DNL Google Cloud Storage] a [!DNL Platform] través de API o de la interfaz de usuario:

### Uso de API

- [Creación de un conector de Almacenamiento de Google Cloud mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/google.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen de Almacenamiento de Google Cloud en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)