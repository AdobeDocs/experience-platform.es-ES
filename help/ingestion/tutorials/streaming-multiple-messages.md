---
keywords: Experience Platform;inicio;temas populares;ingesta de transmisión;ingesta;transmisión de varios mensajes;varios mensajes;
solution: Experience Platform
title: Enviar varios mensajes en una única solicitud HTTP
type: Tutorial
description: Este documento proporciona un tutorial para enviar varios mensajes a Adobe Experience Platform dentro de una sola solicitud HTTP mediante la ingesta por flujo continuo.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 1%

---

# Enviar varios mensajes en una única solicitud HTTP

Al transmitir datos a Adobe Experience Platform, realizar numerosas llamadas HTTP puede resultar caro. Por ejemplo, en lugar de crear 200 solicitudes HTTP con cargas útiles de 1 KB, es mucho más eficiente crear 1 solicitud HTTP con 200 mensajes de 1 KB cada uno, con una sola carga útil de 200 KB. Si se usa correctamente, agrupar varios mensajes en una única solicitud es una manera excelente de optimizar los datos que se envían a [!DNL Experience Platform].

Este documento proporciona un tutorial para enviar varios mensajes a [!DNL Experience Platform] dentro de una sola solicitud HTTP mediante la introducción de transmisión por secuencias.

## Introducción

Este tutorial requiere una comprensión práctica de Adobe Experience Platform [!DNL Data Ingestion]. Antes de comenzar este tutorial, revise la siguiente documentación:

- [Resumen de ingesta de datos](../home.md): Cubre los conceptos principales de [!DNL Experience Platform Data Ingestion], incluidos los métodos de ingesta y los conectores de datos.
- [Información general sobre la ingesta de transmisión](../streaming-ingestion/overview.md): El flujo de trabajo y los componentes básicos de la transmisión por secuencias, como las conexiones de transmisión por secuencias, los conjuntos de datos, [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent].

