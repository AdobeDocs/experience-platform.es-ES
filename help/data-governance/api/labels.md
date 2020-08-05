---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Extremo de etiquetas
topic: developer guide
translation-type: tm+mt
source-git-commit: 80526bc0fea9e1854174a2edf9389ff0c4e98f71
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---


# Extremo de etiquetas

Las etiquetas de uso de datos le permiten clasificar los datos según las políticas de uso que puedan aplicarse a esos datos. El `/labels` punto final de la [!DNL Policy Service API] permite administrar mediante programación las etiquetas de uso de datos dentro de la aplicación de experiencia.

>[!NOTE]
>
>El extremo solo se utiliza para recuperar, crear y actualizar etiquetas de uso de datos. `/labels` Para ver los pasos sobre cómo agregar etiquetas a conjuntos de datos y campos mediante llamadas de API, consulte la guía sobre la [administración de etiquetas](../labels/dataset-api.md)de conjuntos de datos.

## Primeros pasos

El punto final de API utilizado en esta guía forma parte del [!DNL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Recuperar una lista de etiquetas {#list}

Puede realizar la lista de todas `core` o `custom` las etiquetas mediante una solicitud de GET a `/labels/core` o `/labels/custom`, respectivamente.

**Formato API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitud**

La siguiente solicitud lista todas las etiquetas personalizadas creadas en la organización.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de las etiquetas personalizadas recuperadas del sistema. Dado que la solicitud de ejemplo anterior se realizó en `/labels/custom`, la respuesta siguiente solo muestra etiquetas personalizadas.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Buscar una etiqueta {#look-up}

Puede buscar una etiqueta específica incluyendo la propiedad de esa `name` etiqueta en la ruta de una solicitud de GET a la [!DNL Policy Service] API.

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La `name` propiedad de la etiqueta personalizada que desea buscar. |

**Solicitud**

La siguiente solicitud recupera la etiqueta personalizada `L2`, como se indica en la ruta.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Crear o actualizar una etiqueta personalizada {#create-update}

Para crear o actualizar una etiqueta personalizada, debe realizar una solicitud de PUT a la [!DNL Policy Service] API.

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La `name` propiedad de una etiqueta personalizada. Si no existe una etiqueta personalizada con este nombre, se creará una nueva etiqueta. Si existe una, la etiqueta se actualizará. |

**Solicitud**

La siguiente solicitud crea una nueva etiqueta `L3`, que tiene por objeto describir los datos que contienen información relativa a los planes de pago seleccionados por los clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador de cadena único para la etiqueta. Este valor se utiliza para fines de búsqueda y para aplicar la etiqueta a conjuntos de datos y campos, por lo que se recomienda que sea breve y conciso. |
| `category` | La categoría de la etiqueta. Aunque puede crear sus propias categorías para las etiquetas personalizadas, se recomienda encarecidamente que las utilice `Custom` si desea que la etiqueta aparezca en la interfaz de usuario. |
| `friendlyName` | Un nombre descriptivo para la etiqueta, que se utiliza con fines de visualización. |
| `description` | (Opcional) Una descripción de la etiqueta para proporcionar contexto adicional. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada, con el código HTTP 200 (Aceptar) si se actualizó una etiqueta existente o 201 (Creado) si se creó una nueva etiqueta.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Pasos siguientes

Esta guía abarcaba el uso del `/labels` extremo en la API de servicio de directivas. Para ver los pasos sobre cómo aplicar etiquetas a conjuntos de datos y campos, consulte la guía de la API de etiquetas de [conjuntos de datos](../labels/dataset-api.md).