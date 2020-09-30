---
keywords: Experience Platform;home;popular topics;data usage compliance;enforce;enforce data usage compliance;Segmentation Service;segmentation;Segmentation;
solution: Experience Platform
title: Aplicar la conformidad de uso de datos para segmentos de audiencia
topic: tutorial
type: Tutorial
description: En este tutorial se explican los pasos para reforzar la compatibilidad del uso de datos con los segmentos de audiencia de Perfil del cliente en tiempo real mediante API.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 1%

---


# Aplicar la compatibilidad con el uso de datos para un segmento de audiencia mediante API

En este tutorial se explican los pasos para aplicar la compatibilidad con el uso de datos a los segmentos de [!DNL Real-time Customer Profile] audiencia que utilizan API.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de [!DNL Adobe Experience Platform]:

- [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): [!DNL Real-time Customer Profile] es un almacén de entidades de búsqueda genérico y se utiliza para administrar datos [!DNL Experience Data Model] (XDM) dentro de [!DNL Platform]. Perfil combina datos en varios recursos de datos empresariales y proporciona acceso a esos datos en una presentación unificada.
   - [Combinar directivas](../../profile/api/merge-policies.md): Reglas utilizadas por [!DNL Real-time Customer Profile] para determinar qué datos se pueden combinar en una vista unificada bajo ciertas condiciones. Las directivas de combinación se pueden configurar para [!DNL Data Governance] fines específicos.
- [[!Segmentación DNL]](../home.md): Cómo [!DNL Real-time Customer Profile] divide un gran grupo de individuos contenidos en el almacén de perfiles en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de marketing.
- [[!Administración de datos DNL]](../../data-governance/home.md): [!DNL Data Governance] proporciona la infraestructura para el etiquetado y la aplicación del uso de datos mediante los siguientes componentes:
   - [Etiquetas](../../data-governance/labels/user-guide.md)de uso de datos: Etiquetas utilizadas para describir conjuntos de datos y campos en términos del nivel de sensibilidad con el que tratar sus datos respectivos.
   - [Directivas](../../data-governance/policies/overview.md)de uso de datos: Configuraciones que indican qué acciones de mercadotecnia se permiten en los datos clasificados por etiquetas de uso de datos particulares.
   - [Aplicación](../../data-governance/enforcement/overview.md)de políticas: Permite aplicar políticas de uso de datos y evitar operaciones de datos que constituyan infracciones de políticas.
