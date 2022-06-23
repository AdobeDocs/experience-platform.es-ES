---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API;api;eliminar;eliminar flujos de datos de destino
solution: Experience Platform
title: Eliminar un flujo de datos de destino mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo eliminar flujos de datos en destinos de flujo y por lotes mediante la API de servicio de flujo.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Eliminar un flujo de datos de destino mediante la API de servicio de flujo

Puede eliminar flujos de datos que contengan errores o que se hayan vuelto obsoletos mediante la función [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial trata los pasos para eliminar flujos de datos tanto a destinos de lote como de flujo continuo mediante [!DNL Flow Service].

## Primeros pasos {#get-started}

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un ID de flujo válido, seleccione el destino que desee en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) y [activar datos](../ui/activation-overview.md) antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para eliminar correctamente un flujo de datos mediante el [!DNL Flow Service] API.

### Leer llamadas de API de ejemplo {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios {#gather-values-for-required-headers}

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes a [!DNL Flow Service], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` no se ha especificado, las solicitudes se resuelven en la sección `prod` simulador de pruebas.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Eliminar un flujo de datos de destino {#delete-destination-dataflow}

Con un ID de flujo existente, puede eliminar un flujo de datos de destino realizando una solicitud de DELETE al [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El único `id` para el flujo de datos de destino que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) al flujo de datos. La API devolverá un error HTTP 404 (no encontrado), que indica que se ha eliminado el flujo de datos.

## Gestión de errores de API {#api-error-handling}

Los extremos de API de este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](/help/landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform para obtener más información sobre la interpretación de las respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] API para eliminar un flujo de datos existente a un destino.

Para ver los pasos sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminación de flujos de datos en la interfaz de usuario](../ui/delete-destinations.md).

Ahora puede continuar y [eliminar cuentas de destino](/help/destinations/api/delete-destination-account.md) usando la variable [!DNL Flow Service] API.
