---
title: Conexión de Amazon S3
description: Cree una conexión saliente activa a su almacenamiento de Amazon Web Service (AWS) S3 para exportar periódicamente archivos de datos CSV de Adobe Experience Platform a sus propios contenedores de S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] conexión {#s3-connection}

## Registro de cambios de destino {#changelog}

+++ Ver registro de cambios


| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Enero de 2024 | Actualización de funcionalidad y documentación | El conector de destino de Amazon S3 ahora admite un nuevo tipo de autenticación de función asumida. Obtenga más información al respecto en la [sección de autenticación](#assumed-role-authentication). |
| Julio de 2023 | Actualización de funcionalidad y documentación | Con la versión de julio de 2023 de Experience Platform, la variable [!DNL Amazon S3] El destino proporciona nuevas funciones, como se indica a continuación: <br><ul><li>[Compatibilidad con exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md)</li><li>[Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.</li><li>Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Conéctese a su [!DNL Amazon S3] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su [!DNL Amazon S3] Ubicación de almacenamiento mediante la interfaz de usuario de Platform, lea las secciones [Conectar con el destino](#connect) y [Activar audiencias en este destino](#activate) más abajo.
* Para conectarse a su [!DNL Amazon S3] ubicación de almacenamiento mediante programación, lea la guía sobre cómo [activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![El tipo de exportación basado en perfiles de Amazon S3 resaltado en EE. UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

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

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**. El destino de Amazon S3 admite dos métodos de autenticación:

* Autenticación de clave de acceso y clave secreta
* Autenticación de la función asumida

#### Autenticación de clave de acceso y clave secreta

Utilice este método de autenticación cuando desee introducir la clave de acceso y la clave secreta de Amazon S3 para permitir que el Experience Platform exporte los datos a las propiedades de Amazon S3.

![Imagen de los campos obligatorios al seleccionar la autenticación de clave de acceso y clave secreta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]tecla de acceso** y **[!DNL Amazon S3]clave secreta**: en [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso de plataforma a su [!DNL Amazon S3] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la interfaz de usuario.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Función asumida {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Autenticación de la función asumida"
>abstract="Utilice este tipo de autenticación si prefiere no compartir claves de cuenta y claves secretas con Adobe. En su lugar, Experience Platform se conecta a la ubicación de Amazon S3 mediante el acceso basado en funciones. Pegue el ARN de la función que ha creado en AWS para el usuario de Adobe. El patrón es similar a `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Imagen de los campos obligatorios al seleccionar la autenticación de función asumida.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Utilice este tipo de autenticación si prefiere no compartir claves de cuenta y claves secretas con Adobe. En su lugar, el Experience Platform se conecta a la ubicación de Amazon S3 mediante el acceso basado en funciones.

Para ello, debe crear en la consola de AWS un usuario supuesto para el Adobe de [derecho permisos requeridos](#required-s3-permission) para escribir en los bloques de Amazon S3. Crear un **[!UICONTROL Entidad de confianza]** en AWS con la cuenta de Adobe **[!UICONTROL 670664943635]**. Para obtener más información, consulte la [Documentación de AWS sobre la creación de funciones](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: pegue el ARN de la función que ha creado en AWS para el usuario de Adobe. El patrón es similar a `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nombre del segmento"
>abstract="Debe tener entre 3 y 63 caracteres. Debe comenzar y terminar con una letra o un número. Solo debe contener letras minúsculas, números o guiones (-). No se debe aplicar el formato de una dirección IP (por ejemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ruta de carpeta"
>abstract="Debe contener únicamente los caracteres A-Z, a-z, 0-9 y puede incluir los siguientes caracteres especiales: `/!-_.'()"^[]+$%.*"`. Para crear una carpeta por archivo de público, inserte el macro `/%SEGMENT_NAME%` o `/%SEGMENT_ID%` o `/%SEGMENT_NAME%/%SEGMENT_ID%` en el campo de texto. Las macros solo se pueden insertar al final de la ruta de la carpeta. Vea ejemplos de macros en la documentación."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=es#use-macros" text="Utilice macros para crear una carpeta en su ubicación de almacenamiento"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino.
* **[!UICONTROL Nombre del cubo]**: introduzca el nombre del [!DNL Amazon S3] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc. El nombre del manifiesto se asigna mediante el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver una [archivo de manifiesto de muestra](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: La [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: La hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: Ruta de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

>[!TIP]
>
>En el flujo de trabajo Connect destination, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de audiencia exportado. Leer [Usar macros para crear una carpeta en la ubicación de almacenamiento](overview.md#use-macros) para obtener instrucciones.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Requerido [!DNL Amazon S3] permissions {#required-s3-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon S3] ubicación de almacenamiento, crear un usuario de Identity and Access Management (IAM) para [!DNL Platform] in [!DNL Amazon S3] y asigne permisos para las siguientes acciones:

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

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe su [!DNL Amazon S3] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

Consulte la [LISTA DE PERMITIDOS de direcciones IP](ip-address-allow-list.md) artículo si necesita agregar direcciones IP de Adobe a una lista de permitidos.