---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;
title: (Beta) Crear una ejecución de flujo para la ingesta bajo demanda mediante la API de Flow Service
description: Este tutorial cubre los pasos para crear una ejecución de flujo para la ingesta bajo demanda mediante la API de Flow Service
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 2%

---

# (Beta) Cree una ejecución de flujo para la ingesta bajo demanda utilizando [!DNL Flow Service] API

>[!IMPORTANT]
>
>La ingesta bajo demanda está actualmente en fase beta y es posible que su organización aún no tenga acceso a ella. La funcionalidad descrita en esta documentación está sujeta a cambios.

Las ejecuciones de flujo representan una instancia de ejecución de flujo. Por ejemplo, si un flujo está programado para ejecutarse por hora a las 9:00, 10:00 y 11:00 a.m., tendría tres instancias de ejecución de flujo. Las ejecuciones de flujo son específicas de su organización particular.

La ingesta bajo demanda permite crear una ejecución de flujo con un flujo de datos determinado. Esto permite a los usuarios crear una ejecución de flujo basada en parámetros determinados y un ciclo de ingesta sin tokens de servicio. La compatibilidad con la ingesta bajo demanda solo está disponible para orígenes por lotes.

Este tutorial trata los pasos sobre cómo utilizar la ingesta bajo demanda y crear una ejecución de flujo utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

>[!NOTE]
>
>Para crear una ejecución de flujo, primero debe tener el ID de flujo de un flujo de datos programado para una ingesta única.

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Crear una ejecución de flujo para un origen basado en tablas

Para crear un flujo para un origen basado en tablas, realice una solicitud de POST al [!DNL Flow Service] API al tiempo que proporciona el ID del flujo con el que desea crear la ejecución, así como valores para la hora de inicio, la hora de finalización y la columna delta.

>[!TIP]
>
>Las fuentes basadas en tablas incluyen las siguientes categorías de fuentes: publicidad, análisis, consentimiento y preferencias, CRM, éxito del cliente, base de datos, automatización de marketing, pagos y protocolos.

**Formato de API**

```http
POST /runs/
```

**Solicitud**

La siguiente solicitud crea una ejecución de flujo para el ID de flujo `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Solo debe proporcionar la variable `deltaColumn` al crear la primera ejecución de flujo. Después de eso, `deltaColumn` se aplicarán parches como parte de `copy` transformación en el flujo y será tratado como la fuente de la verdad. Cualquier intento de cambiar el `deltaColumn` a través de los parámetros de ejecución de flujo dará como resultado un error.

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
          "startTime": "1663735590",
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
| `flowId` | El ID del flujo con el que se creará la ejecución del flujo. |
| `params.startTime` | Un entero que define la hora de inicio de la ejecución. El valor se representa en unix epoch time. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se extraerán los datos. El valor se representa en tiempo Unix. |
| `params.windowEndTime` | Un entero que define el tiempo de finalización de la ventana durante la cual se extraerán los datos. El valor se representa en tiempo Unix. |
| `params.deltaColumn` | La columna delta es necesaria para dividir los datos y separar los datos recién ingeridos de los datos históricos. **Nota**: La `deltaColumn` solo es necesario al crear la primera ejecución de flujo. |
| `params.deltaColumn.name` | Nombre de la columna delta. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la ejecución de flujo recién creada, incluida su ejecución única `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID de la ejecución del flujo recién creada. Consulte la guía de [recuperación de especificaciones de flujo](../api/collect/database-nosql.md#specs) para obtener más información sobre las especificaciones de ejecución basadas en tablas. |
| `etag` | La versión de recurso de la ejecución de flujo. |
<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Crear una ejecución de flujo para un origen basado en archivos

Para crear un flujo para un origen basado en archivos, realice una solicitud de POST al [!DNL Flow Service] al mismo tiempo que proporciona el ID del flujo con el que desea crear la ejecución y los valores para la hora de inicio y la hora de finalización.

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
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `flowId` | El ID del flujo con el que se creará la ejecución del flujo. |
| `params.startTime` | Un entero que define la hora de inicio de la ejecución. El valor se representa en unix epoch time. |
| `params.windowStartTime` | Un entero que define la hora de inicio de la ventana durante la cual se extraerán los datos. El valor se representa en tiempo Unix. |
| `params.windowEndTime` | Un entero que define el tiempo de finalización de la ventana durante la cual se extraerán los datos. El valor se representa en tiempo Unix. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la ejecución de flujo recién creada, incluida su ejecución única `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID de la ejecución del flujo recién creada. Consulte la guía de [recuperación de especificaciones de flujo](../api/collect/database-nosql.md#specs) para obtener más información sobre las especificaciones de ejecución basadas en tablas. |
| `etag` | La versión de recurso de la ejecución de flujo. |

## Monitorice las ejecuciones de flujo

Una vez creada la ejecución de flujo, puede monitorizar los datos que se están introduciendo a través de ella para ver información sobre las ejecuciones de flujo, el estado de finalización y los errores. Para monitorizar las ejecuciones de flujo mediante la API, consulte el tutorial sobre [monitorización de flujos de datos en la API ](./monitor.md). Para monitorizar las ejecuciones de flujo mediante la interfaz de usuario de Platform, consulte la guía de [fuentes de supervisión flujos de datos mediante el panel de supervisión](../../../dataflows/ui/monitor-sources.md).
