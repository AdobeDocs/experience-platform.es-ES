---
title: Cree una conexión de origen y un flujo de datos para entidades NetSuite de Oracle mediante la API de Flow Service
description: Aprenda a crear una conexión de origen y un flujo de datos para llevar los contactos de NetSuite de Oracle y los datos de clientes a Experience Platform mediante la API de Flow Service.
hide: true
hidefromtoc: true
badge: Beta
exl-id: ddbb413e-a6ca-49df-b68d-37c9d2aab61b
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 2%

---

# Crear una conexión de origen y un flujo de datos para [!DNL Oracle NetSuite Entities] mediante la API de Flow Service

>[!NOTE]
>
>El origen [!DNL Oracle NetSuite Entities] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea el siguiente tutorial para aprender a traer contactos y datos de clientes de su cuenta de [!DNL Oracle NetSuite Activities Entities] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Oracle NetSuite Entities] mediante la API [!DNL Flow Service].

### Autenticación

Lea la [[!DNL Oracle NetSuite] descripción general](../../../../connectors/marketing-automation/oracle-netsuite.md) para obtener información sobre cómo recuperar sus credenciales de autenticación.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Oracle NetSuite Entities] a la plataforma mediante la API [!DNL Flow Service]

A continuación se describen los pasos que debe seguir para autenticar el origen de [!DNL Oracle NetSuite Entities], crear una conexión de origen y crear un flujo de datos para llevar los datos de contacto y del cliente al Experience Platform.

### Crear una conexión base {#base-connection}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Oracle NetSuite Entities] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Oracle NetSuite Entities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Entities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre de la conexión base sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | El ID de especificación de conexión de su origen. Este identificador se puede recuperar una vez que su origen se haya registrado y aprobado mediante la API [!DNL Flow Service]. |
| `auth.specName` | El tipo de autenticación que utiliza para autenticar el origen en Platform. |
| `auth.params.clientId` | El valor ID de cliente al crear el registro de integración. El proceso para crear un registro de integración se encuentra [aquí](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). El valor es una cadena de 64 caracteres similar a `7fce.....b42f`. |
| `auth.params.clientSecret` | El valor ID de cliente al crear el registro de integración. El proceso para crear un registro de integración se encuentra [aquí](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). El valor es una cadena de 64 caracteres similar a `5c98.....1b46`. |
| `auth.params.accessTokenUrl` | La URL del token de acceso de [!DNL NetSuite], similar a `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token`, donde reemplazará ACCOUNT_ID con el identificador de cuenta de [!DNL NetSuite]. |
| `auth.params.accessToken` | El valor del token de acceso se genera al final del [paso dos](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint) del tutorial [Flujo de concesión de código de autorización de OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow). Los tokens de acceso caducan y solo son válidos durante 60 minutos. el valor es una cadena de 1024 caracteres con formato de token web JSON (JWT) similar a `eyJr......f4V0`. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de origen en el siguiente paso.

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### Explorar su origen {#explore}

Una vez que tenga el identificador de conexión base, ahora puede explorar el contenido y la estructura de los datos de origen realizando una solicitud de GET al extremo `/connections` y proporcionando al mismo tiempo el identificador de conexión base como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Solicitud**

Al realizar solicitudes para explorar la estructura de archivos y el contenido de origen, debe incluir los parámetros de GET que se enumeran en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `objectType=rest` | El tipo de objeto que desea explorar. Actualmente, este valor siempre está establecido en `rest`. |
| `{OBJECT}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. Para este origen el valor sería `json`. |
| `fileType=json` | El tipo de archivo del archivo que desea llevar a Platform. Actualmente, `json` es el único tipo de archivo compatible. |
| `{PREVIEW}` | Un valor booleano que define si el contenido de la conexión admite la vista previa. |
| `{SOURCE_PARAMS}` | Define parámetros para el archivo de origen que desea llevar a Platform. Para recuperar el tipo de formato aceptado para `{SOURCE_PARAMS}`, debe codificar toda la cadena en base64. <br> [!DNL Oracle NetSuite Entities] admite la recuperación de datos de clientes y contactos. Según el tipo de objeto que esté aprovechando, pase uno de los siguientes: <ul><li>`customer` : Recupere datos de clientes específicos, incluidos detalles como nombres de clientes, direcciones e identificadores de claves.</li><li>`contact` : Recupere nombres de contactos, correos electrónicos, números de teléfono y cualquier campo personalizado relacionado con contactos asociado con clientes.</li></ul> |

>[!BEGINTABS]

>[!TAB Cliente]

Para [!DNL Oracle NetSuite Entities], para recuperar datos de contacto, el valor de `{SOURCE_PARAMS}` se pasa como `{"object_type":"customer"}`. Cuando se codifica en base64, equivale a `eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D`, como se muestra a continuación.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB Contacto]

Para [!DNL Oracle NetSuite Entities], para recuperar datos de contacto, el valor de `{SOURCE_PARAMS}` se pasa como `{"object_type":"contact"}`. Cuando se codifica en base64, equivale a `eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9`, como se muestra a continuación.


```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**Respuesta**

