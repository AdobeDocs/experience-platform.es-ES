---
title: Cree una conexión de origen y un flujo de datos para Customer.io mediante la API de servicio de flujo
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Customer.io mediante la API de servicio de flujo.
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 2%

---

# Crear una conexión de origen y un flujo de datos para [!DNL Customer.io] uso de la API de servicio de flujo

>[!NOTE]
>
>La variable [!DNL Customer.io] el origen está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

El siguiente tutorial le guía por los pasos para crear un [!DNL Customer.io] conexión de origen y flujo de datos para traer [[!DNL Customer.io]](https://customer.io/) datos de evento a Adobe Experience Platform mediante la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos {#getting-started}

Esta guía requiere una comprensión práctica de los siguientes componentes del Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, a la vez que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Connect [!DNL Customer.io] a Platform que utiliza la variable [!DNL Flow Service] API {#connect-platform-to-flow-api}

A continuación, se describen los pasos que debe seguir para crear una conexión de origen y un flujo de datos que le lleven a su [!DNL Customer.io] datos de eventos a Experience Platform.

### Crear una conexión de origen {#source-connection}

Cree una conexión de origen realizando una solicitud de POST al [!DNL Flow Service] , mientras proporciona el ID de especificación de conexión de su origen, detalles como nombre y descripción, y el formato de sus datos.

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
| `data.format` | El formato de la variable [!DNL Customer.io] datos que desea ingerir. Actualmente, el único formato de datos admitido es `json`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se contienen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST al [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### Creación de un conjunto de datos de destino {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), que proporciona el ID del esquema de destino dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial en [creación de un conjunto de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda al lago de datos. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos, un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino utilizando la variable [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

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
| `connectionSpec.id` | El ID de especificación de conexión que corresponde al lago de datos. Este ID fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | El formato de la variable [!DNL Customer.io] datos que desea ingerir. |
| `params.dataSetId` | El ID del conjunto de datos de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único de la nueva conexión de destino (`id`). Este ID se requiere en pasos posteriores.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
}
```

### Creación de una asignación {#mapping}

Para que los datos de origen se introduzcan en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiera el conjunto de datos de destino. Esto se logra realizando una solicitud de POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con asignaciones de datos definidas dentro de la carga útil de la solicitud.

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
| `outputSchema.schemaRef.id` | El ID de la variable [esquema XDM de destino](#target-schema) generado en un paso anterior. |
| `mappings.sourceType` | El tipo de atributo de origen que se está asignando. |
| `mappings.source` | El atributo de origen que debe asignarse a una ruta XDM de destino. |
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

### Crear un flujo {#flow}

El último paso para obtener datos de [!DNL Customer.io] a Platform es crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de Target](#target-connection)
* [ID de asignación](#mapping)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

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
| `name` | El nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en el flujo de datos. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este ID fijo es: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Versión correspondiente del ID de especificación de flujo. Este valor se establece de forma predeterminada en `1.0`. |
| `sourceConnectionIds` | La variable [ID de conexión de origen](#source-connection) generado en un paso anterior. |
| `targetConnectionIds` | La variable [ID de conexión de target](#target-connection) generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones que deben aplicarse a los datos. Esta propiedad es necesaria al llevar datos que no sean compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | La variable [ID de asignación](#mapping) generado en un paso anterior. |
| `transformations.params.mappingVersion` | Versión correspondiente del ID de asignación. Este valor se establece de forma predeterminada en `0`. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para supervisar, actualizar o eliminar el flujo de datos.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Obtener la URL del extremo de flujo continuo {#get-streaming-endpoint-url}

Con el flujo de datos creado, ahora puede recuperar la URL del extremo de flujo continuo. Utilizará esta URL de extremo para suscribir su fuente a un weblink, permitiendo que su fuente se comunique con el Experience Platform.

Para recuperar la URL del extremo de flujo continuo, realice una solicitud de GET a la variable `/flows` y proporcione el ID de su flujo de datos.

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

Una respuesta correcta devuelve información sobre su flujo de datos, incluida la dirección URL del extremo, marcada como `inletUrl`. Consulte la [Configuración de Weblock](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) para obtener el valor requerido.

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

La siguiente sección proporciona información sobre los pasos que puede seguir para supervisar, actualizar y eliminar el flujo de datos.

### Monitorizar el flujo de datos {#monitor-dataflow}

Una vez creado el flujo de datos, puede supervisar los datos que se están incorporando a través de él para ver información sobre ejecuciones de flujo, estado de finalización y errores. Para ver ejemplos completos de API, consulte la guía de [monitorización de los flujos de datos de fuentes mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Actualizar el flujo de datos {#update-dataflow}

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH al `/flows` punto final de [!DNL Flow Service] al proporcionar el ID de su flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar la variable única de su flujo de datos `etag` en el `If-Match` encabezado. Para ver ejemplos completos de API, consulte la guía de [actualización de flujos de datos de fuentes mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Actualizar la cuenta {#update-account}

Actualice el nombre, la descripción y las credenciales de la cuenta de origen realizando una solicitud de PATCH al [!DNL Flow Service] al proporcionar su ID de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar la variable única de la cuenta de origen `etag` en el `If-Match` encabezado. Para ver ejemplos completos de API, consulte la guía de [actualizar la cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Eliminar el flujo de datos {#delete-dataflow}

Elimine el flujo de datos realizando una solicitud de DELETE al [!DNL Flow Service] mientras proporciona el ID del flujo de datos que desea eliminar como parte del parámetro de consulta. Para ver ejemplos completos de API, consulte la guía de [eliminación de los flujos de datos mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Eliminar su cuenta {#delete-account}

Elimine la cuenta realizando una solicitud de DELETE al [!DNL Flow Service] mientras proporciona el ID de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de API, consulte la guía de [eliminación de la cuenta de origen mediante la API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).