---
title: Destino de zona de aterrizaje de datos
description: Obtenga información sobre cómo conectarse a la zona de aterrizaje de datos para activar audiencias y exportar conjuntos de datos.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: cc7c8c14fe5ee4bb9001cae84d28a385a3b4b448
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 2%

---

# Destino de zona de aterrizaje de datos

>[!IMPORTANT]
>
>Esta página de documentación hace referencia al [!DNL Data Landing Zone] *destino*. También hay un [!DNL Data Landing Zone] *origen* en el catálogo de orígenes. Para obtener más información, lea la documentación de [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md).


## Información general {#overview}

[!DNL Data Landing Zone] es una interfaz de almacenamiento en la nube aprovisionada por Adobe Experience Platform, que le concede acceso a una función de almacenamiento de archivos segura y basada en la nube para exportar archivos fuera de Platform. Tiene acceso a un contenedor [!DNL Data Landing Zone] por zona protegida, y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con su licencia de productos y servicios de Platform. Todos los clientes de Platform y sus aplicaciones, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] y [!DNL Real-Time Customer Data Platform], se han aprovisionado con un contenedor de [!DNL Data Landing Zone] por zona protegida.

Platform aplica un tiempo de vida (TTL) estricto de siete días a todos los archivos cargados en un contenedor de [!DNL Data Landing Zone]. Todos los archivos se eliminan a los siete días.

