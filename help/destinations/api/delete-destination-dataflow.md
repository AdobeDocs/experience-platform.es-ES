---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;API;api;eliminar;eliminar flujos de datos de destino
solution: Experience Platform
title: Eliminar un flujo de datos de destino mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo eliminar flujos de datos en destinos de lote y flujo continuo mediante la API de Flow Service.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Eliminar un flujo de datos de destino mediante la API de Flow Service

Puede eliminar los flujos de datos que contengan errores o que se hayan vuelto obsoletos utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Este tutorial cubre los pasos para eliminar flujos de datos en destinos de lote y de flujo continuo mediante [!DNL Flow Service].

## Primeros pasos {#get-started}

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un ID de flujo válido, seleccione el destino que desee en la [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectar con el destino](../ui/connect-destination.md) y [activar datos](../ui/activation-overview.md) antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
* [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para eliminar correctamente un flujo de datos utilizando [!DNL Flow Service] API.

### Leer llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios {#gather-values-for-required-headers}

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` encabezado no especificado, las solicitudes se resuelven en el `prod` zona protegida.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* `Content-Type: application/json`

## Eliminar un flujo de datos de destino {#delete-destination-dataflow}

Con un ID de flujo existente, puede eliminar un flujo de datos de destino realizando una solicitud del DELETE al [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | La exclusiva `id` para el flujo de datos de destino que desea eliminar. |

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

Una respuesta correcta devuelve el estado HTTP 202 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando una solicitud de búsqueda (GET) al flujo de datos. La API devolverá un error HTTP 404 (no encontrado), que indica que el flujo de datos se ha eliminado.

## Administración de errores de API {#api-error-handling}

Los extremos de la API en este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](/help/landing/troubleshooting.md#request-header-errors) en la Guía de solución de problemas de Platform para obtener más información sobre cómo interpretar las respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] API para eliminar un flujo de datos existente en un destino.

Para ver los pasos sobre cómo realizar estas operaciones mediante la interfaz de usuario, consulte el tutorial sobre [eliminación de flujos de datos en la IU](../ui/delete-destinations.md).

Ahora puede continuar y [eliminar cuentas de destino](/help/destinations/api/delete-destination-account.md) uso del [!DNL Flow Service] API.
