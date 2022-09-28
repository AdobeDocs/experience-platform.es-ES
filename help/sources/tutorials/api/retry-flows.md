---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;
title: Reintentar ejecuciones de flujo de datos fallidas
description: Este tutorial trata los pasos para reintentar las ejecuciones de flujo de datos fallidas mediante la API de servicio de flujo
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# Reintentar ejecuciones de flujo de datos fallidas

>[!IMPORTANT]
>
>La compatibilidad para reintentar ejecuciones de flujo de datos fallidas está disponible para orígenes por lotes. Solo puede reintentar las ejecuciones de flujo de datos que han fallado.

Este tutorial trata los pasos para reintentar las ejecuciones de flujo de datos fallidas mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Reintentar una ejecución de flujo de datos fallida

Para volver a intentar la ejecución fallida de un flujo de datos, realice una solicitud de POST al `/runs` al proporcionar el ID de ejecución de su flujo de datos y la variable `re-trigger` como parte de los parámetros de consulta.

**Formato de API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parámetro | Descripción |
| --- | --- |
| `{RUN_ID}` | El ID de ejecución que corresponde a la ejecución del flujo de datos que desea reintentar. |
| `op` | Operación que determina la acción que se va a realizar. Para volver a intentar la ejecución de un flujo de datos fallido, debe especificar `re-trigger` como su operación. |

**Solicitud**

La siguiente solicitud reintenta la ejecución del flujo de datos para el ID de ejecución `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Respuesta**

Una respuesta correcta devuelve un ID de ejecución de flujo recién creado y su versión de etiqueta correspondiente.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
