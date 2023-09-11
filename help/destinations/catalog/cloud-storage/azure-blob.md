---
title: Conexión de Azure Blob
description: Cree una conexión saliente activa al almacenamiento del blob de Azure para exportar periódicamente archivos de datos CSV de Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 950370683f648771d91689e84c3d782824fb01f4
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 7%

---

# [!DNL Azure Blob] conexión

## Registro de cambios de destino {#changelog}

Con la versión de julio de 2023 de Experience Platform, la variable [!DNL Azure Blob] El destino proporciona nuevas funciones, como se indica a continuación:

* [!BADGE Beta]{type=Informative}[Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* [Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

[!DNL Azure Blob] (en lo sucesivo denominados [!DNL Blob]) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona los pasos para crear una [!DNL Blob] destino con el [!DNL Platform] interfaz de usuario.

## Conéctese a su [!UICONTROL Azure Blob] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su [!UICONTROL Azure Blob] Ubicación de almacenamiento mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar audiencias en este destino](#activate) más abajo.
* Para conectarse a su [!UICONTROL Azure Blob] ubicación de almacenamiento mediante programación, lea el [Activación de audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Blob] destino, puede omitir el resto de este documento y continuar con el tutorial sobre [activación de audiencias en el destino](../../ui/activate-batch-profile-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Formatos de archivo compatibles {#file-formats}

[!DNL Experience Platform] admite el siguiente formato de archivo para exportar a [!DNL Azure Blob]:

* Valores separados por comas (CSV): La compatibilidad con archivos de datos exportados se limita actualmente a valores separados por comas.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticar en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Cadena de conexión]**: la cadena de conexión es necesaria para acceder a los datos del almacenamiento del blob. El [!DNL Blob] el patrón de cadena de conexión comienza con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obtener más información sobre la configuración de [!DNL Blob] cadena de conexión, consulte [Configurar una cadena de conexión para una cuenta de almacenamiento de Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Contenedor]**: introduzca el nombre del [!DNL Azure Blob Storage] contenedor que utilizará este destino.
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

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo: [exportación de conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo: [exportar conjuntos de datos mediante programación utilizando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Datos exportados {#exported-data}

Para [!DNL Azure Blob Storage] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de audiencia.