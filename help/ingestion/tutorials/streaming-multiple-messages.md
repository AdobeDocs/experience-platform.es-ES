---
keywords: Experience Platform;home;popular topics;streaming ingestion;ingestion;streaming multiple messages;multiple messages;
solution: Experience Platform
title: Transmisión de varios mensajes en una sola solicitud HTTP
topic: tutorial
type: Tutorial
description: Este documento proporciona un tutorial para enviar varios mensajes a Adobe Experience Platform dentro de una sola solicitud HTTP mediante la ingesta de flujo continuo.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 1%

---


# Envío de varios mensajes en una sola solicitud HTTP

Al transmitir datos a Adobe Experience Platform, realizar numerosas llamadas HTTP puede resultar costoso. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una sola solicitud es una excelente manera de optimizar los datos que se envían a [!DNL Experience Platform].

Este documento proporciona un tutorial para el envío de varios mensajes a [!DNL Experience Platform] una sola solicitud HTTP mediante la ingesta de flujo continuo.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de Adobe Experience Platform [!DNL Data Ingestion]. Antes de comenzar este tutorial, consulte la siguiente documentación:

- [Información general](../home.md)sobre la inserción de datos: Abarca los conceptos básicos de [!DNL Experience Platform Data Ingestion], incluidos los métodos de inserción y los conectores de datos.
- [Información general](../streaming-ingestion/overview.md)sobre la ingestión de flujo: El flujo de trabajo y los componentes básicos de la inserción de flujo continuo, como conexiones de flujo continuo, conjuntos de datos [!DNL XDM Individual Profile]y [!DNL XDM ExperienceEvent].

Este tutorial también requiere que haya completado el tutorial [Autenticación a Adobe Experience Platform](../../tutorials/authentication.md) para realizar correctamente llamadas a [!DNL Platform] las API. La finalización del tutorial de autenticación proporciona el valor del encabezado Autorización requerido por todas las llamadas de API en este tutorial. El encabezado se muestra en las llamadas de ejemplo de la siguiente manera:

- Autorización: Portador `{ACCESS_TOKEN}`

Todas las solicitudes de POST requieren un encabezado adicional:

- Content-Type: application/json

## Creación de una conexión de flujo continuo

Primero debe crear una conexión de flujo continuo para poder inicio de datos de flujo continuo en [!DNL Experience Platform]. Lea la guía [Crear una conexión](./create-streaming-connection.md) de flujo continuo para aprender a crear una conexión de flujo continuo.

Después de registrar una conexión de flujo continuo, usted, como productor de datos, tendrá una dirección URL única que puede utilizarse para transmitir datos a Platform.

## Flujo a un conjunto de datos

El siguiente ejemplo muestra cómo enviar varios mensajes a un conjunto de datos específico dentro de una sola solicitud HTTP. Inserte la ID del conjunto de datos en el encabezado del mensaje para que ese mensaje se ingrese directamente en él.

