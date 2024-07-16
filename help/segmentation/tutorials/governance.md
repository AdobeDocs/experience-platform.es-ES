---
solution: Experience Platform
title: Aplicar el cumplimiento de uso de datos para un segmento de audiencia mediante API
type: Tutorial
description: Este tutorial cubre los pasos para aplicar definiciones de segmentos conformes con el uso de datos mediante API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 6%

---

# Aplicar el cumplimiento del uso de datos para una definición de segmento mediante API

Este tutorial cubre los pasos para aplicar el cumplimiento del uso de datos para definiciones de segmentos mediante API.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] es un almacén de entidades de búsqueda genérico y se usa para administrar [!DNL Experience Data Model (XDM)] datos en [!DNL Platform]. El perfil combina datos en varios recursos de datos empresariales y proporciona acceso a esos datos en una presentación unificada.
   - [Políticas de combinación](../../profile/api/merge-policies.md): Reglas utilizadas por [!DNL Real-Time Customer Profile] para determinar qué datos se pueden combinar en una vista unificada en ciertas condiciones. Las políticas de combinación se pueden configurar para fines de control de datos.
- [[!DNL Segmentation]](../home.md): cómo [!DNL Real-Time Customer Profile] divide un grupo grande de individuos contenidos en el almacén de perfiles en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de marketing.
- [Control de datos](../../data-governance/home.md): Control de datos proporciona la infraestructura para el etiquetado y la aplicación del uso de datos, utilizando los siguientes componentes:
   - [Etiquetas de uso de datos](../../data-governance/labels/user-guide.md): etiquetas utilizadas para describir conjuntos de datos y campos en términos del nivel de confidencialidad con el que se van a administrar sus datos respectivos.
   - [Políticas de uso de datos](../../data-governance/policies/overview.md): configuraciones que indican qué acciones de marketing se permiten en datos clasificados por etiquetas de uso de datos concretas.
   - [Aplicación de directivas](../../data-governance/enforcement/overview.md): permite aplicar directivas de uso de datos y evitar operaciones de datos que constituyen infracciones de directivas.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para realizar llamadas correctamente a las API de [!DNL Platform].

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Búsqueda de una política de combinación para una definición de segmento {#merge-policy}

Este flujo de trabajo comienza accediendo a una definición de segmento conocida. Las definiciones de segmento habilitadas para usarse en [!DNL Real-Time Customer Profile] contienen un identificador de política de combinación dentro de su definición de segmento. Esta política de combinación contiene información sobre qué conjuntos de datos se van a incluir en la definición del segmento, que a su vez contienen cualquier etiqueta de uso de datos aplicable.

Con la API [!DNL Segmentation], puede buscar una definición de segmento por su ID para encontrar su política de combinación asociada.

**Formato de API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | El ID de la definición del segmento que desea buscar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición del segmento.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `mergePolicyId` | El ID de la política de combinación utilizada para la definición del segmento. Se utilizará en el siguiente paso. |

## Buscar los conjuntos de datos de origen de la política de combinación {#datasets}

Las políticas de combinación contienen información sobre sus conjuntos de datos de origen, que a su vez contienen etiquetas de uso de datos. Puede buscar los detalles de una política de combinación proporcionando el ID de la política de combinación en una solicitud de GET a la API [!DNL Profile]. Encontrará más información sobre las políticas de combinación en la [guía de extremo de políticas de combinación](../../profile/api/merge-policies.md).

**Formato de API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | El identificador de la política de combinación obtenida en el [paso anterior](#merge-policy). |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schema.name` | Nombre del esquema asociado a la política de combinación. |
| `attributeMerge.type` | Tipo de configuración de prioridad de datos para la política de combinación. Si el valor es `dataSetPrecedence`, los conjuntos de datos asociados con esta política de combinación se enumeran en `attributeMerge > data > order`. Si el valor es `timestampOrdered`, la política de combinación utiliza todos los conjuntos de datos asociados con el esquema al que se hace referencia en `schema.name`. |
| `attributeMerge.data.order` | Si `attributeMerge.type` es `dataSetPrecedence`, este atributo será una matriz que contenga los identificadores de los conjuntos de datos utilizados por esta política de combinación. Estos ID se utilizan en el paso siguiente. |

## Evaluar conjuntos de datos para infracciones de directivas

>[!NOTE]
>
> En este paso se da por hecho que hay al menos una directiva de uso de datos activa que impide que se realicen acciones de marketing específicas en datos que contengan determinadas etiquetas. Si no tiene ninguna política de uso aplicable para los conjuntos de datos que se están evaluando, siga el [tutorial de creación de políticas](../../data-governance/policies/create.md) para crear una antes de continuar con este paso.

Una vez que haya obtenido los ID de los conjuntos de datos de origen de la política de combinación, puede usar la [API del servicio de políticas](https://www.adobe.io/experience-platform-apis/references/policy-service/) para evaluar esos conjuntos de datos con respecto a acciones de marketing específicas a fin de comprobar violaciones de la política de uso de datos.

Para evaluar los conjuntos de datos, debe proporcionar el nombre de la acción de marketing en la ruta de una solicitud de POST, a la vez que proporciona los ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | El nombre de la acción de marketing asociada con la política de uso de datos por la que está evaluando los conjuntos de datos. Dependiendo de si la directiva fue definida por el Adobe o por su organización, debe usar `/marketingActions/core` o `/marketingActions/custom`, respectivamente. |

**Solicitud**

La siguiente solicitud prueba la acción de marketing `exportToThirdParty` con los conjuntos de datos obtenidos en el [paso anterior](#datasets). La carga útil solicitada es una matriz que contiene los ID de cada conjunto de datos.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se define. Para este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityID` | Cada elemento de la matriz de carga útil debe proporcionar el ID único para un conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve el URI de la acción de marketing, las etiquetas de uso de datos recopiladas de los conjuntos de datos proporcionados y una lista de cualquier política de uso de datos que se haya violado como resultado de la prueba de la acción contra esas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz `violatedPolicies`, lo que indica que la acción de marketing desencadenó una infracción de directiva.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{ORG_ID}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `duleLabels` | Una lista de etiquetas de uso de datos extraídas de los conjuntos de datos proporcionados. |
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de nivel de campo que se encontraron en cada uno. |
| `violatedPolicies` | Una matriz que enumera todas las directivas de uso de datos que se violaron al probar la acción de marketing (especificada en `marketingActionRef`) con el `duleLabels` proporcionado. |

Con los datos devueltos en la respuesta de API, puede configurar protocolos en su aplicación de experiencia para aplicar correctamente infracciones de directivas cuando se producen.

## Filtrar campos de datos

Si la definición del segmento no supera la evaluación, puede ajustar los datos incluidos en la definición del segmento mediante uno de los dos métodos descritos a continuación.

### Actualizar la política de combinación de la definición del segmento

Al actualizar la política de combinación de una definición de segmento, se ajustarán los conjuntos de datos y los campos que se incluirán cuando se ejecute el trabajo de segmentación. Consulte la sección sobre [actualización de una política de combinación existente](../../profile/api/merge-policies.md#update) en el tutorial de la política de combinación de API para obtener más información.

### Restringir campos de datos específicos al exportar la definición del segmento

Al exportar una definición de segmento a un conjunto de datos mediante la API [!DNL Segmentation], puede filtrar los datos que se incluyen en la exportación mediante el parámetro `fields`. Cualquier campo de datos añadido a este parámetro se incluirá en la exportación, mientras que el resto de campos de datos se excluirán.

Imagine una definición de segmento que tenga campos de datos llamados &quot;A&quot;, &quot;B&quot; y &quot;C&quot;. Si solo desea exportar el campo &quot;C&quot;, el parámetro `fields` contendría el campo &quot;C&quot; solamente. Al hacerlo, los campos &quot;A&quot; y &quot;B&quot; se excluirían al exportar la definición del segmento.

Consulte la sección sobre [exportación de una definición de segmento](./evaluate-a-segment.md#export) en el tutorial de segmentación para obtener más información.

## Pasos siguientes

Al seguir este tutorial, ha buscado las etiquetas de uso de datos asociadas a una definición de segmento y las ha probado para detectar infracciones de directivas en acciones de marketing específicas. Para obtener más información sobre la administración de datos en [!DNL Experience Platform], lea la descripción general de [Administración de datos](../../data-governance/home.md).
