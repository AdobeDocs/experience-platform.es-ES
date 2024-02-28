---
keywords: Experience Platform;inicio;temas populares;aplicación de políticas;api de acciones de marketing;aplicación basada en API;control de datos
solution: Experience Platform
title: Extremo de API de acciones de marketing
description: Una acción de marketing, en el contexto de la gobernanza de datos de Adobe Experience Platform, es una acción que realiza un consumidor de datos Experience Platform, para la cual es necesario comprobar si se han infringido las políticas de uso de datos.
role: Developer
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 3%

---

# Extremo de acciones de marketing

Una acción de marketing, en el contexto de la gobernanza de datos de Adobe Experience Platform, es una acción que [!DNL Experience Platform] toma el consumidor de datos, para lo cual es necesario comprobar si se han infringido las políticas de uso de datos.

Puede administrar las acciones de marketing de su organización mediante el `/marketingActions` en la API del servicio de directivas.

## Introducción

Los extremos de API utilizados en esta guía forman parte de la variable [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier [!DNL Experience Platform] API.

## Recuperación de una lista de acciones de marketing {#list}

Puede recuperar una lista de acciones de marketing principales o personalizadas realizando una solicitud de GET a `/marketingActions/core` o `/marketingActions/custom`, respectivamente.

**Formato de API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud recupera una lista de acciones de marketing personalizadas mantenidas por su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de cada acción de marketing recuperada, incluida su `name` y `href`. El `href` se utiliza para identificar la acción de marketing cuando [crear una política de uso de datos](policies.md#create-policy).

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `_page.count` | Número total de acciones de marketing devueltas. |
| `children` | Matriz de objetos que contiene los detalles de las acciones de marketing recuperadas. |
| `name` | El nombre de la acción de marketing, que actúa como identificador único cuando [búsqueda de una acción de marketing específica](#lookup). |
| `_links.self.href` | Una referencia de URI para la acción de marketing, que se puede utilizar para completar la `marketingActionsRefs` matriz cuando [crear una política de uso de datos](policies.md#create-policy). |

## Búsqueda de una acción de marketing específica {#lookup}

Busca los detalles de una acción de marketing específica incluyendo la acción de marketing `name` en la ruta de una petición GET.

**Formato de API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | El `name` propiedad de la acción de marketing que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una acción de marketing personalizada denominada `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response contiene los detalles de la acción de marketing, incluida la ruta (`_links.self.href`) necesario para hacer referencia a la acción de marketing cuando [definición de una política de uso de datos](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Crear o actualizar una acción de marketing personalizada {#create-update}

Puede crear una nueva acción de marketing personalizada o actualizar una existente, incluyendo el nombre existente o previsto de la acción de marketing en la ruta de una solicitud de PUT.

**Formato de API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a crear o actualizar. Si ya existe una acción de marketing con el nombre proporcionado en el sistema, esa acción de marketing se actualiza. Si no existe, se crea una nueva acción de marketing para el nombre proporcionado. |

**Solicitud**

La siguiente solicitud crea una nueva acción de marketing denominada `crossSiteTargeting`, siempre que una acción de marketing del mismo nombre aún no exista en el sistema. Si un `crossSiteTargeting` La acción de marketing no existe; en su lugar, esta llamada actualiza esa acción de marketing en función de las propiedades proporcionadas en la carga útil.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la acción de marketing que se va a crear o actualizar. <br><br>**IMPORTANTE**: esta propiedad debe coincidir con el `{MARKETING_ACTION_NAME}` en la ruta; de lo contrario, se producirá un error HTTP 400 (Solicitud incorrecta). En otras palabras, una vez creada una acción de marketing, su `name` La propiedad no se puede cambiar. |
| `description` | Una descripción opcional para proporcionar más contexto para la acción de marketing. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la acción de marketing. Si se ha actualizado una acción de marketing existente, la respuesta devuelve el estado HTTP 200 (OK). Si se crea una nueva acción de marketing, la respuesta devuelve el estado HTTP 201 (Creado).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Eliminar una acción de marketing personalizada {#delete}

Puede eliminar una acción de marketing personalizada incluyendo su nombre en la ruta de una petición de DELETE.

>[!NOTE]
>
>Las acciones de marketing a las que hacen referencia las políticas existentes no se pueden eliminar. Si se intenta eliminar una de estas acciones de marketing, se producirá un error HTTP 400 (Solicitud incorrecta) junto con un mensaje que incluye los ID de todas las directivas que hacen referencia a la acción de marketing.

**Formato de API**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) con un cuerpo de respuesta en blanco.

Para confirmar la eliminación, intente lo siguiente [buscar la acción de marketing](#look-up). Debería recibir el error HTTP 404 (no encontrado) si la acción de marketing se ha eliminado del sistema.
