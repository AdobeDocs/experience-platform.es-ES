---
title: Crear una nueva especificación de conexión para el SDK de flujo mediante la API de servicio de flujo
description: En el siguiente documento se proporcionan los pasos para crear una especificación de conexión mediante la API de servicio de flujo e integrar un nuevo origen a través de fuentes de autoservicio.
hide: true
hidefromtoc: true
source-git-commit: 6b78ed695bca5912c9af4371a8423fdcd7471bde
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Cree una nueva especificación de conexión utilizando la variable [!DNL Flow Service] API

Una especificación de conexión representa la estructura de un origen. Contiene información sobre los requisitos de autenticación de una fuente, define cómo se pueden explorar e inspeccionar los datos de origen y proporciona información sobre los atributos de una fuente determinada. La variable `/connectionSpecs` en la variable [!DNL Flow Service] La API de le permite administrar mediante programación las especificaciones de conexión dentro de su organización.

En el siguiente documento se proporcionan los pasos para crear una especificación de conexión mediante el [!DNL Flow Service] API e integrar una nueva fuente a través de fuentes de autoservicio (SDK de transmisión).

## Primeros pasos

Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recopilar artefactos

Para crear una nueva fuente de flujo continuo utilizando fuentes de autoservicio, primero debe coordinarse con el Adobe, solicitar un repositorio de Git privado y alinearse con el Adobe en los detalles sobre la etiqueta, la descripción, la categoría y el icono de la fuente.

Una vez proporcionado, debe estructurar el repositorio privado de Git de esta manera:

* Fuentes
   * {your_source}
      * Artefactos
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefactos (nombres de archivo) | Descripción | Ejemplo |
| --- | --- | --- |
| {your_source} | Nombre de la fuente. Esta carpeta debe contener todos los artefactos relacionados con su origen, dentro del repositorio Git privado. | `medallia` |
| {your_source}-category.txt | Categoría a la que pertenece el origen, con el formato de archivo de texto. **Nota**: Si cree que su fuente no se ajusta a ninguna de las categorías anteriores, póngase en contacto con el representante del Adobe para hablar al respecto. | `medallia-category.txt` Dentro del archivo, especifique la categoría de la fuente, como: `streaming`. |
| {your_source}-description.txt | Breve descripción de la fuente. | [!DNL Medallia] es la fuente de automatización de marketing que puede usar para traer [!DNL Medallia] datos para el Experience Platform. |
| {your_source}-icon.svg | La imagen que se utilizará para representar el origen en el catálogo de fuentes del Experience Platform. Este icono debe ser un archivo SVG. |
| {your_source}-label.txt | El nombre del origen tal como debería aparecer en el catálogo de fuentes del Experience Platform. | Medallia |
| {your_source}-connectionSpec.json | Un archivo JSON que contiene la especificación de conexión de su origen. Este archivo no es necesario inicialmente, ya que se va a rellenar la especificación de conexión al completar esta guía. | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Durante el periodo de prueba de la especificación de conexión, en lugar de los valores clave, puede utilizar `text` en la especificación de conexión.

Una vez que haya agregado los archivos necesarios al repositorio Git privado, debe crear una solicitud de extracción (PR) para que el Adobe lo revise. Cuando su PR se apruebe y fusione, se le proporcionará un ID que puede utilizarse para que su especificación de conexión haga referencia a la etiqueta, la descripción y el icono de su fuente.

A continuación, siga los pasos descritos a continuación para configurar la especificación de conexión. Para obtener instrucciones adicionales sobre las diferentes funcionalidades que puede agregar a su origen, como la programación avanzada, el esquema personalizado o diferentes tipos de paginación, consulte la guía de [configuración de especificaciones de origen](../config/sourcespec.md).

## Copiar plantilla de especificación de conexión

Una vez que haya recopilado los artefactos requeridos, copie y pegue la plantilla de especificación de conexión a continuación en el editor de texto de su elección y, a continuación, actualice los atributos entre corchetes `{}` con información relevante para su fuente específica.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Crear una especificación de conexión {#create}

Una vez adquirida la plantilla de especificación de conexión, ahora puede empezar a crear una nueva especificación de conexión rellenando los valores adecuados que correspondan a su origen.

Una especificación de conexión se puede dividir en dos partes diferentes: las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener más información sobre las secciones de una especificación de conexión:

* [Configurar la especificación de origen](../config/sourcespec.md)
* [Configuración de la especificación de exploración](../config/explorespec.md)

Con la información de especificación actualizada, puede enviar la nueva especificación de conexión realizando una solicitud del POST a la `/connectionSpecs` punto final del [!DNL Flow Service] API.

**Formato de API**

```http
POST /connectionSpecs
```

**Solicitud**

La siguiente solicitud es un ejemplo de especificación de conexión de autoría completa para una fuente de flujo continuo:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Respuesta**

Una respuesta correcta devuelve la especificación de conexión recién creada, incluyendo su `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## Pasos siguientes

Ahora que ha creado una nueva especificación de conexión, debe agregar su ID de especificación de conexión correspondiente a una especificación de flujo existente. Consulte el tutorial en [actualizar especificaciones de flujo](./update-flow-specs.md) para obtener más información.

Para realizar modificaciones en la especificación de conexión que ha creado, consulte el tutorial sobre [actualización de las especificaciones de conexión](./update-connection-specs.md).
