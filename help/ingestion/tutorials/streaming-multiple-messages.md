---
keywords: Experience Platform;inicio;temas populares;ingesta de transmisión;ingesta;transmisión de varios mensajes;varios mensajes;
solution: Experience Platform
title: Enviar varios mensajes en una sola solicitud HTTP
type: Tutorial
description: Este documento proporciona un tutorial para enviar varios mensajes a Adobe Experience Platform dentro de una única solicitud HTTP mediante la ingesta de flujo continuo.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# Enviar varios mensajes en una única solicitud HTTP

Al transmitir datos a Adobe Experience Platform, hacer numerosas llamadas HTTP puede ser caro. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas útiles de 1 KB, es mucho más eficaz crear una solicitud HTTP con 200 mensajes de 1 KB cada uno, con una única carga útil de 200 KB. Cuando se utiliza correctamente, agrupar varios mensajes dentro de una única solicitud es una excelente manera de optimizar los datos que se envían a [!DNL Experience Platform].

Este documento proporciona un tutorial para enviar varios mensajes a [!DNL Experience Platform] en una sola solicitud HTTP que utiliza la ingesta de flujo continuo.

## Primeros pasos

Este tutorial requiere una comprensión práctica de Adobe Experience Platform [!DNL Data Ingestion]. Antes de comenzar este tutorial, consulte la siguiente documentación:

- [Información general sobre la ingesta de datos](../home.md): Abarca los conceptos principales de [!DNL Experience Platform Data Ingestion], incluidos los métodos de ingesta y los conectores de datos.
- [Información general sobre la ingesta de flujos](../streaming-ingestion/overview.md): El flujo de trabajo y los componentes básicos de la ingesta de flujo continuo, como conexiones de flujo continuo, conjuntos de datos, [!DNL XDM Individual Profile]y [!DNL XDM ExperienceEvent].

Este tutorial también requiere que haya completado la [Autenticación en Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] API. Al completar el tutorial de autenticación, se proporciona el valor para el encabezado Autorización requerido por todas las llamadas a la API en este tutorial. El encabezado se muestra en las llamadas de ejemplo de la siguiente manera:

- Autorización: Portador `{ACCESS_TOKEN}`

Todas las solicitudes del POST requieren un encabezado adicional:

- Content-Type: application/json

## Creación de una conexión de flujo continuo

Primero debe crear una conexión de flujo continuo para poder iniciar la transmisión de datos a [!DNL Experience Platform]. Lea el [crear una conexión de flujo continuo](./create-streaming-connection.md) guía para aprender a crear una conexión de flujo continuo.

Después de registrar una conexión de flujo continuo, usted, como productor de datos, tendrá una dirección URL única que puede utilizarse para transmitir datos a Platform.

## Enviar a un conjunto de datos

El siguiente ejemplo muestra cómo enviar varios mensajes a un conjunto de datos específico dentro de una única solicitud HTTP. Inserte el ID del conjunto de datos en el encabezado del mensaje para que ese mensaje se incorpore directamente en él.

