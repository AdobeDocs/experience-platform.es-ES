---
title: Cree una conexión de origen y un flujo de datos para los eventos de SugarCRM mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a eventos de Sugar CRM mediante la API de Flow Service.
exl-id: 12d08010-569c-4111-ba95-697c6ce6f637
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2009'
ht-degree: 2%

---

# (Beta) Crear una conexión de origen y un flujo de datos para [!DNL SugarCRM Events] uso de la API de Flow Service

>[!NOTE]
>
>El [!DNL SugarCRM Events] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

El siguiente tutorial le guiará para crear una [!DNL SugarCRM Events] conexión de origen y cree un flujo de datos para [[!DNL SugarCRM]](https://www.sugarcrm.com/) Datos de eventos a Adobe Experience Platform mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL SugarCRM] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para poder conectarse [!DNL SugarCRM Events] En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `host` | El punto final de la API de SugarCRM al que se conecta el origen. | `developer.salesfusion.com` |
| `username` | Su nombre de usuario de cuenta de desarrollador de SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | Contraseña de su cuenta de desarrollador de SugarCRM. | `123456789` |

## Connect [!DNL SugarCRM Events] a Platform mediante el [!DNL Flow Service] API

A continuación se describen los pasos que debe seguir para autenticar su [!DNL SugarCRM] origen, crear una conexión de origen y crear un flujo de datos para llevar los datos de eventos al Experience Platform.

### Crear una conexión base {#base-connection}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL SugarCRM Events] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Events base connection",
      "description": "Create a live inbound connection to your SugarCRM Events instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
          }
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre de la conexión base sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | El ID de especificación de conexión de su origen. Este ID se puede recuperar una vez registrado su origen y aprobado mediante el [!DNL Flow Service] API. |
| `auth.specName` | El tipo de autenticación que utiliza para autenticar el origen en Platform. |
| `auth.params.host` | El host de API de SugarCRM: *developer.salesfusion.com* |
| `auth.params.username` | Su nombre de usuario de cuenta de desarrollador de SugarCRM. |
| `auth.params.password` | Contraseña de su cuenta de desarrollador de SugarCRM. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de origen en el siguiente paso.

```json
{
     "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
     "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### Explorar su origen {#explore}

Con el ID de conexión base que generó en el paso anterior, puede explorar archivos y directorios realizando solicitudes de GET.
Utilice las siguientes llamadas para encontrar la ruta del archivo que desea introducir en [!DNL Platform]:

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Al realizar solicitudes para explorar la estructura de archivos y el contenido de origen, debe incluir los parámetros de GET que se enumeran en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `objectType=rest` | El tipo de objeto que desea explorar. Actualmente, este valor siempre se establece en `rest`. |
| `{OBJECT}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. Para esta fuente el valor sería `json`. |
| `fileType=json` | El tipo de archivo del archivo que desea llevar a Platform. Actualmente, `json` es el único tipo de archivo compatible. |
| `{PREVIEW}` | Un valor booleano que define si el contenido de la conexión admite la vista previa. |
| `{SOURCE_PARAMS}` | Define parámetros para el archivo de origen que desea llevar a Platform. Para recuperar el tipo de formato aceptado para `{SOURCE_PARAMS}`, debe codificar toda la cadena en base64. <br> [!DNL SugarCRM Events] no requiere ninguna carga útil. El valor de `{SOURCE_PARAMS}` se pasa como `{}`, codificado en base64, equivale a `e30=` como se muestra a continuación. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado. *Se han eliminado algunos registros para permitir una mejor presentación.*

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "sessions": {
                        "type": "string"
                    },
                    "description": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "event_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "event": {
                        "type": "string"
                    },
                    "folder_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 1,
                "event": "https://developer.salesfusion.com/api/2.0/events/1/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/1/sessions/",
                "name": "Test",
                "updated_date": "2022-08-30T11:20:11.813Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-08-28T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Draft",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 2,
                "event": "https://developer.salesfusion.com/api/2.0/events/2/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/2/sessions/",
                "name": "Infy Event",
                "description": "Test Event",
                "updated_date": "2022-09-15T16:26:43.697Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-27T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 3,
                "event": "https://developer.salesfusion.com/api/2.0/events/3/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/3/sessions/",
                "name": "Infy Workshop 1",
                "updated_date": "2022-10-11T18:12:28.767Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-14T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        }
    ]
}
```

### Crear una conexión de origen {#source-connection}

Puede crear una conexión de origen realizando una solicitud de POST a [!DNL Flow Service] API. Una conexión de origen consta de un identificador de conexión, una ruta de acceso al archivo de datos de origen y un identificador de especificación de conexión.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión base de [!DNL SugarCRM Events]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | El formato del [!DNL SugarCRM Events] datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "ffac1ae1-c137-4133-9f8d-0279468c11c9",
    "etag": "\"ed05abc3-0000-0200-0000-6368b3280000\""
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

La siguiente solicitud crea una conexión de destino para [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde al lago de datos. Este ID fijo es: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | El formato del [!DNL SugarCRM Events] datos que desea introducir. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único ( ) de la nueva conexión de destino`id`). Este ID es necesario en pasos posteriores.

```json
{
    "id": "dfe9113e-be98-4d63-80a9-f41761721049",
    "etag": "\"84050267-0000-0200-0000-6368b3640000\""
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
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.name",
          "destination": "_extconndev.name_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_extconndev.id_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.sessions",
          "destination": "_extconndev.sessions"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "timestamp"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event",
          "destination": "_extconndev.event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.description",
          "destination": "_extconndev.description"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.folder_id",
          "destination": "_extconndev.folder_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.status",
          "destination": "_extconndev.status"
      }
      ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `outputSchema.schemaRef.id` | El ID del [esquema XDM de destino](#target-schema) se ha generado en un paso anterior. |
| `mappings.sourceType` | El tipo de atributo de origen que se asigna. |
| `mappings.source` | Atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.destination` | Ruta XDM de destino a la que se asigna el atributo de origen. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "d3845beaceeb49669228973f5f937f89",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creación de un flujo {#flow}

El último paso para obtener datos de [!DNL SugarCRM Events] a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de destino](#target-connection)
* [ID de asignación](#mapping)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en un tiempo récord en segundos. A continuación, debe establecer el valor de frecuencia en uno de `hour` o `day`. El valor de intervalo designa el periodo entre dos ingestas consecutivas. El valor de intervalo debe establecerse como `1` o `24` dependiendo de `scheduleParams.frequency` selección de cualquiera `hour` o `day`.

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
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
      ],
      "targetConnectionIds": [
          "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "d3845beaceeb49669228973f5f937f89",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en él. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este ID fijo es: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | La versión correspondiente del ID de especificación de flujo. El valor predeterminado es `1.0`. |
| `sourceConnectionIds` | El [ID de conexión de origen](#source-connection) se ha generado en un paso anterior. |
| `targetConnectionIds` | El [ID de conexión de destino](#target-connection) se ha generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones necesarias para aplicarse a los datos. Esta propiedad es necesaria al llevar datos no compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | El [ID de asignación](#mapping) se ha generado en un paso anterior. |
| `transformations.params.mappingVersion` | La versión correspondiente del ID de asignación. El valor predeterminado es `0`. |
| `scheduleParams.startTime` | Esta propiedad contiene información sobre la programación de la ingesta del flujo de datos. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `hour` o `day`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. El valor de intervalo debe establecerse como `1` o `24` dependiendo de `scheduleParams.frequency` selección de cualquiera `hour` o `day`. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para monitorizar, actualizar o eliminar el flujo de datos.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
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
