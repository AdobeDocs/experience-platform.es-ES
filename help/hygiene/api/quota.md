---
title: Punto final de API de cuota
description: El punto final /quota en la API de higiene de datos le permite supervisar el uso de la administración avanzada del ciclo de vida de datos con respecto a los límites de cuotas mensuales de su organización para cada tipo de trabajo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# Punto final de cuota

Use el extremo `/quota` en la API de higiene de datos para comprobar el uso y los límites actuales de su organización. Las cuotas varían en función de los derechos, como Privacy and Security Shield o Healthcare Shield.

Supervise el consumo de cuota actual para garantizar el cumplimiento de los límites organizativos para cada tipo de trabajo.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [descripción general](./overview.md) para obtener la siguiente información:

* Vínculos de documentación relacionados
* Cómo leer llamadas de API de muestra
* Encabezados necesarios para las llamadas a la API de Experience Platform

## Cuotas y plazos de procesamiento {#quotas}

Las solicitudes de eliminación de registros están sujetas a cuotas y expectativas de nivel de servicio en función de sus derechos de licencia. Estos límites se aplican a solicitudes de eliminación basadas en la interfaz de usuario y la API.

>[!TIP]
>
>Este documento muestra cómo consultar el uso en relación con los límites basados en derechos. Para obtener una descripción completa de los niveles de cuota, los derechos de eliminación de registros y el comportamiento de SLA, consulte los documentos [eliminación de registros basada en la interfaz de usuario](../ui/record-delete.md#quotas) o [eliminación de registros basada en la API](./workorder.md#quotas).

## Enumerar cuotas {#list}

Puede ver la información de cuota de su organización realizando una petición GET al extremo `/quota`.

**Formato de API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>El consumo de la cuota se restablece diaria y mensualmente el primero de cada mes a las 00:00 GMT.
>
>Solo las solicitudes aceptadas se contabilizan en la cuota. Las órdenes de trabajo rechazadas no reducen su cuota.

| Parámetro | Descripción |
| --- | --- |
| `{QUOTA_TYPE}` | Parámetro de consulta opcional que especifica el tipo de cuota que se va a recuperar. Si no se proporciona ningún parámetro `quotaType`, se devuelven todos los valores de cuota en la respuesta de la API. Los valores aceptados incluyen:<ul><li>`datasetExpirationQuota`: el número de caducidades activas del conjunto de datos y su asignación total.</li><li>`dailyConsumerDeleteIdentitiesQuota`: el número de eliminaciones de registros realizadas hoy y su cuota diaria.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: número de eliminaciones de registros este mes y su cuota mensual.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Propiedad | Descripción |
| -------- | ------- |
| `quotas` | Muestra la información de cuota de cada tipo de trabajo del ciclo vital de datos. Cada objeto de cuota contiene las siguientes propiedades:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | El identificador del tipo de cuota. |
| `description` | Una descripción de los límites de esta cuota. |
| `consumed` | Cantidad de cuota consumida actualmente. La cantidad consumida se restablece el primero del mes a las 00:00 GMT y a las 00:00 GMT para la cuota diaria. |
| `quota` | Asignación máxima de este tipo de cuota para su organización. |
