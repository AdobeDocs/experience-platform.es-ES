---
keywords: Experience Platform;inicio;temas populares;conformidad con el uso de los datos;aplicación;cumplimiento de normas del uso de datos;servicio de segmentación;segmentación;segmentación;
solution: Experience Platform
title: Aplicar el cumplimiento de uso de datos a un segmento de audiencia mediante API
topic-legacy: tutorial
type: Tutorial
description: Este tutorial trata los pasos para aplicar el cumplimiento de los estándares de uso de datos para segmentos de audiencia del perfil del cliente en tiempo real que utilizan API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 1%

---

# Aplique el cumplimiento de los estándares de uso de datos para un segmento de audiencia que utilice API

Este tutorial trata los pasos para aplicar el cumplimiento de las normas de uso de datos para segmentos de audiencia [!DNL Real-time Customer Profile] que utilizan API.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):  [!DNL Real-time Customer Profile] es un almacén de entidades de búsqueda genérico y se utiliza para administrar  [!DNL Experience Data Model (XDM)] datos en  [!DNL Platform]. El perfil combina datos en varios recursos de datos empresariales y proporciona acceso a esos datos en una presentación unificada.
   - [Combinar directivas](../../profile/api/merge-policies.md): Reglas utilizadas por  [!DNL Real-time Customer Profile] para determinar qué datos se pueden combinar en una vista unificada bajo ciertas condiciones. Las directivas de combinación se pueden configurar para [!DNL Data Governance] fines.
- [[!DNL Segmentation]](../home.md): Cómo  [!DNL Real-time Customer Profile] divide un grupo grande de personas incluidas en el almacén de perfiles en grupos más pequeños que comparten características similares y que responderán de manera similar a las estrategias de marketing.
- [[!DNL Data Governance]](../../data-governance/home.md):  [!DNL Data Governance] proporciona la infraestructura para el etiquetado y la aplicación del uso de los datos, utilizando los siguientes componentes:
   - [Etiquetas](../../data-governance/labels/user-guide.md) de uso de datos: Etiquetas utilizadas para describir conjuntos de datos y campos en términos del nivel de sensibilidad con el que gestionar sus datos respectivos.
   - [Políticas](../../data-governance/policies/overview.md) de uso de datos: Configuraciones que indican qué acciones de marketing se permiten en datos categorizados por etiquetas de uso de datos concretas.
   - [Aplicación de políticas](../../data-governance/enforcement/overview.md): Permite aplicar políticas de uso de datos e impedir operaciones de datos que constituyan infracciones de políticas.
