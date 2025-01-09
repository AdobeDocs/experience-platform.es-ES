---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Punto final de API de entidades (acceso a perfil)
type: Documentation
description: Adobe Experience Platform le permite acceder a los datos del perfil del cliente en tiempo real mediante las API de RESTful o la interfaz de usuario de. Esta guía describe cómo acceder a las entidades, más comúnmente conocidas como "perfiles", mediante la API de perfil.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 9f9823a23c488e63b8b938cb885f050849836e36
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 4%

---

# Extremo de entidades (acceso a perfiles)

Adobe Experience Platform le permite acceder a los datos de [!DNL Real-Time Customer Profile] mediante las API RESTful o la interfaz de usuario de. Esta guía describe cómo acceder a las entidades, más comúnmente conocidas como &quot;perfiles&quot;, mediante la API. Para obtener más información sobre el acceso a los perfiles mediante la interfaz de usuario de [!DNL Platform], consulte la [Guía del usuario del perfil](../ui/user-guide.md).

## Introducción

El extremo de API utilizado en esta guía forma parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, revisa la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de [!DNL Experience Platform].

## Recuperación de una entidad {#retrieve-entity}

Puede recuperar una entidad de perfil o sus datos de serie temporal realizando una solicitud de GET al extremo `/access/entities` junto con los parámetros de consulta necesarios.

>[!BEGINTABS]

>[!TAB Entidad de perfil]

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;).

Para tener acceso a una entidad de perfil, **debe** proporcionar los siguientes parámetros de consulta:

- `schema.name`: nombre del esquema XDM de la entidad. En este caso de uso, `schema.name=_xdm.context.profile`.
- `entityId`: ID de la entidad que intenta recuperar.
- `entityIdNS`: área de nombres de la entidad que intenta recuperar. Se debe proporcionar este valor si `entityId` es **no** un XID.

Se proporciona una lista completa de parámetros válidos en la sección [parámetros de consulta](#query-parameters) del apéndice.

**Solicitud**

La siguiente solicitud recupera el correo electrónico y el nombre de un cliente mediante una identidad.

+++ Una solicitud de ejemplo para recuperar una entidad mediante una identidad

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con la entidad solicitada.

+++ Una respuesta de ejemplo que contiene la entidad solicitada

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "johnsmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

+++

>[!NOTE]
>
>Si un gráfico relacionado vincula más de 50 identidades, este servicio devolverá el estado HTTP 422 y el mensaje &quot;Demasiadas identidades relacionadas&quot;. Si recibe este error, considere la posibilidad de agregar más parámetros de consulta para restringir la búsqueda.

>[!TAB Evento de serie temporal]

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;).

Para tener acceso a los datos de eventos de series temporales, **debe** proporcionar los siguientes parámetros de consulta:

- `schema.name`: nombre del esquema XDM de la entidad. En este caso de uso, este valor es `schema.name=_xdm.context.experienceevent`.
- `relatedSchema.name`: nombre del esquema relacionado. Dado que el nombre de esquema es Evento de experiencia, el valor de este **debe** ser `relatedSchema.name=_xdm.context.profile`.
- `relatedEntityId`: ID de la entidad relacionada.
- `relatedEntityIdNS`: área de nombres de la entidad relacionada. Se debe proporcionar este valor si `relatedEntityId` es **no** un XID.

Se proporciona una lista completa de parámetros válidos en la sección [parámetros de consulta](#query-parameters) del apéndice.

**Solicitud**

La siguiente solicitud encuentra una entidad de perfil por identificador y recupera los valores de las propiedades `endUserIDs`, `web` y `channel` para todos los eventos de series temporales asociados a la entidad.

+++ Una solicitud de ejemplo para recuperar los eventos de series temporales asociados a una entidad

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista paginada de eventos de series temporales y campos asociados especificados en los parámetros de consulta de solicitud.

>[!NOTE]
>
>La solicitud especificó un límite de uno (`limit=1`), por lo tanto `count` en la respuesta siguiente es 1 y solo se devuelve una entidad.

+++ Una respuesta de ejemplo que contiene los datos de eventos de series temporales solicitados

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

+++

>[!TAB Cuenta B2B]

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;).

Para acceder a los datos de la cuenta B2B, **debe** proporcionar los siguientes parámetros de consulta:

