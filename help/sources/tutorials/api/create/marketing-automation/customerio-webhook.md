---
title: Cree una conexión de origen y un flujo de datos para Customer.io mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Customer.io mediante la API de Flow Service.
badge: Beta
exl-id: 1c84d818-428f-4097-9f6f-ef0cf1a04785
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 2%

---

# Crear una conexión de origen y un flujo de datos para [!DNL Customer.io] mediante la API de Flow Service

>[!NOTE]
>
>El origen [!DNL Customer.io] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

El siguiente tutorial lo guiará para crear una conexión de origen y un flujo de datos de [!DNL Customer.io] para llevar los datos del evento [[!DNL Customer.io]](https://customer.io/) a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción {#getting-started}

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Conectar [!DNL Customer.io] a la plataforma mediante la API [!DNL Flow Service] {#connect-platform-to-flow-api}

A continuación se describen los pasos que debe seguir para crear una conexión de origen y un flujo de datos que lleve los datos de eventos de [!DNL Customer.io] al Experience Platform.

### Crear una conexión de origen {#source-connection}

Cree una conexión de origen realizando una solicitud de POST a la API [!DNL Flow Service], al mismo tiempo que proporciona el ID de especificación de conexión de su origen, detalles como el nombre y la descripción y el formato de sus datos.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Customer.io",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for customer.io",
      "connectionSpec": {
          "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
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
| `data.format` | Formato de los datos de [!DNL Customer.io] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST a la [API de servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), que proporcione el ID del esquema de destino en la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda al lago de datos. Este identificador es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino utilizando la API [!DNL Flow Service] para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Customer.io",
      "description": "Streaming Target Connection for Customer.io",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ec807d3f5ce91bd2d06c65"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde al lago de datos. Este identificador fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Formato de los datos de [!DNL Customer.io] que desea introducir. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destino. Este ID es necesario en pasos posteriores.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
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
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.cio_id",
            "sourceAttribute": "data.identifiers.cio_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.email",
            "sourceAttribute": "data.identifiers.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.event_id0",
            "sourceAttribute": "event_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.metricx",
            "sourceAttribute": "metric",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.object_type1",
            "sourceAttribute": "object_type",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestampx",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `outputSchema.schemaRef.id` | El ID del [esquema XDM de destino](#target-schema) generado en un paso anterior. |
| `mappings.sourceType` | El tipo de atributo de origen que se asigna. |
| `mappings.source` | Atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.destination` | Ruta XDM de destino a la que se asigna el atributo de origen. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
    "version": 0,
    "createdDate": 1676627988129,
    "modifiedDate": 1676627988129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creación de un flujo {#flow}

El último paso para llevar datos de [!DNL Customer.io] a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

* [ID de conexión de Source](#source-connection)
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
      "name": "Streaming Dataflow for Customer.io",
      "description": "Streaming Dataflow for Customer.io",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "133bb51f-f310-4b4a-b8b2-731aef1e223c"
      ],
      "targetConnectionIds": [
          "da8b75ad-f6ee-4991-95df-291e62936e98"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
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
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este identificador fijo es: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | La versión correspondiente del ID de especificación de flujo. El valor predeterminado es `1.0`. |
| `sourceConnectionIds` | [Id. de conexión de origen](#source-connection) generado en un paso anterior. |
| `targetConnectionIds` | [Id. de conexión de destino](#target-connection) generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones necesarias para aplicarse a los datos. Esta propiedad es necesaria al llevar datos no compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | [ID de asignación](#mapping) generado en un paso anterior. |
| `transformations.params.mappingVersion` | La versión correspondiente del ID de asignación. El valor predeterminado es `0`. |

**Respuesta**

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado. Puede utilizar este ID para monitorizar, actualizar o eliminar el flujo de datos.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint-url}

Con el flujo de datos creado, ahora puede recuperar la URL del extremo de flujo continuo. Utilizará esta URL de punto de conexión para suscribir su origen a un webhook, lo que permite que su origen se comunique con el Experience Platform.

Para recuperar la dirección URL del extremo de flujo continuo, realice una solicitud de GET al extremo `/flows` y proporcione el ID del flujo de datos.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve información sobre el flujo de datos, incluida la dirección URL del extremo, marcado como `inletUrl`. Consulte la página [Configurar webhook](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) para obtener el valor requerido.

```json
{
    "items": [
        {
            "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "createdAt": 1676629979503,
            "updatedAt": 1676629985390,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Customer.io",
            "description": "Streaming Dataflow for Customer.io",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "etag": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "sourceConnectionIds": [
                "133bb51f-f310-4b4a-b8b2-731aef1e223c"
            ],
            "targetConnectionIds": [
                "da8b75ad-f6ee-4991-95df-291e62936e98"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
                        "connectionSpec": {
                            "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e75dcb5247eb65e7385df30270192e80b145566f52ed74d570505bd2e82463f3"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "providerRefId": "c4726e6f-64b4-4b3b-97e3-f128ace0cc74",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## Apéndice {#appendix}

En la siguiente sección se proporciona información sobre los pasos que puede seguir para monitorizar, actualizar y eliminar el flujo de datos.

### Monitorización del flujo de datos {#monitor-dataflow}

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para ver ejemplos completos de API, lee la guía sobre [supervisión de los flujos de datos de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Actualizar el flujo de datos {#update-dataflow}

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH al extremo `/flows` de la API [!DNL Flow Service], proporcionando al mismo tiempo el ID del flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar el `etag` único del flujo de datos en el encabezado `If-Match`. Para ver ejemplos completos de la API, lea la guía sobre [actualización de flujos de datos de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Actualice su cuenta {#update-account}

Actualice el nombre, la descripción y las credenciales de su cuenta de origen realizando una solicitud de PATCH a la API [!DNL Flow Service] y proporcionando al mismo tiempo el identificador de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar el `etag` único de su cuenta de origen en el encabezado `If-Match`. Para ver ejemplos completos de API, lee la guía de [actualización de tu cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Eliminar el flujo de datos {#delete-dataflow}

Elimine el flujo de datos realizando una solicitud de DELETE a la API [!DNL Flow Service] mientras proporciona el ID del flujo de datos que desea eliminar como parte del parámetro query. Para ver ejemplos completos de API, lea la guía sobre [eliminación de flujos de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Eliminar su cuenta {#delete-account}

Elimine la cuenta realizando una solicitud de DELETE a la API [!DNL Flow Service] y proporcionando al mismo tiempo el identificador de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de API, lee la guía sobre [eliminar tu cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
