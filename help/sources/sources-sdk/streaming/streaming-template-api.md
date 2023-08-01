---
title: Plantilla de autoservicio de documentación para la API del SDK de streaming
description: Aprenda a llevar los datos de flujo continuo de una fuente a Adobe Experience Platform mediante la API de Flow Service.
hide: true
hidefromtoc: true
exl-id: a06384a2-cd99-456d-9f00-babcf3f7b7d9
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 2%

---

# Crear una conexión de origen y un flujo de datos para transmitir *SU ORIGEN* datos con el [!DNL Flow Service] API

*A medida que avanza por esta plantilla, reemplace o elimine todos los párrafos en cursiva (empezando por esta).*

*Comience por actualizar los metadatos (título y descripción) en la parte superior de la página. Ignore todas las instancias de DNL en esta página. Esta es una etiqueta que ayuda a nuestros procesos de traducción automática a traducir correctamente la página a los múltiples idiomas que admitimos. Agregaremos etiquetas a su documentación después de que la envíe.*

## Información general

*Proporcione una breve descripción general de su empresa, incluido el valor que proporciona a los clientes. Incluya un vínculo a la página de inicio de la documentación del producto para obtener más información.*

>[!IMPORTANT]
>
>Este conector de origen y esta página de documentación los crea y mantiene el *SU ORIGEN* equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *Insertar vínculo o dirección de correo electrónico donde se pueda contactar para obtener actualizaciones*.

## Requisitos previos

*Agregue información en esta sección sobre todo lo que los clientes deben tener en cuenta antes de comenzar a configurar el origen en la interfaz de usuario de Adobe Experience Platform. Puede tratarse de lo siguiente:*

* *necesidad de añadirse a una lista de permitidos*
* *requisitos para el hash de correo electrónico*
* *cualquier detalle de la cuenta de su parte*
* *Cómo obtener una clave API para conectarse a la plataforma*

### Recopilar credenciales necesarias

Para poder conectarse *SU FUENTE* para acceder a Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| *credencial uno* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |
| *credencial dos* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |
| *credencial tres* | *Agregue una breve descripción a la credencial de autenticación de su fuente aquí* | *Agregue un ejemplo de la credencial de autenticación de su origen aquí* |

Para obtener más información sobre estas credenciales, consulte la *SU ORIGEN* documentación de autenticación. *Agregue un vínculo a la documentación de autenticación de su plataforma aquí*.

### Integrar *SU ORIGEN* con su webhook

*El SDK de streaming requiere que su fuente admita los webhooks para poder comunicarse con el Experience Platform. En esta sección, debe proporcionar los pasos que los usuarios deberán seguir para integrar YOURSOURCE con un webhook.*

## Connect *SU ORIGEN* a Platform mediante el [!DNL Flow Service] API

El siguiente tutorial le guiará para crear una *SU FUENTE* conexión de origen y cree un flujo de datos para *SU ORIGEN* a Platform mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Crear una conexión de origen {#source-connection}

Cree una conexión de origen realizando una solicitud de POST a [!DNL Flow Service] API, mientras proporciona el ID de especificación de conexión de su origen, detalles como el nombre y la descripción, y el formato de sus datos.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para *SU ORIGEN*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | El formato del *SU FUENTE* datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la variable [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), proporcionando el ID del esquema de destinatario dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial sobre [creación de un conjunto de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino con el [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para *SU ORIGEN*:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde al lago de datos. Este ID fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | El formato del *SU ORIGEN* datos que desee llevar a Platform. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |


**Respuesta**

Una respuesta correcta devuelve el identificador único ( ) de la nueva conexión de destino`id`). Este ID es necesario en pasos posteriores.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino. Esto se logra realizando una solicitud de POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con asignaciones de datos definidas dentro de la carga útil de la solicitud.

**Formato de API**

```http
POST /conversion/mappingSets
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `xdmSchema` | El ID del [esquema XDM de destino](#target-schema) se ha generado en un paso anterior. |
| `mappings.destinationXdmPath` | Ruta XDM de destino a la que se asigna el atributo de origen. |
| `mappings.sourceAttribute` | Atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.identity` | Un valor booleano que designa si el conjunto de asignaciones se marcará para [!DNL Identity Service]. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creación de un flujo {#flow}

El último paso para obtener datos de *SU ORIGEN* a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de destino](#target-connection)
* [ID de asignación](#mapping)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en él. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este ID fijo es: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | La versión correspondiente del ID de especificación de flujo. El valor predeterminado es `1.0`. |
| `sourceConnectionIds` | El [ID de conexión de origen](#source-connection) se ha generado en un paso anterior. |
| `targetConnectionIds` | El [ID de conexión de destino](#target-connection) se ha generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones necesarias para aplicarse a los datos. Esta propiedad es necesaria al llevar datos no compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | El [ID de asignación](#mapping) se ha generado en un paso anterior. |
| `transformations.params.mappingVersion` | La versión correspondiente del ID de asignación. El valor predeterminado es `0`. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para monitorizar, actualizar o eliminar el flujo de datos.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Obtener la URL del extremo de flujo continuo

Con el flujo de datos creado, ahora puede recuperar la URL del extremo de flujo continuo. Utilizará esta URL de punto de conexión para suscribir su origen a un webhook, lo que permite que su origen se comunique con el Experience Platform.

Para recuperar la URL de extremo de flujo continuo, realice una solicitud de GET a la `/flows` y proporcione el ID del flujo de datos.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve información sobre el flujo de datos, incluida la dirección URL del punto de conexión, marcada como `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## Apéndice

En la siguiente sección se proporciona información sobre los pasos que puede seguir para monitorizar, actualizar y eliminar el flujo de datos.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para ver ejemplos completos de la API, lea la guía de [monitorización de los flujos de datos de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Actualizar el flujo de datos

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH a `/flows` punto final de [!DNL Flow Service] API, mientras proporciona el ID del flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar la variable única del flujo de datos `etag` en el `If-Match` encabezado. Para ver ejemplos completos de la API, lea la guía de [actualización de flujos de datos de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Actualice su cuenta

Actualice el nombre, la descripción y las credenciales de la cuenta de origen realizando una solicitud al PATCH de [!DNL Flow Service] al proporcionar su ID de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar la cuenta de origen única `etag` en el `If-Match` encabezado. Para ver ejemplos completos de la API, lea la guía de [actualización de la cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Eliminar el flujo de datos

Elimine el flujo de datos realizando una solicitud de DELETE a [!DNL Flow Service] API al proporcionar el ID del flujo de datos que desea eliminar como parte del parámetro de consulta. Para ver ejemplos completos de la API, lea la guía de [eliminación de flujos de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Eliminar su cuenta

Elimine la cuenta realizando una solicitud de DELETE a [!DNL Flow Service] al proporcionar el ID de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de la API, lea la guía de [Eliminar la cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