Puede obtener el ID de un conjunto de datos existente mediante la variable [!DNL Platform] IU o utilizando una operación de listado en la API. El ID del conjunto de datos se puede encontrar en [Experience Platform](https://platform.adobe.com) accediendo a la **[!UICONTROL Conjuntos de datos]** , haga clic en el conjunto de datos para el que desea el ID y copie la cadena del campo ID del conjunto de datos en el **[!UICONTROL Información]** pestaña . Consulte la [Información general del servicio de catálogo](../../catalog/home.md) para obtener información sobre cómo recuperar conjuntos de datos mediante la API.

En lugar de usar un conjunto de datos existente, puede crear un nuevo conjunto de datos. Lea el [crear un conjunto de datos mediante API](../../catalog/api/create-dataset.md) tutorial para obtener más información sobre la creación de un conjunto de datos mediante API.

**Formato de API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | El ID de la conexión de flujo continuo creada. |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

Una respuesta correcta devuelve un estado HTTP 207 (estado múltiple). Al revisar el cuerpo de la respuesta, se proporcionan más detalles sobre el éxito o el fracaso de cada método ejecutado en la solicitud. Se devuelve una respuesta para cada elemento de la matriz de mensajes de solicitud. A continuación se muestra un ejemplo de una respuesta correcta sin errores de mensaje:

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

Para obtener más información sobre los códigos de estado, consulte la [códigos de respuesta](#response-codes) en el apéndice de este tutorial.

## Identificación de mensajes fallidos

En comparación con el envío de una solicitud con un solo mensaje, al enviar una solicitud HTTP con varios mensajes, hay factores adicionales que se deben tener en cuenta, como: cómo identificar cuándo no se han podido enviar los datos, qué mensajes específicos no se han enviado y cómo se pueden recuperar, y qué sucede con los datos que se realizan correctamente cuando fallan otros mensajes de la misma solicitud.

Antes de continuar con este tutorial, se recomienda revisar primero el [recuperación de lotes con errores](../quality/retrieve-failed-batches.md) guía.

### Enviar carga útil de solicitud con mensajes válidos y no válidos

El siguiente ejemplo muestra qué ocurre cuando el lote incluye mensajes válidos y no válidos.

La carga útil de la solicitud es una matriz de objetos JSON que representan el evento en el esquema XDM. Tenga en cuenta que se deben cumplir las siguientes condiciones para validar el mensaje correctamente:
- La variable `imsOrgId` en el encabezado del mensaje debe coincidir con la definición de entrada. Si la carga útil de la solicitud no incluye un `imsOrgId` , el campo [!DNL Data Collection Core Service] (DCCS) añade el campo automáticamente.
- El encabezado del mensaje debe hacer referencia a un esquema XDM existente creado en la variable [!DNL Platform] IU.
- La variable `datasetId` el campo necesita hacer referencia a un conjunto de datos existente en [!DNL Platform], y su esquema debe coincidir con el esquema proporcionado en la variable `header` dentro de cada mensaje incluido en el cuerpo de la solicitud.

**Formato de API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | El ID de la entrada de datos creada. |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

La carga útil de respuesta incluye un estado para cada mensaje junto con un GUID en la variable `xactionId` que se puede utilizar para el seguimiento.

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

La respuesta de ejemplo anterior muestra mensajes de error para la solicitud anterior. Al comparar esta respuesta con la respuesta válida anterior, puede observar que la solicitud tuvo un éxito parcial, con un mensaje que se incorporó correctamente y tres mensajes que tuvieron como resultado un error. Tenga en cuenta que ambas respuestas devuelven un código de estado &quot;207&quot;. Para obtener más información sobre los códigos de estado, consulte la [códigos de respuesta](#response-codes) en el apéndice de este tutorial.

El primer mensaje se envió correctamente a [!DNL Platform] y no se ve afectado por los resultados de los demás mensajes. Como resultado, al intentar reenviar los mensajes fallidos, no es necesario volver a incluir este mensaje.

El segundo mensaje falló porque carecía de un cuerpo de mensaje. La solicitud de recopilación espera que los elementos de mensaje tengan secciones de encabezado y cuerpo válidas. Si se añade el siguiente código después del encabezado del segundo mensaje, se corregirá la solicitud y se permitirá que el segundo mensaje pase la validación:

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

Error en el tercer mensaje debido a que se utiliza un ID de organización de IMS no válido en el encabezado. La organización IMS debe coincidir con el {CONNECTION_ID} al que intenta publicar. Para determinar qué ID de organización de IMS coincide con la conexión de flujo continuo que está utilizando, puede realizar una `GET inlet` solicitud utilizando la variable [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Consulte [recuperación de una conexión de flujo continuo](./create-streaming-connection.md#get-data-collection-url) para ver un ejemplo de cómo recuperar las conexiones de flujo continuo creadas anteriormente.

El cuarto mensaje falló porque no seguía el esquema XDM esperado. La variable `xdmSchema` incluidos en el encabezado y el cuerpo de la solicitud no coinciden con el esquema XDM de la variable `{DATASET_ID}`. La corrección del esquema en el encabezado y el cuerpo del mensaje le permite pasar la validación del DCCS y se envía correctamente a [!DNL Platform]. El cuerpo del mensaje también debe actualizarse para que coincida con el esquema XDM de la variable `{DATASET_ID}` para que pase la validación de flujo continuo a [!DNL Platform]. Para obtener más información sobre lo que sucede con los mensajes que se transmiten correctamente a Platform, consulte la [confirmar mensajes introducidos](#confirm-messages-ingested) de este tutorial.

### Recuperar mensajes fallidos de [!DNL Platform]

Los mensajes fallidos se identifican mediante un código de estado de error en la matriz de respuestas.
Los mensajes no válidos se recopilan y almacenan en un lote &quot;error&quot; dentro del conjunto de datos especificado por `{DATASET_ID}`.

Lea el [recuperación de lotes con errores](../quality/retrieve-failed-batches.md) para obtener más información sobre la recuperación de mensajes fallidos por lotes.

## Confirmar mensajes ingestados

Los mensajes que pasan la validación de DCCS se transmiten a [!DNL Platform]. Activado [!DNL Platform], los mensajes por lotes se prueban validando la transmisión antes de ser introducidos en la variable [!DNL Data Lake]. El estado de los lotes, tanto si son correctos como si no, aparece dentro del conjunto de datos especificado por `{DATASET_ID}`.

Puede ver el estado de los mensajes por lotes que se retransmiten correctamente a [!DNL Platform] usando la variable [IU de Experience Platform](https://platform.adobe.com) accediendo a la **[!UICONTROL Conjuntos de datos]** , haga clic en el conjunto de datos al que está transmitiendo y compruebe el **[!UICONTROL Actividad de conjunto de datos]** pestaña .

Mensajes por lotes que pasan la validación de flujo continuo en [!DNL Platform] se incorporan en la variable [!DNL Data Lake]. Los mensajes están disponibles para su análisis o exportación.

## Pasos siguientes

Ahora que sabe cómo enviar varios mensajes en una sola solicitud y verificar cuándo se introducen correctamente mensajes en el conjunto de datos de Target, puede empezar a transmitir sus propios datos a [!DNL Platform]. Para obtener información general sobre cómo consultar y recuperar datos ingestados de [!DNL Platform], consulte la [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) guía.

## Apéndice

Esta sección contiene información complementaria del tutorial.

### Códigos de respuesta

En la tabla siguiente se muestran los códigos de estado devueltos por los mensajes de respuesta correctos y fallidos.

| Código de estado | Descripción |
| :---: | --- |
| 207 | Aunque se utiliza &quot;207&quot; como código de estado de respuesta general, el destinatario debe consultar el contenido del cuerpo de respuesta de varios estados para obtener más información sobre el éxito o el error de la ejecución del método. El código de respuesta se utiliza en casos de éxito, éxito parcial y también en situaciones de error. |
| 400 | Hubo un problema con la solicitud. Consulte el cuerpo de la respuesta para ver un mensaje de error más específico (por ejemplo, faltaban los campos obligatorios en la carga útil de mensaje o el formato xdm de mensaje era desconocido). |
| 401 | No autorizado: falta el encabezado de autorización válido en la solicitud. Esto solo se devuelve para las entradas que tienen la autenticación habilitada. |
| 403 | No autorizado: El token de autorización proporcionado no es válido o ha caducado. Esto solo se devuelve para las entradas que tienen la autenticación habilitada. |
| 413 | Carga útil demasiado grande: se lanza cuando la solicitud de carga útil total es buena a 1 MB. |
| 429 | Demasiadas solicitudes dentro de un plazo especificado. |
| 500 | Error al procesar la carga útil. Consulte el cuerpo de la respuesta para ver un mensaje de error más específico (por ejemplo, no se especificó el esquema de carga útil de mensaje o no coincide con la definición XDM en [!DNL Platform]). |
| 503 | El servicio no está disponible actualmente. Los clientes deben volver a intentarlo al menos 3 veces usando una estrategia exponencial de back-off. |
