---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;eliminar cuentas;eliminar;api
solution: Experience Platform
title: Eliminar una cuenta mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo eliminar una cuenta mediante la API de servicio de flujo.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Eliminar una cuenta mediante la API de servicio de flujo

Puede eliminar las cuentas de origen que contengan errores o que estén obsoletas mediante la función [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consulte el siguiente tutorial para ver los pasos sobre cómo eliminar una cuenta mediante la API.

## Primeros pasos

Este tutorial requiere que tenga un ID de conexión válido. Si no tiene un ID de conexión válido, seleccione el conector que desee en el [información general sobre fuentes](../../home.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Eliminar cuenta

>[!TIP]
>
>Antes de eliminar la cuenta de origen, debe eliminar los flujos de datos existentes asociados a la cuenta de origen. Para eliminar flujos de datos existentes, consulte el tutorial sobre [eliminar flujos de datos de orígenes](./delete-dataflows.md).

Para eliminar una cuenta, realice una solicitud de DELETE al [!DNL Flow Service] al proporcionar el ID de conexión base que corresponde a la cuenta que desea eliminar.

**Formato de API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base de la cuenta de origen que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) a la conexión.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] para eliminar cuentas existentes.

Para ver los pasos sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminación de cuentas en la interfaz de usuario](../../tutorials/ui/delete-accounts.md).
