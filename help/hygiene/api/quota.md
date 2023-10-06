---
title: Punto final de API de cuota
description: El punto final /quota en la API de higiene de datos le permite supervisar el uso de la administración avanzada del ciclo vital de datos con respecto a los límites de cuotas mensuales de su organización para cada tipo de trabajo.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# Punto final de cuota

El `/quota` El punto final de la API de higiene de datos le permite supervisar el uso de la administración avanzada del ciclo vital de datos con respecto a los límites de cuotas de su organización para cada tipo de trabajo.

Las cuotas se aplican a cada tipo de trabajo del ciclo vital de datos de las siguientes maneras:

* Las eliminaciones y actualizaciones de registros se limitan a un determinado número de solicitudes cada mes.
* La caducidad de los conjuntos de datos tiene un límite plano para el número de trabajos activos simultáneamente, independientemente de cuándo se ejecutará la caducidad.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, consulte la [descripción general](./overview.md) para obtener la siguiente información:

* Vínculos a documentación relacionada
* Una guía para leer las llamadas de API de ejemplo en este documento
* Información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform

## Enumerar cuotas {#list}

Puede ver la información de cuotas de su organización realizando una solicitud de GET a la `/quota` punto final.

**Formato de API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUOTA_TYPE}` | Parámetro de consulta opcional que especifica el tipo de cuota que se va a recuperar. Si no `quotaType` Si se proporciona el parámetro, todos los valores de cuota se devuelven en la respuesta de la API. Los valores de tipo aceptados incluyen:<ul><li>`expirationDatasetQuota`: Caducidad del conjunto de datos</li><li>`deleteIdentityWorkOrderDatasetQuota`: Eliminaciones de registros</li><li>`fieldUpdateWorkOrderDatasetQuota`: Actualizaciones de registros</li></ul> |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de las cuotas del ciclo vital de datos.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `quotas` | Muestra la información de cuota de cada tipo de trabajo del ciclo vital de datos. Cada objeto de cuota contiene las siguientes propiedades:<ul><li>`name`: el tipo de trabajo del ciclo vital de datos:<ul><li>`expirationDatasetQuota`: Caducidad del conjunto de datos</li><li>`deleteIdentityWorkOrderDatasetQuota`: Eliminaciones de registros</li></ul></li><li>`description`: una descripción del tipo de trabajo del ciclo vital de datos.</li><li>`consumed`: el número de trabajos de este tipo ejecutados en el periodo mensual actual.</li><li>`quota`: límite de cuota para este tipo de trabajo. Para las eliminaciones y actualizaciones de registros, esto representa el número de trabajos que se pueden ejecutar para cada período mensual. Para las caducidades del conjunto de datos, representa el número de trabajos que pueden estar activos simultáneamente en un momento determinado.</li></ul> |

{style="table-layout:auto"}
