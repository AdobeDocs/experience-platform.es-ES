---
title: Punto final de API de cuota
description: El extremo /quotas de la API de higiene de datos le permite supervisar el uso de la higiene de los datos en relación con los límites de cuota mensual de la organización para cada tipo de trabajo.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 3%

---

# Punto final de cuota

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos en Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

La variable `/quota` en la API de higiene de datos le permite supervisar el uso de higiene de datos en relación con los límites de cuota de su organización para cada tipo de trabajo.

Las cuotas se aplican para cada tipo de trabajo de higiene de datos de las siguientes maneras:

* Las eliminaciones y actualizaciones de registros se limitan a un determinado número de solicitudes cada mes.
* Las caducidades de los conjuntos de datos tienen un límite fijo para el número de trabajos activos simultáneamente, independientemente de cuándo se ejecutarán las caducidades.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [información general](./overview.md) para obtener la siguiente información:

* Enlaces a documentación relacionada
* Una guía para leer el ejemplo de llamadas de API en este documento
* Información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform

## Enumerar cuotas {#list}

Puede ver la información de cuota de su organización realizando una solicitud de GET al `/quota` punto final.

**Formato de API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUOTA_TYPE}` | Un parámetro de consulta opcional que especifica el tipo de cuota que se recuperará. Si no `quotaType` se proporciona, todos los valores de cuota se devuelven en la respuesta de API. Los valores de tipo aceptados incluyen:<ul><li>`expirationDatasetQuota`: Caducidad de conjuntos de datos</li><li>`deleteIdentityWorkOrderDatasetQuota`: Eliminar registros</li><li>`fieldUpdateWorkOrderDatasetQuota`: Registrar actualizaciones</li></ul> |

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

Una respuesta correcta devuelve los detalles de sus cuotas de higiene de datos.

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
| `quotas` | Muestra la información de cuota de cada tipo de trabajo de higiene de datos. Cada objeto de cuota contiene las siguientes propiedades:<ul><li>`name`: Tipo de trabajo de higiene de datos:<ul><li>`expirationDatasetQuota`: Caducidad de conjuntos de datos</li><li>`deleteIdentityWorkOrderDatasetQuota`: Eliminar registros</li></ul></li><li>`description`: Descripción del tipo de trabajo de higiene de datos.</li><li>`consumed`: Número de trabajos de este tipo ejecutados en el periodo mensual actual.</li><li>`quota`: Límite de cuota para este tipo de trabajo. Para las eliminaciones y actualizaciones de registros, esto representa el número de trabajos que se pueden ejecutar para cada período mensual. Para las caducidades de los conjuntos de datos, esto representa el número de trabajos que pueden estar activos simultáneamente en un momento determinado.</li></ul> |

{style=&quot;table-layout:auto&quot;}
