---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;eliminar cuentas;eliminar;api
solution: Experience Platform
title: Eliminación de una cuenta mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo eliminar una cuenta mediante la API de Flow Service.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 3%

---

# Eliminación de una cuenta mediante la API de Flow Service

Puede eliminar las cuentas de origen que contengan errores o que hayan quedado obsoletas mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consulte el siguiente tutorial para ver los pasos sobre cómo eliminar una cuenta mediante la API.

## Introducción

Este tutorial requiere que tenga un ID de conexión válido. Si no tiene un identificador de conexión válido, seleccione el conector que prefiera en la [descripción general de orígenes](../../home.md) y siga los pasos descritos antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).

## Eliminar cuenta

>[!TIP]
>
>Antes de eliminar la cuenta de origen, primero debe eliminar cualquier flujo de datos existente asociado a la cuenta de origen. Para eliminar flujos de datos existentes, consulte el tutorial sobre [eliminación de flujos de datos de origen](./delete-dataflows.md).

Para eliminar una cuenta, realice una petición DELETE a la API [!DNL Flow Service] y proporcione el identificador de conexión base que corresponda a la cuenta que desea eliminar.

**Formato de API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identificador de conexión base de la cuenta de origen que desea eliminar. |

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

Para confirmar la eliminación, intente una solicitud de búsqueda (GET) a la conexión.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la API [!DNL Flow Service] para eliminar cuentas existentes.

Para obtener información sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminar cuentas en la interfaz de usuario](../../tutorials/ui/delete-accounts.md).
