---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de API de etiquetas
topic-legacy: developer guide
description: Obtenga información sobre cómo administrar las etiquetas de uso de datos en Experience Platform mediante la API del servicio de directivas.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 4%

---

# Extremo de etiquetas

Las etiquetas de uso de datos le permiten clasificar los datos según las políticas de uso que puedan aplicarse a esos datos. La variable `/labels` en la variable [!DNL Policy Service API] le permite administrar mediante programación las etiquetas de uso de datos dentro de la aplicación de experiencia.

>[!NOTE]
>
>La variable `/labels` El extremo solo se utiliza para recuperar, crear y actualizar etiquetas de uso de datos. Para ver los pasos sobre cómo añadir etiquetas a conjuntos de datos y campos mediante llamadas a la API, consulte la guía de [administración de etiquetas de conjuntos de datos](../labels/dataset-api.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, revise la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier [!DNL Experience Platform] API.

## Recuperar una lista de etiquetas {#list}

Puede enumerar todo `core` o `custom` etiquetas realizando una solicitud de GET a `/labels/core` o `/labels/custom`, respectivamente.

**Formato de API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitud**

La siguiente solicitud enumera todas las etiquetas personalizadas creadas en su organización.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de etiquetas personalizadas recuperadas del sistema. Dado que la solicitud de ejemplo anterior se realizó en `/labels/custom`, la respuesta a continuación solo muestra etiquetas personalizadas.

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

Puede buscar una etiqueta específica incluyendo la etiqueta `name` en la ruta de una solicitud de GET al [!DNL Policy Service] API.

**Formato de API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La variable `name` de la etiqueta personalizada que desea buscar. |

**Solicitud**

La siguiente solicitud recupera la etiqueta personalizada `L2`, tal como se indica en la ruta.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

Para crear o actualizar una etiqueta personalizada, debe realizar una solicitud de PUT al [!DNL Policy Service] API.

**Formato de API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La variable `name` propiedad de una etiqueta personalizada. Si no existe una etiqueta personalizada con este nombre, se creará una etiqueta nueva. Si existe una, se actualizará esa etiqueta. |

**Solicitud**

La siguiente solicitud crea una etiqueta nueva, `L3`, que tiene por objeto describir los datos que contienen información relacionada con los planes de pago seleccionados por los clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Identificador de cadena único para la etiqueta. Este valor se utiliza con fines de búsqueda y de aplicación de la etiqueta a conjuntos de datos y campos, por lo que se recomienda que sea corto y conciso. |
| `category` | La categoría de la etiqueta. Aunque puede crear sus propias categorías para etiquetas personalizadas, es muy recomendable que utilice `Custom` si desea que la etiqueta aparezca en la interfaz de usuario. |
| `friendlyName` | Un nombre descriptivo para la etiqueta, que se utiliza para la visualización. |
| `description` | (Opcional) Descripción de la etiqueta para proporcionar más contexto. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada, con el código HTTP 200 (OK) si se actualizó una etiqueta existente o 201 (Creado) si se creó una etiqueta nueva.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
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

Esta guía abarcaba el uso de la variable `/labels` en la API del servicio de directivas. Para ver los pasos sobre cómo aplicar etiquetas a conjuntos de datos y campos, consulte la [guía de API de etiquetas de conjuntos de datos](../labels/dataset-api.md).
