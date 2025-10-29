---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;eliminar cuentas de destino;eliminar;api
solution: Experience Platform
title: Eliminación de una cuenta de destino mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo eliminar una cuenta de destino mediante la API de Flow Service.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 21%

---

# Eliminación de una cuenta de destino mediante la API de Flow Service

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

Antes de activar los datos, debe conectarse al destino configurando primero una cuenta de destino. Este tutorial trata los pasos para eliminar las cuentas de destino que ya no se necesitan mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Actualmente, la eliminación de cuentas de destino solo se admite en la API de Flow Service. Las cuentas de destino no se pueden eliminar mediante la interfaz de usuario de Experience Platform.

## Introducción {#get-started}

Este tutorial requiere que tenga un ID de conexión válido. El ID de conexión representa la conexión de la cuenta al destino. Si no tiene un identificador de conexión válido, seleccione el destino que elija en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
* [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para eliminar correctamente una cuenta de destino mediante la API [!DNL Flow Service].

### Lectura de llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios {#gather-values-for-required-headers}

Para realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si no se especifica el encabezado `x-sandbox-name`, las solicitudes se resuelven en la zona protegida `prod`.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* `Content-Type: application/json`

## Busque el identificador de conexión de la cuenta de destino que desea eliminar {#find-connection-id}

>[!NOTE]
>Este tutorial utiliza [Destino de dirigibles](../catalog/mobile-engagement/airship-attributes.md) como ejemplo, pero los pasos descritos se aplican a cualquiera de los [destinos disponibles](../catalog/overview.md).

El primer paso para eliminar una cuenta de destino es averiguar el ID de conexión que corresponde a la cuenta de destino que desea eliminar.

En la interfaz de usuario de Experience Platform, vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** y seleccione la cuenta que desee eliminar seleccionando el número en la columna **[!UICONTROL Destinations]**.

![Seleccionar cuenta de destino para eliminar](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

A continuación, puede recuperar el ID de conexión de la cuenta de destino desde la dirección URL de su explorador.

![Recuperar ID de conexión de la URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Eliminar conexión {#delete-connection}

>[!IMPORTANT]
>
>Antes de eliminar la cuenta de destino, debe eliminar cualquier flujo de datos existente en la cuenta de destino.
>&#x200B;>Para eliminar flujos de datos existentes, consulte las páginas siguientes:
>
>* [Use la interfaz de usuario de Experience Platform](../ui/delete-destinations.md) para eliminar flujos de datos existentes;
>* [Use la API de Flow Service](delete-destination-dataflow.md) para eliminar los flujos de datos existentes.

Una vez que tenga un ID de conexión y se haya asegurado de que no existen flujos de datos en la cuenta de destino, realice una petición DELETE a la API [!DNL Flow Service].

**Formato de API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor `id` único de la conexión que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco. Para confirmar la eliminación, intente una solicitud de búsqueda (GET) a la conexión. La API devolverá un error HTTP 404 (no encontrado), que indica que la cuenta de destino se ha eliminado.

## Administración de errores de API {#api-error-handling}

Los extremos de la API en este tutorial siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Próximos pasos

Al seguir este tutorial, ha utilizado correctamente la API [!DNL Flow Service] para eliminar las cuentas de destino existentes. Para obtener más información sobre el uso de destinos, consulte [descripción general de destinos](/help/destinations/home.md).