- [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente a las API [!DNL Platform] .

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Buscar una directiva de combinación para una definición de segmento {#merge-policy}

Este flujo de trabajo comienza accediendo a un segmento de audiencia conocido. Los segmentos que están habilitados para su uso en [!DNL Real-time Customer Profile] contienen un ID de política de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre qué conjuntos de datos se incluyen en el segmento, que a su vez contienen cualquier etiqueta de uso de datos aplicable.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrgId": "{IMS_ORG}",
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
| `mergePolicyId` | ID de la directiva de combinación utilizada para la definición del segmento. Se utilizará en el siguiente paso. |

## Busque los conjuntos de datos de origen de la directiva de combinación {#datasets}

Las políticas de combinación contienen información sobre sus conjuntos de datos de origen, que a su vez contienen etiquetas de uso de datos. Puede buscar los detalles de una directiva de combinación proporcionando el ID de la directiva de combinación en una solicitud de GET a la API [!DNL Profile]. Puede encontrar más información sobre las políticas de combinación en la [guía de extremo de directivas de combinación](../../profile/api/merge-policies.md).

**Formato de API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID de la política de combinación obtenida en el [paso anterior](#merge-policy). |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
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
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schema.name` | Nombre del esquema asociado a la política de combinación. |
| `attributeMerge.type` | Tipo de configuración de prioridad de datos para la directiva de combinación. Si el valor es `dataSetPrecedence`, los conjuntos de datos asociados con esta política de combinación se enumeran en `attributeMerge > data > order`. Si el valor es `timestampOrdered`, la directiva de combinación utiliza todos los conjuntos de datos asociados con el esquema al que se hace referencia en `schema.name`. |
| `attributeMerge.data.order` | Si `attributeMerge.type` es `dataSetPrecedence`, este atributo será una matriz que contenga los ID de los conjuntos de datos utilizados por esta directiva de combinación. Estos ID se utilizan en el paso siguiente. |

## Evaluar conjuntos de datos para infracciones de políticas

>[!NOTE]
>
> En este paso se supone que tiene al menos una política de uso de datos activa que impide que se realicen acciones de marketing específicas en datos que contengan determinadas etiquetas. Si no tiene ninguna política de uso aplicable para los conjuntos de datos que se están evaluando, siga el [tutorial de creación de directivas](../../data-governance/policies/create.md) para crear uno antes de continuar con este paso.

Una vez que haya obtenido los ID de los conjuntos de datos de origen de la directiva de combinación, puede utilizar la [API del servicio de directiva](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) para evaluar esos conjuntos de datos con acciones de marketing específicas a fin de comprobar si hay infracciones de la directiva de uso de datos.

Para evaluar los conjuntos de datos, debe proporcionar el nombre de la acción de marketing en la ruta de una solicitud de POST, al mismo tiempo que proporciona los ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada con la política de uso de datos por la que está evaluando los conjuntos de datos. Dependiendo de si la directiva fue definida por Adobe o su organización, debe utilizar `/marketingActions/core` o `/marketingActions/custom`, respectivamente. |

**Solicitud**

La siguiente solicitud prueba la acción de marketing `exportToThirdParty` con los conjuntos de datos obtenidos en el [paso anterior](#datasets). La carga útil de la solicitud es una matriz que contiene los ID de cada conjunto de datos.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se está definiendo. Para este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityID` | Cada elemento de la matriz de carga útil debe proporcionar el ID único para un conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve el URI para la acción de marketing, las etiquetas de uso de datos recopiladas de los conjuntos de datos proporcionados y una lista de cualquier política de uso de datos que se haya infringido como resultado de probar la acción con esas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz `violatedPolicies`, lo que indica que la acción de marketing activó una infracción de directiva.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
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
      "imsOrg": "{IMS_ORG}",
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
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de campo que se encontraron en cada uno. |
| `violatedPolicies` | Una matriz que enumera todas las políticas de uso de datos que se infringieron al probar la acción de marketing (especificada en `marketingActionRef`) en relación con el `duleLabels` proporcionado. |

Con los datos devueltos en la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente infracciones de directiva cuando se produzcan.

## Filtrar campos de datos

Si el segmento de audiencia no supera la evaluación, puede ajustar los datos incluidos en el segmento mediante uno de los dos métodos descritos a continuación.

### Actualizar la directiva de combinación de la definición del segmento

Al actualizar la política de combinación de una definición de segmento, se ajustarán los conjuntos de datos y campos que se incluirán cuando se ejecute el trabajo del segmento. Consulte la sección [actualización de una política de combinación existente](../../profile/api/merge-policies.md#update) en el tutorial de la política de combinación de API para obtener más información.

### Restringir campos de datos específicos al exportar el segmento

Al exportar un segmento a un conjunto de datos mediante la API [!DNL Segmentation] , puede filtrar los datos que se incluyen en la exportación utilizando el parámetro `fields` . Los campos de datos agregados a este parámetro se incluirán en la exportación, mientras que los demás campos de datos se excluirán.

Considere un segmento con campos de datos llamados &quot;A&quot;, &quot;B&quot; y &quot;C&quot;. Si solo desea exportar el campo &quot;C&quot;, el parámetro `fields` contendrá el campo &quot;C&quot; solo. Al hacerlo, los campos &quot;A&quot; y &quot;B&quot; se excluirían al exportar el segmento.

Consulte la sección sobre [exportación de un segmento](./evaluate-a-segment.md#export) en el tutorial de segmentación para obtener más información.

## Pasos siguientes

Al seguir este tutorial, ha buscado las etiquetas de uso de datos asociadas con un segmento de audiencia y las ha probado para detectar infracciones de políticas en acciones de marketing específicas. Para obtener más información sobre [!DNL Data Governance] en [!DNL Experience Platform], lea la descripción general de [[!DNL Data Governance]](../../data-governance/home.md).
