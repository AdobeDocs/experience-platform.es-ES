---
keywords: Experience Platform;inicio;temas populares;comercio electrónico;comercio electrónico
solution: Experience Platform
title: Exploración de una conexión de comercio electrónico mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar las conexiones de comercio electrónico.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# Explore una conexión de comercio electrónico con [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial utiliza el [!DNL Flow Service] API para explorar un tercero **[!UICONTROL eCommerce]** conexión.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un **[!UICONTROL eCommerce]** conexión mediante el [!DNL Flow Service] API.

### Obtener un ID de conexión

Para explorar su **[!UICONTROL eCommerce]** conexión mediante [!DNL Platform] API, debe poseer un ID de conexión válido. Si todavía no dispone de una conexión para **[!UICONTROL eCommerce]** conexión con la que desea trabajar, puede crear una a través del siguiente tutorial:

* [Shopify](../create/ecommerce/shopify.md)

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* `Content-Type: application/json`

## Exploración de las tablas de datos

Uso de su **[!UICONTROL eCommerce]** ID de conexión, puede explorar las tablas de datos realizando solicitudes de GET. Utilice la siguiente llamada para encontrar la ruta de la tabla que desea inspeccionar o introducir en [!DNL Platform].

**Formato de API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{CONNECTION_ID}` | Su **[!UICONTROL eCommerce]** ID de conexión. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de tablas de su **[!UICONTROL eCommerce]** conexión. Encuentre la tabla que desea introducir en [!DNL Platform] y tome nota de su `path` , ya que es necesario proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect la estructura de una tabla

Para inspeccionar la estructura de una tabla desde su **[!UICONTROL eCommerce]** conexión, realice una solicitud de GET mientras especifica la ruta de una tabla dentro de una `object` parámetro de consulta.

**Formato de API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El ID de conexión de su **[!UICONTROL eCommerce]** conexión. |
| `{TABLE_PATH}` | La ruta de una tabla dentro de su **[!UICONTROL eCommerce]** conexión. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de la tabla especificada. Los detalles sobre cada una de las columnas de la tabla se encuentran dentro de los elementos de la variable `columns` matriz.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Pasos siguientes

Al seguir este tutorial, ha explorado su **[!UICONTROL eCommerce]** conexión, encontró la ruta de la tabla que desea introducir en [!DNL Platform]y obtuvo información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para lo siguiente [recopilar datos de comercio electrónico e introducirlos en Platform](../collect/ecommerce.md).
