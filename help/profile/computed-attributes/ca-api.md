---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Punto final de API de atributos calculados
topic-legacy: guide
type: Documentation
description: En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización. Esta guía muestra cómo crear, ver, actualizar y eliminar atributos calculados mediante la API de perfil del cliente en tiempo real.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 3%

---

# (Alpha) Extremo de API de atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada que se describe en este documento está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización. Esta guía incluye ejemplos de llamadas de API para realizar operaciones básicas de CRUD usando la variable `/computedAttributes` punto final.

Para obtener más información sobre los atributos calculados, comience por leer el [información general sobre atributos calculados](overview.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [API de perfil de cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Antes de continuar, revise la [Guía de introducción a la API de perfil](../api/getting-started.md) para ver vínculos a la documentación recomendada, una guía para leer las llamadas de API de ejemplo que aparecen en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Configuración de un campo de atributo calculado

Para crear un atributo calculado, primero debe identificar el campo en un esquema que contendrá el valor del atributo calculado.

Consulte la documentación de [configuración de un atributo calculado](configure-api.md) para obtener una guía completa de extremo a extremo sobre la creación de un campo de atributo calculado en un esquema.

>[!WARNING]
>
>Para continuar con la guía de API, debe tener configurado un campo de atributo calculado.

## Crear un atributo calculado {#create-a-computed-attribute}

Con el campo de atributo calculado definido en el esquema de perfil habilitado, ahora puede configurar un atributo calculado. Si aún no lo ha hecho, siga el flujo de trabajo descrito en la sección [configuración de un atributo calculado](configure-api.md) documentación.

Para crear un atributo calculado, comience por realizar una solicitud de POST al `/config/computedAttributes` con un cuerpo de solicitud que contiene los detalles del atributo calculado que desea crear.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propiedad | Descripción |
|---|---|
| `name` | Nombre del campo de atributo calculado como una cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro de la variable `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los múltiples niveles de `properties` atributos. |
| `{TENANT_ID}` | Si no está familiarizado con su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros miembros de su organización de IMS a determinar el atributo calculado correcto que deben utilizar. |
| `expression.value` | Un [!DNL Profile Query Language] (PQL). Actualmente, los atributos calculados admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [muestras de expresiones PQL](expressions.md) documentación. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent . |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo calculado recién creado. Estos detalles incluyen una variable única, de solo lectura, generada por el sistema `id` que se puede usar para hacer referencia al atributo calculado durante otras operaciones de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
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
| `id` | ID único, de solo lectura, generado por el sistema que se puede usar para hacer referencia al atributo calculado durante otras operaciones de API. |
| `imsOrgId` | La organización IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto sandbox contiene detalles del simulador de pruebas en el que se configuró el atributo calculado. Esta información se extrae del encabezado del simulador de pruebas enviado en la solicitud. Para obtener más información, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene la matriz desconstruida `path` al campo enviado en la solicitud. |
| `returnSchema.meta:xdmType` | Tipo del campo en el que se almacenará el atributo calculado. |
| `definedOn` | Matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha añadido a varios esquemas basados en clases diferentes. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. El valor predeterminado es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | Hora a la que se creó y actualizó por última vez el atributo calculado, respectivamente. |

## Crear un atributo calculado que haga referencia a atributos calculados existentes

También es posible crear un atributo calculado que haga referencia a atributos calculados existentes. Para ello, comience por realizar una solicitud de POST al `/config/computedAttributes` punto final. El cuerpo de la solicitud contiene referencias a los atributos calculados en la variable `expression.value` como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /config/computedAttributes
```

**Solicitud**

En este ejemplo, ya se han creado dos atributos calculados que se utilizarán para definir un tercero. Los atributos calculados existentes son:

* **`totalSpend`:** Captura la cantidad total en dólares que ha gastado un cliente.
* **`countPurchases`:** Cuenta el número de compras que ha realizado un cliente.

La siguiente solicitud hace referencia a los dos atributos calculados existentes, utilizando un PQL válido para dividir para calcular el nuevo `averageSpend` atributo calculado.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propiedad | Descripción |
|---|---|
| `name` | Nombre del campo de atributo calculado como una cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro de la variable `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los múltiples niveles de `properties` atributos. |
| `{TENANT_ID}` | Si no está familiarizado con su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros miembros de su organización de IMS a determinar el atributo calculado correcto que deben utilizar. |
| `expression.value` | Una expresión PQL válida. Actualmente, los atributos calculados admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [muestras de expresiones PQL](expressions.md) documentación.<br/><br/>En este ejemplo, la expresión hace referencia a dos atributos calculados existentes. Se hace referencia a los atributos mediante la variable `path` y `name` del atributo calculado tal como aparecen en el esquema en el que se definieron los atributos calculados. Por ejemplo, la variable `path` del primer atributo calculado al que se hace referencia es `_{TENANT_ID}.purchaseSummary` y `name` es `totalSpend`. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent . |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo calculado recién creado. Estos detalles incluyen una variable única, de solo lectura, generada por el sistema `id` que se puede usar para hacer referencia al atributo calculado durante otras operaciones de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
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
| `id` | ID único, de solo lectura, generado por el sistema que se puede usar para hacer referencia al atributo calculado durante otras operaciones de API. |
| `imsOrgId` | La organización IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto sandbox contiene detalles del simulador de pruebas en el que se configuró el atributo calculado. Esta información se extrae del encabezado del simulador de pruebas enviado en la solicitud. Para obtener más información, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene la matriz desconstruida `path` al campo enviado en la solicitud. |
| `returnSchema.meta:xdmType` | Tipo del campo en el que se almacenará el atributo calculado. |
| `definedOn` | Matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha añadido a varios esquemas basados en clases diferentes. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. El valor predeterminado es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | Hora a la que se creó y actualizó por última vez el atributo calculado, respectivamente. |

## Acceso a atributos calculados

Al trabajar con atributos calculados mediante la API, hay dos opciones para acceder a atributos calculados que han sido definidas por su organización. El primero es enumerar todos los atributos calculados, el segundo es ver un atributo calculado específico por su único `id`.

En este documento se describen los pasos para ambos patrones de acceso. Seleccione una de las siguientes opciones para comenzar:

* **[Enumerar todos los atributos calculados existentes](#list-all-computed-attributes):** Devuelve una lista de todos los atributos calculados existentes que ha creado su organización.
* **[Ver un atributo calculado específico](#view-a-computed-attribute):** Devuelven los detalles de un único atributo calculado especificando su ID durante la solicitud.

### Enumerar todos los atributos calculados {#list-all-computed-attributes}

Su organización IMS puede crear varios atributos calculados y realizar una solicitud de GET al `/config/computedAttributes` El extremo de le permite enumerar todos los atributos calculados existentes para su organización.

**Formato de API**

```http
GET /config/computedAttributes
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta incluye una `_page` que proporciona el número total de atributos calculados (`totalCount`) y el número de atributos calculados en la página (`pageSize`).

La respuesta también incluye un `children` matriz compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un atributo calculado. Si su organización no tiene atributos calculados, la variable `totalCount` y `pageSize` será 0 (cero) y la variable `children` la matriz estará vacía.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
                "type": "PQL", 
                "format": "pql/text", 
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
| `_page.totalCount` | El número total de atributos calculados definidos por su organización de IMS. |
| `_page.pageSize` | Número de atributos calculados devueltos en esta página de resultados. If `pageSize` es igual a `totalCount`, esto significa que solo hay una página de resultados y que se han devuelto todos los atributos calculados. Si no son iguales, hay páginas adicionales de resultados a las que se puede acceder. Consulte `_links.next` para obtener más información. |
| `children` | Matriz compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un único atributo calculado. Si no se han definido atributos calculados, la variable `children` la matriz está vacía. |
| `id` | Valor único, de solo lectura, generado por el sistema y asignado automáticamente a un atributo calculado cuando se crea. Para obtener más información sobre los componentes de un objeto de atributo calculado, consulte la sección de [creación de un atributo calculado](#create-a-computed-attribute) más temprano en este tutorial. |
| `_links.next` | Si se devuelve una sola página de atributos calculados, `_links.next` es un objeto vacío, como se muestra en la respuesta de ejemplo anterior. Si su organización tiene muchos atributos calculados, se devolverán en varias páginas a las que puede acceder realizando una solicitud de GET a la variable `_links.next` valor. |

### Ver un atributo calculado {#view-a-computed-attribute}

Puede ver un atributo calculado específico realizando una solicitud de GET al `/config/computedAttributes` e incluir el ID de atributo calculado en la ruta de solicitud.

**Formato de API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | El ID del atributo calculado que desea ver. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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

Si encuentra que necesita actualizar un atributo calculado existente, esto se puede hacer realizando una solicitud del PATCH al `/config/computedAttributes` e incluye el ID del atributo calculado que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | El ID del atributo calculado que desea actualizar. |

**Solicitud**

Esta solicitud utiliza [Formato de parche JSON](https://datatracker.ietf.org/doc/html/rfc6902) para actualizar el &quot;valor&quot; del campo &quot;expresión&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propiedad | Descripción |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Un [!DNL Profile Query Language] (PQL). Actualmente, los atributos calculados admiten las siguientes funciones: sum, count, min, max y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [muestras de expresiones PQL](expressions.md) documentación. |

**Respuesta**

Una actualización correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Si desea confirmar que la actualización se ha realizado correctamente, puede realizar una solicitud de GET para ver el atributo calculado por su ID.

## Eliminar un atributo calculado

También es posible eliminar un atributo calculado mediante la API. Para ello, realice una solicitud de DELETE al `/config/computedAttributes` e incluye el ID del atributo calculado que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
>Tenga cuidado al eliminar un atributo calculado, ya que puede estar en uso en más de un esquema y la operación de DELETE no se puede deshacer.

**Formato de API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | El ID del atributo calculado que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Respuesta**

Una solicitud de eliminación correcta devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para buscar el atributo calculado por su ID. Si se eliminó el atributo, recibirá un error de estado HTTP 404 (no encontrado).

## Crear una definición de segmento que haga referencia a un atributo calculado

Adobe Experience Platform le permite crear segmentos que definen un grupo de atributos o comportamientos específicos de un grupo de perfiles. Una definición de segmento incluye una expresión que encapsula una consulta escrita en PQL. Estas expresiones también pueden hacer referencia a atributos calculados.

En el siguiente ejemplo se crea una definición de segmento que hace referencia a un atributo calculado existente. Para obtener más información sobre las definiciones de segmentos y cómo trabajar con ellas en la API del servicio de segmentación, consulte la [guía de extremo de API de definiciones de segmentos](../../segmentation/api/segment-definitions.md).

Para empezar, realice una solicitud de POST al `/segment/definitions` , proporcionando el atributo calculado en el cuerpo de la solicitud.

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Un nombre único para el segmento, como una cadena. |
| `description` | Una descripción de la definición legible en lenguaje natural. |
| `schema.name` | El esquema asociado a las entidades del segmento. Consiste en una `id` o `name` campo . |
| `expression` | Un objeto que contiene campos con información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, solo `pql/text` es compatible. |
| `expression.value` | Una expresión PQL válida, en este ejemplo incluye una referencia a un atributo computado existente. |

Para obtener más información sobre los atributos de definición de esquema, consulte los ejemplos proporcionados en la [guía de extremo de API de definiciones de segmentos](../../segmentation/api/segment-definitions.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién creada. Para obtener más información sobre los objetos de respuesta de definición de segmento, consulte [guía de extremo de API de definiciones de segmentos](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
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
