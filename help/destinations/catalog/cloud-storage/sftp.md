---
title: Conexión SFTP
description: Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 93b1c26e85ddd0fa232b26712f88faa824f19f30
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 10%

---

# Conexión SFTP

## Registro de cambios de destino {#changelog}

Con la versión del Experience Platform de julio de 2023, el destino SFTP proporciona nuevas funciones, como se indica a continuación:

* [Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* [Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque Experience Platform admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Conectarse al SFTP mediante la API o la IU {#connect-api-or-ui}

* Para conectarse a la ubicación de almacenamiento SFTP mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar audiencias en este destino](#activate) más abajo.
* Para conectarse mediante programación a la ubicación de almacenamiento SFTP, lea la [Activación de audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

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

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Información de autenticación {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clave SSH privada"
>abstract="La clave SSH privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña."

Si selecciona la opción **[!UICONTROL SFTP con contraseña]** tipo de autenticación para conectarse a su ubicación SFTP:

![Autenticación básica de destino SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Dominio]**: la dirección de la ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Puerto]**: el puerto utilizado por la ubicación de almacenamiento SFTP;
* **[!UICONTROL Contraseña]**: contraseña para iniciar sesión en la ubicación de almacenamiento SFTP.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Si selecciona la opción **[!UICONTROL SFTP con clave SSH]** tipo de autenticación para conectarse a su ubicación SFTP:

![Autenticación de clave SSH de destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: complete la dirección IP o el nombre de dominio de su cuenta SFTP
* **[!UICONTROL Puerto]**: el puerto utilizado por la ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Clave SSH]**: clave SSH privada que se utiliza para iniciar sesión en la ubicación de almacenamiento SFTP. La clave privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Detalles del destino {#destination-details}

Después de establecer la conexión de autenticación con la ubicación SFTP, proporcione la siguiente información para el destino:

![Detalles de destino disponibles para el destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino en la interfaz de usuario del Experience Platform;
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino;
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta en la ubicación SFTP donde se exportarán los archivos.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc. El nombre del manifiesto se asigna mediante el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver una [archivo de manifiesto de muestra](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: La [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: La hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: Ruta de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

## Activar audiencias en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo: [exportación de conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo: [exportar conjuntos de datos mediante programación utilizando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Datos exportados {#exported-data}

Para [!DNL SFTP] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de audiencia.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos SFTP](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.
