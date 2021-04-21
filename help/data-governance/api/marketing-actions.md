---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;api de acciones de marketing;aplicación basada en API;control de datos
solution: Experience Platform
title: Punto final de la API de acciones de marketing
topic-legacy: developer guide
description: Una acción de marketing, en el contexto de la Administración de datos de Adobe Experience Platform, es una acción que realiza un consumidor de datos de Experience Platform, para la cual es necesario comprobar si hay infracciones de las políticas de uso de datos.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# Punto final de las acciones de marketing

Una acción de marketing, en el contexto de Adobe Experience Platform [!DNL Data Governance], es una acción que realiza un [!DNL Experience Platform] consumidor de datos, para la cual es necesario comprobar si hay infracciones de las políticas de uso de datos.

Puede administrar las acciones de marketing para su organización mediante el extremo `/marketingActions` de la API del servicio de directivas.

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

## Recuperar una lista de acciones de marketing {#list}

Puede recuperar una lista de acciones de marketing principales o personalizadas realizando una solicitud de GET a `/marketingActions/core` o `/marketingActions/custom`, respectivamente.

**Formato de API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud recupera una lista de acciones de marketing personalizadas que su organización mantiene.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de cada acción de marketing recuperada, incluidas sus `name` y `href`. El valor `href` se utiliza para identificar la acción de marketing al [crear una directiva de uso de datos](policies.md#create-policy).

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
| `_page.count` | El número total de acciones de marketing devueltas. |
| `children` | Matriz de objetos que contienen los detalles de las acciones de marketing recuperadas. |
| `name` | Nombre de la acción de marketing, que actúa como su identificador único cuando [busca una acción de marketing específica](#lookup). |
| `_links.self.href` | Una referencia URI para la acción de marketing, que se puede utilizar para completar la matriz `marketingActionsRefs` al [crear una directiva de uso de datos](policies.md#create-policy). |

## Buscar una acción de marketing específica {#lookup}

Puede consultar los detalles de una acción de marketing específica incluyendo la propiedad `name` de la acción de marketing en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La propiedad `name` de la acción de marketing que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una acción de marketing personalizada denominada `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response contiene los detalles de la acción de marketing, incluida la ruta (`_links.self.href`) necesaria para hacer referencia a la acción de marketing al [definir una directiva de uso de datos](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
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
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a crear o actualizar. Si ya existe en el sistema una acción de marketing con el nombre proporcionado, se actualiza esa acción de marketing. Si no existe una, se crea una nueva acción de marketing para el nombre proporcionado. |

**Solicitud**

La siguiente solicitud crea una nueva acción de marketing llamada `crossSiteTargeting`, siempre que en el sistema aún no exista una acción de marketing del mismo nombre. Si existe una acción de marketing `crossSiteTargeting`, esta llamada actualiza esa acción de marketing en función de las propiedades proporcionadas en la carga útil.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la acción de marketing que se va a crear o actualizar. <br><br>**IMPORTANTE**: Esta propiedad debe coincidir con  `{MARKETING_ACTION_NAME}` en la ruta de acceso; de lo contrario, se producirá un error HTTP 400 (solicitud incorrecta). En otras palabras, una vez creada una acción de marketing, su propiedad `name` no se puede cambiar. |
| `description` | Una descripción opcional para proporcionar un contexto adicional para la acción de marketing. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la acción de marketing. Si se actualizó una acción de marketing existente, la respuesta devuelve el estado HTTP 200 (OK). Si se ha creado una nueva acción de marketing, la respuesta devuelve el estado HTTP 201 (Creado).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
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

Puede eliminar una acción de marketing personalizada incluyendo su nombre en la ruta de una solicitud de DELETE.

>[!NOTE]
>
>Las acciones de marketing a las que las políticas existentes hacen referencia no se pueden eliminar. Si se intenta eliminar una de estas acciones de marketing, se producirá un error HTTP 400 (solicitud incorrecta) junto con un mensaje que incluye los ID de todas las políticas que hacen referencia a la acción de marketing.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) con un cuerpo de respuesta en blanco.

Puede confirmar la eliminación intentando [buscar la acción de marketing](#look-up). Debería recibir un error HTTP 404 (no encontrado) si la acción de marketing se ha eliminado del sistema.