- [Simuladores](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a las [!DNL Platform] API de forma satisfactoria.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Buscar una directiva de combinación para una definición de segmento {#merge-policy}

Este flujo de trabajo comienza por acceder a un segmento de audiencia conocido. Los segmentos que están habilitados para utilizarse en [!DNL Real-time Customer Profile] contienen un ID de directiva de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre los conjuntos de datos que se deben incluir en el segmento, que a su vez contienen las etiquetas de uso de datos aplicables.

Con la API, puede buscar una definición de segmento por su ID para encontrar la directiva de combinación asociada. [!DNL Segmentation]

**Formato API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID de la definición de segmento que desea buscar. |

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
| `mergePolicyId` | ID de la directiva de combinación utilizada para la definición del segmento. Esto se utilizará en el paso siguiente. |

## Buscar los conjuntos de datos de origen de la directiva de combinación {#datasets}

Las políticas de combinación contienen información sobre sus conjuntos de datos de origen, que a su vez contienen etiquetas de uso de datos. Puede buscar los detalles de una directiva de combinación proporcionando el ID de directiva de combinación en una solicitud de GET a la [!DNL Profile] API. Encontrará más información sobre las directivas de combinación en la guía de extremo de directivas de [combinación](../../profile/api/merge-policies.md).

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID de la directiva de combinación obtenida en el paso [](#merge-policy)anterior. |

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
| `schema.name` | Nombre del esquema asociado a la directiva de combinación. |
| `attributeMerge.type` | Tipo de configuración de prioridad de datos para la directiva de combinación. Si el valor es `dataSetPrecedence`, los conjuntos de datos asociados con esta directiva de combinación se enumeran en `attributeMerge > data > order`. Si el valor es `timestampOrdered`, la directiva de combinación utiliza todos los conjuntos de datos asociados con el esquema al que se hace referencia en `schema.name` . |
| `attributeMerge.data.order` | Si `attributeMerge.type` es `dataSetPrecedence`, este atributo será una matriz que contenga los ID de los conjuntos de datos utilizados por esta directiva de combinación. Estos ID se utilizan en el paso siguiente. |

## Evaluar conjuntos de datos para violaciones de políticas

>[!NOTE]
>
> En este paso se asume que tiene al menos una directiva de uso de datos activa que impide que se realicen acciones de marketing específicas en los datos que contienen determinadas etiquetas. Si no tiene ninguna política de uso aplicable para los conjuntos de datos que se están evaluando, siga el tutorial [de creación de](../../data-governance/policies/create.md) directivas para crear uno antes de continuar con este paso.

Una vez que haya obtenido los ID de los conjuntos de datos de origen de la directiva de combinación, puede utilizar la API [de servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) directivas para evaluar dichos conjuntos de datos en relación con acciones de marketing específicas a fin de comprobar si hay violaciones de directivas de uso de datos.

Para evaluar los conjuntos de datos, debe proporcionar el nombre de la acción de mercadotecnia en la ruta de una solicitud de POST, mientras proporciona los ID de conjuntos de datos dentro del cuerpo de la solicitud, como se muestra en el ejemplo siguiente.

**Formato API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing asociada con la directiva de uso de datos por la que está evaluando los conjuntos de datos. Según si la política fue definida por Adobe o por su organización, debe usar `/marketingActions/core` o `/marketingActions/custom`, respectivamente. |

**Solicitud**

La siguiente solicitud prueba la acción de mercadotecnia con los conjuntos de datos obtenidos en el paso `exportToThirdParty` [anterior](#datasets). La carga útil de la solicitud es una matriz que contiene los ID de cada conjunto de datos.

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
| `entityType` | Cada elemento de la matriz de carga útil debe indicar el tipo de entidad que se está definiendo. En este caso de uso, el valor siempre será &quot;dataSet&quot;. |
| `entityID` | Cada elemento de la matriz de carga útil debe proporcionar la ID única para un conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve el URI de la acción de marketing, las etiquetas de uso de datos recopiladas de los conjuntos de datos proporcionados y una lista de cualquier directiva de uso de datos que se haya infringido como resultado de probar la acción con dichas etiquetas. En este ejemplo, la directiva &quot;Exportar datos a terceros&quot; se muestra en la matriz, lo que indica que la acción de marketing desencadenó una infracción de la directiva. `violatedPolicies`

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
| `duleLabels` | Una lista de las etiquetas de uso de datos que se extrajeron de los conjuntos de datos proporcionados. |
| `discoveredLabels` | Una lista de los conjuntos de datos que se proporcionaron en la carga útil de la solicitud, que muestra las etiquetas de nivel de conjunto de datos y de campo que se encontraron en cada una. |
| `violatedPolicies` | Una matriz que enumera las directivas de uso de datos que se infringieron al probar la acción de mercadotecnia (especificada en `marketingActionRef`) en comparación con la proporcionada `duleLabels`. |

Con los datos devueltos en la respuesta de API, puede configurar protocolos dentro de la aplicación de experiencia para aplicar correctamente las infracciones de directiva cuando se produzcan.

## Filtrar campos de datos

Si el segmento de audiencia no pasa la evaluación, puede ajustar los datos incluidos en el segmento a través de uno de los dos métodos descritos a continuación.

### Actualizar la directiva de combinación de la definición del segmento

Al actualizar la directiva de combinación de una definición de segmento, se ajustarán los conjuntos de datos y los campos que se incluirán cuando se ejecute el trabajo de segmento. Consulte la sección sobre la [actualización de una directiva](../../profile/api/merge-policies.md#update) de combinación existente en el tutorial de políticas de combinación de API para obtener más información.

### Restringir campos de datos específicos al exportar el segmento

Al exportar un segmento a un conjunto de datos mediante la [!DNL Segmentation] API, puede filtrar los datos incluidos en la exportación mediante el `fields` parámetro . Todos los campos de datos agregados a este parámetro se incluirán en la exportación, mientras que todos los demás campos de datos se excluirán.

Considere un segmento que tiene campos de datos con los nombres &quot;A&quot;, &quot;B&quot; y &quot;C&quot;. Si sólo desea exportar el campo &quot;C&quot;, el `fields` parámetro contendrá sólo el campo &quot;C&quot;. Al realizar esto, los campos &quot;A&quot; y &quot;B&quot; se excluirían al exportar el segmento.

Consulte la sección sobre [exportación de un segmento](./evaluate-a-segment.md#export) en el tutorial de segmentación para obtener más información.

## Pasos siguientes

Siguiendo este tutorial, ha buscado las etiquetas de uso de datos asociadas con un segmento de audiencia y las ha probado para detectar infracciones de políticas en relación con acciones de marketing específicas. Para más información sobre [!DNL Data Governance] en [!DNL Experience Platform], lea la descripción general de [[!DNL Data Governance]](../../data-governance/home.md).
