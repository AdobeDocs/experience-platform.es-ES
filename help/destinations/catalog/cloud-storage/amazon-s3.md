---
title: Conexión de Amazon S3
description: Cree una conexión saliente activa a su almacenamiento de Amazon Web Service (AWS) S3 para exportar periódicamente archivos de datos CSV de Adobe Experience Platform a sus propios contenedores de S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 7aff8d9eafb699133e90d3af8ef24f3135f3cade
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 13%

---

# [!DNL Amazon S3] conexión {#s3-connection}

## Registro de cambios de destino {#changelog}

+++ Ver registro de cambios


| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Enero de 2024 | Actualización de funcionalidad y documentación | El conector de destino de Amazon S3 ahora admite un nuevo tipo de autenticación de función asumida. Obtenga más información al respecto en la [sección de autenticación](#assumed-role-authentication). |
| Julio de 2023 | Actualización de funcionalidad y documentación | Con la versión de Experience Platform de julio de 2023, el destino [!DNL Amazon S3] proporciona nuevas funciones, como se indica a continuación: <br><ul><li>[Compatibilidad con la exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md)</li><li>[Opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) adicionales.</li><li>Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través del [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidad para personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Conectar con su almacenamiento de [!DNL Amazon S3] mediante API o IU {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento [!DNL Amazon S3] mediante la interfaz de usuario de Experience Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse mediante programación a la ubicación de almacenamiento [!DNL Amazon S3], lea la guía sobre cómo [activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

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

![Tipo de exportación basado en perfiles de Amazon S3 resaltado en EE. UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

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

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**. El destino de Amazon S3 admite dos métodos de autenticación:

* Autenticación de clave de acceso y clave secreta
* Autenticación de la función asumida

#### Autenticación con clave de acceso S3 y clave secreta

Utilice este método de autenticación cuando desee introducir la clave de acceso y la clave secreta de Amazon S3 para permitir que Experience Platform exporte datos a las propiedades de Amazon S3.

![Imagen de los campos requeridos al seleccionar la clave de acceso y la autenticación de clave secreta.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]clave de acceso** y **[!DNL Amazon S3]clave secreta**: en [!DNL Amazon S3], genere un par de `access key - secret access key` para conceder acceso a Experience Platform a su cuenta de [!DNL Amazon S3]. Obtenga más información en la [documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

  ![Imagen que muestra un ejemplo de una clave PGP correctamente formateada en la interfaz de usuario.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Autenticación con S3 como rol asumido {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Autenticación de la función asumida"
>abstract="Utilice este tipo de autenticación si prefiere no compartir claves de cuenta y claves secretas con Adobe. En su lugar, Experience Platform se conecta a la ubicación de Amazon S3 mediante el acceso basado en funciones. Pegue el ARN de la función que ha creado en AWS para el usuario de Adobe. El patrón es similar a `arn:aws:iam::800873819705:role/destinations-role-customer` "

Utilice este tipo de autenticación si prefiere no compartir claves de cuenta y claves secretas con Adobe. En su lugar, Experience Platform se conecta a su ubicación de Amazon S3 mediante el acceso basado en funciones.

![Imagen de los campos requeridos al seleccionar la autenticación de rol asumido.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**: pegue el ARN del rol que creó en AWS para el usuario de Adobe. El patrón es similar a `arn:aws:iam::800873819705:role/destinations-role-customer`. Consulte los pasos siguientes para obtener instrucciones detalladas sobre cómo configurar correctamente el acceso a S3.
* **[!UICONTROL Clave de cifrado]**: de forma opcional, puede adjuntar la clave pública con formato RSA para agregar el cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

Para ello, debe crear en la consola de AWS una función asumida para Adobe con los [permisos necesarios](#minimum-permissions-iam-user) para escribir en los bloques de Amazon S3.

**Crear una directiva con los permisos necesarios**

1. Abra la consola AWS y vaya a IAM > Políticas > Crear política
2. Seleccione Editor de directivas > JSON y añada los permisos siguientes.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. En la página siguiente, escriba un nombre para la directiva y guárdela como referencia. Necesitará este nombre de directiva al crear la función en el paso siguiente.

**Crear función de usuario en su cuenta de cliente de S3**

1. Abra la consola AWS y vaya a IAM > Funciones > Crear nueva función
2. Seleccione **tipo de entidad de confianza** > **cuenta de AWS**
3. Seleccione **Una cuenta de AWS** > **Otra cuenta de AWS** e introduzca el identificador de la cuenta de Adobe: `670664943635`
4. Añadir permisos mediante la directiva creada anteriormente
5. Escriba un nombre de rol (por ejemplo, `destinations-role-customer`). El nombre de la función debe tratarse como confidencial, de forma similar a una contraseña. Puede contener hasta 64 caracteres y puede contener caracteres alfanuméricos y los siguientes caracteres especiales: `+=,.@-_`. A continuación, compruebe que:
   * El id. de cuenta de Adobe `670664943635` se encuentra en la sección **[!UICONTROL Seleccionar entidades de confianza]**
   * La directiva creada anteriormente está presente en **[!UICONTROL Resumen de directivas de permisos]**

**Proporcione el rol que Adobe debe asumir**

Después de crear la función en AWS, debe proporcionar la función ARN a Adobe. El ARN sigue este patrón: `arn:aws:iam::800873819705:role/destinations-role-customer`

Puede encontrar el ARN en la página principal después de crear la función en la consola de AWS. Utilizará este ARN al crear el destino.

**Verificar permisos de funciones y relaciones de confianza**

Asegúrese de que la función tenga la configuración siguiente:

* **Permisos**: la función debe tener permisos para acceder a S3 (ya sea acceso completo o los permisos mínimos proporcionados en el paso **Crear una directiva con los permisos requeridos** anterior)
* **Relaciones de confianza**: el rol debe tener la cuenta raíz de Adobe (`670664943635`) en sus relaciones de confianza

**Alternativa: restringir a un usuario de Adobe específico (opcional)**

Si prefiere no permitir la cuenta completa de Adobe, puede restringir el acceso solo a un usuario de Adobe específico. Para ello, edite la directiva de confianza con la siguiente configuración:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

Para obtener más información, consulte la [documentación de AWS sobre la creación de funciones](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).



### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nombre del segmento"
>abstract="Debe tener entre 3 y 63 caracteres. Debe comenzar y terminar con una letra o un número. Solo debe contener letras minúsculas, números o guiones (-). No debe tener el formato de una dirección IP (por ejemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ruta de carpeta"
>abstract="Debe contener únicamente los caracteres A-Z, a-z, 0-9 y puede incluir los siguientes caracteres especiales: `/!-_.'()"^[]+$%.*"`. Para crear una carpeta por archivo de público, inserte el macro `/%SEGMENT_NAME%` o `/%SEGMENT_ID%` o `/%SEGMENT_NAME%/%SEGMENT_ID%` en el campo de texto. Las macros solo se pueden insertar al final de la ruta de la carpeta. Vea ejemplos de macros en la documentación."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=es#use-macros" text="Utilice macros para crear una carpeta en su ubicación de almacenamiento"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: escriba un nombre que le ayude a identificar este destino.
* **[!UICONTROL Descripción]**: escriba una descripción para este destino.
* **[!UICONTROL Nombre del contenedor]**: Escriba el nombre del contenedor [!DNL Amazon S3] que usará este destino.
* **[!UICONTROL Ruta de carpeta]**: escriba la ruta de acceso a la carpeta de destino que alojará los archivos exportados.
* **[!UICONTROL Tipo de archivo]**: seleccione el formato que Experience Platform debe usar para los archivos exportados. Al seleccionar la opción [!UICONTROL CSV], también puede [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que Experience Platform debe usar para los archivos exportados.
* **[!UICONTROL Incluir archivo de manifiesto]**: Active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de la exportación, etc. Se ha asignado un nombre al manifiesto con el formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Ver [archivo de manifiesto de ejemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). El archivo de manifiesto incluye los campos siguientes:
   * `flowRunId`: la [ejecución de flujo de datos](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) que generó el archivo exportado.
   * `scheduledTime`: la hora en UTC en que se exportó el archivo.
   * `exportResults.sinkPath`: ruta de acceso de la ubicación de almacenamiento en la que se deposita el archivo exportado.
   * `exportResults.name`: nombre del archivo exportado.
   * `size`: tamaño del archivo exportado, en bytes.

>[!TIP]
>
>En el flujo de trabajo Connect destination, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de audiencia exportado. Lee [Usar macros para crear una carpeta en tu ubicación de almacenamiento](overview.md#use-macros) para obtener instrucciones.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

### Permisos necesarios de [!DNL Amazon S3] {#required-s3-permission}

Para conectar y exportar datos correctamente a la ubicación de almacenamiento [!DNL Amazon S3], cree un usuario de Identity and Access Management (IAM) para [!DNL Experience Platform] en [!DNL Amazon S3] y asigne permisos para las siguientes acciones:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Permisos mínimos necesarios para la autenticación de funciones asumidas por IAM {#minimum-permissions-iam-user}

Al configurar el rol de IAM como cliente, asegúrese de que la política de permisos asociada al rol incluya las acciones necesarias en la carpeta de destino en el bloque y la acción `s3:ListBucket` en la raíz del bloque. Vea a continuación un ejemplo de la directiva de permisos mínimos para este tipo de autenticación:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el almacenamiento de [!DNL Amazon S3] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.

## LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

Consulte el artículo [lista de permitidos de direcciones IP](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.