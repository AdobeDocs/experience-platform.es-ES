---
title: Punto final de API de cuota
description: El punto final /quota en la API de higiene de datos le permite supervisar el uso de la administración avanzada del ciclo de vida de datos con respecto a los límites de cuotas mensuales de su organización para cada tipo de trabajo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---

# Punto final de cuota

El extremo `/quota` de la API de higiene de datos le permite supervisar el uso de la administración avanzada del ciclo de vida de datos en relación con los límites de cuota de su organización para cada tipo de trabajo.

Las cuotas se aplican a cada tipo de trabajo del ciclo vital de datos de las siguientes maneras:

* Las eliminaciones y actualizaciones de registros se limitan a un determinado número de solicitudes cada mes.
* La caducidad de los conjuntos de datos tiene un límite plano para el número de trabajos activos simultáneamente, independientemente de cuándo se ejecutará la caducidad.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [descripción general](./overview.md) para obtener la siguiente información:

* Vínculos a documentación relacionada
* Una guía para leer las llamadas de API de ejemplo en este documento
* Información importante sobre los encabezados necesarios para realizar llamadas a cualquier API de Experience Platform

## Enumerar cuotas {#list}

Puede ver la información de cuota de su organización realizando una solicitud de GET al extremo `/quota`.

**Formato de API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUOTA_TYPE}` | Parámetro de consulta opcional que especifica el tipo de cuota que se va a recuperar. Si no se proporciona ningún parámetro `quotaType`, se devuelven todos los valores de cuota en la respuesta de la API. Los valores de tipo aceptados incluyen:<ul><li>`datasetExpirationQuota`: este objeto muestra el número de caducidades del conjunto de datos activas simultáneamente para su organización y la asignación total de caducidades. </li><li>`dailyConsumerDeleteIdentitiesQuota`: este objeto muestra el número total de solicitudes de eliminación de registros realizadas por su organización hoy y su asignación diaria total.<br>Nota: solo se cuentan las solicitudes aceptadas. Si se rechaza una orden de trabajo porque no supera la validación, esas eliminaciones de identidad no se contabilizan en la cuota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: este objeto muestra el número total de solicitudes de eliminación de registros realizadas por su organización este mes y su asignación mensual total.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: este objeto muestra el número total de solicitudes de actualización de registros realizadas por su organización este mes y su asignación mensual total.</li></ul> |

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
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `quotas` | Muestra la información de cuota de cada tipo de trabajo del ciclo vital de datos. Cada objeto de cuota contiene las siguientes propiedades:<ul><li>`name`: el tipo de trabajo del ciclo vital de datos:<ul><li>`expirationDatasetQuota`: caducidades del conjunto de datos</li><li>`deleteIdentityWorkOrderDatasetQuota`: eliminaciones de registros</li></ul></li><li>`description`: una descripción del tipo de trabajo del ciclo vital de datos.</li><li>`consumed`: número de trabajos de este tipo ejecutados en el período actual. El nombre del objeto indica el período de cuota.</li><li>`quota`: asignación para este tipo de trabajo para su organización. Para las eliminaciones y actualizaciones de registros, la cuota representa el número de trabajos que se pueden ejecutar para cada período mensual. Para las caducidades del conjunto de datos, la cuota representa el número de trabajos que pueden estar activos simultáneamente en un momento determinado.</li></ul> |

{style="table-layout:auto"}
