---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Punto final de la API de políticas de combinación
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 1%

---

# Combinar extremo de directivas

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.

Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente. Cuando los datos de múltiples fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;soltero&quot; mientras que el otro indica que el cliente está &quot;casado&quot;), la política de combinación determina qué información incluir en el perfil del individuo.

Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Esta guía proporciona los pasos para trabajar con políticas de combinación mediante la API.

Para trabajar con políticas de combinación mediante la interfaz de usuario, consulte la [guía de la interfaz de usuario de directivas de combinación](../ui/merge-policies.md).

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, consulte la [guía de introducción](getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

## Componentes de directivas de combinación {#components-of-merge-policies}

Las políticas de combinación son privadas para su organización de IMS, lo que le permite crear distintas políticas para combinar esquemas de las formas específicas que necesite. Cualquier API que acceda a datos [!DNL Profile] requiere una directiva de combinación, aunque se utilizará una predeterminada si no se proporciona explícitamente. [!DNL Platform] proporciona a las organizaciones una directiva de combinación predeterminada, o bien puede crear una directiva de combinación para una clase de esquema de Experience Data Model (XDM) específica y marcarla como predeterminada para su organización.

Aunque cada organización puede tener varias directivas de combinación por clase de esquema, cada clase solo puede tener una directiva de combinación predeterminada. Cualquier directiva de combinación establecida como predeterminada se utilizará en los casos en que se proporcione el nombre de la clase de esquema y se requiera una directiva de combinación, pero no se proporcione.

>[!NOTE]
>
>Cuando se establece una nueva directiva de combinación como predeterminada, cualquier directiva de combinación existente previamente establecida como predeterminada se actualizará automáticamente para que ya no se use como predeterminada.

### Completar objeto de directiva de combinación

El objeto de directiva de combinación completa representa un conjunto de preferencias que controlan los aspectos de la combinación de fragmentos de perfil.

**Combinar objeto de directiva**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
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
| `name` | Nombre descriptivo mediante el cual se puede identificar la política de combinación en las vistas de lista. |
| `imsOrgId` | ID de organización al que pertenece esta directiva de combinación |
| `identityGraph` | [Objeto ](#identity-graph) gráfico de identidad que indica el gráfico de identidad desde el que se obtendrán las identidades relacionadas. Se combinarán los fragmentos de perfil encontrados para todas las identidades relacionadas. |
| `attributeMerge` | [Atributo ](#attribute-merge) mergeobject que indica la forma en que la política de combinación prioriza los atributos de perfil en caso de conflictos de datos. |
| `schema.name` | Parte del objeto [`schema`](#schema), el campo `name` contiene la clase de esquema XDM con la que se relaciona la política de combinación. Para obtener más información sobre esquemas y clases, lea la [documentación de XDM](../../xdm/home.md). |
| `default` | Valor booleano que indica si esta política de combinación es la predeterminada para el esquema especificado. |
| `version` | [!DNL Platform] versión mantenida de la directiva de combinación. Este valor de solo lectura se incrementa cada vez que se actualiza una directiva de combinación. |
| `updateEpoch` | Fecha de la última actualización de la directiva de combinación. |

**Ejemplo de política de combinación**

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

[Adobe Experience Platform Identity ](../../identity-service/home.md) Services gestiona los gráficos de identidad que se usan de forma global y para cada organización en  [!DNL Experience Platform]. El atributo `identityGraph` de la política de combinación define cómo determinar las identidades relacionadas para un usuario.

**objeto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Donde `{IDENTITY_GRAPH_TYPE}` es uno de los siguientes:

* **&quot;ninguno&quot;:** no realice ninguna vinculación de identidad.
* **&quot;pdg&quot;:** realice la vinculación de identidad en función del gráfico de identidad privada.

**Ejemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Combinación de atributos {#attribute-merge}

Un fragmento de perfil es la información de perfil de una sola identidad de la lista de identidades que existe para un usuario en particular. Cuando el tipo de gráfico de identidad utilizado da como resultado más de una identidad, existe la posibilidad de que haya atributos de perfil en conflicto y se debe especificar la prioridad. Con `attributeMerge`, se puede especificar qué atributos de perfil se priorizarán en caso de que surja un conflicto de combinación entre conjuntos de datos del tipo Valor clave (datos de registro).

**attributeMerge, objeto**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Donde `{ATTRIBUTE_MERGE_TYPE}` es uno de los siguientes:

* **`timestampOrdered`**: (predeterminado) Asigne prioridad al perfil que se actualizó por última vez. Con este tipo de combinación, el atributo `data` no es obligatorio. `timestampOrdered` también admite marcas de hora personalizadas que tendrán prioridad al combinar fragmentos de perfil dentro de conjuntos de datos o entre ellos. Para obtener más información, consulte la sección Apéndice sobre [uso de marcas de hora personalizadas](#custom-timestamps).
* **`dataSetPrecedence`** : Asigne prioridad a los fragmentos de perfil en función del conjunto de datos del que proceden. Esto se puede usar cuando se prefiere o confía en la información presente en un conjunto de datos sobre los datos de otro conjunto de datos. Al utilizar este tipo de combinación, se requiere el atributo `order` , ya que enumera los conjuntos de datos en orden de prioridad.
   * **`order`**: Cuando se utiliza &quot;dataSetPrecedence&quot;, se debe proporcionar una  `order` matriz con una lista de conjuntos de datos. Los conjuntos de datos que no estén incluidos en la lista no se combinarán. En otras palabras, los conjuntos de datos deben enumerarse explícitamente para combinarse en un perfil. La matriz `order` enumera los ID de los conjuntos de datos en orden de prioridad.

#### Ejemplo de objeto `attributeMerge` con tipo `dataSetPrecedence`

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

#### Ejemplo de objeto `attributeMerge` con tipo `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Esquema {#schema}

El objeto schema especifica la clase de esquema Experience Data Model (XDM) para la que se crea esta política de combinación.

**`schema`object**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Donde el valor de `name` es el nombre de la clase XDM en la que se basa el esquema asociado a la política de combinación.

**Ejemplo`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Para obtener más información sobre XDM y trabajar con esquemas en Experience Platform, comience leyendo la [información general del sistema XDM](../../xdm/home.md).

## Acceso a directivas de combinación {#access-merge-policies}

Con la API [!DNL Real-time Customer Profile], el extremo `/config/mergePolicies` permite realizar una solicitud de búsqueda para ver una política de combinación específica por su ID, o acceder a todas las directivas de combinación de su organización de IMS, filtradas según criterios específicos. También puede utilizar el extremo `/config/mergePolicies/bulk-get` para recuperar varias políticas de combinación por sus ID. Los pasos para realizar cada una de estas llamadas se describen en las siguientes secciones.

### Acceder a una directiva de combinación única por ID

Puede acceder a una única política de combinación por su ID realizando una solicitud de GET al extremo `/config/mergePolicies` e incluyendo el `mergePolicyId` en la ruta de solicitud.

**Formato de API**

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

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

### Recuperar varias directivas de combinación por sus ID

Puede recuperar varias directivas de combinación realizando una solicitud de POST al extremo `/config/mergePolicies/bulk-get` e incluyendo los ID de las políticas de combinación que desea recuperar en el cuerpo de la solicitud.

**Formato de API**

```http
POST /config/mergePolicies/bulk-get
```

**Solicitud**

El cuerpo de la solicitud incluye una matriz de &quot;id&quot; con objetos individuales que contienen el &quot;id&quot; para cada política de combinación para la que desea recuperar detalles.

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

Una respuesta correcta devuelve el Estado HTTP 207 (Multi-Status) y los detalles de las políticas de combinación cuyos ID se proporcionaron en la solicitud del POST.

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

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

### Enumerar varias directivas de combinación por criterios

Puede enumerar varias directivas de combinación dentro de su organización de IMS enviando una solicitud de GET al extremo `/config/mergePolicies` y utilizando parámetros de consulta opcionales para filtrar, ordenar y paginar la respuesta. Se pueden incluir varios parámetros, separados por el símbolo &amp;. Al realizar una llamada a este extremo sin parámetros, se recuperarán todas las directivas de combinación disponibles para su organización.

**Formato de API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parámetro | Descripción |
|---|---|
| `default` | Valor booleano que filtra los resultados según si las políticas de combinación son o no las predeterminadas para una clase de esquema. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. Valor predeterminado: 20 |
| `orderBy` | Especifica el campo por el que se ordenan los resultados como `orderBy=name` o `orderBy=+name` para ordenarlos por nombre en orden ascendente o `orderBy=-name` para ordenarlos en orden descendente. Si se omite este valor, el orden predeterminado es `name` en orden ascendente. |
| `schema.name` | Nombre del esquema para el que se recuperan las directivas de combinación disponibles. |
| `identityGraph.type` | Filtra los resultados por tipo de gráfico de identidad. Los valores posibles incluyen &quot;ninguno&quot; y &quot;pdg&quot; (gráfico privado). |
| `attributeMerge.type` | Filtra los resultados por el tipo de combinación de atributos utilizado. Los valores posibles incluyen &quot;timestampOrdered&quot; y &quot;dataSetPrecedence&quot;. |
| `start` | Desplazamiento de página : especifique el ID de inicio de los datos que se van a recuperar. Valor predeterminado: 0 |
| `version` | Especifique esto si desea utilizar una versión específica de la directiva de combinación. De forma predeterminada, se utilizará la versión más reciente. |

Para obtener más información sobre `schema.name`, `identityGraph.type` y `attributeMerge.type`, consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) que se ha proporcionado anteriormente en esta guía.


**Solicitud**

La siguiente solicitud enumera todas las directivas de combinación para un esquema determinado:

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
| `_links.next.href` | Una dirección URI para la siguiente página de resultados. Utilice este URI como parámetro de solicitud para otra llamada de API al mismo extremo para ver la página. Si no existe ninguna página siguiente, este valor será una cadena vacía. |

## Crear una directiva de combinación

Puede crear una nueva directiva de combinación para su organización realizando una solicitud de POST al extremo `/config/mergePolicies` .

**Formato de API**

```http
POST /config/mergePolicies
```

****
SolicitudLa siguiente solicitud crea una nueva directiva de combinación, que se configura con los valores de atributo proporcionados en la carga útil:

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
| `name` | Nombre reconocible mediante el cual se puede identificar la política de combinación en las vistas de lista. |
| `identityGraph.type` | Tipo de gráfico de identidad desde el cual obtener identidades relacionadas para combinar. Valores posibles: &quot;none&quot; o &quot;pdg&quot; (gráfico privado). |
| `attributeMerge` | Modo en el que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | La clase de esquema XDM asociada a la directiva de combinación. |
| `default` | Especifica si esta directiva de combinación es la predeterminada para el esquema. |

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.

**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación recién creada.

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

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que conforman una política de combinación.

## Actualizar una directiva de combinación {#update}

Puede modificar una política de combinación existente editando atributos individuales (PATCH) o sobrescribiendo toda la política de combinación con atributos nuevos (PUT). A continuación se muestran ejemplos de cada uno.

### Editar campos de política de combinación individuales

Puede editar campos individuales para una política de combinación realizando una solicitud de PATCH al extremo `/config/mergePolicies/{mergePolicyId}` :

**Formato de API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la directiva de combinación que desea eliminar. |

**Solicitud**

La siguiente solicitud actualiza una directiva de combinación especificada cambiando el valor de su propiedad `default` a `true`:

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
| `op` | Especifica la operación que se va a realizar. Se pueden encontrar ejemplos de otras operaciones de PATCH en la [JSON Patch documentation](http://jsonpatch.com) |
| `path` | Ruta del campo que se va a actualizar. Los valores aceptados son: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | El valor en el que se va a establecer el campo especificado. |

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.


**Respuesta**

Una respuesta correcta devuelve los detalles de la directiva de combinación recién actualizada.

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

Otra forma de modificar una política de combinación es utilizar una solicitud de PUT, que sobrescribe toda la política de combinación.

**Formato de API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | Identificador de la política de combinación que desea sobrescribir. |

**Solicitud**

La siguiente solicitud sobrescribe la directiva de combinación especificada, reemplazando sus valores de atributo por los suministrados en la carga útil. Dado que esta solicitud sustituye completamente una política de combinación existente, es necesario proporcionar todos los campos necesarios al definir originalmente la política de combinación. Sin embargo, esta vez se proporcionan valores actualizados para los campos que se desea cambiar.

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
| `name` | Nombre reconocible mediante el cual se puede identificar la política de combinación en las vistas de lista. |
| `identityGraph` | Gráfico de identidad desde el cual obtener identidades relacionadas para fusionar. |
| `attributeMerge` | Modo en el que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | La clase de esquema XDM asociada a la directiva de combinación. |
| `default` | Especifica si esta directiva de combinación es la predeterminada para el esquema. |

Consulte la sección [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.


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

Una directiva de combinación se puede eliminar realizando una solicitud de DELETE al extremo `/config/mergePolicies` e incluyendo el ID de la directiva de combinación que desea eliminar en la ruta de solicitud.

**Formato de API**

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

Una solicitud de eliminación correcta devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para ver la directiva de combinación por su ID. Si se eliminó la directiva de combinación, recibirá un error de estado HTTP 404 (no encontrado).

## Pasos siguientes

Ahora que sabe cómo crear y configurar políticas de combinación para su organización, puede utilizarlas para ajustar la vista de perfiles de cliente dentro de Platform y para crear segmentos de audiencia a partir de sus datos [!DNL Real-time Customer Profile] . Consulte la [documentación del servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md) para empezar a definir y trabajar con segmentos.

## Apéndice

Esta sección proporciona información complementaria relacionada con el trabajo con políticas de combinación.

### Uso de marcas de hora personalizadas {#custom-timestamps}

A medida que los registros se incorporan en el Experience Platform, se obtiene una marca de tiempo del sistema en el momento de la ingesta y se añade al registro. Cuando se selecciona `timestampOrdered` como tipo `attributeMerge` para una directiva de combinación, los perfiles se combinan en función de la marca de tiempo del sistema. En otras palabras, la combinación se realiza en función de la marca de tiempo para cuando el registro se incorporó a Platform.

Ocasionalmente puede haber casos de uso, como rellenar datos o garantizar el orden correcto de los eventos si los registros se introducen de forma desordenada, en los que es necesario proporcionar una marca de tiempo personalizada y hacer que la directiva de combinación respete la marca de tiempo personalizada en lugar de la marca de tiempo del sistema.

Para utilizar una marca de tiempo personalizada, se debe agregar [[!DNL External Source System Audit Details Mixin]](#mixin-details) al esquema de perfil. Una vez añadida, la marca de tiempo personalizada se puede rellenar con el campo `xdm:lastUpdatedDate` . Cuando se ingesta un registro con el campo `xdm:lastUpdatedDate` rellenado, el Experience Platform utilizará ese campo para combinar registros o fragmentos de perfil dentro y entre conjuntos de datos. Si `xdm:lastUpdatedDate` no está presente o no se rellena, Platform seguirá usando la marca de tiempo del sistema.

>[!NOTE]
>
>Debe asegurarse de que la marca de tiempo `xdm:lastUpdatedDate` se rellene al enviar un PATCH en el mismo registro.

Para obtener instrucciones paso a paso sobre cómo trabajar con esquemas mediante la API del Registro de esquemas, incluido cómo añadir mezclas a esquemas, visite el [tutorial para crear un esquema con la API](../../xdm/tutorials/create-schema-api.md).

Para trabajar con marcas de hora personalizadas mediante la interfaz de usuario, consulte la sección [Uso de marcas de hora personalizadas](../ui/merge-policies.md#custom-timestamps) en la [guía del usuario de políticas de combinación](../ui/merge-policies.md).

#### [!DNL External Source System Audit Details Mixin] detalles  {#mixin-details}

El siguiente ejemplo muestra campos rellenados correctamente en el [!DNL External Source System Audit Details Mixin]. La mezcla completa JSON también se puede ver en el repositorio [public Experience Data Model (XDM)](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) de GitHub.

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
