---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API;api;eliminar;eliminar flujos de datos
solution: Experience Platform
title: Eliminación de un flujo de datos mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo eliminar flujos de datos de flujo y por lotes mediante la API de servicio de flujo.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Eliminación de un flujo de datos mediante la API de servicio de flujo

Puede eliminar flujos de datos de flujo continuo y por lotes que contengan errores o que se hayan vuelto obsoletos mediante la función [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial trata los pasos para eliminar flujos de datos realizados tanto con orígenes de lote como de flujo continuo mediante [!DNL Flow Service].

## Primeros pasos

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un ID de flujo válido, seleccione el conector que desee en el [información general sobre fuentes](../../home.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Eliminar un flujo de datos

Con un ID de flujo existente, puede eliminar un flujo de datos realizando una solicitud de DELETE al [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El único `id` para el flujo de datos que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) al flujo de datos. La API devolverá un error HTTP 404 (no encontrado), que indica que se ha eliminado el flujo de datos.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] para eliminar un flujo de datos existente.

Para ver los pasos sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminación de flujos de datos en la interfaz de usuario](../../tutorials/ui/delete.md)