El conector de destino [!DNL Data Landing Zone] está disponible para los clientes que usan la compatibilidad con la nube de Azure o Amazon Web Service. El mecanismo de autenticación es diferente en función de la nube en la que se aprovisiona el destino, todo lo demás sobre el destino y sus casos de uso son los mismos. Obtenga más información acerca de los dos mecanismos de autenticación diferentes en las secciones [Autenticar en la zona de aterrizaje de datos aprovisionada en Azure Blob] y [Autenticar en la zona de aterrizaje de datos aprovisionada por AWS](#authenticate-dlz-aws).

![Diagrama que muestra cómo la implementación del destino de zona de aterrizaje de datos es diferente según la compatibilidad con la nube.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png)

## Conéctese a su almacenamiento de [!UICONTROL zona de aterrizaje de datos] mediante la API o la interfaz de usuario {#connect-api-or-ui}

* Para conectarse a su ubicación de almacenamiento de la [!UICONTROL zona de aterrizaje de datos] mediante la interfaz de usuario de Platform, lea las secciones [Conectarse al destino](#connect) y [Activar audiencias en este destino](#activate) a continuación.
* Para conectarse a su ubicación de almacenamiento de [!UICONTROL Zona de aterrizaje de datos] mediante programación, lea [Activar audiencias en destinos basados en archivos mediante el tutorial de la API de Flow Service](../../api/activate-segments-file-based-destinations.md).

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
| Tipo de exportación | **[!UICONTROL Basado en perfil]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema aplicables (por ejemplo, su PPID), tal como se eligió en la pantalla Seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Obtenga más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea los tutoriales:

* Cómo [exportar conjuntos de datos mediante la interfaz de usuario de Platform](/help/destinations/ui/export-datasets.md).
* Cómo [exportar conjuntos de datos mediante programación usando la API de Flow Service](/help/destinations/api/export-datasets.md).

## Formato de archivo de los datos exportados {#file-format}

Al exportar *datos de audiencia*, Platform crea un archivo de `.csv`, `parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [formatos de archivo compatibles con la exportación](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) en el tutorial de activación de audiencia.

Al exportar *conjuntos de datos*, Platform crea un archivo de `.parquet` o `.json` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte la sección [verificar la exportación correcta del conjunto de datos](../../ui/export-datasets.md#verify) en el tutorial exportar conjuntos de datos.

## Autenticar en la zona de aterrizaje de datos aprovisionada en Azure Blob {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Microsoft Azure. Para obtener más información acerca de la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Puede leer y escribir archivos en el contenedor a través de [!DNL Azure Storage Explorer] o de la interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con mecanismos de seguridad de almacenamiento estándar de [!DNL Azure Blob] en reposo y en tránsito. SAS significa [firma de acceso compartido](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

La autenticación basada en SAS le permite tener acceso de forma segura a su contenedor de [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para tener acceso al contenedor de [!DNL Data Landing Zone], lo que significa que no es necesario configurar listas de permitidos ni configuraciones entre regiones para la red.

### Conectar su contenedor de [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer]

Puede usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) para administrar el contenido de su contenedor de [!DNL Data Landing Zone]. Para empezar a usar [!DNL Data Landing Zone], primero debe recuperar las credenciales, introducirlas en [!DNL Azure Storage Explorer] y conectar el contenedor de [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer].

En la interfaz de usuario [!DNL Azure Storage Explorer], seleccione el icono de conexión en la barra de navegación izquierda. Aparecerá la ventana **Seleccionar recurso**, que le proporcionará las opciones para conectarse a. Seleccione **[!DNL Blob container]** para conectarse a su almacenamiento de [!DNL Data Landing Zone].

![Seleccione el recurso resaltado en la interfaz de usuario de Azure.](/help/sources/images/tutorials/create/dlz/select-resource.png)

A continuación, seleccione **URL de firma de acceso compartido (SAS)** como método de conexión y, a continuación, seleccione **Siguiente**.

![Seleccione el método de conexión resaltado en la interfaz de usuario de Azure.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Después de seleccionar el método de conexión, debe proporcionar un **nombre para mostrar** y la URL de SAS de contenedor **[!DNL Blob]** que corresponda a su contenedor [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Recuperar las credenciales de su [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Debe usar las API de Platform para recuperar sus credenciales de [!DNL Data Landing Zone]. A continuación, se describe la llamada de API para recuperar sus credenciales. Para obtener información sobre cómo obtener los valores requeridos para los encabezados, consulte la guía [Introducción a las API de Adobe Experience Platform](/help/landing/api-guide.md).

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `dlz_destination` | El tipo `dlz_destination` permite a la API distinguir un contenedor de destino de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |

{style="table-layout:auto"}

**Solicitud**

El siguiente ejemplo de solicitud recupera las credenciales de una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve la información de credenciales de la zona de aterrizaje, incluidos los `SASToken` y `SASUri` actuales, y el `storageAccountName` que corresponde al contenedor de la zona de aterrizaje.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | El nombre de su zona de aterrizaje. |
| `SASToken` | El token de firma de acceso compartido para su zona de aterrizaje. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `SASUri` | El URI de firma de acceso compartido para su zona de aterrizaje. Esta cadena es una combinación del URI de la zona de aterrizaje para la que se está autenticando y su token SAS correspondiente, |

{style="table-layout:auto"}

### Actualizar credenciales de [!DNL Data Landing Zone] {#update-dlz-credentials}

También puede actualizar sus credenciales cuando lo desee. Puede actualizar su `SASToken` realizando una solicitud de POST al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `dlz_destination` | El tipo `dlz_destination` permite a la API distinguir un contenedor de destino de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |
| `refresh` | La acción `refresh` le permite restablecer las credenciales de su zona de aterrizaje y generar automáticamente un nuevo `SASToken`. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud actualiza las credenciales de la zona de aterrizaje.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve valores actualizados para su `SASToken` y `SASUri`.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Proporcione su nombre para mostrar (`containerName`) y la URL SAS [!DNL Data Landing Zone], tal como se devolvió en la llamada de API descrita anteriormente, y luego seleccione **Siguiente**.

![Escriba la información de conexión resaltada en la interfaz de usuario de Azure.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Aparece la ventana **Resumen**, que le proporciona una descripción general de la configuración, incluida información sobre el extremo y los permisos de [!DNL Blob]. Cuando esté listo, seleccione **Conectar**.

![Resumen de la configuración mostrada en la interfaz de usuario de Azure.](/help/sources/images/tutorials/create/dlz/summary.png)

Una conexión correcta actualiza la interfaz de usuario de [!DNL Azure Storage Explorer] con el contenedor de [!DNL Data Landing Zone].

![Resumen del contenedor de usuario DLZ resaltado en la interfaz de usuario de Azure.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con el contenedor [!DNL Data Landing Zone] conectado a [!DNL Azure Storage Explorer], ahora puede empezar a exportar archivos del Experience Platform al contenedor [!DNL Data Landing Zone]. Para exportar archivos, debe establecer una conexión con el destino [!DNL Data Landing Zone] en la interfaz de usuario del Experience Platform, tal como se describe en la sección siguiente.

## Autenticar en la zona de aterrizaje de datos aprovisionada por AWS {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Un Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información acerca de la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Realice las operaciones siguientes para obtener credenciales de la instancia de zona de aterrizaje de datos aprovisionada en AWS. A continuación, utilice un cliente de su elección para conectarse a la instancia de la zona de aterrizaje de datos.

>[!BEGINSHADEBOX]

### Recuperar las credenciales de su [!DNL Data Landing Zone] {#retrieve-dlz-credentials-aws}

Debe usar las API de Platform para recuperar sus credenciales de [!DNL Data Landing Zone]. A continuación, se describe la llamada de API para recuperar sus credenciales. Para obtener información sobre cómo obtener los valores requeridos para los encabezados, consulte la guía [Introducción a las API de Adobe Experience Platform](/help/landing/api-guide.md).

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `dlz_destination` | El tipo `dlz_destination` permite a la API distinguir un contenedor de destino de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |

{style="table-layout:auto"}

**Solicitud**

El siguiente ejemplo de solicitud recupera las credenciales de una zona de aterrizaje existente.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Respuesta**

La siguiente respuesta devuelve la información de credenciales de la zona de aterrizaje, incluidos los datos actuales `awsAccessKeyId`, `awsSecretAccessKey` y otros datos.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Propiedad | Descripción |
| --- | --- |
| `credentials` | Este objeto incluye `awsAccessKeyId`, `awsSecretAccessKey` y `awsSessionToken` que el Experience Platform utiliza para exportar archivos a la ubicación de la zona de aterrizaje de datos aprovisionada. |
| `dlzPath` | Este objeto incluye la ruta de la ubicación de AWS aprovisionada de Adobe en la que se depositan los archivos exportados. |
| `dlzProvider` | Indica que se trata de una zona de aterrizaje de datos aprovisionada para Amazon S3. |
| `expiryTime` | Indica cuándo caducarán las credenciales del objeto situado más arriba. Puede actualizarlas realizando de nuevo la llamada. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Asegúrese de haber conectado su contenedor de [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer] tal como se describe en la sección [requisitos previos](#prerequisites). Dado que [!DNL Data Landing Zone] es un almacenamiento aprovisionado por Adobe, no es necesario que realice ningún paso adicional en la interfaz de usuario del Experience Platform para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
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

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación

En el paso **[!UICONTROL Programación]**, puede [configurar la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su destino [!DNL Data Landing Zone] y también [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignar atributos e identidades {#map}

En el paso **[!UICONTROL Asignación]**, puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, vea el [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial de la interfaz de usuario para activar destinos por lotes.

## Validación de la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, compruebe el almacenamiento de [!DNL Data Landing Zone] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
