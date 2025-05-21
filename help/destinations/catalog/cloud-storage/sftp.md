---
title: Conexión SFTP
description: Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 45f22addbff9ec81d64e9e756e4c27e8af4b477d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Conexión SFTP

## Registro de cambios de destino {#changelog}

Con la versión de Experience Platform de julio de 2023, el destino SFTP proporciona nuevas funciones, como se indica a continuación:

* [Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* [Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque Experience Platform admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Conectarse al SFTP mediante la API o la IU {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento SFTP mediante la interfaz de usuario de Experience Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse a su ubicación de almacenamiento SFTP mediante programación, lea [Activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

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
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo de exportación basado en perfiles SFTP resaltado en el catálogo de destinos.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo [exportar conjuntos de datos mediante la interfaz de usuario de Experience Platform](/help/destinations/ui/export-datasets.md).
* Cómo [exportar conjuntos de datos mediante programación usando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Formato de archivo de los datos exportados {#file-format}

Al exportar *datos de audiencia*, Experience Platform crea un archivo de `.csv`, `parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [formatos de archivo compatibles con la exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en el tutorial de activación de audiencia.

Al exportar *conjuntos de datos*, Experience Platform crea un archivo de `.parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [verificar la exportación correcta del conjunto de datos](../../ui/export-datasets.md#verify) en el tutorial exportar conjuntos de datos.

## Requisitos de conexión del servidor SFTP {#sftp-connection-requirements}

Para garantizar el éxito de las exportaciones de datos, debe configurar el servidor SFTP de destino para permitir un número suficiente de conexiones simultáneas. Si el servidor SFTP limita el número de conexiones simultáneas, pueden producirse errores en los trabajos de exportación, especialmente al exportar varias audiencias o conjuntos de datos al mismo tiempo.

**Recomendación**
Para obtener un rendimiento óptimo, el servidor SFTP debe permitir al menos una conexión simultánea para cada audiencia o conjunto de datos que se exporte. Como mínimo, el servidor debe admitir al menos el 30 % del número total de audiencias o conjuntos de datos programados para la exportación al mismo tiempo.

**Ejemplo**\
Si programa exportaciones para 100 audiencias o conjuntos de datos simultáneamente, su servidor SFTP debe permitir al menos 30 conexiones simultáneas.

La configuración correcta de los límites de conexión del servidor SFTP ayuda a evitar errores en las exportaciones y garantiza una entrega de datos fiable desde Adobe Experience Platform.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[[!UICONTROL permisos de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Información de autenticación {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clave SSH privada"
>abstract="La clave SSH privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña."

Si selecciona el tipo de autenticación **[!UICONTROL SFTP con contraseña]** para conectarse a su ubicación SFTP:

![Autenticación básica de destino SFTP con contraseña.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Dominio]**: la dirección de su ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Puerto]**: el puerto que usa su ubicación de almacenamiento SFTP;
* **[!UICONTROL Contraseña]**: Contraseña para iniciar sesión en la ubicación de almacenamiento SFTP.
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Si selecciona el tipo de autenticación **[!UICONTROL SFTP con clave SSH]** para conectarse a su ubicación SFTP:

![Autenticación de clave SSH de destino SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: indica la dirección IP o el nombre de dominio de tu cuenta SFTP
* **[!UICONTROL Puerto]**: el puerto que usa su ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Clave SSH]**: La clave SSH privada utilizada para iniciar sesión en la ubicación de almacenamiento SFTP. La clave privada debe ser una cadena codificada en Base64 con formato RSA y no debe estar protegida con contraseña.
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Detalles del destino {#destination-details}

Después de establecer la conexión de autenticación con la ubicación SFTP, proporcione la siguiente información para el destino:

![Campos de detalles de destino para el destino SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nombre]**: escriba un nombre que le ayude a identificar este destino en la interfaz de usuario de Experience Platform;
* **[!UICONTROL Descripción]**: escriba una descripción para este destino;
* **[!UICONTROL Ruta de la carpeta]**: escriba la ruta de acceso a la carpeta de la ubicación SFTP donde se exportarán los archivos.
* **[!UICONTROL Tipo de archivo]**: seleccione el formato que Experience Platform debe usar para los archivos exportados. Al seleccionar la opción [!UICONTROL CSV], también puede [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que Experience Platform debe usar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de la exportación, etc. Se ha asignado un nombre al manifiesto con el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver [archivo de manifiesto de ejemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: la [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: la hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: ruta de acceso de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el almacenamiento SFTP y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

Consulte el artículo [lista de permitidos de direcciones IP](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.
