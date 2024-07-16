---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;actualizar flujos de datos de destino
solution: Experience Platform
title: Actualización de flujos de datos de destino mediante la API de Flow Service
type: Tutorial
description: Este tutorial cubre los pasos para actualizar un flujo de datos de destino. Obtenga información sobre cómo habilitar o deshabilitar el flujo de datos, actualizar su información básica o agregar y quitar audiencias y atributos mediante la API de Flow Service.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: c1d4a0586111d9cd8a66f4239f67f2f7e6ac8633
workflow-type: tm+mt
source-wordcount: '2404'
ht-degree: 4%

---

# Actualización de flujos de datos de destino mediante la API de Flow Service

Este tutorial cubre los pasos para actualizar un flujo de datos de destino. Obtenga información sobre cómo habilitar o deshabilitar el flujo de datos, actualizar su información básica o agregar y quitar audiencias y atributos mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Para obtener información sobre cómo editar flujos de datos de destino mediante la interfaz de usuario del Experience Platform, lea [Editar flujos de activación](/help/destinations/ui/edit-activation.md).

## Introducción {#get-started}

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un identificador de flujo válido, seleccione el destino que elija en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) y [activar los datos](../ui/activation-overview.md) antes de intentar este tutorial.

>[!NOTE]
>
> Los términos *flow* y *dataflow* se usan indistintamente en este tutorial. En el contexto de este tutorial, tienen el mismo significado.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
* [Zonas protegidas](../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para actualizar correctamente el flujo de datos mediante la API [!DNL Flow Service].

### Lectura de llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilación de valores para los encabezados obligatorios {#gather-values-for-required-headers}

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si no se especifica el encabezado `x-sandbox-name`, las solicitudes se resuelven en la zona protegida `prod`.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* `Content-Type: application/json`

## Búsqueda de detalles de flujo de datos {#look-up-dataflow-details}

El primer paso para actualizar el flujo de datos de destino es recuperar los detalles del flujo de datos con el ID de flujo. Puede ver los detalles actuales de un flujo de datos existente realizando una solicitud de GET al extremo `/flows`.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El valor `id` único del flujo de datos de destino que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información sobre el ID de flujo.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales del flujo de datos, incluida su versión, el identificador único (`id`) y otra información relevante.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Actualizar nombre y descripción del flujo de datos {#update-dataflow}

Para actualizar el nombre y la descripción del flujo de datos, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el identificador de flujo, la versión y los nuevos valores que desee utilizar.

>[!IMPORTANT]
>
>Se requiere el encabezado `If-Match` al realizar una solicitud de PATCH. El valor de este encabezado es la versión única del flujo de datos que desea actualizar. El valor de la etiqueta se actualiza con cada actualización correcta de un flujo de datos.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza el nombre y la descripción del flujo de datos.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Habilitar o deshabilitar flujo de datos {#enable-disable-dataflow}

Cuando se habilita, un flujo de datos exporta perfiles al destino. Los flujos de datos están habilitados de forma predeterminada, pero se pueden deshabilitar para pausar las exportaciones de perfil.

Puede habilitar o deshabilitar un flujo de datos de destino existente realizando una solicitud de POST a la API [!DNL Flow Service] y proporcionando el estado en el que desea actualizar el flujo.

**Formato de API**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Solicitud**

La siguiente solicitud actualiza el estado del flujo de datos a habilitado.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

La siguiente solicitud actualiza el estado del flujo de datos a deshabilitado.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Añadir una audiencia a un flujo de datos {#add-segment}

Para agregar una audiencia al flujo de datos de destino, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el ID de flujo, la versión y la audiencia que desee agregar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud agrega una audiencia nueva a un flujo de datos de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. Para agregar una audiencia a un flujo de datos, utilice la operación `add`. |
| `path` | Define la parte del flujo que se va a actualizar. Al añadir una audiencia a un flujo de datos, utilice la ruta especificada en el ejemplo. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |
| `id` | Especifique el ID de la audiencia que está agregando al flujo de datos de destino. |
| `name` | **(Opcional)**. Especifique el nombre de la audiencia que está agregando al flujo de datos de destino. Tenga en cuenta que este campo no es obligatorio y puede añadir correctamente una audiencia al flujo de datos de destino sin proporcionar su nombre. |
| `filenameTemplate` | Solo para *destinos por lotes*. Este campo solo es necesario cuando se añade una audiencia a un flujo de datos en destinos de exportación de archivos por lotes como Amazon S3, SFTP o Azure Blob. <br> Este campo determina el formato de nombre de archivo de los archivos que se exportan al destino. <br> Las siguientes opciones están disponibles: <br> <ul><li>`%DESTINATION_NAME%`: obligatorio. Los archivos exportados contienen el nombre de destino.</li><li>`%SEGMENT_ID%`: obligatorio. Los archivos exportados contienen el ID de la audiencia exportada.</li><li>`%SEGMENT_NAME%`: **(Opcional)**. Los archivos exportados contienen el nombre de la audiencia exportada.</li><li>`DATETIME(YYYYMMdd_HHmmss)` o `%TIMESTAMP%`: **(opcional)**. Seleccione una de estas dos opciones para que los archivos incluyan el momento en que los genera el Experience Platform.</li><li>`custom-text`: **(Opcional)**. Reemplace este marcador de posición por cualquier texto personalizado que desee anexar al final de los nombres de archivo.</li></ul> <br> Para obtener más información sobre cómo configurar nombres de archivo, consulte la sección [configurar nombres de archivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) en el tutorial de activación de destinos por lotes. |
| `exportMode` | Solo para *destinos por lotes*. Este campo solo es necesario cuando se añade una audiencia a un flujo de datos en destinos de exportación de archivos por lotes como Amazon S3, SFTP o Azure Blob. <br> obligatorio. Seleccione `"DAILY_FULL_EXPORT"` o `"FIRST_FULL_THEN_INCREMENTAL"`. Para obtener más información sobre las dos opciones, consulte [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) en el tutorial de activación de destinos por lotes. |
| `startDate` | Seleccione la fecha en la que la audiencia debe comenzar a exportar perfiles a su destino. |
| `frequency` | Solo para *destinos por lotes*. Este campo solo es necesario cuando se añade una audiencia a un flujo de datos en destinos de exportación de archivos por lotes como Amazon S3, SFTP o Azure Blob. <br> obligatorio. <br> <ul><li>Para el modo de exportación `"DAILY_FULL_EXPORT"`, puede seleccionar `ONCE` o `DAILY`.</li><li>Para el modo de exportación `"FIRST_FULL_THEN_INCREMENTAL"`, puede seleccionar `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Solo para *destinos por lotes*. Este campo solo es necesario al seleccionar el modo `"DAILY_FULL_EXPORT"` en el selector `frequency`. <br> obligatorio. <br> <ul><li>Seleccione `"AFTER_SEGMENT_EVAL"` para que el trabajo de activación se ejecute inmediatamente después de que se complete el trabajo diario de segmentación por lotes de Platform. Esto garantiza que, cuando se ejecute el trabajo de activación, los perfiles más actualizados se exporten al destino.</li><li>Seleccione `"SCHEDULED"` para que el trabajo de activación se ejecute a una hora fija. Esto garantiza que los datos de perfil del Experience Platform se exporten a la misma hora cada día, pero es posible que los perfiles exportados no estén los más actualizados, en función de si el trabajo de segmentación por lotes se ha completado antes de que se inicie el trabajo de activación. Al seleccionar esta opción, también debe agregar un `startTime` para indicar a qué hora en UTC se deben producir las exportaciones diarias.</li></ul> |
| `endDate` | Solo para *destinos por lotes*. Este campo solo es necesario cuando se añade una audiencia a un flujo de datos en destinos de exportación de archivos por lotes como Amazon S3, SFTP o Azure Blob. <br> No aplicable al seleccionar `"exportMode":"DAILY_FULL_EXPORT"` y `"frequency":"ONCE"`. <br>: establece la fecha en la que los miembros de la audiencia dejan de exportarse al destino. |
| `startTime` | Solo para *destinos por lotes*. Este campo solo es necesario cuando se añade una audiencia a un flujo de datos en destinos de exportación de archivos por lotes como Amazon S3, SFTP o Azure Blob. <br> obligatorio. Seleccione el momento en que se deben generar y exportar al destino los archivos que contienen miembros de la audiencia. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Eliminación de una audiencia de un flujo de datos {#remove-segment}

Para quitar una audiencia de un flujo de datos de destino existente, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el ID de flujo, la versión y el selector de índice de la audiencia que desee quitar. La indexación comienza en `0`. Por ejemplo, la solicitud de ejemplo que se muestra más abajo elimina la primera y la segunda audiencia del flujo de datos.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud elimina dos audiencias de un flujo de datos de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. Para quitar una audiencia de un flujo de datos, use la operación `remove`. |
| `path` | Especifica qué audiencia existente debe eliminarse del flujo de datos de destino, según el índice del selector de audiencia. Para recuperar el orden de las audiencias en un flujo de datos, realice una llamada de GET al extremo `/flows` e inspeccione la propiedad `transformations.segmentSelectors`. Para eliminar la primera audiencia en el flujo de datos, use `"path":"/transformations/0/params/segmentSelectors/selectors/0"`. |


**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Actualización de componentes de una audiencia en un flujo de datos {#update-segment}

Puede actualizar los componentes de una audiencia en un flujo de datos de destino existente. Por ejemplo, puede cambiar la frecuencia de exportación o editar la plantilla de nombre de archivo. Para ello, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el ID de flujo, la versión y el selector de índice de la audiencia que desea actualizar. La indexación comienza en `0`. Por ejemplo, la solicitud siguiente actualiza la novena audiencia de un flujo de datos.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

Al actualizar una audiencia en un flujo de datos de destino existente, primero debe realizar una operación de GET para recuperar los detalles de la audiencia que desea actualizar. A continuación, proporcione toda la información de audiencia en la carga útil, no solo los campos que desee actualizar. En el ejemplo siguiente, se agrega texto personalizado al final de la plantilla de nombre de archivo y la frecuencia de programación de exportación se actualiza de 6 horas a 12 horas.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Para obtener descripciones de las propiedades de la carga útil, consulte la sección [Agregar una audiencia a un flujo de datos](#add-segment).


**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Consulte los ejemplos siguientes para ver más ejemplos de componentes de audiencia que puede actualizar en un flujo de datos.

## Actualizar el modo de exportación de una audiencia de programada a después de la evaluación de audiencia {#update-export-mode}

+++ Haga clic para ver un ejemplo en el que una exportación de audiencia se actualiza desde que se activa todos los días a una hora especificada a que se activa todos los días después de que se complete el trabajo de segmentación por lotes de Platform.

La audiencia se exporta todos los días a las 16:00 UTC.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

La audiencia se exporta todos los días después de que se complete el trabajo de segmentación por lotes diario.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Actualice la plantilla de nombre de archivo para incluir campos adicionales en el nombre del archivo {#update-filename-template}

+++ Haga clic para ver un ejemplo en el que la plantilla de nombre de archivo se actualiza para incluir campos adicionales en el nombre del archivo

Los archivos exportados contienen el nombre de destino y el ID de audiencia del Experience Platform

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Los archivos exportados contienen el nombre de destino, el ID de audiencia del Experience Platform, la fecha y la hora en que el Experience Platform generó el archivo y el texto personalizado anexado al final de los archivos.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Añadir un atributo de perfil a un flujo de datos {#add-profile-attribute}

Para agregar un atributo de perfil al flujo de datos de destino, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el identificador de flujo, la versión y el atributo de perfil que desee agregar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud agrega un nuevo atributo de perfil a un flujo de datos de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. Para agregar un atributo de perfil a un flujo de datos, utilice la operación `add`. |
| `path` | Define la parte del flujo que se va a actualizar. Al añadir un atributo de perfil a un flujo de datos, utilice la ruta especificada en el ejemplo. |
| `value.path` | El valor del atributo de perfil que está agregando al flujo de datos. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Eliminación de un atributo de perfil de un flujo de datos {#remove-profile-attribute}

Para quitar un atributo de perfil de un flujo de datos de destino existente, realice una solicitud de PATCH a la API [!DNL Flow Service] y proporcione el identificador de flujo, la versión y el selector de índice del atributo de perfil que desee quitar. La indexación comienza en `0`. Por ejemplo, la solicitud de ejemplo que se muestra más abajo elimina el quinto atributo de perfil del flujo de datos.


**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud elimina un atributo de perfil de un flujo de datos de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. Para quitar una audiencia de un flujo de datos, use la operación `remove`. |
| `path` | Especifica qué atributo de perfil existente debe eliminarse del flujo de datos de destino, según el índice del selector de audiencia. Para recuperar el orden de los atributos de perfil en un flujo de datos, realice una llamada de GET al extremo `/flows` e inspeccione la propiedad `transformations.profileSelectors`. Para eliminar la primera audiencia en el flujo de datos, use `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Administración de errores de API {#api-error-handling}

Los extremos de la API en este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](/help/landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform para obtener más información sobre la interpretación de respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha aprendido a actualizar varios componentes de un flujo de datos de destino, como agregar o eliminar audiencias o atributos de perfil mediante la API [!DNL Flow Service]. Para obtener más información sobre los destinos, consulte la [descripción general de los destinos](../home.md).
