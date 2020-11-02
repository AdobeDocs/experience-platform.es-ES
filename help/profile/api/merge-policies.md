---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 'Políticas de combinación: API de Perfil del cliente en tiempo real'
topic: guide
translation-type: tm+mt
source-git-commit: 47c65ef5bdd083c2e57254189bb4a1f1d9c23ccc
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 1%

---


# Combinar extremo de directivas

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se ingieren en la plataforma, se combinan para crear un solo perfil para ese cliente. Cuando los datos de varias fuentes entran en conflicto (por ejemplo, un fragmento lista al cliente como &quot;soltero&quot; mientras que el otro lista al cliente como &quot;casado&quot;), la política de combinación determina qué información incluir en el perfil del individuo.

Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona los pasos para trabajar con políticas de combinación mediante la API.

Para trabajar con directivas de combinación mediante la interfaz de usuario, consulte la guía [del usuario de directivas de](../ui/merge-policies.md)combinación.

## Primeros pasos

El punto final de API utilizado en esta guía forma parte del [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Componentes de políticas de combinación {#components-of-merge-policies}

Las políticas de combinación son privadas para la organización de IMS, lo que le permite crear diferentes políticas para combinar esquemas de la manera específica que necesite. Cualquier API que acceda a [!DNL Profile] los datos requiere una directiva de combinación, aunque se utilizará una predeterminada si no se proporciona una de forma explícita. [!DNL Platform] proporciona una directiva de combinación predeterminada o puede crear una directiva de combinación para un esquema específico y marcarla como predeterminada para su organización. Cada organización puede tener varias directivas de combinación por esquema, pero cada esquema solo puede tener una directiva de combinación predeterminada. Cualquier directiva de combinación establecida como predeterminada se utilizará en los casos en que se proporcione el nombre del esquema y se requiera una directiva de combinación pero no se proporcione. Cuando se establece una directiva de combinación como predeterminada, cualquier directiva de combinación existente que se haya establecido anteriormente como predeterminada se actualizará automáticamente para que ya no se utilice como predeterminada.

### Completar objeto de directiva de combinación

El objeto de directiva de combinación completa representa un conjunto de preferencias que controlan los aspectos de la combinación de fragmentos de perfil.

**Combinar objeto de directiva**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propiedad | Descripción |
|---|---|
| `id` | El sistema generó un identificador único asignado en el momento de la creación |
| `name` | Nombre descriptivo por el cual se puede identificar la directiva de combinación en vistas de lista. |
| `imsOrgId` | ID de organización a la que pertenece esta directiva de combinación |
| `identityGraph` | [Objeto gráfico](#identity-graph) de identidad que indica el gráfico de identidad desde el que se obtendrán las identidades relacionadas. Se combinarán los fragmentos de perfil encontrados para todas las identidades relacionadas. |
| `attributeMerge` | [Objeto de combinación](#attribute-merge) de atributos que indica la forma en que la directiva de combinación dará prioridad a los atributos de perfil en caso de conflictos de datos. |
| `schema` | El objeto [esquema](#schema) en el que se puede utilizar la directiva de combinación. |
| `default` | Valor booleano que indica si esta directiva de combinación es la predeterminada para el esquema especificado. |
| `version` | [!DNL Platform] versión mantenida de la directiva de combinación. Este valor de solo lectura se incrementa cada vez que se actualiza una directiva de combinación. |
| `updateEpoch` | Fecha de la última actualización de la directiva de combinación. |

**Ejemplo de directiva de combinación**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Gráfico de identidad {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) administra los gráficos de identidad utilizados globalmente y para cada organización en [!DNL Experience Platform]. El `identityGraph` atributo de la directiva de combinación define cómo determinar las identidades relacionadas para un usuario.

**identityGraph, objeto**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Donde `{IDENTITY_GRAPH_TYPE}` es uno de los siguientes:

* **&quot;ninguno&quot;:** No realice ninguna vinculación de identidad.
* **&quot;pdg&quot;:** Realice la vinculación de identidad en función del gráfico de identidad privado.

**Ejemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Combinación de atributos {#attribute-merge}

Un fragmento de perfil es la información de perfil para una sola identidad de la lista de identidades que existen para un usuario en particular. Cuando el tipo de gráfico de identidad utilizado da como resultado más de una identidad, es posible que haya atributos de perfil en conflicto y se debe especificar la prioridad. Con `attributeMerge`, puede especificar qué atributos de perfil se priorizarán en el evento de un conflicto de combinación entre conjuntos de datos de tipo Valor clave (datos de registro).

**attributeMerge, objeto**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Donde `{ATTRIBUTE_MERGE_TYPE}` es uno de los siguientes:

* **`timestampOrdered`**:: (predeterminado) Asigne prioridad al perfil que se actualizó por última vez. Con este tipo de combinación, no es necesario el `data` atributo. `timestampOrdered` también admite marcas de hora personalizadas que tendrán prioridad al combinar fragmentos de perfil dentro de conjuntos de datos o entre conjuntos de datos. Para obtener más información, consulte la sección Apéndice sobre el [uso de marcas de hora](#custom-timestamps)personalizadas.
* **`dataSetPrecedence`** :: Asigne prioridad a los fragmentos de perfil en función del conjunto de datos del que provienen. Esto se puede utilizar cuando la información presente en un conjunto de datos es preferible o de confianza sobre los datos de otro conjunto de datos. Cuando se utiliza este tipo de combinación, el `order` atributo es obligatorio, ya que lista los conjuntos de datos en el orden de prioridad.
   * **`order`**:: Cuando se utiliza &quot;dataSetPrience&quot;, se debe proporcionar una `order` matriz con una lista de conjuntos de datos. Los conjuntos de datos no incluidos en la lista no se combinarán. En otras palabras, los conjuntos de datos deben enumerarse explícitamente para combinarse en un perfil. La `order` matriz lista los ID de los conjuntos de datos en orden de prioridad.

**Ejemplo de objeto attributeMerge con `dataSetPrecedence` type**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Ejemplo de objeto attributeMerge con `timestampOrdered` type**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Esquema {#schema}

El objeto esquema especifica el esquema del modelo de datos de experiencia (XDM) para el que se crea esta directiva de combinación.

**`schema`object**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Donde el valor de `name` es el nombre de la clase XDM en la que se basa el esquema asociado con la política de combinación.

**Ejemplo`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Para obtener más información sobre XDM y trabajar con esquemas en Experience Platform, lea la información general [del sistema](../../xdm/home.md)XDM.

## Directivas de combinación de acceso {#access-merge-policies}

Con la [!DNL Real-time Customer Profile] API, el `/config/mergePolicies` punto final permite realizar una solicitud de búsqueda para la vista de una directiva de combinación específica por su ID o acceder a todas las directivas de combinación de la organización de IMS, filtradas por criterios específicos. También puede utilizar el extremo para recuperar varias directivas de combinación por sus ID. `/config/mergePolicies/bulk-get` Los pasos para realizar cada una de estas llamadas se describen en las siguientes secciones.

### Acceso a una única directiva de combinación por ID

Puede acceder a una única directiva de combinación mediante su ID realizando una solicitud de GET al extremo e incluyendo la `/config/mergePolicies` `mergePolicyId` en la ruta de la solicitud.

**Formato API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la directiva de combinación que desea eliminar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Consulte los [componentes de la sección de políticas](#components-of-merge-policies) de combinación al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

### Recuperar varias directivas de combinación por sus ID

Puede recuperar varias directivas de combinación haciendo una solicitud de POST al extremo e incluyendo los ID de las directivas de combinación que desee recuperar en el cuerpo de la solicitud. `/config/mergePolicies/bulk-get`

**Formato API**

```http
POST /config/mergePolicies/bulk-get
```

**Solicitud**

El cuerpo de la solicitud incluye una matriz &quot;ids&quot; con objetos individuales que contienen la &quot;id&quot; de cada directiva de combinación para la que desea recuperar detalles.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Respuesta**

Una respuesta correcta devuelve Estado HTTP 207 (Varios estados) y los detalles de las directivas de combinación cuyos ID se proporcionaron en la solicitud del POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Consulte los [componentes de la sección de políticas](#components-of-merge-policies) de combinación al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

### Lista de varias directivas de combinación por criterios

Puede lista de varias directivas de combinación dentro de la organización de IMS enviando una solicitud de GET al extremo y utilizando parámetros de consulta opcionales para filtrar, ordenar y paginar la respuesta. `/config/mergePolicies` Se pueden incluir varios parámetros, separados por signos de &amp;. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las directivas de combinación disponibles para su organización.

**Formato API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parámetro | Descripción |
|---|---|
| `default` | Valor booleano que filtros los resultados según si las directivas de combinación son o no el valor predeterminado para una clase de esquema. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. Valor predeterminado: 20 |
| `orderBy` | Especifica el campo por el que se ordenan los resultados como `orderBy=name` o `orderBy=+name` se ordenan por nombre en orden ascendente o `orderBy=-name`en orden descendente. Si se omite este valor, se ordenará de forma predeterminada `name` en orden ascendente. |
| `schema.name` | Nombre del esquema para el que se recuperan las directivas de combinación disponibles. |
| `identityGraph.type` | Filtros los resultados según el tipo de gráfico de identidad. Los valores posibles incluyen &quot;none&quot; y &quot;pdg&quot; (gráfico privado). |
| `attributeMerge.type` | Filtros los resultados según el tipo de combinación de atributos utilizado. Los valores posibles incluyen &quot;timestampOrdered&quot; y &quot;dataSetPrience&quot;. |
| `start` | Desplazamiento de página: especifique el ID de inicio de los datos que se van a recuperar. Valor predeterminado: 0 |
| `version` | Especifique esto si desea utilizar una versión específica de la directiva de combinación. De forma predeterminada, se utilizará la última versión. |

Para obtener más información acerca de `schema.name`, `identityGraph.type`y `attributeMerge.type`, consulte la sección [Componentes de directivas](#components-of-merge-policies) de combinación que se proporcionó anteriormente en esta guía.


**Solicitud**

La siguiente solicitud lista todas las directivas de combinación para un esquema determinado:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Respuesta**

Una respuesta correcta devuelve una lista paginada de directivas de combinación que cumplen los criterios especificados por los parámetros de consulta enviados en la solicitud.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Propiedad | Descripción |
|---|---|
| `_links.next.href` | Una dirección URI para la siguiente página de resultados. Use este URI como parámetro de solicitud para otra llamada de API al mismo extremo para realizar una vista de la página. Si no existe ninguna página siguiente, este valor será una cadena vacía. |

## Crear una directiva de combinación

Puede crear una nueva directiva de combinación para su organización haciendo una solicitud de POST al `/config/mergePolicies` extremo.

**Formato API**

```http
POST /config/mergePolicies
```

**Solicitud** La siguiente solicitud crea una nueva directiva de combinación, que se configura con los valores de atributo proporcionados en la carga útil:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Propiedad | Descripción |
|---|---|
| `name` | Un nombre descriptivo que permite identificar la política de combinación en vistas de lista. |
| `identityGraph.type` | Tipo de gráfico de identidad del que se van a combinar las identidades relacionadas. Valores posibles: &quot;none&quot; o &quot;pdg&quot; (gráfico privado). |
| `attributeMerge` | Modo en el que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | Clase de esquema XDM asociada a la directiva de combinación. |
| `default` | Especifica si esta directiva de combinación es la predeterminada para el esquema. |

Consulte la sección [Componentes de políticas](#components-of-merge-policies) de combinación para obtener más información.

**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación recién creada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Consulte los [componentes de la sección de políticas](#components-of-merge-policies) de combinación al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

## Actualizar una directiva de combinación {#update}

Puede modificar una directiva de combinación existente editando atributos individuales (PATCH) o sobrescribiendo toda la directiva de combinación con atributos nuevos (PUT). A continuación se muestran ejemplos de cada uno.

### Editar campos de directiva de combinación individuales

Puede editar campos individuales para una directiva de combinación realizando una solicitud de PATCH al punto final `/config/mergePolicies/{mergePolicyId}` :

**Formato API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la directiva de combinación que desea eliminar. |

**Solicitud**

La siguiente solicitud actualiza una directiva de combinación especificada cambiando el valor de su `default` propiedad a `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Propiedad | Descripción |
|---|---|
| `op` | Especifica la operación que se va a realizar. Encontrará ejemplos de otras operaciones de PATCH en la documentación del parche [JSON](http://jsonpatch.com) |
| `path` | Ruta del campo que se va a actualizar. Los valores aceptados son: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | El valor en el que se va a establecer el campo especificado. |

Consulte la sección [Componentes de políticas](#components-of-merge-policies) de combinación para obtener más información.


**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación recientemente actualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Sobrescribir una directiva de combinación

Otra forma de modificar una directiva de combinación es utilizar una solicitud de PUT, que sobrescribe toda la directiva de combinación.

**Formato API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la directiva de combinación que desea sobrescribir. |

**Solicitud**

La siguiente solicitud sobrescribe la directiva de combinación especificada y sustituye sus valores de atributo por los proporcionados en la carga útil. Dado que esta solicitud reemplaza por completo una directiva de combinación existente, es necesario proporcionar todos los campos necesarios al definir originalmente la directiva de combinación. Sin embargo, esta vez se proporcionan valores actualizados para los campos que se desean cambiar.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propiedad | Descripción |
|---|---|
| `name` | Un nombre descriptivo que permite identificar la política de combinación en vistas de lista. |
| `identityGraph` | El gráfico de identidad desde el cual se van a combinar las identidades relacionadas. |
| `attributeMerge` | Modo en el que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | Clase de esquema XDM asociada a la directiva de combinación. |
| `default` | Especifica si esta directiva de combinación es la predeterminada para el esquema. |

Consulte la sección [Componentes de políticas](#components-of-merge-policies) de combinación para obtener más información.


**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación actualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Eliminar una directiva de combinación

Una directiva de combinación se puede eliminar realizando una solicitud de DELETE al extremo e incluyendo el ID de la directiva de combinación que desea eliminar en la ruta de la solicitud. `/config/mergePolicies`

**Formato API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la directiva de combinación que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina una directiva de combinación.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una solicitud de eliminación correcta devuelve Estado HTTP 200 (Aceptar) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para la vista de la directiva de combinación por su ID. Si se eliminó la directiva de combinación, recibirá un error de estado HTTP 404 (no encontrado).

## Pasos siguientes

Ahora que sabe cómo crear y configurar directivas de combinación para su organización de IMS, puede utilizarlas para crear segmentos de audiencia a partir de sus [!DNL Real-time Customer Profile] datos. Consulte la documentación [del servicio de segmentación de](../../segmentation/home.md) Adobe Experience Platform para empezar a definir y trabajar con segmentos.

## Apéndice

Esta sección proporciona información adicional relacionada con el trabajo con políticas de combinación.

### Uso de marcas de hora personalizadas {#custom-timestamps}

Como los registros se ingieren en Experience Platform, se obtiene una marca de hora del sistema en el momento de la ingestión y se agrega al registro. Cuando `timestampOrdered` se selecciona como `attributeMerge` tipo para una directiva de combinación, los perfiles se combinan en función de la marca de tiempo del sistema. En otras palabras, la combinación se realiza en función de la marca de tiempo para cuando el registro se ingesta en la plataforma.

Ocasionalmente puede haber casos de uso, como rellenar datos o asegurar el orden correcto de eventos si los registros se ingieren por orden, donde es necesario proporcionar una marca de tiempo personalizada y que la directiva de combinación respete la marca de tiempo personalizada en lugar de la marca de tiempo del sistema.

Para utilizar una marca de tiempo personalizada, [[!DNL External Source System Audit Details Mixin]](#mixin-details) debe agregarla al esquema de Perfil. Una vez agregada, la marca de tiempo personalizada se puede rellenar mediante el `xdm:lastUpdatedDate` campo. Cuando se ingesta un registro con el `xdm:lastUpdatedDate` campo rellenado, el Experience Platform utilizará ese campo para combinar registros o fragmentos de perfil dentro y entre conjuntos de datos. Si no `xdm:lastUpdatedDate` está presente, o no se ha rellenado, Platform seguirá usando la marca de tiempo del sistema.

>[!NOTE]
>
>Debe asegurarse de que la `xdm:lastUpdatedDate` marca de tiempo se rellena al enviar un PATCH en el mismo registro.

Para obtener instrucciones paso a paso sobre cómo trabajar con esquemas mediante la API del Registro de Esquemas, incluida la forma de agregar mezclas a esquemas, visite el [tutorial para crear un esquema mediante la API](../../xdm/tutorials/create-schema-api.md).

Para trabajar con marcas de hora personalizadas mediante la interfaz de usuario, consulte la sección sobre el [uso de marcas de hora](../ui/merge-policies.md#custom-timestamps) personalizadas en la guía [del usuario de directivas de](../ui/merge-policies.md)combinación.

#### [!DNL External Source System Audit Details Mixin] detalles {#mixin-details}

En el siguiente ejemplo se muestran los campos rellenados correctamente en el [!DNL External Source System Audit Details Mixin]. La combinación completa JSON también se puede ver en la repo [pública del Modelo de datos de experiencia (XDM) en GitHub](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) .

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```




