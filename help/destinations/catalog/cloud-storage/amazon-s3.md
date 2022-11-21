---
keywords: Amazon S3;destino S3;s3;amazon s3
title: Conexión Amazon S3
description: Cree una conexión saliente en directo al almacenamiento de Amazon Web Service (AWS) S3 para exportar periódicamente archivos de datos CSV de Adobe Experience Platform a sus propios bloques S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: f841b27a2d2700b0b68a386b89d1a5c62d3910ff
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Registro de cambios del destino {#changelog}

>[!IMPORTANT]
>
>Con la versión beta de la funcionalidad de exportación de conjuntos de datos y la funcionalidad mejorada de exportación de archivos, es posible que ahora vea dos [!DNL Amazon S3] en el catálogo de destinos.
>* Si ya está exportando archivos al **[!UICONTROL Amazon S3]** destino: Cree nuevos flujos de datos para el nuevo **[!UICONTROL Amazon S3 beta]** destino.
>* Si aún no ha creado ningún flujo de datos en la variable **[!UICONTROL Amazon S3]** destino, utilice el nuevo **[!UICONTROL Amazon S3 beta]** tarjeta para exportar archivos a **[!UICONTROL Amazon S3]**.


![Imagen de las dos tarjetas de destino de Amazon S3 en una vista en paralelo.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Mejoras en el nuevo [!DNL Amazon S3] la tarjeta de destino incluye:

* [Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados mediante la variable [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Posibilidad de personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

Cree una conexión de salida activa con su [!DNL Amazon S3] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios bloques S3.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo de exportación basado en perfiles de Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!DNL Amazon S3]clave de acceso** y **[!DNL Amazon S3]clave secreta**: En [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso a Platform a su [!DNL Amazon S3] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la imagen siguiente.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la interfaz de usuario](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nombre del depósito"
>abstract="Debe tener entre 3 y 63 caracteres de longitud. Debe comenzar y terminar con una letra o un número. Solo debe contener letras minúsculas, números o guiones ( - ). No se debe dar formato a una dirección IP (por ejemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ruta de carpeta"
>abstract="Debe contener únicamente los caracteres A-Z, a-z, 0-9 y puede incluir los siguientes caracteres especiales: `/!-_.'()"^[]+$%.*"`. Para crear una carpeta por archivo de segmento, inserte la macro `/%SEGMENT_NAME%` o `/%SEGMENT_ID%` o `/%SEGMENT_NAME%/%SEGMENT_ID%` en el campo de texto. Las macros solo se pueden insertar al final de la ruta de la carpeta. Vea ejemplos de macros en la documentación."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Utilice macros para crear una carpeta en su ubicación de almacenamiento"

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Nombre del depósito]**: introduzca el nombre del [!DNL Amazon S3] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

>[!TIP]
>
>En el flujo de trabajo de conexión de destino, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de segmento exportado. Lectura [Utilice macros para crear una carpeta en su ubicación de almacenamiento](overview.md#use-macros) para obtener instrucciones.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Requerido [!DNL Amazon S3] permissions {#required-s3-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon S3] ubicación de almacenamiento, cree un usuario de Identity and Access Management (IAM) para [!DNL Platform] en [!DNL Amazon S3] y asigne permisos para las siguientes acciones:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar las exportaciones de conjuntos de datos, lea la [tutorial de exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Datos exportados {#exported-data}

Para [!DNL Amazon S3] destinos, [!DNL Platform] crea un archivo de datos en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.