Puede obtener el ID de un conjunto de datos existente mediante la [!DNL Platform] interfaz de usuario o mediante una operación de listado en la API. La ID del conjunto de datos se puede encontrar en el [Experience Platform](https://platform.adobe.com) si ingresa a la ficha **[!UICONTROL Conjuntos]** de datos, hace clic en el conjunto de datos para el que desea la ID y copia la cadena desde el campo ID **[!UICONTROL del]** conjunto de datos en la ficha **[!UICONTROL Información]** . Consulte la descripción general [del servicio de](../../catalog/home.md) catálogo para obtener información sobre cómo recuperar conjuntos de datos mediante la API.

En lugar de utilizar un conjunto de datos existente, puede crear un nuevo conjunto de datos. Lea el tutorial [Crear un conjunto de datos mediante API](../../catalog/api/create-dataset.md) para obtener más información sobre cómo crear un conjunto de datos mediante API.

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de la conexión de flujo creada. |

**Solicitud**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Respuesta**

Una respuesta correcta devuelve un estado HTTP 207 (estado múltiple). La revisión del cuerpo de respuesta proporciona más detalles sobre el éxito o el error de cada método ejecutado en la solicitud. Se devuelve una respuesta para cada elemento de la matriz de mensajes de solicitud. A continuación se muestra un ejemplo de una respuesta correcta sin errores de mensaje:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Para obtener más información sobre los códigos de estado, consulte la tabla de códigos [de](#response-codes) respuesta en el Apéndice de este tutorial.

## Identifique los mensajes fallidos

En comparación con el envío de una solicitud con un solo mensaje, al enviar una solicitud HTTP con varios mensajes, hay factores adicionales que hay que tener en cuenta, como: cómo identificar cuándo no se han podido enviar los datos, qué mensajes específicos no se han podido enviar y cómo se pueden recuperar, y qué sucede con los datos que tienen éxito cuando fallan otros mensajes de la misma solicitud.

Antes de continuar con este tutorial, se recomienda revisar primero la guía de [recuperación de lotes](../quality/retrieve-failed-batches.md) con errores.

### Enviar carga útil de solicitud con mensajes válidos y no válidos

El siguiente ejemplo muestra qué sucede cuando el lote incluye mensajes válidos y no válidos.

La carga útil de la solicitud es una matriz de objetos JSON que representan el evento en el esquema XDM. Tenga en cuenta que se deben cumplir las siguientes condiciones para validar correctamente el mensaje:
- El `imsOrgId` campo del encabezado del mensaje debe coincidir con la definición de entrada. Si la carga útil de la solicitud no incluye un `imsOrgId` campo, el [!DNL Data Collection Core Service] (DCCS) agregará el campo automáticamente.
- El encabezado del mensaje debe hacer referencia a un esquema XDM existente creado en la [!DNL Platform] interfaz de usuario.
- El `datasetId` campo debe hacer referencia a un conjunto de datos existente en [!DNL Platform], y su esquema debe coincidir con el esquema proporcionado en el `header` objeto dentro de cada mensaje incluido en el cuerpo de la solicitud.

**Formato API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de la entrada de datos creada. |

**Solicitud**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Respuesta**

La carga útil de respuesta incluye un estado para cada mensaje junto con un GUID en el `xactionId` que se puede utilizar para el seguimiento.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

La respuesta de ejemplo anterior muestra mensajes de error para la solicitud anterior. Al comparar esta respuesta con la respuesta válida anterior, puede observar que la solicitud tuvo un éxito parcial, con un mensaje que se ingestaba correctamente y tres mensajes que resultaban en un error. Tenga en cuenta que ambas respuestas devuelven un código de estado &#39;207&#39;. Para obtener más información sobre los códigos de estado, consulte la tabla de códigos [de](#response-codes) respuesta en el Apéndice de este tutorial.

El primer mensaje se envió correctamente a [!DNL Platform] y no se ve afectado por los resultados de los otros mensajes. Como resultado, al intentar reenviar los mensajes fallidos, no es necesario volver a incluir este mensaje.

El segundo mensaje falló porque no tenía cuerpo de mensaje. La solicitud de recopilación espera que los elementos de mensaje tengan secciones de encabezado y cuerpo válidas. Si se añade el siguiente código después del encabezado del segundo mensaje, se corregirá la solicitud y se permitirá que el segundo mensaje pase la validación:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Error en el tercer mensaje debido a que se está utilizando un ID de organización de IMS no válido en el encabezado. La organización de IMS debe coincidir con el {CONNECTION_ID} al que intenta publicar. Para determinar qué ID de organización de IMS coincide con la conexión de flujo que está utilizando, puede realizar una `GET inlet` solicitud utilizando la [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Consulte [Recuperación de una conexión](./create-streaming-connection.md#get-data-collection-url) de flujo para ver un ejemplo de cómo recuperar las conexiones de flujo creadas anteriormente.

El cuarto mensaje falló porque no seguía el esquema XDM esperado. El `xdmSchema` contenido incluido en el encabezado y el cuerpo de la solicitud no coincide con el esquema XDM del `{DATASET_ID}`. La corrección del esquema en el encabezado y el cuerpo del mensaje le permite pasar la validación de DCCS y enviarse correctamente a [!DNL Platform]. El cuerpo del mensaje también debe actualizarse para que coincida con el esquema XDM de `{DATASET_ID}` para que pase la validación de flujo en [!DNL Platform]. Para obtener más información sobre lo que sucede con los mensajes que se transmiten correctamente a la plataforma, consulte la sección [confirmar mensajes ingestados](#confirm-messages-ingested) de este tutorial.

### Recuperar mensajes fallidos de [!DNL Platform]

Los mensajes fallidos se identifican mediante un código de estado de error en la matriz de respuestas.
Los mensajes no válidos se recopilan y almacenan en un lote &quot;error&quot; dentro del conjunto de datos especificado por `{DATASET_ID}`.

Lea la [guía de recuperación de lotes](../quality/retrieve-failed-batches.md) fallidos para obtener más información sobre la recuperación de mensajes fallidos por lotes.

## Confirmar la ingesta de mensajes

Los mensajes que pasan la validación de DCCS se transmiten a [!DNL Platform]. En [!DNL Platform], los mensajes por lotes se prueban mediante la validación de flujo antes de ser ingeridos en el [!DNL Data Lake]. El estado de los lotes, sean exitosos o no, aparece dentro del conjunto de datos especificado por `{DATASET_ID}`.

Puede realizar la vista del estado de los mensajes por lotes que se transmiten correctamente a [!DNL Platform] través de la interfaz de usuario [del](https://platform.adobe.com) Experience Platform. Para ello, vaya a la ficha **[!UICONTROL Conjuntos]** de datos, haga clic en el conjunto de datos en el que está transmitiendo y compruebe la ficha Actividad **[!UICONTROL del]** conjunto de datos.

Los mensajes por lotes que pasan la validación de flujo continuo [!DNL Platform] se ingieren en la [!DNL Data Lake]. Los mensajes están disponibles para su análisis o exportación.

## Pasos siguientes

Ahora que ya sabe cómo enviar varios mensajes en una sola solicitud y comprobar cuándo se ingieren correctamente en el conjunto de datos de destinatario, puede enviar por inicio sus propios datos a [!DNL Platform]. Para obtener información general sobre cómo consulta y recuperación de datos ingestados desde [!DNL Platform], consulte la guía [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) .

## Apéndice

Esta sección contiene información adicional para el tutorial.

### Códigos de respuesta

La siguiente tabla muestra los códigos de estado devueltos por los mensajes de respuesta correctos y erróneos.

| Código de estado | Descripción |
| :---: | --- |
| 207 | Aunque se utiliza &#39;207&#39; como código de estado de respuesta global, el destinatario debe consultar el contenido del cuerpo de respuesta de varios estados para obtener más información sobre el éxito o el fracaso de la ejecución del método. El código de respuesta se utiliza en casos de éxito, éxito parcial y también en situaciones de error. |
| 400 | Hubo un problema con la solicitud. Consulte el cuerpo de la respuesta para ver un mensaje de error más específico (por ejemplo, faltaban los campos obligatorios en la carga útil del mensaje o el mensaje tenía un formato xdm desconocido). |
| 401 | No autorizado: la solicitud no tiene encabezado de autorización válido. Esto solo se devuelve para las entradas que tienen habilitada la autenticación. |
| 403 | No autorizado:  El token de autorización proporcionado no es válido o ha caducado. Esto solo se devuelve para las entradas que tienen habilitada la autenticación. |
| 413 | Carga útil demasiado grande: se genera cuando la solicitud de carga útil total es buena a 1 MB. |
| 429 | Demasiadas solicitudes dentro de un período de tiempo especificado. |
| 500 | Error al procesar la carga útil. Consulte el cuerpo de la respuesta para ver un mensaje de error más específico (por ejemplo, no se especificó el esquema de carga útil del mensaje o no coincidió con la definición de XDM en [!DNL Platform]). |
| 503 | El servicio no está disponible en este momento. Los clientes deben volver a intentarlo al menos tres veces con una estrategia exponencial de retroceso. |