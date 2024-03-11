---
title: Conexión de Azure Data Lake Storage Gen2
description: Obtenga información sobre cómo conectarse a Azure Data Lake Storage Gen2 para activar audiencias y exportar conjuntos de datos.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 2%

---

# [!DNL Azure Data Lake Storage Gen2] conexión

## Información general {#overview}

Lea esta página para aprender a crear una conexión saliente activa con su [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) lago de datos para exportar periódicamente archivos de datos del Experience Platform.

## Conéctese a su [!DNL ADLS Gen2] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su [!DNL ADLS Gen2] Ubicación de almacenamiento mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar audiencias en este destino](#activate) más abajo.
* Para conectarse a su [!DNL ADLS Gen2] ubicación de almacenamiento mediante programación, lea el [Activación de audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se elige en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo: [exportación de conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo: [exportar conjuntos de datos mediante programación utilizando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Formato de archivo de los datos exportados {#file-format}

Al exportar *datos de audiencia*, Platform crea un `.csv`, `parquet`, o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la [formatos de archivo compatibles para la exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en el tutorial de activación de audiencia.

Al exportar *conjuntos de datos*, Platform crea un `.parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la [verificar exportación correcta del conjunto de datos](../../ui/export-datasets.md#verify) en el tutorial exportar conjuntos de datos.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL URL]**: el punto final para [!DNL Azure Data Lake Storage Gen2]. El patrón de extremo es: `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Inquilino]**: la información del inquilino que contiene la aplicación.
* **[!UICONTROL ID principal de servicio]**: ID de cliente de la aplicación.
* **[!UICONTROL Clave principal de servicio]**: la clave de la aplicación.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc. El nombre del manifiesto se asigna mediante el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver una [archivo de manifiesto de muestra](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: La [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: La hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: Ruta de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación {#scheduling}

En el **[!UICONTROL Programación]** paso, puede [configuración de la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su [!DNL Azure Data Lake Storage Gen2] y también puede hacer lo siguiente [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Asignación]** paso, puede seleccionar qué campos de atributo e identidad desea exportar para los perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario activar destinos por lotes.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Azure Data Lake Storage Gen2] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
