---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;
title: (Beta) Crear un flujo de ejecución para la ingesta a petición mediante la API de servicio de flujo
description: Este tutorial trata los pasos para crear una ejecución de flujo para la ingesta bajo demanda mediante la API de servicio de flujo
hide: true
hidefromtoc: true
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 24f16e315607a1076ff2efef129d9e97040a9500
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 1%

---

# (Beta) Cree una ejecución de flujo para la ingesta bajo demanda usando la variable [!DNL Flow Service] API

>[!IMPORTANT]
>
>La ingesta a petición está actualmente en fase beta y es posible que su organización no tenga acceso a ella aún. La funcionalidad descrita en esta documentación está sujeta a cambios.

Las ejecuciones de flujo representan una instancia de ejecución de flujo. Por ejemplo, si un flujo está programado para ejecutarse cada hora a las 9:00 AM, 10:00 AM y 11:00 AM, entonces tendría tres instancias de una ejecución de flujo. Las ejecuciones de flujo son específicas de su organización en particular.

La ingesta bajo demanda le permite crear un flujo de trabajo con un flujo de datos determinado. Esto permite a los usuarios crear una ejecución de flujo, basada en parámetros determinados y crear un ciclo de ingesta, sin tokens de servicio.

Este tutorial trata los pasos sobre cómo utilizar la ingesta bajo demanda y crear una ejecución de flujo mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

>[!NOTE]
>
>Para crear una ejecución de flujo, primero debe tener el ID de flujo de un flujo de datos programado para una ingesta única.

Este tutorial requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Creación de una ejecución de flujo para un origen basado en tablas

Para crear un flujo para un origen basado en tablas, realice una solicitud de POST al [!DNL Flow Service] al proporcionar el ID del flujo con el que desea crear la ejecución, así como los valores de las columnas hora de inicio, hora de finalización y delta.

>[!TIP]
>
>Las fuentes basadas en tablas incluyen las siguientes categorías de fuentes: publicidad, análisis, consentimiento y preferencias, CRM, éxito de clientes, base de datos, automatización de marketing, pagos y protocolos.

**Formato de API**

```http
POST /runs/
```

**Solicitud**

La siguiente solicitud crea una ejecución de flujo para el ID de flujo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Solo debe proporcionar la variable `deltaColumn` al crear su primer flujo, ejecute. Después de eso, `deltaColumn` se parpadearán como parte de `copy` transformación en el flujo y será tratada como la fuente de la verdad. Cualquier intento de cambiar la variable `deltaColumn` a través de los parámetros de ejecución de flujo resultarán en un error.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `flowId` | ID del flujo con el que se creará la ejecución de flujo. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.windowEndTime` | Un entero que define la hora de finalización de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.deltaColumn` | La columna delta es necesaria para dividir los datos y separar los nuevos datos introducidos de los datos históricos. |
| `params.deltaColumn.name` | Nombre de la columna delta. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la ejecución de flujo recién creada, incluida su ejecución única `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID de la ejecución del flujo recién creado. Consulte la guía de [recuperación de especificaciones de flujo](../api/collect/database-nosql.md#specs) para obtener más información sobre las especificaciones de ejecución basadas en tablas. |
| `createdAt` | Marca de tiempo Unix que designa cuándo se creó la ejecución del flujo. |
| `updatedAt` | La marca de tiempo unix que designa cuándo se actualizó por última vez la ejecución del flujo. |
| `createdBy` | ID de organización del usuario que creó la ejecución de flujo. |
| `updatedBy` | ID de organización del usuario que actualizó por última vez la ejecución del flujo. |
| `createdClient` | El cliente de aplicación que creó el flujo se ejecuta. |
| `updatedClient` | El cliente de aplicación que actualizó por última vez la ejecución del flujo. |
| `sandboxId` | ID del simulador de pruebas que contiene la ejecución del flujo. |
| `sandboxName` | Nombre del simulador de pruebas que contiene la ejecución del flujo. |
| `imsOrgId` | El ID de organización. |
| `flowId` | ID del flujo con el que se crea la ejecución del flujo. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.windowEndTime` | Un entero que define la hora de finalización de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.deltaColumn` | La columna delta es necesaria para dividir los datos y separar los nuevos datos introducidos de los datos históricos. **Nota**: La variable `deltaColumn` solo es necesario al crear la primera ejecución de flujo. |
| `params.deltaColumn.name` | Nombre de la columna delta. |
| `etag` | La versión de recurso de la ejecución del flujo. |
| `metrics` | Esta propiedad muestra un resumen de estado para la ejecución del flujo. |

## Creación de una ejecución de flujo para un origen basado en archivos

Para crear un flujo para un origen basado en archivos, realice una solicitud de POST al [!DNL Flow Service] al proporcionar el ID del flujo con el que desea crear los valores de ejecución y para la hora de inicio y finalización.

>[!TIP]
>
>Las fuentes basadas en archivos incluyen todas las fuentes de almacenamiento en la nube.

**Formato de API**

```http
POST /runs/
```

**Solicitud**

La siguiente solicitud crea una ejecución de flujo para el ID de flujo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `flowId` | ID del flujo con el que se creará la ejecución de flujo. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.windowEndTime` | Un entero que define la hora de finalización de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la ejecución de flujo recién creada, incluida su ejecución única `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID de la ejecución del flujo recién creado. Consulte la guía de [recuperación de especificaciones de flujo](../api/collect/cloud-storage.md#specs) para obtener más información sobre las especificaciones de ejecución basadas en archivos. |
| `createdAt` | Marca de tiempo Unix que designa cuándo se creó la ejecución del flujo. |
| `updatedAt` | La marca de tiempo unix que designa cuándo se actualizó por última vez la ejecución del flujo. |
| `createdBy` | ID de organización del usuario que creó la ejecución de flujo. |
| `updatedBy` | ID de organización del usuario que actualizó por última vez la ejecución del flujo. |
| `createdClient` | El cliente de aplicación que creó el flujo se ejecuta. |
| `updatedClient` | El cliente de aplicación que actualizó por última vez la ejecución del flujo. |
| `sandboxId` | ID del simulador de pruebas que contiene la ejecución del flujo. |
| `sandboxName` | Nombre del simulador de pruebas que contiene la ejecución del flujo. |
| `imsOrgId` | El ID de organización. |
| `flowId` | ID del flujo con el que se crea la ejecución del flujo. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `params.windowEndTime` | Un entero que define la hora de finalización de la ventana durante la cual se deben extraer los datos. El valor se representa en tiempo unix. |
| `etag` | La versión de recurso de la ejecución del flujo. |
| `metrics` | Esta propiedad muestra un resumen de estado para la ejecución del flujo. |


## Monitorización de las ejecuciones de flujo

Una vez creada la ejecución del flujo, puede monitorizar los datos que se están incorporando a través de él para ver información sobre ejecuciones de flujo, estado de finalización y errores. Para monitorizar las ejecuciones de flujo mediante API, consulte el tutorial en [monitorización de flujos de datos en la API ](./monitor.md). Para monitorizar las ejecuciones de flujo mediante la interfaz de usuario de Platform, consulte la guía de [control de fuentes de datos flujos de datos mediante el panel de monitorización](../../../dataflows/ui/monitor-sources.md).
