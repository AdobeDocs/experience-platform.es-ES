---
title: Cree una conexión de origen y un flujo de datos para SAP Commerce mediante la API de Flow Service
description: Aprenda a crear una conexión de origen y un flujo de datos para llevar los datos de SAP Commerce al Experience Platform mediante la API de Flow Service.
badge: Beta
exl-id: 580731b9-0c04-4f83-a475-c1890ac5b7cd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 1%

---

# Crear una conexión de origen y un flujo de datos para [!DNL SAP Commerce] mediante la API de Flow Service

>[!NOTE]
>
>El origen [!DNL SAP Commerce] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

El siguiente tutorial lo acompañará durante los pasos para crear una conexión de origen de [!DNL SAP Commerce] y un flujo de datos para llevar los contactos de [[!DNL SAP] facturación de suscripción](https://www.sap.com/products/financial-management/subscription-billing.html) y los datos de clientes a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL SAP Commerce] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para conectar [!DNL SAP Commerce] al Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `clientId` | El valor de `clientId` de la clave de servicio. |
| `clientSecret` | El valor de `clientSecret` de la clave de servicio. |
| `tokenEndpoint` | El valor de `url` de la clave de servicio será similar a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| `region` | Su ubicación del centro de datos. La región está presente en `url` y tiene un valor similar a `eu10` o `us10`. Por ejemplo, si `url` es `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`, necesitará `eu10`. |

Para obtener más información sobre estas credenciales, consulte la [[!DNL SAP Commerce] documentación](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

## Conectar [!DNL SAP Commerce] a la plataforma mediante la API [!DNL Flow Service]

A continuación se describen los pasos que debe seguir para autenticar el origen de [!DNL SAP Commerce], crear una conexión de origen y crear un flujo de datos para llevar los datos de cuentas y contactos al Experience Platform.

### Crear una conexión base {#base-connection}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL SAP Commerce] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce base connection",
      "description": "Authenticated base connection for SAP Commerce",
      "connectionSpec": {
          "id": "d8ee38de-7ae9-4058-9610-c79ce75f8e92",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "region": "{REGION}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "tokenEndpoint": "{TOKEN_ENDPOINT}"
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
| `auth.params.region` | Su ubicación del centro de datos. La región está presente en `url` y tiene un valor similar a `eu10` o `us10`. Por ejemplo, si `url` es `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`, necesitará `eu10`. |
| `auth.params.clientId` | El valor de `clientId` de la clave de servicio. |
| `auth.params.clientSecret` | El valor de `clientSecret` de la clave de servicio. |
| `auth.params.tokenEndpoint` | El valor de `url` de la clave de servicio será similar a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de origen en el siguiente paso.

```json
{
     "id": "5f6d6022-3f64-400c-ba01-d4010de2d8ff",
     "etag": "\"f8018de1-0000-0200-0000-6482d7210000\""
}
```

### Explorar su origen {#explore}

Una vez que tenga el identificador de conexión base, ahora puede explorar el contenido y la estructura de los datos de origen realizando una solicitud de GET al extremo `/connections` y proporcionando al mismo tiempo el identificador de conexión base como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Al realizar solicitudes para explorar la estructura de archivos y el contenido de origen, debe incluir los parámetros de GET que se enumeran en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `objectType=rest` | El tipo de objeto que desea explorar. Actualmente, este valor siempre está establecido en `rest`. |
| `{OBJECT}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. Para este origen el valor sería `json`. |
| `fileType=json` | El tipo de archivo del archivo que desea llevar a Platform. Actualmente, `json` es el único tipo de archivo compatible. |
| `{PREVIEW}` | Un valor booleano que define si el contenido de la conexión admite la vista previa. |
| `{SOURCE_PARAMS}` | Define parámetros para el archivo de origen que desea llevar a Platform. Para recuperar el tipo de formato aceptado para `{SOURCE_PARAMS}`, debe codificar toda la cadena en base64. <br> [!DNL SAP Commerce] admite varias API. Según el tipo de objeto que esté aprovechando, pase uno de los siguientes: <ul><li>`customers`</li><li>`contacts`</li></ul> |

El origen [!DNL SAP Commerce] admite varias API. Según el tipo de objeto que utilice, la solicitud que se va a enviar es la siguiente:

>[!NOTE]
>
>Algunos registros de respuestas se han truncado para permitir una mejor presentación.

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitud

Para la API de clientes [!DNL SAP Commerce], el valor de `{SOURCE_PARAMS}` se pasa como `{"object_type":"customers"}`. Cuando se codifica en base64, equivale a `eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9`, como se muestra a continuación.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve una estructura JSON como la siguiente:

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "addresses": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "isDefault": {
                            "type": "boolean"
                        },
                        "phone": {
                            "type": "string"
                        },
                        "city": {
                            "type": "string"
                        },
                        "street": {
                            "type": "string"
                        },
                        "postalCode": {
                            "type": "string"
                        },
                        "addressUUID": {
                            "type": "string"
                        },
                        "houseNumber": {
                            "type": "string"
                        },
                        "additionalAddressInfo": {
                            "type": "string"
                        },
                        "state": {
                            "type": "string"
                        },
                        "email": {
                            "type": "string"
                        }
                    }
                }
            },
            "customerNumber": {
                "type": "string"
            },
            "corporateInfo": {
                "type": "object",
                "properties": {}
            },
            "customReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "externalSystemId": {
                            "type": "string"
                        },
                        "externalId": {
                            "type": "string"
                        },
                        "externalIdTypeCode": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "customerType": {
                "type": "string"
            },
            "markets": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "salesArea": {
                            "type": "object",
                            "properties": {
                                "division": {
                                    "type": "string"
                                },
                                "distributionChannel": {
                                    "type": "string"
                                },
                                "salesOrganization": {
                                    "type": "string"
                                }
                            }
                        },
                        "priceType": {
                            "type": "string"
                        },
                        "active": {
                            "type": "boolean"
                        },
                        "currency": {
                            "type": "string"
                        },
                        "marketId": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            },
            "defaultAddress": {
                "type": "object",
                "properties": {
                    "country": {
                        "type": "string"
                    },
                    "isDefault": {
                        "type": "boolean"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "city": {
                        "type": "string"
                    },
                    "street": {
                        "type": "string"
                    },
                    "postalCode": {
                        "type": "string"
                    },
                    "addressUUID": {
                        "type": "string"
                    },
                    "houseNumber": {
                        "type": "string"
                    },
                    "additionalAddressInfo": {
                        "type": "string"
                    },
                    "state": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "addresses": [
                {
                    "email": "user1@test.com",
                    "phone": "123456890",
                    "houseNumber": "123",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                    "isDefault": true
                }
            ],
            "customerNumber": "2863620303",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t090000",
                    "externalId": "1324566",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.499Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedAt": "2023-05-31T06:39:28.499Z",
            "defaultAddress": {
                "email": "user1@test.com",
                "phone": "123456890",
                "houseNumber": "123",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                "isDefault": true
            }
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "addresses": [
                {
                    "email": "user2@test.com",
                    "phone": "1234567899",
                    "houseNumber": "876",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                    "isDefault": true
                }
            ],
            "customerNumber": "6776445404",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t089999",
                    "externalId": "1324565",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.142Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedAt": "2023-05-31T06:39:28.142Z",
            "defaultAddress": {
                "email": "user2@test.com",
                "phone": "1234567899",
                "houseNumber": "876",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                "isDefault": true
            }
        }
    ]
}
```

+++

>[!TAB Contactos]

+++Solicitud

Para la API de contactos de [!DNL SAP Commerce], el valor de `{SOURCE_PARAMS}` se pasa como `{"object_type":"contacts"}`. Cuando se codifica en base64, equivale a `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=`, como se muestra a continuación.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

Una respuesta correcta devuelve una estructura JSON como la siguiente:

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "contactNumber": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "createdAt": "2023-05-31T13:33:52.689Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4365374130",
            "changedAt": "2023-05-31T13:33:52.689Z"
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "createdAt": "2023-05-31T13:33:52.37Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4075431868",
            "changedAt": "2023-05-31T13:33:52.37Z"
        }
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

Según el tipo de objeto que esté aprovechando, seleccione una de las pestañas siguientes:

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitud

La siguiente solicitud crea una conexión de origen para los datos de clientes de [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "customers"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | Identificador de conexión base de [!DNL SAP Commerce]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | Formato de los datos de [!DNL SAP Commerce] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `object_type` | [!DNL SAP Commerce] admite varias API. Para la API de clientes, el parámetro `object_type` debe establecerse en `customers`. |
| `path` | Tendrá el mismo valor que seleccionó para `object_type`. |

+++

+++Respuesta

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!TAB Contactos]

+++Solicitud

La siguiente solicitud crea una conexión de origen para los datos de contactos de [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | Identificador de conexión base de [!DNL SAP Commerce]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | Formato de los datos de [!DNL SAP Commerce] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `object_type` | [!DNL SAP Commerce] admite varias API. Para la API de contactos, el parámetro `object_type` debe establecerse en `contacts`. |
| `path` | Tendrá el mismo valor que seleccionó para *`object_type`*. |

+++

+++Respuesta

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!ENDTABS]

### Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la [API de Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../../../xdm/api/schemas.md#create-a-schema).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST a la [API de servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), que proporcione el ID del esquema de destino en la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

### Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que se van a almacenar los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda al lago de datos. Este identificador es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos de un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino utilizando la API [!DNL Flow Service] para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para [!DNL SAP Commerce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Target Connection Generic Rest",
      "description": "SAP Commerce Target Connection Generic Rest",
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
          "dataSetId": "645923cd7aeeea1c06c5e92e"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde al lago de datos. Este identificador fijo es: `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | Formato de los datos de [!DNL SAP Commerce] que desea introducir. |
| `params.dataSetId` | ID del conjunto de datos de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la nueva conexión de destino. Este ID es necesario en pasos posteriores.

```json
{
    "id": "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c",
    "etag": "\"db00c6dc-0000-0200-0000-6482d8280000\""
}
```

### Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino. Esto se logra realizando una solicitud de POST a [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con asignaciones de datos definidas dentro de la carga útil de la solicitud.

**Formato de API**

```http
POST /conversion/mappingSets
```

>[!BEGINTABS]

>[!TAB Clientes]

+++Solicitud

La siguiente solicitud crea una asignación para los datos de la API de clientes [!DNL SAP Commerce]

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
            "source": "customerNumber",
            "destination": "_extconndev.customerNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerType",
            "destination": "_extconndev.customerType"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].email",
            "destination": "_extconndev.addresses[*].email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].city",
            "destination": "_extconndev.addresses[*].city"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].addressUUID",
            "destination": "_extconndev.addresses[*].addressUUID"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].id",
            "destination": "_extconndev.customReferences[*].id"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].typeCode",
            "destination": "_extconndev.customReferences[*].typeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `outputSchema.schemaRef.id` | El ID del [esquema XDM de destino](#target-schema) generado en un paso anterior. |
| `mappings.sourceType` | El tipo de atributo de origen que se asigna. |
| `mappings.source` | Atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.destination` | Ruta XDM de destino a la que se asigna el atributo de origen. |

+++

+++Respuesta

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

+++

>[!TAB Contactos]

+++Solicitud

La siguiente solicitud crea una asignación para los datos de la API de contactos de [!DNL SAP Commerce]

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
            "source": "contactNumber",
            "destination": "_extconndev.contactNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "createdAt",
            "destination": "_extconndev.createdAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.lastName",
            "destination": "_extconndev.personalInfo.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.firstName",
            "destination": "_extconndev.personalInfo.firstName"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectRefereneces[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/extconndev/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `outputSchema.schemaRef.id` | El ID del [esquema XDM de destino](#target-schema) generado en un paso anterior. |
| `mappings.sourceType` | El tipo de atributo de origen que se asigna. |
| `mappings.source` | Atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.destination` | Ruta XDM de destino a la que se asigna el atributo de origen. |

+++

+++Respuesta

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

+++

>[!ENDTABS]

### Creación de un flujo {#flow}

El último paso para llevar datos de [!DNL SAP Commerce] a Platform es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

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
      "name": "SAP Commerce Connector Description Flow Generic Rest",
      "description": "SAP Commerce Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "2ef2e831-f4f1-4363-a0f7-08b4ea347164"
      ],
      "targetConnectionIds": [
          "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "ddf0592bcc9d4ac391803f15f2429f87",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "once",
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
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
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
