---
keywords: Experience Platform;inicio;temas populares;sistema de publicidad;sistema de publicidad
solution: Experience Platform
title: Explorar un sistema publicitario mediante la API de servicio de flujo
description: El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas. Este tutorial utiliza la API de servicio de flujo para explorar los sistemas publicitarios.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# Explorar un sistema publicitario usando la variable [!DNL Flow Service] API

Con la creación de una conexión de base, ahora puede utilizar el ID de conexión de base único para desplazarse por la estructura de datos y el contenido de la fuente y explorarlos. Esto le permite identificar los elementos específicos, así como sus respectivos tipos de datos y formatos, antes de crear un flujo de datos y llevarlos a Adobe Experience Platform.

Este tutorial utiliza la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para explorar los sistemas publicitarios.

## Primeros pasos

>[!IMPORTANT]
>
>Este tutorial requiere que tenga el ID de conexión base único para la fuente de publicidad. Si no tiene este ID, consulte el tutorial sobre [conexión de una fuente de publicidad a Platform](../../api/create/advertising/ads.md) tutorial.

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a un sistema publicitario mediante el [!DNL Flow Service] API.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../landing/api-guide.md).

## Explorar las tablas de datos

Con la conexión base para el sistema de publicidad, puede explorar las tablas de datos realizando solicitudes de GET. Utilice la siguiente llamada para encontrar la ruta de la tabla en la que desea inspeccionar o introducir [!DNL Platform].

**Formato de API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base para su sistema publicitario. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta es una matriz de tablas desde a su sistema de publicidad. Encuentre la tabla en la que desea traer [!DNL Platform] y tome nota de su `path` , tal y como se le pedirá en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la estructura de una tabla

Para inspeccionar la estructura de una tabla desde el sistema de publicidad, realice una solicitud de GET al especificar la ruta de una tabla como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión de su sistema de publicidad. |
| `{TABLE_PATH}` | Ruta de una tabla dentro del sistema de publicidad. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de una tabla. Los detalles sobre cada una de las columnas de la tabla se encuentran dentro de los elementos de la variable `columns` matriz.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Pasos siguientes

Al seguir este tutorial, ha explorado su sistema de publicidad y ha encontrado la ruta de la tabla a la que desea traer [!DNL Platform]y obtuvo información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos de su sistema publicitario e introducirlos en Platform](../collect/advertising.md).
