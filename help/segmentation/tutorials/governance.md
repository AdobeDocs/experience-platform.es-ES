---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aplicar la conformidad de uso de datos para segmentos de audiencia
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# Aplicar la compatibilidad con el uso de datos para un segmento de audiencia mediante API

En este tutorial se explican los pasos para reforzar la compatibilidad del uso de datos con los segmentos de audiencia de Perfil del cliente en tiempo real mediante API.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Perfil](../../profile/home.md)del cliente en tiempo real: Perfil del cliente en tiempo real es un almacén de entidades de búsqueda genérico y se utiliza para administrar datos del modelo de datos de experiencia (XDM) en la plataforma. Perfil combina datos en varios recursos de datos empresariales y proporciona acceso a esos datos en una presentación unificada.
   - [Combinar directivas](../../profile/api/merge-policies.md): Reglas utilizadas por el Perfil del cliente en tiempo real para determinar qué datos se pueden combinar en una vista unificada bajo ciertas condiciones. Las directivas de combinación se pueden configurar para fines de administración de datos.
- [Segmentación](../home.md): Cómo el Perfil del cliente en tiempo real divide un grupo grande de individuos contenidos en el almacén de perfiles en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.
- [Administración](../../data-governance/home.md)de datos: La Administración de datos proporciona la infraestructura para el etiquetado y la aplicación del uso de datos (DULE), utilizando los siguientes componentes:
   - [Etiquetas](../../data-governance/labels/user-guide.md)de uso de datos: Etiquetas utilizadas para describir conjuntos de datos y campos en términos del nivel de sensibilidad con el que tratar sus datos respectivos.
   - [Directivas](../../data-governance/api/getting-started.md)de uso de datos: Configuraciones que indican qué acciones de mercadotecnia se permiten en los datos clasificados por etiquetas de uso de datos particulares.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

> [!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Buscar una directiva de combinación para una definición de segmento

Este flujo de trabajo comienza por acceder a un segmento de audiencia conocido. Los segmentos que están habilitados para su uso en el Perfil del cliente en tiempo real contienen un ID de directiva de combinación dentro de su definición de segmento. Esta directiva de combinación contiene información sobre los conjuntos de datos que se deben incluir en el segmento, que a su vez contienen las etiquetas de uso de datos aplicables.

Con la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentación, puede buscar una definición de segmento por su ID para encontrar la directiva de combinación asociada.

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

## Buscar los conjuntos de datos de origen de la directiva de combinación

Las políticas de combinación contienen información sobre sus conjuntos de datos de origen, que a su vez contienen etiquetas DULE. Puede buscar los detalles de una directiva de combinación proporcionando el ID de directiva de combinación en una solicitud GET a la API de Perfil.

**Formato API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID de la directiva de combinación obtenida en el paso [](#lookup-a-merge-policy-for-a-segment-definition)anterior. |

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

## Buscar etiquetas de uso de datos para los conjuntos de datos de origen

Una vez recopilados los ID de los conjuntos de datos de origen de la directiva de combinación, puede utilizar estos ID para buscar las etiquetas de uso de datos configuradas para los propios conjuntos de datos y los campos de datos específicos contenidos en ellos.

La siguiente llamada a la API [del servicio de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catálogo recupera las etiquetas de uso de datos asociadas con un único conjunto de datos proporcionando su ID en la ruta de solicitud:

**Formato API**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{DATASET_ID}` | ID del conjunto de datos cuyas etiquetas de uso de datos desea buscar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de las etiquetas de uso de datos asociadas con el conjunto de datos en su conjunto, así como cualquier campo de datos en particular asociado con el esquema de origen.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `dataset` | Objeto que contiene las etiquetas de uso de datos aplicadas al conjunto de datos en su conjunto. |
| `schemaFields` | Matriz de objetos que representa campos de esquema específicos a los que se les han aplicado etiquetas de uso de datos. |
| `schemaFields.path` | Ruta del campo de esquema cuyas etiquetas de uso de datos aparecen en el mismo objeto. |

## Filtrar campos de datos

> [!NOTE] Este paso es opcional. Si no desea ajustar los datos incluidos en el segmento en función de los resultados del paso anterior de [búsqueda de etiquetas](#lookup-data-usage-labels-for-the-source-datasets)de uso de datos, puede continuar con el paso final de [evaluación de los datos en caso de infracciones](#evaluate-data-for-policy-violations)de políticas.

Si desea ajustar los datos incluidos en el segmento de audiencia, puede hacerlo mediante uno de los dos métodos siguientes:

### Actualizar la directiva de combinación de la definición del segmento

Al actualizar la directiva de combinación de una definición de segmento, se ajustarán los conjuntos de datos y los campos que se incluirán cuando se ejecute el trabajo de segmento. Consulte la sección sobre la [actualización de una directiva](../../profile/api/merge-policies.md) de combinación existente en el tutorial de políticas de combinación para obtener más información.

### Restringir campos de datos específicos al exportar el segmento

Al exportar un segmento a un conjunto de datos mediante la API de Perfil del cliente en tiempo real, puede filtrar los datos incluidos en la exportación mediante el `fields` parámetro . Todos los campos de datos agregados a este parámetro se incluirán en la exportación, mientras que todos los demás campos de datos se excluirán.

Considere un segmento que tiene campos de datos con los nombres &quot;A&quot;, &quot;B&quot; y &quot;C&quot;. Si sólo desea exportar el campo &quot;C&quot;, el `fields` parámetro contendrá sólo el campo &quot;C&quot;. Al realizar esto, los campos &quot;A&quot; y &quot;B&quot; se excluirían al exportar el segmento.

Consulte la sección sobre [exportación de un segmento](./evaluate-a-segment.md#export-a-segment) en el tutorial de segmentación para obtener más información.

## Evaluar datos para infracciones de directivas

Ahora que ha recopilado las etiquetas de uso de datos asociadas con el segmento de audiencia, puede probar estas etiquetas con acciones de marketing para evaluar cualquier infracción de la directiva de uso de datos. Para ver los pasos detallados sobre cómo realizar evaluaciones de políticas mediante la API [del servicio de políticas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE, consulte el documento sobre evaluación [de](../../data-governance/enforcement/overview.md)políticas.

## Pasos siguientes

Siguiendo este tutorial, ha buscado las etiquetas de uso de datos asociadas con un segmento de audiencia y las ha probado para detectar infracciones de políticas en relación con acciones de marketing específicas. Para obtener más información sobre la administración de datos en la plataforma de experiencias, consulte la descripción general [de la administración de](../../data-governance/home.md)datos.