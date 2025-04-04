---
title: Reintentar ejecuciones de flujo de datos fallidas
description: Obtenga información sobre cómo reintentar las ejecuciones de flujo de datos fallidas mediante la API de Flow Service.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# Reintentar ejecuciones de flujo de datos fallidas

>[!IMPORTANT]
>
>La compatibilidad con la reintentos de ejecuciones de flujo de datos fallidas está disponible para las fuentes por lotes. Solo puede reintentar las ejecuciones de flujo de datos que han fallado.

Este tutorial explica los pasos para reintentar las ejecuciones de flujo de datos fallidas mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).

## Reintentar una ejecución de flujo de datos fallida

Para reintentar una ejecución de flujo de datos fallida, realice una petición POST al extremo `/runs` y proporcione el identificador de ejecución del flujo de datos y la operación `re-trigger` como parte de los parámetros de consulta.

**Formato de API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parámetro | Descripción |
| --- | --- |
| `{RUN_ID}` | El ID de ejecución que corresponde a la ejecución del flujo de datos que desea reintentar. |
| `op` | Una operación que determina la acción que se va a realizar. Para reintentar una ejecución de flujo de datos fallida, debe especificar `re-trigger` como su operación. |

**Solicitud**

>[!NOTE]
>
>Puede utilizar la operación `re-trigger` para reintentar las ejecuciones correctas del flujo de datos, dado que la ejecución correcta del flujo de datos tiene cero registros ingeridos.

La siguiente solicitud reintenta ejecutar el flujo de datos para el identificador de ejecución `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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