Este tutorial también requiere que haya completado el tutorial [Autenticación en Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para poder realizar llamadas a las API [!DNL Experience Platform] correctamente. Al completar el tutorial de autenticación, se proporciona el valor para el encabezado Autorización requerido por todas las llamadas de API en este tutorial. El encabezado se muestra en llamadas de ejemplo de la siguiente manera:

- Autorización: Portador `{ACCESS_TOKEN}`

Todas las solicitudes de POST requieren un encabezado adicional:

- Content-Type: application/json

## Creación de una conexión de flujo continuo

Primero debe crear una conexión de flujo continuo para poder iniciar la transmisión de datos a [!DNL Experience Platform]. Lea la guía [crear una conexión de flujo continuo](./create-streaming-connection.md) para aprender a crear una conexión de flujo continuo.

Después de registrar una conexión de flujo continuo, usted, como productor de datos, tendrá una URL única que se puede utilizar para transmitir datos a Experience Platform.

## Transmitir a un conjunto de datos

El siguiente ejemplo muestra cómo enviar varios mensajes a un conjunto de datos específico dentro de una única solicitud HTTP. Inserte la ID del conjunto de datos en el encabezado del mensaje para que ese mensaje se incorpore directamente en él.

Puede obtener el ID de un conjunto de datos existente mediante la interfaz de usuario de [!DNL Experience Platform] o mediante una operación de listado en la API. La ID del conjunto de datos se puede encontrar en [Experience Platform](https://platform.adobe.com). Para ello, vaya a la pestaña **[!UICONTROL Conjuntos de datos]**, haga clic en el conjunto de datos para el que desee la ID y copie la cadena del campo de ID del conjunto de datos en la pestaña **[!UICONTROL Información]**. Consulte la [descripción general del servicio de catálogo](../../catalog/home.md) para obtener información sobre cómo recuperar conjuntos de datos mediante la API.

En lugar de utilizar un conjunto de datos existente, puede crear uno nuevo. Lea el tutorial [Crear un conjunto de datos con API](../../catalog/api/create-dataset.md) para obtener más información sobre cómo crear un conjunto de datos con API.

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

Una respuesta correcta devuelve un estado HTTP 207 (varios estados). La revisión del cuerpo de respuesta proporciona más detalles sobre el éxito o el error de cada método ejecutado en la solicitud. Se devuelve una respuesta para cada elemento de la matriz de mensajes de solicitud. A continuación se muestra un ejemplo de una respuesta correcta sin errores de mensaje:

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

Para obtener más información sobre los códigos de estado, consulte la tabla [códigos de respuesta](#response-codes) en el apéndice de este tutorial.

## Identificación de mensajes fallidos

En comparación con el envío de una solicitud con un solo mensaje, al enviar una solicitud HTTP con varios mensajes, hay factores adicionales que se deben tener en cuenta, como: cómo identificar cuándo se han producido errores al enviar datos, qué mensajes específicos no se han enviado y cómo se pueden recuperar y qué sucede con los datos que tienen éxito cuando fallan otros mensajes en la misma solicitud.

Antes de continuar con este tutorial, se recomienda revisar primero la guía [recuperación de lotes con errores](../quality/retrieve-failed-batches.md).

### Enviar carga útil de solicitud con mensajes válidos y no válidos

El siguiente ejemplo muestra lo que sucede cuando el lote incluye mensajes válidos y no válidos.

La carga útil solicitada es una matriz de objetos JSON que representan el evento en el esquema XDM. Tenga en cuenta que deben cumplirse las siguientes condiciones para que la validación del mensaje se realice correctamente:
- El campo `imsOrgId` del encabezado del mensaje debe coincidir con la definición de entrada. Si la carga de la solicitud no incluye un campo `imsOrgId`, el [!DNL Data Collection Core Service] (DCCS) agregará el campo automáticamente.
- El encabezado del mensaje debe hacer referencia a un esquema XDM existente creado en la interfaz de usuario de [!DNL Experience Platform].
- El campo `datasetId` debe hacer referencia a un conjunto de datos existente en [!DNL Experience Platform], y su esquema debe coincidir con el esquema proporcionado en el objeto `header` dentro de cada mensaje incluido en el cuerpo de la solicitud.

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

La carga de respuesta incluye un estado para cada mensaje junto con un GUID en el `xactionId` que se puede utilizar para el seguimiento.

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

La respuesta de ejemplo anterior muestra mensajes de error para la solicitud anterior. Al comparar esta respuesta con la respuesta válida anterior, puede observar que la solicitud resultó en un éxito parcial, con un mensaje que se ingirió correctamente y tres mensajes que resultaron en un error. Tenga en cuenta que ambas respuestas devuelven un código de estado &quot;207&quot;. Para obtener más información sobre los códigos de estado, consulte la tabla [códigos de respuesta](#response-codes) en el apéndice de este tutorial.

El primer mensaje se envió correctamente a [!DNL Experience Platform] y no se ve afectado por los resultados de los demás mensajes. Como resultado, al intentar reenviar los mensajes fallidos, no es necesario volver a incluir este mensaje.

Error en el segundo mensaje porque carecía de cuerpo de mensaje. La solicitud de colección espera que los elementos de mensaje tengan secciones de encabezado y cuerpo válidas. Añadir el siguiente código después del encabezado del segundo mensaje corregirá la solicitud, lo que permite que el segundo mensaje apruebe la validación:

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

Error en el tercer mensaje debido a que se está utilizando un ID de organización no válido en el encabezado. La organización debe coincidir con el(la) {CONNECTION_ID} en el(la) que usted intenta publicar. Para determinar qué identificador de organización coincide con la conexión de flujo continuo que está utilizando, puede realizar una solicitud de `GET inlet` con [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Consulte [recuperación de una conexión de flujo continuo](./create-streaming-connection.md#get-data-collection-url) para ver un ejemplo de cómo recuperar las conexiones de flujo continuo creadas anteriormente.

Error en el cuarto mensaje porque no seguía el esquema XDM esperado. El `xdmSchema` incluido en el encabezado y el cuerpo de la solicitud no coinciden con el esquema XDM de `{DATASET_ID}`. La corrección del esquema en el encabezado y el cuerpo del mensaje le permite pasar la validación de DCCS y enviarlo correctamente a [!DNL Experience Platform]. El cuerpo del mensaje también debe actualizarse para que coincida con el esquema XDM de `{DATASET_ID}` para que pase la validación de flujo continuo en [!DNL Experience Platform]. Para obtener más información sobre lo que sucede con los mensajes que se transmiten correctamente a Experience Platform, consulte la sección [confirmar mensajes introducidos](#confirm-messages-ingested) de este tutorial.

### Recuperar mensajes fallidos de [!DNL Experience Platform]

Los mensajes fallidos se identifican mediante un código de estado de error en la matriz de respuesta.
Los mensajes no válidos se recopilan y almacenan en un lote de &quot;error&quot; dentro del conjunto de datos especificado por `{DATASET_ID}`.

Lea la guía [recuperación de lotes con errores](../quality/retrieve-failed-batches.md) para obtener más información sobre la recuperación de mensajes por lotes con errores.

## Confirmar mensajes introducidos

Los mensajes que superen la validación de DCCS se transmitirán a [!DNL Experience Platform]. En [!DNL Experience Platform], la validación de flujo prueba los mensajes por lotes antes de ingerirlos en [!DNL Data Lake]. El estado de los lotes, independientemente de si son correctos o no, aparece dentro del conjunto de datos especificado por `{DATASET_ID}`.

Puede ver el estado de los mensajes por lotes que se transmitieron correctamente a [!DNL Experience Platform] mediante la [IU de Experience Platform](https://platform.adobe.com). Para ello, vaya a la pestaña **[!UICONTROL Conjuntos de datos]**, haga clic en el conjunto de datos al que está transmitiendo y compruebe la pestaña **[!UICONTROL Actividad de conjuntos de datos]**.

Los mensajes por lotes que pasan la validación de flujo continuo en [!DNL Experience Platform] se incorporan en [!DNL Data Lake]. Los mensajes están disponibles para su análisis o exportación.

## Pasos siguientes

Ahora que sabe cómo enviar varios mensajes en una sola solicitud y comprobar cuándo los mensajes se incorporan correctamente en el conjunto de datos de destino, puede empezar a transmitir sus propios datos a [!DNL Experience Platform]. Para obtener información general sobre cómo consultar y recuperar datos ingeridos de [!DNL Experience Platform], consulte la guía [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

## Apéndice

Esta sección contiene información suplementaria para el tutorial.

### Códigos de respuesta

La tabla siguiente muestra los códigos de estado devueltos por los mensajes de respuesta correctos y fallidos.

| Código de estado | Descripción |
| :---: | --- |
| 207 | Aunque se utiliza &quot;207&quot; como código de estado de respuesta general, el destinatario debe consultar el contenido del cuerpo de respuesta de varios estados para obtener más información sobre el éxito o el fracaso de la ejecución del método. El código de respuesta se utiliza en situaciones de éxito, de éxito parcial y también de error. |
| 400 | Se ha producido un error con la solicitud. Consulte el cuerpo de respuesta para ver un mensaje de error más específico (por ejemplo, en la carga del mensaje faltaban campos obligatorios o el mensaje tenía un formato xdm desconocido). |
| 401 | No autorizado: a la solicitud le falta un encabezado de autorización válido. Esto solo se devuelve para las entradas que tienen la autenticación habilitada. |
| 403 | No autorizado: el token de autorización proporcionado no es válido o ha caducado. Esto solo se devuelve para las entradas que tienen la autenticación habilitada. |
| 413 | Carga útil demasiado grande: se produce cuando la solicitud de carga útil total es mayor de 1 MB. |
| 429 | Demasiadas solicitudes en una duración de tiempo especificada. |
| 500 | Error al procesar la carga útil. Consulte el cuerpo de respuesta para ver un mensaje de error más específico (por ejemplo, el esquema de carga útil del mensaje no especificado o no coincide con la definición XDM en [!DNL Experience Platform]). |
| 503 | El servicio no está disponible actualmente. Los clientes deben reintentarlo al menos 3 veces con una estrategia de retroceso exponencial. |
