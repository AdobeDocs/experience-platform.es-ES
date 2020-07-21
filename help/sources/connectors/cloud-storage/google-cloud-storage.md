---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Almacenamiento de Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Conector de Almacenamiento de Google Cloud

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS [!DNL Google Cloud Platform], y [!DNL Azure], lo que le permite traer sus datos de estos sistemas.

Las fuentes de almacenamiento de nube pueden incorporar sus propios datos [!DNL Platform] sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] le permite traer datos desde [!DNL Google Cloud Storage] lotes.

## lista de permitidos de direcciones IP

Las siguientes direcciones IP deben agregarse a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes.

### Región del este de EE.UU.

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Región de Europa Occidental

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australia Oriental

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Configuración de requisitos previos para conectar su [!DNL Google Cloud Storage] cuenta

Para conectarse a [!DNL Platform], primero debe habilitar la interoperabilidad para su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** en la opción **[!UICONTROL Almacenamiento]** del panel de navegación.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Aparece la página **[!UICONTROL Configuración]** . Desde aquí puede ver información sobre su ID [!DNL Google] de proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La página **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de usuario. Si todavía no ha establecido un proyecto predeterminado para el acceso interoperable, puede configurarlo desde la sección Proyecto *[!UICONTROL predeterminado para el acceso]* interoperable. Si ya se ha establecido un proyecto predeterminado, la sección mostrará una confirmación de que se ha establecido un proyecto como predeterminado.

Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de usuario, seleccione **[!UICONTROL Crear una clave]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreto recién generados para conectar su [!DNL Google Cloud Storage] cuenta a [!DNL Platform].

## Conectar [!DNL Google Cloud Storage] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectarse [!DNL Google Cloud Storage] a [!DNL Platform] través de API o de la interfaz de usuario:

### Uso de API

- [Creación de un conector de Almacenamiento de Google Cloud mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/google.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen de Almacenamiento de Google Cloud en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)