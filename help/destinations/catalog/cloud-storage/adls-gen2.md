---
title: Conexión de Azure Data Lake Storage Gen2
description: Obtenga información sobre cómo conectarse a Azure Data Lake Storage Gen2 para activar audiencias y exportar conjuntos de datos.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 3%

---

# [!DNL Azure Data Lake Storage Gen2] conexión

## Información general {#overview}

Lea esta página para aprender a crear una conexión saliente activa al repositorio de datos [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) y exportar periódicamente archivos de datos de Experience Platform.

## Conectar con su almacenamiento de [!DNL ADLS Gen2] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento [!DNL ADLS Gen2] mediante la interfaz de usuario de Experience Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse mediante programación a la ubicación de almacenamiento [!DNL ADLS Gen2], lea [Activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo [exportar conjuntos de datos mediante la interfaz de usuario de Experience Platform](/help/destinations/ui/export-datasets.md).
* Cómo [exportar conjuntos de datos mediante programación usando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Formato de archivo de los datos exportados {#file-format}

Al exportar *datos de audiencia*, Experience Platform crea un archivo de `.csv`, `parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [formatos de archivo compatibles con la exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en el tutorial de activación de audiencia.

Al exportar *conjuntos de datos*, Experience Platform crea un archivo de `.parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [verificar la exportación correcta del conjunto de datos](../../ui/export-datasets.md#verify) en el tutorial exportar conjuntos de datos.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL URL]**: El extremo de [!DNL Azure Data Lake Storage Gen2]. El patrón de extremo es: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Inquilino]**: La información de inquilino que contiene su aplicación.
* **[!UICONTROL ID principal de servicio]**: ID de cliente de la aplicación.
* **[!UICONTROL Clave principal de servicio]**: La clave de la aplicación.
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Ruta de carpeta]**: escriba la ruta de acceso a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el formato que Experience Platform debe usar para los archivos exportados. Al seleccionar la opción [!UICONTROL CSV], también puede [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que Experience Platform debe usar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de la exportación, etc. Se ha asignado un nombre al manifiesto con el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver [archivo de manifiesto de ejemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: la [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: la hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: ruta de acceso de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación {#scheduling}

En el paso **[!UICONTROL Programación]**, puede [configurar la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su destino [!DNL Azure Data Lake Storage Gen2] y también [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el paso **[!UICONTROL Asignación]**, puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, vea el [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario para activar destinos por lotes.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el almacenamiento de [!DNL Azure Data Lake Storage Gen2] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
