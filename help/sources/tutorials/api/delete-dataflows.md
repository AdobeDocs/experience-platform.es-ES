---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API;api;eliminar;eliminar flujos de datos
solution: Experience Platform
title: Eliminar un flujo de datos mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo eliminar flujos de datos por lotes y de flujo continuo mediante la API de Flow Service.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# Eliminar un flujo de datos mediante la API de Flow Service

Puede eliminar los flujos de datos por lotes y de flujo continuo que contengan errores o que hayan quedado obsoletos mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial cubre los pasos para eliminar flujos de datos realizados con fuentes por lotes y de flujo continuo mediante [!DNL Flow Service].

## Primeros pasos

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un ID de flujo válido, seleccione el conector que desee en el [información general de orígenes](../../home.md) y siga los pasos descritos antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Eliminación de un flujo de datos

Con un ID de flujo existente, puede eliminar un flujo de datos realizando una solicitud al DELETE para que [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | La exclusiva `id` para el flujo de datos que desea eliminar. |

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

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando una solicitud de búsqueda (GET) al flujo de datos. La API devolverá un error HTTP 404 (no encontrado), que indica que el flujo de datos se ha eliminado.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] API a para eliminar un flujo de datos existente.

Para ver los pasos sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminación de flujos de datos en la IU](../../tutorials/ui/delete.md)
