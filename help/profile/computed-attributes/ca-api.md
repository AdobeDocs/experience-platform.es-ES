---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Punto final de API de atributos calculados
type: Documentation
description: En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Esta guía muestra cómo crear, ver, actualizar y eliminar atributos calculados mediante la API de perfil del cliente en tiempo real.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 3%

---

# (Alpha) Extremo de API de atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada que se describe en este documento está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. Esta guía incluye llamadas de API de ejemplo para realizar operaciones básicas de CRUD mediante `/computedAttributes` punto final.

Para obtener más información acerca de los atributos calculados, comience por leer el [información general sobre atributos calculados](overview.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte del [API de perfil del cliente en tiempo real](https://www.adobe.com/go/profile-apis-en).

Antes de continuar, consulte la [Guía de introducción a la API de perfil](../api/getting-started.md) para obtener vínculos a la documentación recomendada, una guía para leer las llamadas de API de ejemplo que aparecen en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Configuración de un campo de atributo calculado

Para crear un atributo calculado, primero debe identificar el campo en un esquema que contenga el valor del atributo calculado.

Consulte la documentación sobre [configuración de un atributo calculado](configure-api.md) para obtener una guía completa de extremo a extremo sobre la creación de un campo de atributo calculado en un esquema.

>[!WARNING]
>
>Para continuar con la guía de la API, debe tener configurado un campo de atributo calculado.

## Creación de un atributo calculado {#create-a-computed-attribute}

Con el campo de atributo calculado definido en el esquema Perfil habilitado, ahora puede configurar un atributo calculado. Si aún no lo ha hecho, siga el flujo de trabajo descrito en la [configuración de un atributo calculado](configure-api.md) documentación.

Para crear un atributo calculado, comience por realizar una solicitud de POST a `/config/computedAttributes` extremo con un cuerpo de solicitud que contiene los detalles del atributo calculado que desea crear.

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
| `name` | Nombre del campo de atributo calculado, como cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro de `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los varios niveles de `properties` atributos. |
| `{TENANT_ID}` | Si no conoce su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Una descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros usuarios de la organización a determinar el atributo calculado correcto que se debe utilizar. |
| `expression.value` | Un válido [!DNL Profile Query Language] Expresión (PQL). Actualmente, los atributos calculados admiten las siguientes funciones: suma, recuento, mínimo, máximo y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [expresiones PQL de ejemplo](expressions.md) documentación. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent. |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo calculado recién creado. Estos detalles incluyen un único, de solo lectura, generado por el sistema `id` que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de API.

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
| `id` | ID único, de solo lectura y generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de la API. |
| `imsOrgId` | La organización de IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto de zona protegida contiene detalles de la zona protegida en la que se configuró el atributo calculado. Esta información se obtiene del encabezado de la zona protegida enviado en la solicitud. Para obtener más información, consulte la [información general sobre zonas protegidas](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene el elemento deconstruido `path` al campo que se envió en la solicitud. |
| `returnSchema.meta:xdmType` | El tipo de campo donde se almacenará el atributo calculado. |
| `definedOn` | Matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha agregado a varios esquemas basados en diferentes clases. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. El valor predeterminado es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | La hora a la que se creó el atributo calculado y la última actualización, respectivamente. |

## Crear un atributo calculado que haga referencia a atributos calculados existentes

También es posible crear un atributo calculado que haga referencia a atributos calculados existentes. Para ello, comience por realizar una solicitud de POST a la `/config/computedAttributes` punto final. El cuerpo de la solicitud contendrá referencias a los atributos calculados en la variable `expression.value` como se muestra en el ejemplo siguiente.

**Formato de API**

```http
POST /config/computedAttributes
```

**Solicitud**

En este ejemplo, ya se han creado dos atributos calculados que se utilizarán para definir un tercero. Los atributos calculados existentes son:

* **`totalSpend`:** Registra la cantidad total en dólares que ha gastado un cliente.
* **`countPurchases`:** Cuenta el número de compras que ha realizado un cliente.

La solicitud siguiente hace referencia a los dos atributos calculados existentes, utilizando un PQL válido para dividir a fin de calcular el nuevo `averageSpend` atributo calculado.

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
| `name` | Nombre del campo de atributo calculado, como cadena. |
| `path` | Ruta al campo que contiene el atributo calculado. Esta ruta se encuentra dentro de `properties` del esquema y NO debe incluir el nombre del campo en la ruta. Al escribir la ruta, omita los varios niveles de `properties` atributos. |
| `{TENANT_ID}` | Si no conoce su ID de inquilino, consulte los pasos para encontrar su ID de inquilino en la [Guía para desarrolladores de Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Una descripción del atributo calculado. Esto resulta especialmente útil una vez que se han definido varios atributos calculados, ya que ayudará a otros usuarios de la organización IMS a determinar el atributo calculado correcto que se debe utilizar. |
| `expression.value` | Una expresión PQL válida. Actualmente, los atributos calculados admiten las siguientes funciones: suma, recuento, mínimo, máximo y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [expresiones PQL de ejemplo](expressions.md) documentación.<br/><br/>En este ejemplo, la expresión hace referencia a dos atributos calculados existentes. Se hace referencia a los atributos mediante la variable `path` y el `name` del atributo calculado tal como aparece en el esquema en el que se definieron los atributos calculados. Por ejemplo, la variable `path` del primer atributo calculado al que se hace referencia es `_{TENANT_ID}.purchaseSummary` y el `name` es `totalSpend`. |
| `schema.name` | La clase en la que se basa el esquema que contiene el campo de atributo calculado. Ejemplo: `_xdm.context.experienceevent` para un esquema basado en la clase XDM ExperienceEvent. |

**Respuesta**

Un atributo calculado creado correctamente devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta que contiene los detalles del atributo calculado recién creado. Estos detalles incluyen un único, de solo lectura, generado por el sistema `id` que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de API.

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
| `id` | ID único, de solo lectura y generado por el sistema que se puede utilizar para hacer referencia al atributo calculado durante otras operaciones de la API. |
| `imsOrgId` | La organización de IMS relacionada con el atributo calculado debe coincidir con el valor enviado en la solicitud. |
| `sandbox` | El objeto de zona protegida contiene detalles de la zona protegida en la que se configuró el atributo calculado. Esta información se obtiene del encabezado de la zona protegida enviado en la solicitud. Para obtener más información, consulte la [información general sobre zonas protegidas](../../sandboxes/home.md). |
| `positionPath` | Matriz que contiene el elemento deconstruido `path` al campo que se envió en la solicitud. |
| `returnSchema.meta:xdmType` | El tipo de campo donde se almacenará el atributo calculado. |
| `definedOn` | Matriz que muestra los esquemas de unión en los que se ha definido el atributo calculado. Contiene un objeto por esquema de unión, lo que significa que puede haber varios objetos dentro de la matriz si el atributo calculado se ha agregado a varios esquemas basados en diferentes clases. |
| `active` | Un valor booleano que muestra si el atributo calculado está activo o no. El valor predeterminado es `true`. |
| `type` | El tipo de recurso creado, en este caso &quot;ComputedAttribute&quot; es el valor predeterminado. |
| `createEpoch` y `updateEpoch` | La hora a la que se creó el atributo calculado y la última actualización, respectivamente. |

## Acceso a atributos calculados

Al trabajar con atributos calculados mediante la API, existen dos opciones para acceder a los atributos calculados definidos por su organización. El primero es enumerar todos los atributos calculados, el segundo es ver un atributo calculado específico por su único `id`.

Los pasos para ambos patrones de acceso se describen en este documento. Seleccione una de las siguientes opciones para empezar:

* **[Enumerar todos los atributos calculados existentes](#list-all-computed-attributes):** Devuelve una lista de todos los atributos calculados existentes que ha creado su organización.
* **[Ver un atributo calculado específico](#view-a-computed-attribute):** Devuelva los detalles de un único atributo calculado especificando su ID durante la solicitud.

### Enumerar todos los atributos calculados {#list-all-computed-attributes}

GET Su organización de IMS puede crear varios atributos calculados y realizar una solicitud a la `/config/computedAttributes` el punto de conexión le permite enumerar todos los atributos calculados existentes para su organización.

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

La respuesta también incluye una `children` matriz compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un atributo calculado. Si su organización no tiene ningún atributo calculado, la variable `totalCount` y `pageSize` será 0 (cero) y el `children` la matriz estará vacía.

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
| `_page.totalCount` | Número total de atributos calculados definidos por su organización de IMS. |
| `_page.pageSize` | El número de atributos calculados devueltos en esta página de resultados. If `pageSize` is equal to `totalCount`, esto significa que solo hay una página de resultados y que se han devuelto todos los atributos calculados. Si no son iguales, se puede acceder a otras páginas de resultados. Consulte `_links.next` para obtener más información. |
| `children` | Matriz compuesta por uno o más objetos, cada uno de los cuales contiene los detalles de un único atributo calculado. Si no se han definido atributos calculados, la variable `children` la matriz está vacía. |
| `id` | Valor único, de sólo lectura y generado por el sistema que se asigna automáticamente a un atributo calculado cuando se crea. Para obtener más información sobre los componentes de un objeto de atributo calculado, consulte la sección sobre [creación de un atributo calculado](#create-a-computed-attribute) anteriormente en este tutorial. |
| `_links.next` | Si se devuelve una sola página de atributos calculados, `_links.next` es un objeto vacío, como se muestra en la respuesta de ejemplo anterior. Si su organización tiene muchos atributos calculados, estos se devolverán en varias páginas a las que puede acceder realizando una solicitud de GET a `_links.next` valor. |

### Ver un atributo calculado {#view-a-computed-attribute}

Puede ver un atributo calculado específico realizando una solicitud de GET a la variable `/config/computedAttributes` extremo e inclusión del ID de atributo calculado en la ruta de solicitud.

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

## Actualización de un atributo calculado

Si necesita actualizar un atributo calculado existente, puede hacerlo realizando una solicitud de PATCH a la variable `/config/computedAttributes` y que incluye el ID del atributo calculado que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parámetro | Descripción |
|---|---|
| `{ATTRIBUTE_ID}` | El ID del atributo calculado que desea actualizar. |

**Solicitud**

Esta solicitud utiliza [Formato de parche de JSON](https://datatracker.ietf.org/doc/html/rfc6902) para actualizar el &quot;valor&quot; del campo &quot;expresión&quot;.

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
| `{NEW_EXPRESSION_VALUE}` | Un válido [!DNL Profile Query Language] Expresión (PQL). Actualmente, los atributos calculados admiten las siguientes funciones: suma, recuento, mínimo, máximo y booleano. Para obtener una lista de expresiones de ejemplo, consulte la [expresiones PQL de ejemplo](expressions.md) documentación. |

**Respuesta**

Una actualización correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Si desea confirmar que la actualización se ha realizado correctamente, puede realizar una solicitud de GET para ver el atributo calculado por su ID.

## Eliminación de un atributo calculado

También es posible eliminar un atributo calculado mediante la API. Esto se hace realizando una solicitud de DELETE a la `/config/computedAttributes` punto final e incluir el ID del atributo calculado que desea eliminar en la ruta de solicitud.

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

Una solicitud de eliminación correcta devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para buscar el atributo calculado por su ID. Si se ha eliminado el atributo, recibirá un error de estado HTTP 404 (no encontrado).

## Creación de una definición de segmento que haga referencia a un atributo calculado

Adobe Experience Platform le permite crear segmentos que definen un grupo de atributos o comportamientos específicos a partir de un grupo de perfiles. Una definición de segmento incluye una expresión que encapsula una consulta escrita en PQL. Estas expresiones también pueden hacer referencia a atributos calculados.

En el ejemplo siguiente se crea una definición de segmento que hace referencia a un atributo calculado existente. Para obtener más información sobre las definiciones de segmentos y cómo trabajar con ellas en la API del servicio de segmentación, consulte la [guía de extremo de API de definiciones de segmento](../../segmentation/api/segment-definitions.md).

Para empezar, realice una solicitud de POST a `/segment/definitions` extremo, que proporciona el atributo calculado en el cuerpo de la solicitud.

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
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre único para el segmento, en forma de cadena. |
| `description` | Una descripción legible en lenguaje natural de la definición. |
| `schema.name` | El esquema asociado a las entidades del segmento. Consta de un `id` o `name` field. |
| `expression` | Objeto que contiene campos con información sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en el valor. Actualmente, solo `pql/text` es compatible. |
| `expression.value` | Una expresión PQL válida, en este ejemplo incluye una referencia a un atributo calculado existente. |

Para obtener más información sobre los atributos de definición de esquema, consulte los ejemplos proporcionados en la [guía de extremo de API de definiciones de segmento](../../segmentation/api/segment-definitions.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién creada. Para obtener más información sobre los objetos de respuesta de definición de segmento, consulte la [guía de extremo de API de definiciones de segmento](../../segmentation/api/segment-definitions.md).

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
