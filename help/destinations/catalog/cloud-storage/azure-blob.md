---
keywords: Azure Blob;destino de blob;s3;destino de blob de Azure
title: Conexión de Azure Blob
description: Cree una conexión saliente activa al almacenamiento del blob de Azure para exportar periódicamente archivos de datos CSV de Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# [!DNL Azure Blob] conexión

## Registro de cambios de destino {#changelog}

>[!IMPORTANT]
>
>Con la versión beta de la funcionalidad exportar conjuntos de datos y la funcionalidad mejorada de exportación de archivos, es posible que ahora vea dos [!DNL Azure Blob] tarjetas en el catálogo de destinos.
>* Si ya está exportando archivos a **[!UICONTROL Azure Blob]** destino: cree nuevos flujos de datos para el nuevo **[!UICONTROL Azure Blob beta]** destino.
>* Si todavía no ha creado ningún flujo de datos en **[!UICONTROL Azure Blob]** destino, utilice el nuevo **[!UICONTROL Azure Blob beta]** para exportar archivos a **[!UICONTROL Azure Blob]**.


![Imagen de las dos tarjetas de destino de Azure Blob en una vista en paralelo.](../../assets/catalog/cloud-storage/blob/two-azure-blob-destination-cards.png)

Mejoras en el nuevo [!DNL Azure Blob] la tarjeta de destino incluye:

* [Compatibilidad con exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través de [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

[!DNL Azure Blob] (en lo sucesivo denominados [!DNL Blob]) es la solución de almacenamiento de objetos de Microsoft para la nube. Este tutorial proporciona los pasos para crear una [!DNL Blob] destino con el [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Blob] destino, puede omitir el resto de este documento y continuar con el tutorial sobre [activación de segmentos en su destino](../../ui/activate-batch-profile-destinations.md).

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
>abstract="Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Cadena de conexión]**: la cadena de conexión es necesaria para acceder a los datos del almacenamiento del blob. El [!DNL Blob] el patrón de cadena de conexión comienza con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Para obtener más información sobre la configuración de [!DNL Blob] cadena de conexión, consulte [Configurar una cadena de conexión para una cuenta de almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) en la documentación de Microsoft.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Contenedor]**: introduzca el nombre del [!DNL Azure Blob Storage] contenedor que utilizará este destino.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Esta opción solo está disponible para **[!UICONTROL Azure Blob beta]** destino. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados. Esta opción solo está disponible para **[!UICONTROL Azure Blob beta]** destino.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea la [tutorial de exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Datos exportados {#exported-data}

Para [!DNL Azure Blob Storage] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.