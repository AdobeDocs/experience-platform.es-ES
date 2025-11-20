---
title: Conexión de Azure Blob
description: Crear una conexión saliente activa a la almacenamiento de Azure Blob para exportar periódicamente archivos de datos de CSV desde Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 7%

---

# [!DNL Azure Blob] conexión

## Registro de cambios de destino {#changelog}

Con la versión de Experience Platform de julio de 2023, el destino [!DNL Azure Blob] proporciona nuevas funciones, como se indica a continuación:

* [Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* [Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

[!DNL Azure Blob] (en adelante, [!DNL Blob]) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona los pasos para crear un destino [!DNL Blob] mediante la interfaz de usuario [!DNL Experience Platform].

## Conectar con su almacenamiento de [!UICONTROL Azure Blob] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento [!UICONTROL Azure Blob] mediante la interfaz de usuario de Experience Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse mediante programación a la ubicación de almacenamiento [!UICONTROL Azure Blob], lea [Activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Introducción

Esto tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco de trabajo estandarizado por el cual Experience Platform organiza experiencia del cliente datos.
   * [Aspectos básicos de la composición de esquemas](../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un destino [!DNL Blob] válido, puede omitir el resto de este documento y continuar con el tutorial sobre [activación de audiencias en su destino](../../ui/activate-batch-profile-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Profile-based]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportar Frecuencia | **[!UICONTROL Batch]** | Lote destinos exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo [exportar conjuntos de datos mediante la interfaz de usuario de Experience Platform](/help/destinations/ui/export-datasets.md).
* Cómo [exportar conjuntos de datos mediante programación usando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Archivo formato de los datos exportados {#file-format}

Al exportar *audiencia datos*, Experience Platform crea un `.csv`, `parquet`, o `.json` archivo en la ubicación almacenamiento proporcionada. Para obtener más información acerca de los archivos, consulte la sección Formatos de archivo admitidos para la [exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en la tutorial activación audiencia.

Al exportar *conjuntos* de datos, Experience Platform crea un `.parquet` archivo OR `.json` en la ubicación almacenamiento proporcionada. Para obtener más información acerca de los archivos, consulte la [sección Verificar la exportación](../../ui/export-datasets.md#verify) conjunto de datos correcta del tutorial Exportar conjuntos de datos.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Connection string]**: la cadena de conexión es necesaria para acceder a los datos del almacenamiento del blob. El [!DNL Blob] patrón de la cadena de conexión empieza por: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obtener más información acerca de cómo configurar la cadena de conexión de [!DNL Blob], consulte [Configurar una cadena de conexión para una cuenta de almacenamiento de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.
* **[!UICONTROL Encryption key]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y obligatorios que aparecen a continuación. Un asterisco junto al campo de la IU indica que el campo es obligatorio.

* **[!UICONTROL Name]**: Introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Description]**: escriba una descripción para este destino.
* **[!UICONTROL Folder path]**: escriba la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Container]**: escriba el nombre del contenedor [!DNL Azure Blob Storage] que utilizará este destino.
* **[!UICONTROL File type]**: seleccione el formato que Experience Platform debe usar para los archivos exportados. Al seleccionar la opción [!UICONTROL CSV], también puede [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: seleccione el tipo de compresión que Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Include manifest file]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc. Se ha asignado un nombre al manifiesto con el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver [archivo de manifiesto de ejemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: la [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: la hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: ruta de acceso de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: Nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL View Destinations]** permisos **[!UICONTROL Activate Destinations]** , **[!UICONTROL View Profiles]**, **[!UICONTROL View Segments]**, y [ ](/help/access-control/home.md#permissions)control de acceso. Lea la control de acceso descripción general[ o póngase en contacto con el ](/help/access-control/ui/overview.md)administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [control de acceso permiso](/help/access-control/home.md#permissions). <br> ![Seleccione el espacio de nombres de identidad resaltado en la flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el espacio de nombres de identidad resaltado en la flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el almacenamiento de [!DNL Azure Blob] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.