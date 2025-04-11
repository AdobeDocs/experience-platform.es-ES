---
solution: Experience Platform
title: Exportación de conjuntos de datos mediante la API de servicio Flujo
description: Aprenda a utilizar la API de Flujo Service para exportar conjuntos de datos a destinos seleccionados.
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: 29fb232ecfbd119ef84d62599fc79249513dca43
workflow-type: tm+mt
source-wordcount: '5151'
ht-degree: 3%

---

# Exporte conjuntos de datos mediante la [!DNL Flow Service API]

>[!AVAILABILITY]
>
>* Este funcionalidad está disponible para los clientes que hayan adquirido el paquete Real-Time CDP Prime and Ultimate, Adobe Systems Journey Optimizer o Customer Journey Analytics. Póngase en contacto con su representante de Adobe para obtener más información.

>[!IMPORTANT]
>
>**Elemento** de acción: La [versión de septiembre de 2024 de Experience Platform](/help/release-notes/latest/latest.md#destinations) introdujo la opción de establecer una `endTime` fecha para la exportación conjunto de datos flujos de datos. Adobe Systems también ha introducido una fecha de finalización predeterminada del 1 de mayo de 2025 para todos los flujos de datos de exportación de conjunto de datos creados *antes de la versión* de septiembre de 2024.
>
>Para cualquiera de esos flujos de datos, debe actualizar la fecha de finalización en el flujo de datos manualmente antes de la fecha de finalización; de lo contrario, las exportaciones se detendrán en esa fecha. Utilice el IU Experience Platform para vista qué flujos de datos se detendrán el 1 de mayo de 2025.
>
>Del mismo modo, para cualquier flujo de datos que cree sin especificar una `endTime` fecha, el valor predeterminado será una hora de finalización de seis meses a partir del momento en que se crean.

<!--

>You can retrieve a list of such dataflows by performing the following API call: `https://platform.adobe.io/data/foundation/flowservice/flows?property=scheduleParams.endTime==UNIXTIMESTAMPTHATWEWILLUSE`
>

-->

En este artículo se explica la flujo de trabajo necesaria para exportar [!DNL Flow Service API] conjuntos de datos desde Adobe Experience Platform a su ubicación almacenamiento de nube preferida, como [!DNL Amazon S3], ubicaciones SFTP o [!DNL Google Cloud Storage].](/help/catalog/datasets/overview.md) [

>[!TIP]
>
>También puede utilizar la interfaz de usuario de Experience Platform para exportar conjuntos de datos. Lea el tutorial de la interfaz de usuario de [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) para obtener más información.

## Conjuntos de datos disponibles para exportar {#datasets-to-export}

Los conjuntos de datos que puede exportar dependen del aplicación de Experience Platform (CDP en tiempo real, Adobe Systems Journey Optimizer), del nivel (Prime o Ultimate) y de los complementos que haya adquirido (por ejemplo: Data Distiller).

Consulte la [tabla de la IU tutorial Página](/help/destinations/ui/export-datasets.md#datasets-to-export) para saber qué conjuntos de datos puede exportar.

## Destinos admitidos {#supported-destinations}

Actualmente, puede exportar conjuntos de datos a los destinos de almacenamiento en la nube resaltados en la captura de pantalla y que se enumeran a continuación.

![Destinos que admiten exportaciones de conjuntos de datos](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Introducción {#get-started}

![Información general: Pasos para crear un destino y exportar conjuntos de datos](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): todos los datos que se han ingerido correctamente en Adobe Experience Platform se mantienen dentro de [!DNL Data Lake] como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.
   * [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para exportar conjuntos de datos a destinos de almacenamiento en la nube en Experience Platform.

### Permisos necesarios {#permissions}

Para exportar conjuntos de datos, necesita **[!UICONTROL Ver destinos]**, **[!UICONTROL Ver conjuntos de datos]** y **[!UICONTROL Administrar y activar destinos de conjuntos de datos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para asegurarse de que dispone de los permisos necesarios para exportar conjuntos de datos y de que el destino admite la exportación de conjuntos de datos, examine el catálogo de destinos. Si un destino tiene un **[!UICONTROL control Activar]** o Exportar **[!UICONTROL conjuntos]** de datos, tiene los permisos adecuados.

### Lectura de llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona ejemplos de llamadas API para demostrar cómo formato las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en el guía de solución de [!DNL Experience Platform] problemas.

### Recopilar valores para encabezados opcionales y obligatorios {#gather-values-headers}

Para realizar llamadas a [!DNL Experience Platform] las API, primero debe completar el tutorial de autenticación Experience Platform[](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos se [!DNL Experience Platform] pueden aislar en entornos de pruebas virtuales específicos. En las solicitudes a [!DNL Experience Platform] las API, puede especificar el nombre y el ID del entorno limitado en el que se llevará a cabo la operación. Estos son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Experience Platform], consulte la documentación](../../sandboxes/home.md) general del [entorno de pruebas.

Todas las solicitudes que contienen una carga útil (POST, PUT PATCH) requieren un encabezado de tipo medios adicional:

* Tipo de contenido: `application/json`

### Documentación de referencia del API {#api-reference-documentation}

Puede encontrar la documentación de referencia adjunta para todas las operaciones de API en este tutorial. Consulte la documentación de la API [[!DNL Flow Service] - Destinos en el sitio web de Adobe Developer](https://developer.adobe.com/experience-platform-apis/references/destinations/). Le recomendamos que utilice este tutorial y la documentación de referencia de la API en paralelo.

### Glosario {#glossary}

Para obtener descripciones de los términos que encontrará en este tutorial de API, lea la [sección del glosario](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) de la documentación de referencia de la API.

### Recopile las especificaciones de conexión y de flujo para el destino deseado {#gather-connection-spec-flow-spec}

Antes de iniciar el flujo de trabajo para exportar un conjunto de datos, identifique la especificación de conexión y los ID de especificación de flujo del destino al que desea exportar los conjuntos de datos. Utilice la tabla siguiente como referencia.


| Destino | Especificación de conexión | Especificación de flujo |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

Necesita estos ID para construir varias [!DNL Flow Service] entidades. También es necesario hacer referencia a partes de la [!DNL Connection Spec] propia para configurar ciertas entidades de modo que pueda recuperar el [!DNL Connection Spec] de [!DNL Flow Service APIs]. Consulte los ejemplos siguientes de recuperación de especificaciones de conexión para todos los destinos de la tabla:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

+++Recuperar [!DNL connection spec] para [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++[!DNL Amazon S3] - Especificaciones de conexión

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Almacenamiento de blob de Azure]

**Solicitud**

+++Recuperar [!DNL connection spec] para [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitud**

+++Recuperar [!DNL connection spec] para [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

**Solicitud**

+++Recuperar [!DNL connection spec] para [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Almacenamiento en la nube de Google]

**Solicitud**

+++Recuperar [!DNL connection spec] para [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**Solicitud**

+++Recuperar [!DNL connection spec] para SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Respuesta**

+++SFTP: [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

Siga los pasos que se indican a continuación para configurar un flujo de datos de conjunto de datos a un destino almacenamiento nube. Para algunos pasos, las solicitudes y respuestas difieren entre las distintas nube almacenamiento destinos. En esos casos, utilice las pestañas del Página para recuperar las solicitudes y respuestas específicas del destino al que desea conectarse y exportar conjuntos de datos. Asegúrese de utilizar el correcto [!DNL connection spec] y [!DNL flow spec] para el destino que está configurando.

## Recuperar un lista de conjuntos de datos {#retrieve-list-of-available-datasets}

![Diagrama que muestra el paso 1 en la flujo de trabajo de conjuntos de datos de exportación](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

Para recuperar una lista de conjuntos de datos aptos para activación, inicio realizando una llamada de API al punto final que se muestra a continuación.

>[!BEGINSHADEBOX]

**Solicitud**

+++Recuperar conjuntos de datos aptos - Solicitud

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

Tenga en cuenta que para recuperar conjuntos de datos aptos, el ID de [!DNL connection spec] utilizado en la dirección URL de solicitud debe ser el ID de especificación de conexión de origen de datos `23598e46-f560-407b-88d5-ea6207e49db0`, y se deben especificar los dos parámetros de consulta `outputField=datasets` y `outputType=activationDatasets`. Todos los demás parámetros de consulta son los estándar admitidos por la [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/).

+++

**Respuesta**

+++Recuperar conjuntos de datos: respuesta

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

Una respuesta correcta contiene una lista de conjuntos de datos aptos para la activación. Estos conjuntos de datos se pueden utilizar al construir la conexión de origen en el siguiente paso.

Para obtener información sobre los distintos parámetros de respuesta para cada conjunto de datos devuelto, consulte la documentación](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets) del desarrollador de la API de [conjuntos de datos.

## Crear una conexión de origen {#create-source-connection}

![Diagrama que muestra el paso 2 en la flujo de trabajo de conjuntos de datos de exportación](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

Después de recuperar el lista de conjuntos de datos que desea exportar, puede crear una conexión de origen utilizando esos ID de conjunto de datos.

>[!BEGINSHADEBOX]

**Solicitud**

+++Crear conexión de origen: Solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**Respuesta**

+++Crear conexión de origen: respuesta

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Una respuesta correcta devuelve el identificador (`id`) de la conexión de origen recién creada y un `etag`. Tenga en cuenta el ID de conexión de origen, ya que lo necesitará más adelante al crear el flujo de datos.

Recuerde también lo siguiente:

* La conexión de origen creada en este paso debe vincularse a un flujo de datos para que sus conjuntos de datos se activen en un destino. Consulte la sección [crear un flujo de datos](#create-dataflow) para obtener información sobre cómo vincular una conexión de origen a un flujo de datos.
* Los ID de conjuntos de datos de una conexión de origen no se pueden modificar después de la creación. Si necesita agregar o quitar conjuntos de datos de una conexión de origen, debe crear una nueva conexión de origen y vincular el ID de la nueva conexión de origen al flujo de datos.

## Crear una (destino) conexión de base {#create-base-connection}

![Diagrama que muestra el paso 3 en el flujo de trabajo de exportar conjuntos de datos](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

Una conexión base almacena de forma segura las credenciales en su destino. Según el tipo de destino, las credenciales necesarias para autenticarse en ese destino pueden variar. Para encontrar estos parámetros de autenticación, primero recupere [!DNL connection spec] para el destino deseado tal como se describe en la sección [Recopilar especificaciones de conexión y especificaciones de flujo](#gather-connection-spec-flow-spec) y luego observe `authSpec` de la respuesta. Haga referencia a las fichas siguientes para las propiedades de `authSpec` de todos los destinos admitidos.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe la línea resaltada con comentarios en línea del [!DNL connection spec] ejemplo siguiente, que proporciona información adicional sobre dónde encontrar los parámetros de autenticación en el [!DNL connection spec]archivo .

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Almacenamiento de blob de Azure]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe la línea resaltada con comentarios en línea del [!DNL connection spec] ejemplo siguiente, que proporciona información adicional sobre dónde encontrar los parámetros de autenticación en el [!DNL connection spec]archivo .

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe la línea resaltada con comentarios en línea del [!DNL connection spec] ejemplo siguiente, que proporciona información adicional sobre dónde encontrar los parámetros de autenticación en el [!DNL connection spec]archivo .

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Zona de aterrizaje de datos (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mostrando [!DNL auth spec]

>[!NOTE]
>
>El destino de la zona de aterrizaje de datos no requiere un [!DNL auth spec]archivo .

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Almacenamiento en la nube de Google]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe la línea resaltada con comentarios en línea del [!DNL connection spec] ejemplo siguiente, que proporciona información adicional sobre dónde encontrar los parámetros de autenticación en el [!DNL connection spec]archivo .

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP: [!DNL Connection spec] muestra [!DNL auth spec]

>[!NOTE]
>
>El destino SFTP contiene dos elementos independientes en el [!DNL auth spec], ya que admite la autenticación de claves contraseña y SSH.

Observe la línea resaltada con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros de autenticación en [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

Con las propiedades especificadas en la especificación de autenticación (es decir, `authSpec` de la respuesta) puede crear una conexión base con las credenciales necesarias, específicas para cada tipo de destino, como se muestra en los ejemplos siguientes:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

+++[!DNL Amazon S3] - Solicitud de conexión base

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación necesarias, consulte la sección [autenticar en destino](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) de la página de documentación de destino de Amazon S3.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++[!DNL Amazon S3] respuesta de conexión base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento de blob de Azure]

**Solicitud**

+++[!DNL Azure Blob Storage] - Conexión base solicitud

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación necesarias, consulte la sección Autenticar en](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) destino [del Página de documentación de destino del Almacenamiento de blobs de Azure.

Observe las líneas resaltadas con comentarios en línea del ejemplo de solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++[!DNL Azure Blob Storage] - Respuesta de conexión base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitud**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Solicitud de conexión base

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación necesarias, consulte la sección [autenticar en el destino](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) de la página de documentación de destino de Azure Data Lake Gen 2(ADLS Gen2).

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Respuesta de conexión base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

**Solicitud**

+++[!DNL Data Landing Zone(DLZ)] - Solicitud de conexión base

>[!TIP]
>
>No se requieren credenciales de autenticación para el destino de la zona de aterrizaje de datos. Para obtener más información, consulte la sección [autenticar en destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) de la página de documentación de destino de la zona de aterrizaje de datos.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone Base Connection",
  "connectionSpec": {
    "id": "3567r537-2a7b-4583-ac39-ed38d4b848e8",
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++[!DNL Data Landing Zone] - Respuesta de conexión base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento en la nube de Google]

**Solicitud**

+++[!DNL Google Cloud Storage] - Solicitud de conexión base

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación necesarias, consulte la sección [autenticar en destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) de la página de documentación de destino de Google Cloud Storage.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++[!DNL Google Cloud Storage] - Respuesta de conexión base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitud**

+++SFTP con contraseña: solicitud de conexión base

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación requeridas, consulte la sección [autenticar en destino](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) de la página de documentación de destino SFTP.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++SFTP con clave SSH - solicitud de conexión base

>[!TIP]
>
>Para obtener información sobre cómo obtener las credenciales de autenticación necesarias, consulte la sección Autenticar en](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) destino [del Página de documentación de destino SFTP.

Observe las líneas resaltadas con comentarios en línea del ejemplo de solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**Respuesta**

+++SFTP: Respuesta de conexión básica

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Anote el ID de conexión de la respuesta. Este ID será necesario en el siguiente paso al crear la conexión destino.

## Crear una conexión destino {#create-target-connection}

![Diagrama que muestra el paso 4 en la flujo de trabajo de conjuntos de datos de exportación](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

Siguiente, debe crear una conexión destino que almacene los parámetros de exportación de los conjuntos de datos. Los parámetros de exportación incluyen la ubicación, el formato del archivo, la compresión y otros detalles. Consulte las `targetSpec` propiedades proporcionadas en las especificaciones de conexión del destino para conocer las propiedades admitidas para cada tipo de destino. Haga referencia a las fichas siguientes para las propiedades de `targetSpec` de todos los destinos admitidos.

>[!IMPORTANT]
>
>Las exportaciones a archivos JSON solo se admiten en modo comprimido. Las exportaciones a [!DNL Parquet] archivos se admiten en los modos comprimido y sin comprimir.
>
>El formato del archivo JSON exportado es NDJSON, que es el formato de intercambio estándar en el ecosistema de big data. Adobe recomienda utilizar un cliente compatible con NDJSON para leer los archivos exportados.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mostrando parámetros de conexión de destino

Observe las líneas resaltadas con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros [!DNL target spec] en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino son *no* aplicables a los destinos de exportación del conjunto de datos.

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Almacenamiento de blob de Azure]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mostrando parámetros de conexión de destino

Observe las líneas resaltadas con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros [!DNL target spec] en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino son *no* aplicables a los destinos de exportación del conjunto de datos.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mostrando parámetros de conexión de destino

Observe las líneas resaltadas con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros [!DNL target spec] en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino son *no* aplicables a los destinos de exportación del conjunto de datos.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mostrando parámetros de conexión de destino

Observe las líneas resaltadas con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros [!DNL target spec] en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino son *no* aplicables a los destinos de exportación del conjunto de datos.

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Almacenamiento en la nube de Google]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mostrar destino parámetros de conexión

Observe las líneas resaltadas con comentarios en línea en el [!DNL connection spec] ejemplo siguiente, que proporcionan información adicional sobre dónde encontrar los [!DNL target spec] parámetros en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino no *son* aplicables a conjunto de datos destinos de exportación.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP: [!DNL Connection spec] muestra los parámetros de conexión de destino

Observe las líneas resaltadas con comentarios en línea en el ejemplo [!DNL connection spec] siguiente, que proporciona información adicional sobre dónde encontrar los parámetros [!DNL target spec] en la especificación de conexión. También puede ver en el ejemplo siguiente qué parámetros de destino son *no* aplicables a los destinos de exportación del conjunto de datos.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


Con la especificación anterior, puede construir una solicitud de conexión de destino específica para el destino de almacenamiento en la nube deseado, como se muestra en las pestañas a continuación.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

+++[!DNL Amazon S3] - Target conexión solicitud

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino necesarios, consulte la sección Complete los [detalles](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) del destino del Página de documentación [!DNL Amazon S3] del destino.
>Para conocer otros valores admitidos de , consulte la documentación de referencia de `datasetFileType`API.

Observe las líneas resaltadas con comentarios en línea del ejemplo de solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Conexión de destino: respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento de blob de Azure]

**Solicitud**

+++[!DNL Azure Blob Storage] - Solicitud de conexión de destino

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino requeridos, consulte la sección [rellenar detalles de destino](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) de la página de documentación de destino [!DNL Azure Blob Storage].
>Para otros valores compatibles de `datasetFileType`, consulte la documentación de referencia de la API.


Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Conexión de destino: respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitud**

+++[!DNL Azure Blob Storage] - Solicitud de conexión de destino

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino requeridos, consulte la sección [rellenar detalles de destino](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) de la página de documentación de destino de Azure [!DNL Data Lake Gen 2(ADLS Gen2)].
>Para otros valores compatibles de `datasetFileType`, consulte la documentación de referencia de la API.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Target conexión - Respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

**Solicitud**

+++[!DNL Data Landing Zone] - Target conexión solicitud

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino requeridos, consulte la sección [rellenar detalles de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) de la página de documentación de destino [!DNL Data Landing Zone].
>Para otros valores compatibles de `datasetFileType`, consulte la documentación de referencia de la API.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Target conexión - Respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento en la nube de Google]

**Solicitud**

+++[!DNL Google Cloud Storage] - Solicitud de conexión de destino

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino requeridos, consulte la sección [rellenar detalles de destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) de la página de documentación de destino [!DNL Google Cloud Storage].
>Para otros valores compatibles de `datasetFileType`, consulte la documentación de referencia de la API.


Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Conexión de destino: respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitud**

+++SFTP: solicitud de conexión de destino

>[!TIP]
>
>Para obtener información sobre cómo obtener los parámetros de destino requeridos, consulte la sección [rellenar detalles de destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) de la página de documentación de destino SFTP.
>Para otros valores compatibles de `datasetFileType`, consulte la documentación de referencia de la API.

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**Respuesta**

+++Conexión de destino: respuesta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Tenga en cuenta el ID de conexión de Target de la respuesta. Este ID será necesario en el siguiente paso al crear el flujo de datos para exportar conjuntos de datos.

## Crear un flujo de datos {#create-dataflow}

![Diagrama que muestra el paso 5 en la flujo de trabajo de conjuntos de datos de exportación](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

El paso final en la configuración del destino es configurar un flujo de datos. Un flujo de datos une entidades creadas previamente y también proporciona opciones para configurar la programación de exportación de conjunto de datos. Para crear el flujo de datos, utilice las cargas útiles que se indican a continuación, en función del nube almacenamiento destino deseados, y reemplace los ID de entidad de los pasos anteriores.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

+++Crear flujo de datos del conjunto de datos al destino [!DNL Amazon S3] - Solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección `scheduleParams`, lo que le permite personalizar los tiempos de exportación, la frecuencia, la ubicación y mucho más para las exportaciones de conjuntos de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte Exportar [archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) completos y [Exportar archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) incrementales en los destinos del lote activación tutorial. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede utilizar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones diarias incrementales**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` y `interval` :`1` para las exportaciones incrementales diarias. <br> **Exportaciones incrementales por hora**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` y `interval` :`3`,`6`,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` según la frecuencia con la que desee exportar los archivos del conjunto de datos. |
| `interval` | Seleccione `1` cuando `timeUnit` sea un día y `3`,`6`,`9`,`12` cuando la unidad de tiempo sea `hour`. |
| `startTime` | La fecha y la hora en segundos de UNIX en que deben comenzar las exportaciones de conjuntos de datos. |
| `endTime` | La fecha y la hora en segundos de UNIX en que deben finalizar las exportaciones de conjuntos de datos. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta esperada en la ubicación de almacenamiento en la que se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> = <span>Identificador único del conjunto de datos.</span></li><li><code>DESTINO</code> = <span>Nombre del destino.</span></li><li><code>FECHA Y HORA</code> = <span>Fecha y hora con formato aaaaMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> = <span>Hora programada para la exportación de datos con el formato `exportTime=YYYYMMDDHHMM`.</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> = <span>Nombre de la instancia específica del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> <span>= Un identificador único para el instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> <span>= Nombre del entorno del entorno de pruebas.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> = <span>Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}
+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento de blob de Azure]

**Solicitud**

+++Crear conjunto de datos flujo de datos al [!DNL Azure Blob Storage] destino - Solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección `scheduleParams`, lo que le permite personalizar los tiempos de exportación, la frecuencia, la ubicación y mucho más para las exportaciones de conjuntos de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) en el tutorial de activación de destinos por lotes. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede usar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones diarias incrementales**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` y `interval` :`1` para las exportaciones incrementales diarias. <br> **Exportaciones incrementales por hora**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` y `interval` :`3`,`6`,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` dependiendo de la Frecuencia con la que desee exportar conjunto de datos archivos. |
| `interval` | Seleccione `1` cuando `timeUnit` sea un día y `3`,`6`,`9`,`12` cuando la unidad de tiempo sea `hour`. |
| `startTime` | La fecha y la hora en segundos de UNIX en que deben comenzar las exportaciones de conjuntos de datos. |
| `endTime` | La fecha y la hora en segundos de UNIX en que deben finalizar las exportaciones de conjuntos de datos. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta esperada en la ubicación de almacenamiento en la que se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> <span>= Un identificador único para el conjunto de datos.</span></li><li><code>DESTINO</code> <span>= El nombre del destino.</span></li><li><code>FECHA y HORA</code> <span>= Fecha y hora con el formato yyyyMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> = <span>Hora programada para la exportación de datos con el formato `exportTime=YYYYMMDDHHMM`.</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> = <span>Nombre de la instancia específica del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> <span>= Un identificador único para el instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> <span>= Nombre del entorno del entorno de pruebas.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> <span>= Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}

+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitud**

+++Crear conjunto de datos flujo de datos al [!DNL Azure Data Lake Gen 2(ADLS Gen2)] destino - Solicitud

Observe las líneas resaltadas con comentarios en línea del ejemplo de solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección, lo que le permite personalizar los tiempos de exportación, la Frecuencia, la `scheduleParams` ubicación y más para sus exportaciones conjunto de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) en el tutorial de activación de destinos por lotes. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede usar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones diarias incrementales**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` y `interval` :`1` para las exportaciones incrementales diarias. <br> **Exportaciones incrementales por hora**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` y `interval` :`3`,`6`,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` según la frecuencia con la que desee exportar los archivos del conjunto de datos. |
| `interval` | Seleccione `1` cuando `timeUnit` sea un día y `3`,`6`,`9`,`12` cuando la unidad de tiempo sea `hour`. |
| `startTime` | La fecha y la hora en segundos de UNIX en que deben comenzar las exportaciones de conjuntos de datos. |
| `endTime` | La fecha y hora, en segundos UNIX, en la que deben finalizar conjunto de datos exportaciones. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta prevista en la ubicación del almacenamiento donde se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> <span>= Un identificador único para el conjunto de datos.</span></li><li><code>DESTINO</code> = <span>Nombre del destino.</span></li><li><code>FECHA Y HORA</code> <span>= Fecha y hora con el formato yyyyMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> <span>= La hora programada para la exportación de datos con formato .`exportTime=YYYYMMDDHHMM`</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> = <span>Nombre de la instancia específica del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>Identificador único de la instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> = <span>Nombre del entorno de espacio aislado.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> = <span>Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}

+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de aterrizaje de datos (DLZ)]

**Solicitud**

+++Crear flujo de datos del conjunto de datos al destino [!DNL Data Landing Zone] - Solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección `scheduleParams`, lo que le permite personalizar los tiempos de exportación, la frecuencia, la ubicación y mucho más para las exportaciones de conjuntos de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte Exportar [archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) completos y [Exportar archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) incrementales en los destinos del lote activación tutorial. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede utilizar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones diarias incrementales**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day` y `interval` :`1` para las exportaciones incrementales diarias. <br> **Exportaciones incrementales por hora**: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour` y `interval` :`3`,`6`,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` según la frecuencia con la que desee exportar los archivos del conjunto de datos. |
| `interval` | Seleccione `1` cuando `timeUnit` sea un día y `3`,`6`,`9`,`12` cuando la unidad de tiempo sea `hour`. |
| `startTime` | La fecha y la hora en segundos de UNIX en que deben comenzar las exportaciones de conjuntos de datos. |
| `endTime` | La fecha y la hora en segundos de UNIX en que deben finalizar las exportaciones de conjuntos de datos. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta esperada en la ubicación de almacenamiento en la que se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> = <span>Identificador único del conjunto de datos.</span></li><li><code>DESTINO</code> <span>= El nombre del destino.</span></li><li><code>FECHA y HORA</code> <span>= Fecha y hora con el formato yyyyMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> <span>= La hora programada para la exportación de datos con formato .`exportTime=YYYYMMDDHHMM`</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> <span>= El nombre del instancia específico del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> <span>= Un identificador único para el instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> = <span>Nombre del entorno de espacio aislado.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> = <span>Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}
+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Almacenamiento en la nube de Google]

**Solicitud**

+++Crear flujo de datos del conjunto de datos al destino [!DNL Google Cloud Storage] - Solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Quitar el comentarios en línea en el solicitud al copiar y pegar el solicitud en el terminal de su elección.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección, lo que le permite personalizar los tiempos de exportación, la Frecuencia, la `scheduleParams` ubicación y más para sus exportaciones conjunto de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) en el tutorial de activación de destinos por lotes. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede usar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones** diarias incrementales: Seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, y `interval` :`1` para exportaciones incrementales diarias. <br> **Exportaciones** incrementales por hora: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, y `interval` :`3`,`6`,,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` según la frecuencia con la que desee exportar los archivos del conjunto de datos. |
| `interval` | Seleccione `1` cuando `timeUnit` sea un día y `3`,`6`,`9`,`12` cuando la unidad de tiempo sea `hour`. |
| `startTime` | La fecha y la hora en segundos de UNIX en que deben comenzar las exportaciones de conjuntos de datos. |
| `endTime` | La fecha y la hora en segundos de UNIX en que deben finalizar las exportaciones de conjuntos de datos. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta esperada en la ubicación de almacenamiento en la que se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> = <span>Identificador único del conjunto de datos.</span></li><li><code>DESTINO</code> = <span>Nombre del destino.</span></li><li><code>FECHA Y HORA</code> <span>= Fecha y hora con el formato yyyyMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> <span>= La hora programada para la exportación de datos con formato .`exportTime=YYYYMMDDHHMM`</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> <span>= El nombre del instancia específico del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> <span>= Un identificador único para el instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> <span>= Nombre del entorno del entorno de pruebas.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> = <span>Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}

+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitud**

+++Crear flujo de datos del conjunto de datos al destino SFTP: solicitud

Observe las líneas resaltadas con comentarios en línea en el ejemplo de la solicitud, que proporcionan información adicional. Elimine los comentarios en línea de la solicitud al copiar y pegar la solicitud en el terminal que desee.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

La tabla siguiente proporciona descripciones de todos los parámetros de la sección `scheduleParams`, lo que le permite personalizar los tiempos de exportación, la frecuencia, la ubicación y mucho más para las exportaciones de conjuntos de datos.

| Parámetro | Descripción |
|---------|----------|
| `exportMode` | Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte Exportar [archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) completos y [Exportar archivos](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) incrementales en los destinos del lote activación tutorial. Las tres opciones de exportación disponibles son: <br> **Archivo completo - Una vez**: `"DAILY_FULL_EXPORT"` solo se puede utilizar en combinación con `timeUnit`:`day` y `interval`:`0` para una exportación completa única del conjunto de datos. No se admiten las exportaciones completas diarias de conjuntos de datos. Si necesita exportaciones diarias, utilice la opción de exportación incremental. <br> **Exportaciones** diarias incrementales: Seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`day`, y `interval` :`1` para exportaciones incrementales diarias. <br> **Exportaciones** incrementales por hora: seleccione `"FIRST_FULL_THEN_INCREMENTAL"`, `timeUnit`:`hour`, y `interval` :`3`,`6`,,`9` o `12` para exportaciones incrementales por hora. |
| `timeUnit` | Seleccione `day` o `hour` dependiendo de la Frecuencia con la que desee exportar conjunto de datos archivos. |
| `interval` | Seleccione `1` cuando es `timeUnit` día y `3`,`6`,`9`,`12` cuando la unidad de tiempo es `hour`. |
| `startTime` | La fecha y la hora, en segundos UNIX, en el momento en que conjunto de datos exportaciones deben inicio. |
| `endTime` | La fecha y hora, en segundos UNIX, en la que deben finalizar conjunto de datos exportaciones. |
| `foldernameTemplate` | Especifique la estructura de nombres de carpeta esperada en la ubicación de almacenamiento en la que se depositarán los archivos exportados. <ul><li><code>ID_CONJUNTO_DATOS</code> = <span>Identificador único del conjunto de datos.</span></li><li><code>DESTINO</code> = <span>Nombre del destino.</span></li><li><code>FECHA Y HORA</code> = <span>Fecha y hora con formato aaaaMMdd_HHmmss.</span></li><li><code>TIEMPO_EXPORTACIÓN</code> = <span>Hora programada para la exportación de datos con el formato `exportTime=YYYYMMDDHHMM`.</span></li><li><code>NOMBRE_INSTANCIA_DESTINO</code> <span>= El nombre del instancia específico del destino.</span></li><li><code>DESTINATION_INSTANCE_ID</code> <span>= Un identificador único para el instancia de destino.</span></li><li><code>NOMBRE_DE_ZONA_PROTEGIDA</code> = <span>Nombre del entorno de espacio aislado.</span></li><li><code>NOMBRE_ORGANIZACIÓN</code> = <span>Nombre de la organización.</span></li></ul> |

{style="table-layout:auto"}

+++

**Respuesta**

+++Crear flujo de datos: respuesta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Anote el ID de flujo de datos de la respuesta. Este ID será necesario en el siguiente paso, cuando se ejecute la recuperación del flujo de datos para validar las exportaciones de conjuntos de fechas satisfactorias.

## Obtener las ejecuciones del flujo de datos {#get-dataflow-runs}

![Diagrama que muestra el paso 6 en el flujo de trabajo de exportar conjuntos de datos](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

Para comprobar las ejecuciones de un flujo de datos, utilice la API de ejecuciones de flujo de datos:

>[!BEGINSHADEBOX]

**Solicitud**

+++Obtener ejecuciones de flujo de datos - Solicitud

En la solicitud para recuperar las ejecuciones de flujo de datos, agregue como parámetro de consulta el ID de flujo de datos que obtuvo en el paso anterior, al crear el flujo de datos.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Respuesta**

+++Obtener ejecuciones del flujo de datos: respuesta

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

Puede encontrar información sobre los [diversos parámetros devueltos por el flujo de datos ejecuta la API](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) en la documentación de referencia de la API.

## Verificar exportación correcta del conjunto de datos {#verify}

Al exportar conjuntos de datos, Experience Platform crea un archivo de `.json` o `.parquet` en la ubicación de almacenamiento proporcionada. Espere que se deposite un nuevo archivo en su ubicación de almacenamiento según la programación de exportación que proporcionó al [crear un flujo de datos](#create-dataflow).

Experience Platform crea una estructura de carpetas en la ubicación de almacenamiento especificada, donde deposita los archivos del conjunto de datos exportados. Se crea una nueva carpeta para cada tiempo de exportación, siguiendo el patrón siguiente:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

El nombre de archivo predeterminado se genera de forma aleatoria y garantiza que los nombres de archivo exportados sean únicos.

### Archivos de conjuntos de datos de muestra {#sample-files}

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de una exportación correcta. Para comprender cómo se estructuran los archivos exportados, puede descargar un archivo de muestra [.parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [.json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Archivos de conjunto de datos comprimidos {#compressed-dataset-files}

En el paso para [crear una conexión](#create-target-connection) destino, puede seleccionar los archivos de conjunto de datos exportados que desea comprimir.

Tenga en cuenta la diferencia en el formato de archivo entre los dos tipos de archivo, cuando se comprime:

* Al exportar archivos JSON comprimidos, el formato de archivo exportado se clasifica `json.gz`
* Al exportar archivos parquet comprimidos, el formato de archivo exportado se `gz.parquet`
* Los archivos JSON solo se pueden exportar en modo comprimido.

## Gestión de errores de API {#api-error-handling}

Los extremos de API de este tutorial seguir los principios generales de mensajes de error de API de Experience Platform. Consulte los [códigos](/help/landing/troubleshooting.md#api-status-codes) de estado de API y [los errores](/help/landing/troubleshooting.md#request-header-errors) de encabezado de solicitud en el guía de solución de problemas de Experience Platform para obtener más información sobre la interpretación de las respuestas de error.

## Limitaciones conocidas {#known-limitations}

[Ver limitaciones](/help/destinations/ui/export-datasets.md#known-limitations) conocidas sobre conjunto de datos exportaciones.

## Preguntas frecuentes {#faq}

Ver una [lista de preguntas](/help/destinations/ui/export-datasets.md#faq) frecuentes sobre conjunto de datos exportaciones.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha conectado correctamente Experience Platform a uno de sus lotes preferidos nube destinos almacenamiento y ha configurado un flujo de datos al destino respectivo para exportar conjuntos de datos. Consulte las páginas siguientes para obtener más información, como editar flujos de datos existentes mediante la API de servicio Flujo:

* [Información general sobre los destinos](../home.md)
* [Descripción general del catálogo de destinos](../catalog/overview.md)
* [Actualización de flujos de datos de destino mediante la API de servicio Flujo](../api/update-destination-dataflows.md)