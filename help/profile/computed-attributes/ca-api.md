---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Extremo de API de atributos calculados
topic: guía
type: Documentación
description: En Adobe Experience Platform, los atributos calculados son funciones utilizadas para acumulados datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Esta guía muestra cómo crear, vista, actualizar y eliminar atributos calculados mediante la API de Perfil del cliente en tiempo real.
translation-type: tm+mt
source-git-commit: 6ae96ab25bd7992fe93d15bfc16b58a2fe7b4b7c
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 2%

---


# Extremo de API de atributos calculados (alfa)

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada descrita en este documento se encuentra actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumulados datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Esta guía incluye ejemplos de llamadas de API para realizar operaciones CRUD básicas mediante el extremo `/computedAttributes`.

Para obtener más información sobre los atributos calculados, lea la [descripción general de los atributos calculados](overview.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [API de Perfil del cliente en tiempo real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Antes de continuar, consulte la [guía de introducción a la API de Perfil](../api/getting-started.md) para ver los vínculos a la documentación recomendada, una guía para leer las llamadas a la API de muestra que aparecen en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Configuración de un campo de atributo calculado

Para crear un atributo calculado, primero debe identificar el campo en un esquema que contendrá el valor del atributo calculado.

Consulte la documentación sobre [configuración de un atributo calculado](configure-api.md) para obtener una guía completa de extremo a extremo sobre la creación de un campo de atributo calculado en un esquema.

>[!WARNING]
>
>Para continuar con la guía de API, debe tener configurado un campo de atributo calculado.

## Crear un atributo calculado {#create-a-computed-attribute}

Con el campo de atributo calculado definido en el esquema habilitado para Perfil, ahora puede configurar un atributo calculado. Si aún no lo ha hecho, siga el flujo de trabajo descrito en la [configuración de un atributo calculado](configure-api.md) documentación.

Para crear un atributo calculado, comience por realizar una solicitud de POST al extremo `/config/computedAttributes` con un cuerpo de solicitud que contenga los detalles del atributo calculado que desea crear.

**Formato API**

```http
POST /config/computedAttributes
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propiedad | Descripción |
|---|---|
| `name` | El nombre del campo de atributo calculado, como una cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro del atributo `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los múltiples niveles de atributos `properties`. |
| `{TENANT_ID}` | Si no está familiarizado con su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía del desarrollador del Registro de Esquema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros miembros de la organización de IMS a determinar el atributo calculado correcto que se debe utilizar. |
| `expression.value` | Una expresión [!DNL Profile Query Language] (PQL) válida. Los atributos calculados actualmente admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de muestra, consulte la [documentación de expresiones PQL de muestra](expressions.md). |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent. |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo computado recién creado. Estos detalles incluyen un `id` único, de sólo lectura y generado por el sistema que puede utilizarse para hacer referencia al atributo calculado durante otras operaciones de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Propiedad | Descripción |
|---|---|
| `id` | ID único, de sólo lectura, generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de API. |
| `imsOrgId` | La organización de IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto sandbox contiene detalles del entorno limitado en el que se configuró el atributo calculado. Esta información se obtiene a partir del encabezado del simulador para pruebas enviado en la solicitud. Para obtener más información, consulte la [información general de los entornos limitados](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene el `path` desconstruido en el campo que se envió en la solicitud. |
| `returnSchema.meta:xdmType` | Tipo del campo en el que se almacenará el atributo calculado. |
| `definedOn` | Una matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha agregado a varios esquemas en función de diferentes clases. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. De forma predeterminada, el valor es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | Hora a la que se creó y actualizó por última vez el atributo calculado, respectivamente. |

## Crear un atributo calculado que haga referencia a atributos calculados existentes

También es posible crear un atributo calculado que haga referencia a atributos calculados existentes. Para ello, comience por realizar una solicitud de POST al extremo `/config/computedAttributes`. El cuerpo de la solicitud contendrá referencias a los atributos calculados en el campo `expression.value` como se muestra en el ejemplo siguiente.

**Formato API**

```http
POST /config/computedAttributes
```

**Solicitud**

En este ejemplo, ya se han creado dos atributos calculados que se utilizarán para definir un tercero. Los atributos calculados existentes son:

* **`totalSpend`:** Captura la cantidad total en dólares que un cliente ha gastado.
* **`countPurchases`:** Cuenta el número de compras realizadas por un cliente.

La solicitud siguiente hace referencia a los dos atributos computados existentes, utilizando PQL válido para dividir a fin de calcular el nuevo atributo calculado `averageSpend`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propiedad | Descripción |
|---|---|
| `name` | El nombre del campo de atributo calculado, como una cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro del atributo `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los múltiples niveles de atributos `properties`. |
| `{TENANT_ID}` | Si no está familiarizado con su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía del desarrollador del Registro de Esquema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros miembros de la organización de IMS a determinar el atributo calculado correcto que se debe utilizar. |
| `expression.value` | Una expresión PQL válida. Los atributos calculados actualmente admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de muestra, consulte la [documentación de expresiones PQL de muestra](expressions.md).<br/><br/>En este ejemplo, la expresión hace referencia a dos atributos calculados existentes. Se hace referencia a los atributos mediante `path` y el `name` del atributo calculado tal como aparecen en el esquema en el que se definieron los atributos calculados. Por ejemplo, el `path` del primer atributo calculado al que se hace referencia es `_{TENANT_ID}.purchaseSummary` y el `name` es `totalSpend`. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent. |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo computado recién creado. Estos detalles incluyen un `id` único, de sólo lectura y generado por el sistema que puede utilizarse para hacer referencia al atributo calculado durante otras operaciones de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Propiedad | Descripción |
|---|---|
| `id` | ID único, de sólo lectura, generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de API. |
| `imsOrgId` | La organización de IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto sandbox contiene detalles del entorno limitado en el que se configuró el atributo calculado. Esta información se obtiene a partir del encabezado del simulador para pruebas enviado en la solicitud. Para obtener más información, consulte la [información general de los entornos limitados](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene el `path` desconstruido en el campo que se envió en la solicitud. |
| `returnSchema.meta:xdmType` | Tipo del campo en el que se almacenará el atributo calculado. |
| `definedOn` | Una matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha agregado a varios esquemas en función de diferentes clases. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. De forma predeterminada, el valor es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | Hora a la que se creó y actualizó por última vez el atributo calculado, respectivamente. |

## Acceso a atributos calculados

Al trabajar con atributos calculados mediante la API, hay dos opciones para acceder a atributos calculados que han sido definidas por su organización. La primera es la lista de todos los atributos calculados; la segunda es la vista de un atributo calculado específico por su `id` único.

En este documento se describen los pasos para ambos patrones de acceso. Seleccione una de las siguientes opciones para comenzar:

* **[Lista de todos los atributos](#list-all-computed-attributes) calculados existentes:** Devuelva una lista de todos los atributos calculados existentes que haya creado la organización.
* **[Vista de un atributo](#view-a-computed-attribute) calculado específico:** Devuelva los detalles de un único atributo calculado especificando su ID durante la solicitud.

### Lista de todos los atributos calculados {#list-all-computed-attributes}

La organización de IMS puede crear varios atributos calculados y realizar una solicitud de GET al extremo `/config/computedAttributes` le permite realizar la lista de todos los atributos calculados existentes para su organización.

**Formato API**

```http
GET /config/computedAttributes
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta incluye un atributo `_page` que proporciona el número total de atributos calculados (`totalCount`) y el número de atributos calculados en la página (`pageSize`).

La respuesta también incluye una matriz `children` compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un atributo calculado. Si su organización no tiene atributos calculados, la `totalCount` y `pageSize` serán 0 (cero) y la matriz `children` estará vacía.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propiedad | Descripción |
|---|---|
| `_page.totalCount` | El número total de atributos calculados definidos por la organización de IMS. |
| `_page.pageSize` | El número de atributos calculados devueltos en esta página de resultados. Si `pageSize` es igual a `totalCount`, significa que sólo hay una página de resultados y se han devuelto todos los atributos calculados. Si no son iguales, hay páginas adicionales de resultados a las que se puede acceder. Consulte `_links.next` para obtener más información. |
| `children` | Matriz compuesta de uno o varios objetos, cada uno de los cuales contiene los detalles de un único atributo calculado. Si no se han definido atributos calculados, la matriz `children` está vacía. |
| `id` | Un valor único, de sólo lectura, generado por el sistema y asignado automáticamente a un atributo calculado cuando se crea. Para obtener más información sobre los componentes de un objeto de atributo calculado, consulte la sección sobre [creación de un atributo calculado](#create-a-computed-attribute) anterior en este tutorial. |
| `_links.next` | Si se devuelve una sola página de atributos calculados, `_links.next` es un objeto vacío, como se muestra en la respuesta de ejemplo anterior. Si su organización tiene muchos atributos calculados, se devolverán en varias páginas a las que puede acceder realizando una solicitud de GET al valor `_links.next`. |

### Vista de un atributo calculado {#view-a-computed-attribute}

Puede realizar una vista de un atributo calculado específico realizando una solicitud de GET al extremo `/config/computedAttributes` e incluyendo el ID de atributo calculado en la ruta de la solicitud.

**Formato API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea vista. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Actualizar un atributo calculado

En caso de que necesite actualizar un atributo calculado existente, esto se puede hacer haciendo una solicitud de PATCH al extremo `/config/computedAttributes` e incluyendo el ID del atributo calculado que desea actualizar en la ruta de solicitud.

**Formato API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea actualizar. |

**Solicitud**

Esta solicitud utiliza el formato [JSON Patch](http://jsonpatch.com/) para actualizar el &quot;valor&quot; del campo &quot;expresión&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propiedad | Descripción |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Una expresión [!DNL Profile Query Language] (PQL) válida. Los atributos calculados actualmente admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de muestra, consulte la [documentación de expresiones PQL de muestra](expressions.md). |

**Respuesta**

Una actualización correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Si desea confirmar que la actualización se ha realizado correctamente, puede realizar una solicitud de GET para vista del atributo calculado por su ID.

## Eliminar un atributo calculado

También es posible eliminar un atributo calculado mediante la API. Esto se realiza realizando una solicitud de DELETE al extremo `/config/computedAttributes` e incluyendo el ID del atributo calculado que desea eliminar en la ruta de la solicitud.

>[!NOTE]
>
>Tenga cuidado al eliminar un atributo calculado, ya que puede estar en uso en más de un esquema y la operación de DELETE no se puede deshacer.

**Formato API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | ID del atributo calculado que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Respuesta**

Una solicitud de eliminación correcta devuelve Estado HTTP 200 (Aceptar) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para buscar el atributo calculado por su ID. Si se eliminó el atributo, recibirá un error de estado HTTP 404 (no encontrado).

## Crear una definición de segmento que haga referencia a un atributo calculado

Adobe Experience Platform permite crear segmentos que definen un grupo de atributos o comportamientos específicos a partir de un grupo de perfiles. Una definición de segmento incluye una expresión que encapsula una consulta escrita en PQL. Estas expresiones también pueden hacer referencia a atributos calculados.

El ejemplo siguiente crea una definición de segmento que hace referencia a un atributo calculado existente. Para obtener más información sobre las definiciones de segmentos y cómo trabajar con ellos en la API de servicio de segmentación, consulte la [guía de extremo de la API de definiciones de segmentos](../../segmentation/api/segment-definitions.md).

Para comenzar, realice una solicitud de POST al extremo `/segment/definitions`, proporcionando el atributo calculado en el cuerpo de la solicitud.

**Formato API**

```http
POST /segment/definitions
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre único para el segmento, como cadena. |
| `description` | Una descripción de la definición legible por el usuario. |
| `schema.name` | El esquema asociado a las entidades del segmento. Consiste en un campo `id` o `name`. |
| `expression` | Objeto que contiene campos con información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, solo se admite `pql/text`. |
| `expression.value` | Una expresión PQL válida, en este ejemplo incluye una referencia a un atributo computado existente. |

Para obtener más información sobre los atributos de definición de esquema, consulte los ejemplos que se proporcionan en la [guía de extremo de la API de definiciones de segmentos](../../segmentation/api/segment-definitions.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición de segmento recién creada. Para obtener más información sobre los objetos de respuesta de definición de segmento, consulte la guía de extremo de la API de definiciones de segmento [](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Pasos siguientes

Ahora que ha aprendido los conceptos básicos de los atributos calculados, está listo para empezar a definirlos para su organización.