---
title: Conexión de Google Cloud Storage
description: Obtenga información sobre cómo conectarse a Google Cloud Storage y activar audiencias o exportar conjuntos de datos.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 679c1723965271b6a9c1b5b873cf8ac8de67458d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] conexión

## Información general {#overview}

Cree una conexión saliente activa con [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios contenedores.

## Conectar con su almacenamiento de [!DNL Google Cloud Storage] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento [!DNL Google Cloud Storage] mediante la interfaz de usuario de Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse mediante programación a la ubicación de almacenamiento [!DNL Google Cloud Storage], lea [Activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables, tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo [exportar conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo [exportar conjuntos de datos mediante programación usando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Formato de archivo de los datos exportados {#file-format}

Al exportar *datos de audiencia*, Platform crea un archivo de `.csv`, `parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [formatos de archivo compatibles con la exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en el tutorial de activación de audiencia.

Al exportar *conjuntos de datos*, Platform crea un archivo de `.parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [verificar la exportación correcta del conjunto de datos](../../ui/export-datasets.md#verify) en el tutorial exportar conjuntos de datos.

## Configuración de requisitos previos para conectar su cuenta de [!DNL Google Cloud Storage] {#prerequisites}

Para conectar Platform a [!DNL Google Cloud Storage], primero debe habilitar la interoperabilidad para su cuenta de [!DNL Google Cloud Storage]. Para obtener acceso a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** en la opción **[!UICONTROL Almacenamiento en la nube]** del panel de navegación.

![Panel de Google Cloud Platform con Almacenamiento en la nube y Configuración resaltados.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

Aparecerá la página **[!UICONTROL Configuración]**. Desde aquí puede ver información sobre el identificador de proyecto [!DNL Google] y detalles sobre la cuenta [!DNL Google Cloud Storage]. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![La ficha Interoperabilidad resaltada en el panel de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

La página **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo identificador de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Crear una clave para una cuenta de servicio]**.

![Cree una clave para un control de cuenta de servicio resaltado en el panel de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puede usar el identificador de la clave de acceso recién generada y la clave de acceso secreta para conectar su cuenta de [!DNL Google Cloud Storage] a Platform.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Id. de clave de acceso]**: cadena alfanumérica de 61 caracteres usada para autenticar su cuenta de [!DNL Google Cloud Storage] en Platform. Para obtener información sobre cómo obtener este valor, lea la sección [requisitos previos](#prerequisites) más arriba.
* **[!UICONTROL Clave de acceso secreta]**: cadena de 40 caracteres codificada en Base64 que se usa para autenticar la cuenta de [!DNL Google Cloud Storage] en Platform. Para obtener información sobre cómo obtener este valor, lea la sección [requisitos previos](#prerequisites) más arriba.
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obtener más información sobre estos valores, lea la guía [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para ver los pasos sobre cómo generar tu propio identificador de clave de acceso y clave de acceso secreta, consulta la [[!DNL Google Cloud Storage] descripción general de origen](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL Nombre del contenedor]**: Escriba el nombre del contenedor [!DNL Google Cloud Storage] que usará este destino.
* **[!UICONTROL Ruta de carpeta]**: escriba la ruta de acceso a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el formato que el Experience Platform debe usar para los archivos exportados. Al seleccionar la opción [!UICONTROL CSV], también puede [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe usar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de la exportación, etc. Se ha asignado un nombre al manifiesto con el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver [archivo de manifiesto de ejemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: la [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: la hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: ruta de acceso de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Permisos necesarios de [!DNL Google Cloud Storage] {#required-google-cloud-storage-permission}

Para conectar y exportar datos correctamente a la ubicación de almacenamiento [!DNL Google Cloud Storage], necesita los siguientes permisos de [!DNL Google Cloud Storage] para los contenedores:

*`orgpolicy.policy.get`
*`resourcemanager.projects.get`
*`resourcemanager.projects.list`
*`storage.managedFolders.create`
*`storage.multipartUploads.abort`
*`storage.multipartUploads.create`
*`storage.multipartUploads.listParts`
*`storage.objects.create`
*`storage.objects.list`

Más información sobre [control de acceso y permisos](https://cloud.google.com/storage/docs/access-control/iam-permissions) en [!DNL Google Cloud Storage].

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación

En el paso **[!UICONTROL Programación]**, puede [configurar la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su destino [!DNL Google Cloud Storage] y también [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el paso **[!UICONTROL Asignación]**, puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, vea el [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario para activar destinos por lotes.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el bloque [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

Consulte el artículo [lista de permitidos de direcciones IP](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.