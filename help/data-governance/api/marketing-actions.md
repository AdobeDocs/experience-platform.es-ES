---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Acciones de mercadotecnia
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# Acciones de mercadotecnia

Una acción de marketing, en el contexto de la gobernanza de datos de la plataforma de experiencia de Adobe, es una acción que realiza un consumidor de datos de la plataforma de experiencia, para la cual es necesario comprobar si hay infracciones de las políticas de uso de datos.

Trabajar con acciones de marketing en la API requiere que utilice el `/marketingActions` punto final.

## Lista de todas las acciones de mercadotecnia

Para vista de una lista de todas las acciones de marketing, se puede realizar una solicitud GET `/marketingActions/core` o `/marketingActions/custom` que devuelve todas las directivas del contenedor especificado.

**Formato API**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Solicitud**

La siguiente solicitud devolverá una lista de todas las acciones de marketing personalizadas definidas por la organización de IMS.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response proporciona el número total de acciones de marketing en el contenedor (`count`) y la `children` matriz contiene los detalles de cada acción de marketing, incluidos el `name` y un `href` para la acción de marketing. Esta ruta (`_links.self.href`) se utiliza para completar la `marketingActionsRefs` matriz al [crear una directiva](policies.md#create-policy)de uso de datos.

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
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

## Buscar una acción de mercadotecnia específica

También puede realizar una solicitud de búsqueda (GET) para vista de los detalles de una acción de mercadotecnia específica. Esto se lleva a cabo mediante el uso `name` de la acción de mercadotecnia. Si el nombre es desconocido, se puede encontrar usando la solicitud de listado (GET) que se mostró anteriormente.

**Formato API**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response contiene los detalles de la acción de marketing, incluida la ruta (`_links.self.href`) necesaria para hacer referencia a la acción de marketing al definir una directiva de uso de datos (`marketingActionsRefs`).

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

## Crear o actualizar una acción de marketing

La API de servicio de directivas permite definir sus propias acciones de marketing, así como actualizar las existentes. Tanto la creación como la actualización se realizan mediante una operación PUT en el nombre de la acción de marketing.

**Formato API**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Solicitud**

En la solicitud siguiente, observe que la carga útil `name` de la solicitud es la misma que la de la llamada `{marketingActionName}` de API. A diferencia `id` de lo que sucede con una política de solo lectura y generada por el sistema, la creación de una acción de marketing requiere que proporcione el nombre _deseado_ de la acción de marketing a medida que la crea.

>[!NOTE] Si no se proporciona el `{marketingActionName}` en la llamada, se producirá un error 405 (método no permitido), ya que no se le permitirá realizar directamente una PUT en el `/marketingActions/custom` extremo. Además, si la `name` carga útil no coincide con la `{marketingActionName}` de la ruta, recibirá un error 400 (solicitud incorrecta).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Respuesta**

Si se crea correctamente, recibirá un estado HTTP 201 (Creado) y el cuerpo de respuesta contendrá los detalles de la acción de marketing recién creada. El `name` contenido de la respuesta debe coincidir con lo que se envió en la solicitud.

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

## Eliminar una acción de mercadotecnia

Es posible eliminar las acciones de marketing enviando una solicitud DELETE a la parte `{marketingActionName}` de la acción de marketing que desee eliminar.

>[!NOTE] No puede eliminar las acciones de marketing a las que se hace referencia al salir de las directivas. Al intentar hacerlo, se producirá un error 400 (solicitud incorrecta) junto con un mensaje de error que incluye los ID `id` (o múltiples) de cualquier directiva (o directivas) que contenga una referencia a la acción de marketing que intenta eliminar.

**Formato API**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Solicitud**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Si la acción de marketing se ha eliminado correctamente, el cuerpo de la respuesta estará en blanco con un estado HTTP 200 (correcto).

Para confirmar la eliminación, intente buscar (OBTENER) la acción de marketing. Debe recibir un estado HTTP 404 (no encontrado) junto con un mensaje de error &quot;No encontrado&quot; porque la acción de marketing se ha eliminado.
