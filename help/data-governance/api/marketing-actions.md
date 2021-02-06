---
keywords: Experience Platform;inicio;temas populares;Aplicación de políticas;aplicación de acciones de marketing;aplicación basada en API;administración de datos
solution: Experience Platform
title: Extremo de la API de acciones de marketing
topic: developer guide
description: Una acción de mercadotecnia, en el contexto de la Administración de datos de Adobe Experience Platform, es una acción que realiza un consumidor de datos de Experience Platform, para la cual es necesario verificar las infracciones de las políticas de uso de datos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---


# Extremo de acciones de marketing

Una acción de mercadotecnia, en el contexto de Adobe Experience Platform [!DNL Data Governance], es una acción que realiza un [!DNL Experience Platform] consumidor de datos, para la cual es necesario verificar las violaciones de las políticas de uso de datos.

Puede administrar las acciones de marketing de su organización mediante el extremo `/marketingActions` de la API de servicio de directivas.

## Primeros pasos

Los extremos de API utilizados en esta guía forman parte de la [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de muestra en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas exitosas a cualquier API [!DNL Experience Platform].

## Recuperar una lista de acciones de mercadotecnia {#list}

Puede recuperar una lista de acciones de mercadotecnia principales o personalizadas haciendo una solicitud de GET a `/marketingActions/core` o `/marketingActions/custom`, respectivamente.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud recupera una lista de acciones de mercadotecnia personalizadas que mantiene su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de cada acción de mercadotecnia recuperada, incluidos sus `name` y `href`. El valor `href` se utiliza para identificar la acción de mercadotecnia al [crear una directiva de uso de datos](policies.md#create-policy).

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
| `_page.count` | Número total de acciones de marketing devueltas. |
| `children` | Matriz de objetos que contiene los detalles de las acciones de mercadotecnia recuperadas. |
| `name` | El nombre de la acción de mercadotecnia, que actúa como su identificador único cuando [busca una acción de mercadotecnia específica](#lookup). |
| `_links.self.href` | Una referencia URI para la acción de mercadotecnia, que puede utilizarse para completar la matriz `marketingActionsRefs` cuando [crea una directiva de uso de datos](policies.md#create-policy). |

## Buscar una acción de mercadotecnia específica {#lookup}

Puede consultar los detalles de una acción de mercadotecnia específica incluyendo la propiedad `name` de la acción de mercadotecnia en la ruta de una solicitud de GET.

**Formato API**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | La propiedad `name` de la acción de marketing que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una acción de mercadotecnia personalizada denominada `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response contiene los detalles de la acción de mercadotecnia, incluida la ruta (`_links.self.href`) necesaria para hacer referencia a la acción de mercadotecnia cuando [define una directiva de uso de datos](policies.md#create-policy) (`marketingActionsRefs`).

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

## Crear o actualizar una acción de mercadotecnia personalizada {#create-update}

Puede crear una nueva acción de marketing personalizada o actualizar una existente incluyendo el nombre existente o previsto de la acción de marketing en la ruta de una solicitud de PUT.

**Formato API**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nombre de la acción de marketing que se va a crear o actualizar. Si ya existe en el sistema una acción de marketing con el nombre proporcionado, se actualiza esa acción de marketing. Si no existe una, se crea una nueva acción de marketing para el nombre proporcionado. |

**Solicitud**

La siguiente solicitud crea una nueva acción de mercadotecnia denominada `crossSiteTargeting`, siempre que no exista aún una acción de mercadotecnia con el mismo nombre en el sistema. Si existe una acción de mercadotecnia `crossSiteTargeting`, esta llamada actualiza esa acción de mercadotecnia en función de las propiedades proporcionadas en la carga útil.

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
| `name` | Nombre de la acción de marketing que se va a crear o actualizar. <br><br>**IMPORTANTE**: Esta propiedad debe coincidir con la  `{MARKETING_ACTION_NAME}` de la ruta; de lo contrario, se producirá un error HTTP 400 (Solicitud incorrecta). En otras palabras, una vez creada una acción de mercadotecnia, su propiedad `name` no se puede cambiar. |
| `description` | Una descripción opcional que proporciona un contexto adicional para la acción de marketing. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la acción de marketing. Si se actualizó una acción de marketing existente, la respuesta devuelve el estado HTTP 200 (correcto). Si se ha creado una nueva acción de marketing, la respuesta devuelve el estado HTTP 201 (Creado).

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

## Eliminar una acción de mercadotecnia personalizada {#delete}

Puede eliminar una acción de marketing personalizada incluyendo su nombre en la ruta de una solicitud de DELETE.

>[!NOTE]
>
>No se pueden eliminar las acciones de marketing a las que hacen referencia las directivas existentes. Si intenta eliminar una de estas acciones de marketing, se producirá un error HTTP 400 (Solicitud incorrecta) junto con un mensaje que incluye los ID de todas las directivas que hacen referencia a la acción de marketing.

**Formato API**

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

Una respuesta correcta devuelve Estado HTTP 200 (Aceptar) con un cuerpo de respuesta en blanco.

Puede confirmar la eliminación intentando [buscar la acción de mercadotecnia](#look-up). Debe recibir un error HTTP 404 (no encontrado) si la acción de mercadotecnia se ha eliminado del sistema.