Del mismo modo, según el tipo de objeto que aproveche, la respuesta recibida es la siguiente:

>[!NOTE]
>
>Algunos registros se han truncado para permitir una mejor presentación.

>[!BEGINTABS]

>[!TAB Cliente]

Una respuesta correcta devuelve una estructura como se muestra a continuación.

+++Seleccione para ver la carga útil JSON

```json
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "weblead": {
                        "type": "string"
                    },
                    "emailtransactions": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "dateclosed": {
                        "type": "string"
                    },
                    "entitynumber": {
                        "type": "string"
                    },
                    "emailpreference": {
                        "type": "string"
                    },
                    "creditholdoverride": {
                        "type": "string"
                    },
                    "entitystatus": {
                        "type": "string"
                    },
                    "giveaccess": {
                        "type": "string"
                    },
                    "isbudgetapproved": {
                        "type": "string"
                    },
                    "receivablesaccount": {
                        "type": "string"
                    },
                    "shippingcarrier": {
                        "type": "string"
                    },
                    "isperson": {
                        "type": "string"
                    },
                    "balancesearch": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "currency": {
                        "type": "string"
                    },
                    "overduebalancesearch": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "displaysymbol": {
                        "type": "string"
                    },
                    "searchstage": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "oncredithold": {
                        "type": "string"
                    },
                    "probability": {
                        "type": "string"
                    },
                    "faxtransactions": {
                        "type": "string"
                    },
                    "altname": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "printtransactions": {
                        "type": "string"
                    },
                    "alcoholrecipienttype": {
                        "type": "string"
                    },
                    "overridecurrencyformat": {
                        "type": "string"
                    },
                    "companyname": {
                        "type": "string"
                    },
                    "unbilledorderssearch": {
                        "type": "string"
                    },
                    "shipcomplete": {
                        "type": "string"
                    },
                    "symbolplacement": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2022-12-15",
                "datecreated": "2022-12-15",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "4",
                "entitynumber": "4",
                "entitystatus": "13",
                "entitytitle": "4 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "404",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2022-12-15",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-01-19",
                "datecreated": "2023-01-19",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "6",
                "entitynumber": "6",
                "entitystatus": "13",
                "entitytitle": "6 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "605",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-01-19",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-02-01",
                "datecreated": "2023-02-01",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "9",
                "entitynumber": "9",
                "entitystatus": "13",
                "entitytitle": "9 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "710",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-02-01",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
    ]
},
```

+++

>[!TAB Contacto]

Una respuesta correcta devuelve una estructura como se muestra a continuación.

+++Seleccione para ver la carga útil JSON

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "isprivate": {
                        "type": "string"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "company": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe2",
                "entitytitle": "John Doe2",
                "id": "1210",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999998"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe4",
                "entitytitle": "John Doe4",
                "id": "1212",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999996"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe6",
                "entitytitle": "John Doe6",
                "id": "1214",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999994"
            }
        },
    ]
}
```

+++

>[!ENDTABS]

### Crear una conexión de origen {#source-connection}

Puede crear una conexión de origen realizando una solicitud de POST al extremo `/sourceConnections` de la API [!DNL Flow Service]. Una conexión de origen consta de un identificador de conexión, una ruta de acceso al archivo de datos de origen y un identificador de especificación de conexión.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para [!DNL Oracle NetSuite Entities]:

>[!BEGINTABS]

>[!TAB Cliente]

Al recuperar los datos del cliente, el valor de la propiedad `object_type` debe ser `customer`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "customer"        
      }
  }'
```

>[!TAB Contacto]

Al recuperar los datos de contacto, el valor de la propiedad `object_type` debe ser `contact`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "contact"        
      }
  }'
