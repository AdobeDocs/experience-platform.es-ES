---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Punto final de API de entidades (acceso a perfil)
type: Documentation
description: Adobe Experience Platform le permite acceder a los datos del perfil del cliente en tiempo real mediante las API de RESTful o la interfaz de usuario. Esta guía describe cómo acceder a entidades, más comúnmente conocidas como "perfiles", mediante la API de perfil.
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 2%

---

# Extremo de entidades (acceso de perfil)

Adobe Experience Platform le permite acceder a [!DNL Real-Time Customer Profile] datos mediante las API de RESTful o la interfaz de usuario. Esta guía describe cómo acceder a entidades, más comúnmente denominadas &quot;perfiles&quot;, mediante la API de . Para obtener más información sobre el acceso a perfiles mediante la variable [!DNL Platform] Interfaz de usuario, consulte [Guía del usuario del perfil](../ui/user-guide.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, revise la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier [!DNL Experience Platform] API.

## Acceso a los datos de perfil por identidad

Puede acceder a un [!DNL Profile] realizando una solicitud de GET a la `/access/entities` y proporcionando la identidad de la entidad como una serie de parámetros de consulta. Esta identidad consiste en un valor de ID (`entityId`) y el área de nombres de identidad (`entityIdNS`).

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &amp;. Se proporciona una lista completa de los parámetros válidos en la [parámetros de consulta](#query-parameters) del apéndice.

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitud**

La siguiente solicitud recupera el correo electrónico y el nombre de un cliente mediante una identidad:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

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

>[!NOTE]
>
>Si un gráfico relacionado vincula más de 50 identidades, este servicio devolverá el estado HTTP 422 y el mensaje &quot;Demasiadas identidades relacionadas&quot;. Si recibe este error, considere la posibilidad de agregar más parámetros de consulta para restringir la búsqueda.

## Acceso a los datos de perfil por lista de identidades

Puede acceder a varias entidades de perfil según sus identidades enviando una solicitud de POST al `/access/entities` y proporcionando las identidades en la carga útil. Estas identidades constan de un valor de ID (`entityId`) y un área de nombres de identidad (`entityIdNS`).

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera los nombres y las direcciones de correo electrónico de varios clientes mediante una lista de identidades:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Propiedad | Descripción |
|---|---|
| `schema.name` | ***(Obligatorio)*** Nombre del esquema XDM al que pertenece la entidad. |
| `fields` | Los campos XDM que se van a devolver, como una matriz de cadenas. De forma predeterminada, se devuelven todos los campos. |
| `identities` | ***(Obligatorio)*** Matriz que contiene una lista de identidades para las entidades a las que desea acceder. |
| `identities.entityId` | El ID de una entidad a la que desea acceder. |
| `identities.entityIdNS.code` | El espacio de nombres de un ID de entidad al que desea acceder. |
| `timeFilter.startTime` | Hora de inicio del filtro de intervalo de tiempo, incluido. Debe tener una granularidad de milisegundos. El valor predeterminado, si no se especifica, es el comienzo del tiempo disponible. |
| `timeFilter.endTime` | Filtro de intervalo de tiempo de finalización, excluido. Debe tener una granularidad de milisegundos. El valor predeterminado, si no se especifica, es el final del tiempo disponible. |
| `limit` | Número de registros que se van a devolver. Solo se aplica al número de eventos de experiencia devueltos. Predeterminado: 1000. |
| `orderby` | El orden de los eventos de experiencia recuperados por marca de tiempo, escrito como `(+/-)timestamp` con el valor predeterminado `+timestamp`. |
| `withCA` | Indicador de características para activar atributos calculados para la búsqueda. Predeterminado: false. |

**Respuesta**
Una respuesta correcta devuelve los campos solicitados de entidades especificadas en el cuerpo de la solicitud.

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

## Acceso a eventos de series temporales de un perfil por identidad

Puede acceder a los eventos de series temporales según la identidad de su entidad de perfil asociada realizando una solicitud de GET al `/access/entities` punto final. Esta identidad consiste en un valor de ID (`entityId`) y un área de nombres de identidad (`entityIdNS`).

Los parámetros de consulta proporcionados en la ruta de solicitud especifican a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &amp;. Se proporciona una lista completa de los parámetros válidos en la [parámetros de consulta](#query-parameters) del apéndice.

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitud**

La siguiente solicitud encuentra una entidad de perfil por ID y recupera los valores de las propiedades `endUserIDs`, `web`y `channel` para todos los eventos de series temporales asociados a la entidad.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista paginada de eventos de series temporales y campos asociados especificados en los parámetros de consulta de solicitud.

>[!NOTE]
>
>La solicitud especificó un límite de uno (`limit=1`), por lo tanto, la variable `count` en la respuesta siguiente es 1 y solo se devuelve una entidad.

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

### Acceso a una página de resultados posterior

Los resultados se paginan al recuperar eventos de series temporales. Si hay páginas de resultados subsiguientes, la variable `_page.next` contiene un ID. Además, la variable `_links.next.href` proporciona un URI de solicitud para recuperar la página siguiente. Para recuperar los resultados, realice otra solicitud de GET a la variable `/access/entities` , sin embargo, debe asegurarse de reemplazar `/entities` con el valor del URI proporcionado.

>[!NOTE]
>
>Asegúrese de no repetir accidentalmente `/entities/` en la ruta de solicitud. Solo debería aparecer una vez como, `/access/entities?start=...`

**Formato de API**

```http
GET /access/{NEXT_URI}
```

| Parámetro | Descripción |
|---|---|
| `{NEXT_URI}` | El valor de URI tomado de `_links.next.href`. |

**Solicitud**

La siguiente solicitud recupera la siguiente página de resultados utilizando la variable `_links.next.href` URI como ruta de solicitud.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la siguiente página de resultados. Esta respuesta no tiene páginas de resultados posteriores, como indican los valores de cadena vacíos de `_page.next` y `_links.next.href`.

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

## Acceso a eventos de series temporales para varios perfiles por identidades

Puede acceder a los eventos de series temporales de varios perfiles asociados realizando una solicitud de POST al `/access/entities` y proporcionando las identidades de perfil en la carga útil. Cada una de estas identidades consta de un valor de ID (`entityId`) y un área de nombres de identidad (`entityIdNS`).

**Formato de API**

```http
POST /access/entities
```

**Solicitud**

La siguiente solicitud recupera los ID de usuario, las horas locales y los códigos de país para los eventos de serie temporal asociados con una lista de identidades de perfil:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
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
    "limit": 10
}'
```

| Propiedad | Descripción |
|---|---|
| `schema.name` | **(OBLIGATORIO)** El esquema XDM de la entidad que se va a recuperar |
| `relatedSchema.name` | If `schema.name` es `_xdm.context.experienceevent` este valor debe especificar el esquema para la entidad de perfil a la que están relacionados los eventos de series temporales. |
| `identities` | **(OBLIGATORIO)** Una lista de matriz de perfiles desde los que recuperar los eventos de series temporales asociados. Cada entrada de la matriz se configura de una de las dos maneras siguientes: 1) usar una identidad completa que consista en un valor de ID y un área de nombres o 2) proporcionar un XID. |
| `fields` | Aísla los datos devueltos a un conjunto específico de campos. Utilice esto para filtrar qué campos de esquema se incluyen en los datos recuperados. Ejemplo: personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifica la directiva de combinación por la que se rigen los datos devueltos. Si no se especifica uno en la llamada de servicio, se utilizará el esquema predeterminado de la organización para ese esquema. Si no se ha configurado ninguna directiva de combinación predeterminada, el valor predeterminado es sin combinación de perfiles ni vinculación de identidad. |
| `orderby` | El orden de los eventos de experiencia recuperados por marca de tiempo, escrito como `(+/-)timestamp` con el valor predeterminado `+timestamp`. |
| `timeFilter.startTime` | Especifique la hora de inicio para filtrar objetos de series temporales (en milisegundos). |
| `timeFilter.endTime` | Especifique la hora de finalización para filtrar objetos de series temporales (en milisegundos). |
| `limit` | Valor numérico que especifica el número máximo de objetos que se van a devolver. Predeterminado: 1000 |
| `withCA` | Indicador de características para activar atributos calculados para la búsqueda. Predeterminado: false |

**Respuesta**

Una respuesta correcta devuelve una lista paginada de eventos de series temporales asociados con los múltiples perfiles especificados en la solicitud.

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

En esta respuesta de ejemplo, el primer perfil enumerado (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) proporciona un valor para `_links.next.payload`, lo que significa que hay páginas de resultados adicionales para este perfil. Consulte la siguiente sección sobre [acceso a resultados adicionales](#access-additional-results) para obtener más información sobre cómo acceder a estos resultados adicionales.

### Acceso a resultados adicionales {#access-additional-results}

Al recuperar eventos de series temporales, es posible que se devuelvan muchos resultados, por lo que los resultados se suelen paginar. Si hay páginas de resultados subsiguientes para un perfil en particular, la variable `_links.next.payload` para ese perfil contiene un objeto de carga útil.

Con esta carga útil en el cuerpo de la solicitud, puede realizar una solicitud de POST adicional al `access/entities` para recuperar la página siguiente de datos de serie temporal para ese perfil.

## Acceso a eventos de series temporales en varias entidades de esquema

Puede acceder a varias entidades conectadas a través de un descriptor de relación. La siguiente llamada de API de ejemplo supone que ya se ha definido una relación entre dos esquemas. Para obtener más información sobre los descriptores de relaciones, lea la [!DNL Schema Registry] Guía para desarrolladores de API [guía de extremo de descriptores](../../xdm/api/descriptors.md).

Puede incluir parámetros de consulta en la ruta de solicitud para especificar a qué datos acceder. Puede incluir varios parámetros, separados por el símbolo &amp;. Se proporciona una lista completa de los parámetros válidos en la [parámetros de consulta](#query-parameters) del apéndice.

**Formato de API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitud**

La siguiente solicitud recupera una entidad que contiene un descriptor de relación establecido anteriormente para acceder a la información en diferentes esquemas.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista paginada de eventos de series temporales asociados a las distintas entidades.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Acceso a una página de resultados posterior

Los resultados se paginan al recuperar eventos de series temporales. Si hay páginas de resultados subsiguientes, la variable `_page.next` contiene un ID. Además, la variable `_links.next.href` proporciona un URI de solicitud para recuperar la página siguiente realizando solicitudes de GET adicionales al `access/entities` punto final.

## Pasos siguientes

Al seguir esta guía, ha accedido correctamente a [!DNL Real-Time Customer Profile] campos de datos, perfiles y datos de series temporales. Para aprender a acceder a otros recursos de datos almacenados en [!DNL Platform], consulte la [Información general sobre el acceso a los datos](../../data-access/home.md).

## Apéndice {#appendix}

La siguiente sección proporciona información complementaria sobre el acceso a [!DNL Profile] datos mediante la API.

### Parámetros de consulta {#query-parameters}

Los siguientes parámetros se utilizan en la ruta para las solicitudes de GET a la variable `/access/entities` punto final. Sirven para identificar la entidad de perfil a la que desea acceder y filtrar los datos devueltos en la respuesta. Los parámetros requeridos están etiquetados, mientras que el resto son opcionales.

| Parámetro | Descripción | Ejemplo |
|---|---|---|
| `schema.name` | **(OBLIGATORIO)** El esquema XDM de la entidad que se va a recuperar | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | If `schema.name` es &quot;_xdm.context.experienceevent&quot;, este valor debe especificar el esquema de la entidad de perfil con la que están relacionados los eventos de series temporales. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBLIGATORIO)** El ID de la entidad. Si el valor de este parámetro no es un XID, también debe proporcionarse un parámetro de área de nombres de identidad (consulte `entityIdNS` más abajo). | `entityId=janedoe@example.com` |
| `entityIdNS` | If `entityId` no se proporciona como un XID, este campo debe especificar el área de nombres de identidad. | `entityIdNE=email` |
| `relatedEntityId` | If `schema.name` es &quot;_xdm.context.experienceevent&quot;, este valor debe especificar el área de nombres de identidad de la entidad de perfil relacionada. Este valor sigue las mismas reglas que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | If `schema.name` es &quot;_xdm.context.experienceevent&quot;, este valor debe especificar el área de nombres de identidad para la entidad especificada en `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra los datos devueltos en la respuesta. Utilice esto para especificar qué valores de campo de esquema incluir en los datos recuperados. Para varios campos, separe los valores por una coma sin espacios entre | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica la directiva de combinación por la que se rigen los datos devueltos. Si no se especifica uno en la llamada a , se utilizará el valor predeterminado de la organización para ese esquema. Si no se ha configurado ninguna directiva de combinación predeterminada, el valor predeterminado es sin combinación de perfiles ni vinculación de identidad. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | El orden de los eventos de experiencia recuperados por marca de tiempo, escrito como `(+/-)timestamp` con el valor predeterminado `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Especifique la hora de inicio para filtrar objetos de series temporales (en milisegundos). | `startTime=1539838505` |
| `endTime` | Especifique la hora de finalización para filtrar objetos de series temporales (en milisegundos). | `endTime=1539838510` |
| `limit` | Valor numérico que especifica el número máximo de objetos que se van a devolver. Predeterminado: 1000 | `limit=100` |
| `property` | Filtra por el valor de la propiedad. Admite los siguientes evaluadores: =, !=, &lt;, &lt;=, >, >=. Solo se puede utilizar con eventos de experiencia, con un máximo de tres propiedades admitidas. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | Indicador de características para activar atributos calculados para la búsqueda. Predeterminado: false | `withCA=true` |
