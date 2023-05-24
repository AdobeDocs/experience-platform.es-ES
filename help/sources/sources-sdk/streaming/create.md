---
title: Cree una nueva especificación de conexión para el SDK de streaming mediante la API de Flow Service
description: El siguiente documento proporciona pasos sobre cómo crear una especificación de conexión mediante la API de Flow Service e integrar una nueva fuente a través de fuentes de autoservicio.
hide: true
hidefromtoc: true
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# Cree una nueva especificación de conexión utilizando [!DNL Flow Service] API

Una especificación de conexión representa la estructura de un origen. Contiene información sobre los requisitos de autenticación de una fuente, define cómo se pueden explorar e inspeccionar los datos de la fuente y proporciona información sobre los atributos de una fuente determinada. El `/connectionSpecs` punto final en la [!DNL Flow Service] La API de le permite administrar mediante programación las especificaciones de conexión de su organización.

En el siguiente documento se proporcionan los pasos para crear una especificación de conexión utilizando [!DNL Flow Service] API e integrar una nueva fuente a través de fuentes de autoservicio (SDK de streaming).

## Primeros pasos

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recopilar artefactos

Para crear una nueva fuente de flujo continuo mediante fuentes de autoservicio, primero debe coordinarse con Adobe, solicitar un repositorio Git privado y alinearse con Adobe en los detalles relacionados con la etiqueta, descripción, categoría e icono de la fuente.

Una vez proporcionado, debe estructurar el repositorio Git privado de esta manera:

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
| {your_source} | El nombre de su origen. Esta carpeta debe contener todos los artefactos relacionados con su origen, dentro de su repositorio Git privado. | `medallia` |
| {your_source}-category.txt | Categoría a la que pertenece el origen, con formato de archivo de texto. **Nota**: Si cree que su fuente no se ajusta a ninguna de las categorías anteriores, póngase en contacto con su representante de Adobe para discutir. | `medallia-category.txt` Dentro del archivo, especifique la categoría de su fuente, como: `streaming`. |
| {your_source}-description.txt | Breve descripción de la fuente. | [!DNL Medallia] es una fuente de automatización de marketing que puede utilizar para [!DNL Medallia] datos al Experience Platform. |
| {your_source}-icon.svg | La imagen que se utilizará para representar el origen en el catálogo de fuentes de Experience Platform. Este icono debe ser un archivo de SVG. |
| {your_source}-label.txt | Nombre del origen tal como debería aparecer en el catálogo de orígenes de Experience Platform. | Medallia |
| {your_source}-connectionSpec.json | Archivo JSON que contiene la especificación de conexión del origen. Inicialmente, este archivo no es necesario, ya que se rellenará la especificación de conexión al completar esta guía. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Durante el periodo de prueba de la especificación de conexión, en lugar de valores clave, puede utilizar `text` en la especificación de conexión.

Una vez añadidos los archivos necesarios al repositorio Git privado, debe crear una solicitud de extracción (PR) para que el Adobe la revise. Cuando se apruebe y fusione su PR, se le proporcionará un ID que se puede utilizar para que la especificación de conexión haga referencia a la etiqueta, la descripción y el icono de su fuente.

A continuación, siga los pasos descritos a continuación para configurar la especificación de conexión. Para obtener instrucciones adicionales sobre las diferentes funcionalidades que puede agregar a su origen, como programación avanzada, esquema personalizado o diferentes tipos de paginación, consulte la guía sobre [configuración de especificaciones de origen](../config/sourcespec.md).

## Copiar plantilla de especificación de conexión

Una vez que haya recopilado los artefactos necesarios, copie y pegue la plantilla de especificación de conexión siguiente en el editor de texto de su elección y, a continuación, actualice los atributos entre corchetes `{}` con información relevante para su fuente específica.

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

Una especificación de conexión se puede dividir en dos partes distintas: las especificaciones de origen y las especificaciones de exploración.

Consulte los siguientes documentos para obtener más información sobre las secciones de una especificación de conexión:

* [Configuración de la especificación de origen](../config/sourcespec.md)
* [Configuración de la especificación de exploración](../config/explorespec.md)

Con la información de especificación actualizada, puede enviar la nueva especificación de conexión realizando una solicitud de POST a `/connectionSpecs` punto final del [!DNL Flow Service] API.

**Formato de API**

```http
POST /connectionSpecs
```

**Solicitud**

La siguiente solicitud es un ejemplo de una especificación de conexión totalmente creada para una fuente de flujo continuo:

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

Una respuesta correcta devuelve la especificación de conexión recién creada, incluida su variable única `id`.

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

Ahora que ha creado una nueva especificación de conexión, debe agregar su ID de especificación de conexión correspondiente a una especificación de flujo existente. Consulte el tutorial sobre [actualización de especificaciones de flujo](./update-flow-specs.md) para obtener más información.

Para realizar modificaciones en la especificación de conexión que ha creado, consulte el tutorial sobre [actualización de especificaciones de conexión](./update-connection-specs.md).
