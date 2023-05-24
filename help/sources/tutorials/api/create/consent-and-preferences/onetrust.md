---
keywords: Experience Platform;inicio;temas populares;OneTrust
solution: Experience Platform
title: Crear un flujo de datos para una fuente de integración de OneTrust mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a la integración de OneTrust mediante la API de Flow Service.
exl-id: e224efe0-4756-4b8a-b446-a3e1066f2050
source-git-commit: 9846dc24321d7b32a110cfda9df3511b1e3a82ed
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 2%

---

# Creación de un flujo de datos para una [!DNL OneTrust Integration] origen mediante el [!DNL Flow Service] API

>[!NOTE]
>
>El [!DNL OneTrust Integration] La fuente solo admite la ingesta de datos de consentimiento y preferencias, y no cookies.

El siguiente tutorial le guiará por los pasos para crear una conexión de origen y un flujo de datos para importar datos de consentimiento históricos y programados de [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) a Adobe Experience Platform mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Requisitos previos

>[!IMPORTANT]
>
>El [!DNL OneTrust Integration] el conector de origen y la documentación fueron creados por el [!DNL OneTrust Integration] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con el [[!DNL OneTrust] equipo](https://my.onetrust.com/s/contactsupport?language=en_US) directamente.

Antes de conectarse [!DNL OneTrust Integration] En Platform, primero debe recuperar el token de acceso. Para obtener instrucciones detalladas sobre cómo encontrar el token de acceso, consulte la [[!DNL OneTrust Integration] Guía de OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

El token de acceso no se actualiza automáticamente una vez caducado porque no admite tokens de actualización de sistema a sistema [!DNL OneTrust]. Por lo tanto, es necesario asegurarse de que el token de acceso se actualice en la conexión antes de que caduque. La duración máxima configurable de un token de acceso es de un año. Para obtener más información sobre cómo actualizar el token de acceso, consulte la [[!DNL OneTrust] documento sobre la administración de las credenciales del cliente de OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

## Connect [!DNL OneTrust Integration] a Platform mediante el [!DNL Flow Service] API

>[!NOTE]
>
>El [!DNL OneTrust Integration] Las especificaciones de la API se comparten con el Adobe para la ingesta de datos.

El siguiente tutorial le guiará para crear una [!DNL OneTrust Integration] conexión de origen y cree un flujo de datos para [!DNL OneTrust Integration] a Platform mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Crear una conexión base {#base-connection}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL OneTrust Integration] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST base connection",
      "description": "ONETRUST base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "accessToken": "{ACCESS_TOKEN}"
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
| `auth.params.` | Contiene las credenciales necesarias para autenticar el origen, incluido el token de acceso para conectarse a la API. |
| `auth.params.accessToken` | El token de acceso que corresponde a su [!DNL OneTrust Integration] cuenta. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de origen en el siguiente paso.

```json
{
     "id": "622124ca-6d18-47f7-999c-66f599955309",
     "etag": "\"2e026443-0000-0200-0000-621f1af80000\""
}
```

### Explorar su origen {#explore}

Con el ID de conexión base que generó en el paso anterior, puede explorar archivos y directorios realizando solicitudes de GET.

Utilice las siguientes llamadas para encontrar la ruta del archivo que desea introducir en [!DNL Platform]:

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

Al realizar solicitudes para explorar la estructura de archivos y el contenido de origen, debe incluir los parámetros de GET que se enumeran en la tabla siguiente:


| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `objectType=rest` | El tipo de objeto que desea explorar. Actualmente, este valor siempre se establece en `rest`. |
| `{OBJECT}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |
| `fileType=json` | El tipo de archivo del archivo que desea llevar a Platform. Actualmente, `json` es el único tipo de archivo compatible. |
| `{PREVIEW}` | Un valor booleano que define si el contenido de la conexión admite la vista previa. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/622124ca-6d18-47f7-999c-66f599955309/explore?objectType=rest&object=json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado.

>[!NOTE]
>
>La carga útil de respuesta JSON a continuación está oculta para la brevedad. Seleccione Haga clic para ver la carga útil de respuesta.

+++Haga clic aquí

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "numberOfElements": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "last": {
                "type": "boolean"
            },
            "pageable": {
                "type": "object",
                "properties": {
                    "paged": {
                        "type": "boolean"
                    },
                    "pageNumber": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "offset": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "tokenId": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "limit": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "pageSize": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "unpaged": {
                        "type": "boolean"
                    },
                    "sort": {
                        "type": "object",
                        "properties": {
                            "unsorted": {
                                "type": "boolean"
                            },
                            "sorted": {
                                "type": "boolean"
                            },
                            "empty": {
                                "type": "boolean"
                            }
                        }
                    }
                }
            },
            "sort": {
                "type": "object",
                "properties": {
                    "unsorted": {
                        "type": "boolean"
                    },
                    "sorted": {
                        "type": "boolean"
                    },
                    "empty": {
                        "type": "boolean"
                    }
                }
            },
            "content": {
                "type": "object",
                "properties": {
                    "LastUpdatedDate": {
                        "type": "string"
                    },
                    "Identifier": {
                        "type": "string"
                    },
                    "Language": {
                        "type": "string"
                    },
                    "TestDataSubject": {
                        "type": "boolean"
                    },
                    "CreatedDate": {
                        "type": "string"
                    },
                    "DataElements": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "Id": {
                        "type": "string"
                    },
                    "Purposes": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "Status": {
                                    "type": "string"
                                },
                                "LastTransactionDate": {
                                    "type": "string"
                                },
                                "CustomPreferences": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {}
                                    }
                                },
                                "LastUpdatedDate": {},
                                "ExpiryDate": {},
                                "Topics": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {
                                            "IsConsented": {
                                                "type": "boolean"
                                            },
                                            "Id": {
                                                "type": "string"
                                            },
                                            "Name": {
                                                "type": "string"
                                            }
                                        }
                                    }
                                },
                                "TotalTransactionCount": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "LastReceiptId": {},
                                "ConsentDate": {
                                    "type": "string"
                                },
                                "LastInteractionDate": {},
                                "Name": {
                                    "type": "string"
                                },
                                "FirstTransactionDate": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointId": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointVersion": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "Version": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "attributes": {
                                    "type": "object",
                                    "properties": {}
                                },
                                "Id": {
                                    "type": "string"
                                },
                                "PurposeNote": {},
                                "WithdrawalDate": {
                                    "type": "string"
                                }
                            }
                        }
                    }
                }
            },
            "first": {
                "type": "boolean"
            },
            "empty": {
                "type": "boolean"
            }
        }
    },
    "data": [
        {
            "number": 0,
            "size": 100,
            "numberOfElements": 100,
            "last": false,
            "pageable": {
                "limit": 100,
                "offset": 0,
                "sort": {
                    "sorted": true,
                    "unsorted": false,
                    "empty": false
                },
                "tokenId": 100,
                "pageSize": 100,
                "pageNumber": 0,
                "unpaged": false,
                "paged": true
            },
            "sort": {
                "sorted": true,
                "unsorted": false,
                "empty": false
            },
            "content": {
                "Id": "de1ab4d2-6ccf-42bd-b363-2d8cac60c88c",
                "Language": "en-us",
                "Identifier": "gkumar@onetrust.com",
                "LastUpdatedDate": "2019-06-05T12:02:07Z",
                "CreatedDate": "2018-05-02T03:14:28Z",
                "Purposes": [
                    {
                        "Id": "9edf57bb-0449-4c15-98e4-8641522e5ff4",
                        "Name": "Purpose_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:14:27Z",
                        "LastTransactionDate": "2019-05-29T11:08:26Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2018-05-02T03:14:27Z",
                        "TotalTransactionCount": 5,
                        "Topics": [
                            {
                                "Id": "d6e3d675-3d6f-4f4e-a157-bd93829ee632",
                                "Name": "Topic_UAT",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "814c073a-95f1-4fc9-8263-1ec62225c5e9",
                        "Name": "Multi Pur_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:17:33Z",
                        "LastTransactionDate": "2018-05-02T03:19:49Z",
                        "ConsentDate": "2018-05-02T03:17:33Z",
                        "TotalTransactionCount": 4,
                        "LastTransactionCollectionPointId": "9a5b7375-bc13-47e8-8a58-1ca7d9c06c8e",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4d52dcc4-82bf-44bf-ac49-854eba6ff8f3",
                        "Name": "Eloqua_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:26:36Z",
                        "LastTransactionDate": "2019-03-07T03:23:25Z",
                        "ConsentDate": "2018-05-02T03:26:36Z",
                        "TotalTransactionCount": 3,
                        "Topics": [
                            {
                                "Id": "690ad782-6280-4ea4-b62a-1514c39fc838",
                                "Name": "Eloqua_topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "723300e3-96cb-4da4-abdd-4913c05be215",
                        "Name": "Purpose 1",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-02-27T06:29:48Z",
                        "LastTransactionDate": "2019-02-28T12:00:45Z",
                        "ConsentDate": "2019-02-27T06:29:48Z",
                        "ExpiryDate": "2019-02-28T12:00:45Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "3dbfb978-10f9-44a9-9669-d699674edd9d",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4a5e6278-17f1-4283-beee-29f81cde2bd0",
                        "Name": "kbpurpose1",
                        "Version": 1,
                        "Status": "NO_CONSENT",
                        "FirstTransactionDate": "2019-03-07T03:21:58Z",
                        "LastTransactionDate": "2019-05-29T03:56:37Z",
                        "TotalTransactionCount": 6,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a36f98d0-c662-4f61-a2a1-8bdab69e3c3a",
                        "Name": "Pur 1",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:23:25Z",
                        "LastTransactionDate": "2019-03-07T03:23:27Z",
                        "ConsentDate": "2019-03-07T03:23:25Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "41ebdf32-068b-4239-89ac-42e20262c5a9",
                        "Name": "Send Notifications about Changes to Preferences",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:24:11Z",
                        "LastTransactionDate": "2019-03-07T03:27:29Z",
                        "ConsentDate": "2019-03-07T03:24:11Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "759d8b24-e4c0-4107-86e2-3a408db13e6b",
                        "Name": "GJ Purpose 07",
                        "Version": 2,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-07T03:27:29Z",
                        "LastTransactionDate": "2019-05-29T11:09:03Z",
                        "WithdrawalDate": "2019-05-29T11:09:03Z",
                        "ConsentDate": "2019-03-07T03:27:29Z",
                        "TotalTransactionCount": 18,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a57ee9da-b494-49e2-b562-6dfa31f190df",
                        "Name": "kbpurpose2",
                        "Version": 1,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-28T03:23:44Z",
                        "LastTransactionDate": "2019-03-28T03:24:29Z",
                        "WithdrawalDate": "2019-03-28T03:24:29Z",
                        "ConsentDate": "2019-03-28T03:23:44Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a1ccd810-94a0-4b58-946b-6705eae15c5b",
                        "Name": "Purpose01 v2",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-06-05T12:02:06Z",
                        "WithdrawalDate": "2019-05-29T11:09:12Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "ExpiryDate": "2019-06-05T12:02:06Z",
                        "TotalTransactionCount": 8,
                        "Topics": [
                            {
                                "Id": "af7bf604-2058-4089-985c-c84083e3e3e3",
                                "Name": "New_Topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a313353a-e13b-4554-be08-22cf4a78a31c",
                        "Name": "Purpose_1804 v2",
                        "Version": 2,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-05-29T11:09:30Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "TotalTransactionCount": 4,
                        "CustomPreferences": [
                            {
                                "Id": "4935d35a-7216-480d-9da9-1aef0e078b89",
                                "Name": "Custom_S",
                                "Options": [
                                    {
                                        "Id": "8acc2f9f-37f8-4ace-a513-fae6b7dd0aa9",
                                        "Name": "Option2",
                                        "IsConsented": true
                                    }
                                ]
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    }
                ],
                "TestDataSubject": false
            },
            "first": true,
            "empty": false
        }
    ]
}
```

+++

### Crear una conexión de origen {#source-connection}

Puede crear una conexión de origen realizando una solicitud de POST a [!DNL Flow Service] API. Una conexión de origen consta de un identificador de conexión, una ruta de acceso al archivo de datos de origen y un identificador de especificación de conexión.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Source Connection",
      "description": "ONETRUST Source Connection",
      "baseConnectionId": "622124ca-6d18-47f7-999c-66f599955309",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {}
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión base de [!DNL OneTrust Integration]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | El formato del [!DNL OneTrust Integration] datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
     "id": "eb5833d3-230d-4700-80cc-bda396e7af8a",
     "etag": "\"da04c07f-0000-0200-0000-621f1afc0000\""
}
```

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la variable [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../../../xdm/api/schemas.md).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), proporcionando el ID del esquema de destinatario dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial sobre [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda a la [!DNL Data Lake]. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión a [!DNL Data Lake]. Con estos identificadores, puede crear una conexión de destino con el [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Target Connection",
      "description": "ONETRUST Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "dataSetId": "61f6ca3f33978c19486bb463"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | Id. de especificación de conexión correspondiente a [!DNL Data Lake]. Este ID fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | El formato del [!DNL OneTrust Integration] datos que desee llevar a Platform. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |


**Respuesta**

Una respuesta correcta devuelve el identificador único ( ) de la nueva conexión de destino`id`). Este ID es necesario en pasos posteriores.

```json
{
     "id": "495f761f-310a-4a7b-ae78-5b1152d74b38",
     "etag": "\"410a7b0c-0000-0200-0000-621f1afd0000\""
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
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/cfc8cee182e546c1fb35071185524b465e06bf1acb74f30d",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [{
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_id",
              "name": "id",
              "description": "Identifier field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_exchangesandboxbravo.Identifier"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Language",
              "destination": "_exchangesandboxbravo.Language",
              "description": "Language field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.CreatedDate",
              "destination": "_exchangesandboxbravo.CreatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.LastUpdatedDate",
              "destination": "_exchangesandboxbravo.LastUpdatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.DataElements",
              "destination": "_exchangesandboxbravo.DataElements"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Purposes",
              "destination": "_exchangesandboxbravo.Purposes"
          }

      ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `xdmSchema` | El ID del [esquema XDM de destino](#target-schema) se ha generado en un paso anterior. |
| `mappings.destinationXdmPath` | Ruta XDM de destino a la que se asigna el atributo de origen. |
| `mappings.sourceAttribute` | Atributo de origen que debe asignarse a una ruta XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "a87f130e82f04d5188da01f087805c4b",
    "version": 0,
    "createdDate": 1646205694395,
    "modifiedDate": 1646205694395,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Creación de un flujo {#flow}

El último paso para obtener datos de [!DNL OneTrust Integration] a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de destino](#target-connection)
* [ID de asignación](#mapping)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en un tiempo récord en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day`, o `week`. El valor de intervalo designa el periodo entre dos ingestas consecutivas; sin embargo, la creación de una ingesta única no requiere que se establezca un intervalo. Para las demás frecuencias, el valor del intervalo debe ser igual o bueno que `15`.

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
      "name": "ONETRUST dataflow",
      "description": "ONETRUST dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "eb5833d3-230d-4700-80cc-bda396e7af8a"
      ],
      "targetConnectionIds": [
          "495f761f-310a-4a7b-ae78-5b1152d74b38"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "a87f130e82f04d5188da01f087805c4b",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "minute",
          "interval": 15
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
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day`, o `week`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. El intervalo no es obligatorio cuando la frecuencia está establecida como `once` y debe ser bueno o igual a `15` para otros valores de frecuencia. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para monitorizar, actualizar o eliminar el flujo de datos.

```json
{
     "id": "70045189-42f0-493d-9b9e-be1045a9f4fa",
     "etag": "\"1601e900-0000-0200-0000-621f1b080000\""
}
```

## Apéndice

En la siguiente sección se proporciona información sobre los pasos que puede seguir para monitorizar, actualizar y eliminar el flujo de datos.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para ver ejemplos completos de la API, lea la guía de [monitorización de los flujos de datos de origen mediante la API](../../monitor.md).

### Actualizar el flujo de datos

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH a `/flows` punto final de [!DNL Flow Service] API, mientras proporciona el ID del flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar la variable única del flujo de datos `etag` en el `If-Match` encabezado. Para ver ejemplos completos de la API, lea la guía de [actualización de flujos de datos de origen mediante la API](../../update-dataflows.md).

### Actualice su cuenta

Actualice el nombre, la descripción y las credenciales de la cuenta de origen realizando una solicitud al PATCH de [!DNL Flow Service] al proporcionar su ID de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar la cuenta de origen única `etag` en el `If-Match` encabezado. Para ver ejemplos completos de la API, lea la guía de [actualización de la cuenta de origen mediante la API](../../update.md).

### Eliminar el flujo de datos

Elimine el flujo de datos realizando una solicitud de DELETE a [!DNL Flow Service] API al proporcionar el ID del flujo de datos que desea eliminar como parte del parámetro de consulta. Para ver ejemplos completos de la API, lea la guía de [eliminación de flujos de datos mediante la API](../../delete-dataflows.md).

### Eliminar su cuenta

Elimine la cuenta realizando una solicitud de DELETE a [!DNL Flow Service] al proporcionar el ID de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de la API, lea la guía de [Eliminar la cuenta de origen mediante la API](../../delete.md).