```

>[!ENDTABS]

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | Identificador de conexión base de [!DNL Oracle NetSuite Entities]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | Formato de los datos de [!DNL Oracle NetSuite Entities] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `object_type` | [!DNL Oracle NetSuite Entities] admite la recuperación de clientes y contactos. Dependiendo de la entidad que desee, pase una de las siguientes acciones: <ul><li>`customer` : Recupere datos de clientes específicos, incluidos detalles como nombres de clientes, direcciones e identificadores de claves.</li><li>`contact` : Recupere nombres de contactos, correos electrónicos, números de teléfono y cualquier campo personalizado relacionado con contactos asociado con clientes.</li></ul> |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../../../xdm/api/schemas.md#create-a-schema).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST a la [API de servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), que proporcione el ID del esquema de destino en la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda al lago de datos. Este identificador es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino utilizando la API [!DNL Flow Service] para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para [!DNL Oracle NetSuite Entities]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Target Connection Generic Rest",
      "description": " Oracle NetSuite Entities Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde al lago de datos. Este identificador fijo es: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | Formato de los datos de [!DNL Oracle NetSuite Entities] que desea introducir. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destino. Este ID es necesario en pasos posteriores.

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino. Esto se logra realizando una solicitud de POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con asignaciones de datos definidas dentro de la carga útil de la solicitud.

**Formato de API**

```http
POST /conversion/mappingSets
```

**Solicitud**

La siguiente solicitud crea una asignación para [!DNL DNL NetSuite Entities]

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
            "source": "items.id",
            "destination": "_extconndev.NS_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.entitytitle",
            "destination": "_extconndev.NS_entity_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.datecreated",
            "destination": "_extconndev.NS_datecreated"
        },
        {
            "sourceType": "ATTRIBUTE",
            "destination": "_extconndev.NS_email",
            "source": "items.email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NS_lastmodified"
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
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creación de un flujo {#flow}

El último paso para llevar datos de [!DNL Oracle NetSuite Entities] a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

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
    "name": "Oracle NetSuite Entities connector Flow Generic Rest",
    "description": "Oracle NetSuite Entities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en él. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este identificador fijo es: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | La versión correspondiente del ID de especificación de flujo. El valor predeterminado es `1.0`. |
| `sourceConnectionIds` | [Id. de conexión de origen](#source-connection) generado en un paso anterior. |
| `targetConnectionIds` | [Id. de conexión de destino](#target-connection) generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones necesarias para aplicarse a los datos. Esta propiedad es necesaria al llevar datos no compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | [ID de asignación](#mapping) generado en un paso anterior. |
| `transformations.params.mappingVersion` | La versión correspondiente del ID de asignación. El valor predeterminado es `0`. |
| `scheduleParams.startTime` | Esta propiedad contiene información sobre la programación de la ingesta del flujo de datos. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. |

**Respuesta**

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado. Puede utilizar este ID para monitorizar, actualizar o eliminar el flujo de datos.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## Apéndice

En la siguiente sección se proporciona información sobre los pasos que puede seguir para monitorizar, actualizar y eliminar el flujo de datos.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para ver ejemplos completos de API, lee la guía sobre [supervisión de los flujos de datos de origen mediante la API](../../monitor.md).

### Actualizar el flujo de datos

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH al extremo `/flows` de la API [!DNL Flow Service], proporcionando al mismo tiempo el ID del flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar el `etag` único del flujo de datos en el encabezado `If-Match`. Para ver ejemplos completos de la API, lea la guía sobre [actualización de orígenes y flujos de datos mediante la API](../../update-dataflows.md).

### Actualice su cuenta

Actualice el nombre, la descripción y las credenciales de su cuenta de origen realizando una solicitud de PATCH a la API [!DNL Flow Service] y proporcionando al mismo tiempo el identificador de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar el `etag` único de su cuenta de origen en el encabezado `If-Match`. Para ver ejemplos completos de API, lee la guía de [actualización de tu cuenta de origen mediante la API](../../update.md).

### Eliminar el flujo de datos

Elimine el flujo de datos realizando una solicitud de DELETE a la API [!DNL Flow Service] mientras proporciona el ID del flujo de datos que desea eliminar como parte del parámetro query. Para ver ejemplos completos de API, lea la guía sobre [eliminación de flujos de datos mediante la API](../../delete-dataflows.md).

### Eliminar su cuenta

Elimine la cuenta realizando una solicitud de DELETE a la API [!DNL Flow Service] y proporcionando al mismo tiempo el identificador de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de API, lee la guía sobre [eliminar tu cuenta de origen mediante la API](../../delete.md).