- `schema.name`: nombre del esquema XDM de la entidad. En este caso de uso, este valor es `schema.name=_xdm.context.account`.
- `entityId`: ID de la entidad que intenta recuperar.
- `entityIdNS`: área de nombres de la entidad que intenta recuperar. Se debe proporcionar este valor si `entityId` es **no** un XID.

Se proporciona una lista completa de parámetros válidos en la sección [parámetros de consulta](#query-parameters) del apéndice.

**Solicitud**

+++ Una solicitud de ejemplo para recuperar una cuenta B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con la entidad solicitada.

+++ Una respuesta de ejemplo que contiene la entidad solicitada

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB Oportunidad B2B]

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;).

Para acceder a una entidad de oportunidad B2B, **debe** proporcionar los siguientes parámetros de consulta:

- `schema.name`: nombre del esquema XDM de la entidad. En este caso de uso, `schema.name=_xdm.context.opportunity`.
- `entityId`: ID de la entidad que intenta recuperar.
- `entityIdNS`: área de nombres de la entidad que intenta recuperar. Se debe proporcionar este valor si `entityId` es **no** un XID.

Se proporciona una lista completa de parámetros válidos en la sección [parámetros de consulta](#query-parameters) del apéndice.

**Solicitud**

+++ Una solicitud de muestra para recuperar una entidad de oportunidad B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con la entidad solicitada.

+++ Una respuesta de ejemplo que contiene la entidad solicitada

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Recuperar varias entidades {#retrieve-entities}

Puede recuperar varias entidades de perfil o eventos de series temporales realizando una solicitud de POST al extremo `/access/entities` y proporcionando las identidades en la carga útil.

>[!BEGINTABS]

>[!TAB Entidades de perfil]

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera los nombres y direcciones de correo electrónico de varios clientes mediante una lista de identidades.

+++Una solicitud de ejemplo para recuperar varias entidades.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp"
      }'
```

| Propiedad | Tipo | Descripción |
| -------- |----- | ----------- |
| `schema.name` | Cadena | **(Obligatorio)** El nombre del esquema XDM al que pertenece la entidad. |
| `fields` | Matriz | Los campos XDM que se van a devolver, como una matriz de cadenas. De forma predeterminada, se devuelven todos los campos. |
| `identities` | Matriz | **(Obligatorio)** Una matriz que contiene una lista de identidades para las entidades a las que desea tener acceso. |
| `identities.entityId` | Cadena | El ID de una entidad a la que desea acceder. |
| `identities.entityIdNS.code` | Cadena | El área de nombres de un ID de entidad al que desea acceder. |
| `timeFilter.startTime` | Entero | Especifica la hora de inicio del filtro de entidades de perfil (en milisegundos). De forma predeterminada, este valor se establece como el principio del tiempo disponible. |
| `timeFilter.endTime` | Entero | Especifica la hora de finalización para filtrar entidades de perfil (en milisegundos). De forma predeterminada, este valor se establece como el final del tiempo disponible. |
| `limit` | Entero | Número máximo de registros que se van a devolver. De forma predeterminada, este valor se establece en 1000. |
| `orderby` | Cadena | Orden de los eventos de experiencia recuperados por marca de tiempo, escritos como `(+/-)timestamp` con el valor predeterminado `+timestamp`. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los campos solicitados de entidades especificadas en el cuerpo de la solicitud.

+++ Una respuesta de ejemplo que contiene las entidades solicitadas

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

+++

>[!TAB Eventos de series temporales]

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera los ID de usuario, las horas locales y los códigos de país de los eventos de series temporales asociados a una lista de identidades de perfil.

+++ Una solicitud de ejemplo para recuperar los datos de la serie temporal

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10,
    "orderby": "-timestamp"
}'
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `schema.name` | Cadena | **(Obligatorio)** El nombre del esquema XDM al que pertenece la entidad. |
| `relatedSchema.name` | Cadena | Si `schema.name` es `_xdm.context.experienceevent`, este valor debe especificar el esquema para la entidad de perfil con la que están relacionados los eventos de series temporales. |
| `identities` | Matriz | **(Obligatorio)** Una matriz con una lista de perfiles desde los que recuperar los eventos de series temporales asociados. Cada entrada de la matriz se establece de una de las dos maneras siguientes: <ol><li>Uso de una identidad completa formada por el valor de ID y el área de nombres</li><li>Proporcionar un XID</li></ol> |
| `fields` | Cadena | Los campos XDM que se van a devolver, como una matriz de cadenas. De forma predeterminada, se devuelven todos los campos. |
| `orderby` | Cadena | Orden de los eventos de experiencia recuperados por marca de tiempo, escritos como `(+/-)timestamp` con el valor predeterminado `+timestamp`. |
| `timeFilter.startTime` | Entero | Especifique la hora de inicio para filtrar los objetos de series temporales (en milisegundos). De forma predeterminada, este valor se establece como el principio del tiempo disponible. |
| `timeFilter.endTime` | Entero | Especifique la hora de finalización para filtrar los objetos de series temporales (en milisegundos). De forma predeterminada, este valor se establece como el final del tiempo disponible. |
| `limit` | Entero | Número máximo de registros que se van a devolver. De forma predeterminada, este valor se establece en 1000. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista paginada de eventos de series temporales asociados con varios perfiles especificados en la solicitud.

+++ Una respuesta de ejemplo que contiene los eventos de series temporales

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

+++

>[!NOTE]
>
>En esta respuesta de ejemplo, el primer perfil enumerado (&quot;GkouAW-yD9aoRCPhRYROJ-TestAFW&quot;) proporciona un valor para `_links.next.payload`, lo que significa que hay páginas de resultados adicionales para este perfil.
>
>Para acceder a estos resultados, puede realizar una solicitud de POST adicional al extremo `/access/entities` con la carga útil indicada como cuerpo de la solicitud.

>[!TAB Cuenta B2B]

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera las cuentas B2B solicitadas.

+++Una solicitud de ejemplo para recuperar varias entidades.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Propiedad | Tipo | Descripción |
| -------- |----- | ----------- |
| `schema.name` | Cadena | **(Obligatorio)** El nombre del esquema XDM al que pertenece la entidad. |
| `identities` | Matriz | **(Obligatorio)** Una matriz que contiene una lista de identidades para las entidades a las que desea tener acceso. |
| `identities.entityId` | Cadena | El ID de una entidad a la que desea acceder. |
| `identities.entityIdNS.code` | Cadena | El área de nombres de un ID de entidad al que desea acceder. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con las entidades solicitadas.

+++ Una respuesta de ejemplo que contiene las entidades solicitadas

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB Oportunidad B2B]

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera las oportunidades B2B solicitadas.

+++ Una solicitud de ejemplo para recuperar varias entidades

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Propiedad | Tipo | Descripción |
| -------- |----- | ----------- |
| `schema.name` | Cadena | **(Obligatorio)** El nombre del esquema XDM al que pertenece la entidad. |
| `identities` | Matriz | **(Obligatorio)** Una matriz que contiene una lista de identidades para las entidades a las que desea tener acceso. |
| `identities.entityId` | Cadena | El ID de una entidad a la que desea acceder. |
| `identities.entityIdNS.code` | Cadena | El área de nombres de un ID de entidad al que desea acceder. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con las entidades solicitadas.

+++ Una respuesta de ejemplo que contiene las entidades solicitadas

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Acceso a una página posterior de resultados

Los resultados se paginan al recuperar eventos de series temporales. Si hay páginas de resultados subsiguientes, la propiedad `_page.next` contendrá un ID. Además, la propiedad `_links.next.href` proporciona un URI de solicitud para recuperar la página siguiente. Para recuperar los resultados, realice otra solicitud de GET al extremo `/access/entities` y reemplace `/entities` por el valor del URI proporcionado.

>[!NOTE]
>
>Asegúrese de no repetir accidentalmente `/entities/` en la ruta de solicitud. Solo debería aparecer una vez como `/access/entities?start=...`

**Formato de API**

```http
GET /access/{NEXT_URI}
```

| Parámetro | Descripción |
|---|---|
| `{NEXT_URI}` | El valor de URI tomado de `_links.next.href`. |

**Solicitud**

La siguiente solicitud recupera la siguiente página de resultados usando el URI `_links.next.href` como ruta de solicitud.

+++ Una solicitud de ejemplo para acceder a la siguiente página de resultados

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve la siguiente página de resultados. Esta respuesta no tiene páginas de resultados subsiguientes, como indican los valores de cadena vacíos de `_page.next` y `_links.next.href`.

+++ Una respuesta de ejemplo que contiene la siguiente página de entidades

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

+++

## Eliminar una entidad {#delete-entity}

Puede eliminar una entidad del almacén de perfiles realizando una solicitud de DELETE al extremo `/access/entities` junto con los parámetros de consulta necesarios.

**Formato de API**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;).

Para eliminar una entidad, **debe** proporcionar los siguientes parámetros de consulta:

- `schema.name`: nombre del esquema XDM de la entidad. En este caso de uso, puede **solamente** usar `schema.name=_xdm.context.profile`.
- `entityId`: ID de la entidad que intenta recuperar.
- `entityIdNS`: área de nombres de la entidad que intenta recuperar. Se debe proporcionar este valor si `entityId` es **no** un XID.
- `mergePolicyId`: ID de política de combinación de la entidad. La política de combinación contiene información sobre la vinculación de identidad y la combinación de objetos XDM clave-valor. Si no se proporciona este valor, se utilizará la política de combinación predeterminada.

**Solicitud**

La siguiente solicitud elimina la entidad especificada.

+++ Una solicitud de ejemplo para eliminar una entidad

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 con un cuerpo de respuesta vacío.

## Pasos siguientes

Al seguir esta guía, ha accedido correctamente a [!DNL Real-Time Customer Profile] campos de datos, perfiles y datos de series temporales. Para obtener información sobre cómo tener acceso a otros recursos de datos almacenados en [!DNL Platform], vea la [descripción general del acceso a datos](../../data-access/home.md).

## Apéndice {#appendix}

La siguiente sección proporciona información adicional sobre el acceso a los datos de [!DNL Profile] mediante la API.

### Parámetros de consulta {#query-parameters}

Los siguientes parámetros se utilizan en la ruta de acceso de las solicitudes de GET al extremo `/access/entities`. Sirven para identificar la entidad de perfil a la que desea acceder y filtrar los datos devueltos en la respuesta. Los parámetros obligatorios están etiquetados, mientras que el resto son opcionales.

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `schema.name` | **(Obligatorio)** El nombre del esquema XDM de la entidad. | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Si `schema.name` es `_xdm.context.experienceevent`, este valor **debe** especificar el esquema para la entidad de perfil con la que están relacionados los eventos de series temporales. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Obligatorio)** El identificador de la entidad. Si el valor de este parámetro no es un XID, también se debe proporcionar un parámetro de área de nombres de identidad (`entityIdNS`). | `entityId=janedoe@example.com` |
| `entityIdNS` | Si `entityId` no se proporciona como un XID, este campo **debe** especificar el área de nombres de identidad. | `entityIdNS=email` |
| `relatedEntityId` | Si `schema.name` es `_xdm.context.experienceevent`, este valor **debe** especificar el identificador de la entidad de perfil relacionada. Este valor sigue las mismas reglas que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Si `schema.name` es &quot;_xdm.context.experienceevent&quot;, este valor debe especificar el área de nombres de identidad para la entidad especificada en `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra los datos devueltos en la respuesta. Utilice esto para especificar qué valores de campo de esquema incluir en los datos recuperados. Para varios campos, separe los valores con una coma sin espacios entre ellos. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica la política de combinación que rige los datos devueltos. Si no se especifica uno en la llamada de, se utilizará el valor predeterminado de su organización para ese esquema. Si no se ha configurado ninguna política de combinación predeterminada, el valor predeterminado es sin combinación de perfiles ni vinculación de identidad. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Orden de las entidades recuperadas por marca de tiempo. Esto se escribe como `(+/-)timestamp`, con el valor predeterminado `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Especifica el tiempo de inicio para filtrar las entidades (en milisegundos). | `startTime=1539838505` |
| `endTime` | Especifica el tiempo de finalización para filtrar entidades (en milisegundos). | `endTime=1539838510` |
| `limit` | Especifica el número máximo de entidades que se van a devolver. De forma predeterminada, este valor se establece en 1000. | `limit=100` |
| `property` | Filtra por el valor de propiedad. Este parámetro de consulta admite los siguientes evaluadores: =, !=, &lt;, &lt;=, >, >=. Esto solo se puede utilizar con eventos de experiencia, con un máximo de tres propiedades admitidas. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
