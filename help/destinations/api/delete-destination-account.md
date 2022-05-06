---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;eliminar cuentas de destino;eliminar;api
solution: Experience Platform
title: Eliminar una cuenta de destino mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo eliminar una cuenta de destino mediante la API de servicio de flujo.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Eliminar una cuenta de destino mediante la API de servicio de flujo

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

Antes de activar los datos, debe conectarse al destino configurando primero una cuenta de destino. Este tutorial trata los pasos para eliminar las cuentas de destino que ya no se necesitan mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Actualmente, la eliminación de cuentas de destino solo se admite en la API de servicio de flujo. Las cuentas de destino no se pueden eliminar mediante la interfaz de usuario del Experience Platform.

## Primeros pasos {#get-started}

Este tutorial requiere que tenga un ID de conexión válido. El ID de conexión representa la conexión de la cuenta al destino. Si no tiene un ID de conexión válido, seleccione el destino que desee en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para eliminar correctamente una cuenta de destino mediante la [!DNL Flow Service] API.

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

## Busque el ID de conexión de la cuenta de destino que desea eliminar {#find-connection-id}

>[!NOTE]
>Este tutorial utiliza la variable [Destino de la aeronave](../catalog/mobile-engagement/airship-attributes.md) como ejemplo, pero los pasos descritos se aplican a cualquiera de los [destinos disponibles](../catalog/overview.md).

El primer paso para eliminar una cuenta de destino es averiguar el ID de conexión que corresponde a la cuenta de destino que desea eliminar.

En la interfaz de usuario del Experience Platform, vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Cuentas]** y seleccione la cuenta que desee eliminar seleccionando el número en la variable **[!UICONTROL Destinos]** para abrir el Navegador.

![Seleccionar cuenta de destino para eliminar](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

A continuación, puede recuperar el ID de conexión de la cuenta de destino desde la dirección URL en el explorador.

![Recuperar el ID de conexión de la URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
>Antes de eliminar la cuenta de destino, debe eliminar los flujos de datos existentes en la cuenta de destino.
>Para eliminar flujos de datos existentes, consulte las páginas siguientes:
>* [Uso de la interfaz de usuario del Experience Platform](../ui/delete-destinations.md) eliminar flujos de datos existentes;
>* [Uso de la API de servicio de flujo](delete-destination-dataflow.md) para eliminar flujos de datos existentes.


Una vez que tenga un ID de conexión y se haya asegurado de que no existen flujos de datos en la cuenta de destino, realice una solicitud de DELETE a la [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El único `id` para la conexión que desea eliminar. |

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

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) a la conexión. La API devolverá un error HTTP 404 (no encontrado), que indica que la cuenta de destino se ha eliminado.

## Gestión de errores de API {#api-error-handling}

Los extremos de API de este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!DNL Flow Service] para eliminar cuentas de destino existentes. Para obtener más información sobre el uso de destinos, consulte la [información general sobre destinos](/help/destinations/home.md).