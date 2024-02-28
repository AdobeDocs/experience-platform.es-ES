---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Extremo de API de políticas de combinación
type: Documentation
description: Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2465'
ht-degree: 2%

---

# Extremo de políticas de combinación

Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.

Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Platform, se combinan para crear un único perfil para ese cliente. Cuando los datos de varias fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;único&quot;, mientras que el otro indica al cliente como &quot;casado&quot;), la política de combinación determina qué información se incluye en el perfil de la persona.

Mediante las API de RESTful o la interfaz de usuario de, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Esta guía proporciona los pasos para trabajar con las políticas de combinación mediante la API.

Para trabajar con políticas de combinación mediante la interfaz de usuario, consulte la [guía de IU de políticas de combinación](../merge-policies/ui-guide.md). Para obtener más información sobre las políticas de combinación en general y su función dentro de Experience Platform, comience por leer la [resumen de políticas de combinación](../merge-policies/overview.md).

## Introducción

El extremo de API utilizado en esta guía forma parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte la [guía de introducción](getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier [!DNL Experience Platform] API.

## Componentes de las políticas de combinación {#components-of-merge-policies}

Las políticas de combinación son privadas para su organización, lo que le permite crear diferentes políticas para combinar esquemas de las formas específicas que necesite. Cualquier acceso a API [!DNL Profile] Los datos de requieren una política de combinación, aunque se utilizará una predeterminada si no se proporciona una de forma explícita. [!DNL Platform] proporciona a las organizaciones una política de combinación predeterminada, o bien puede crear una política de combinación para una clase de esquema del Modelo de datos de experiencia (XDM) específica y marcarla como predeterminada para su organización.

Aunque cada organización puede tener potencialmente varias políticas de combinación por clase de esquema, cada clase solo puede tener una política de combinación predeterminada. Cualquier política de combinación establecida como predeterminada se utilizará en los casos en que se proporcione el nombre de la clase de esquema y se requiera una política de combinación, pero no se proporcione.

>[!NOTE]
>
>Cuando se establece una nueva política de combinación como predeterminada, cualquier política de combinación existente que se haya establecido anteriormente como predeterminada se actualizará automáticamente para que ya no se utilice como predeterminada.

Para garantizar que todos los consumidores de perfiles trabajen con la misma vista en los bordes, las políticas de combinación se pueden marcar como activas en el borde. Para que una audiencia se active en Edge (marcada como audiencia Edge), debe estar vinculada a una política de combinación marcada como activa en Edge. Si una audiencia es **no** ligada a una política de combinación marcada como activa en edge, la audiencia no se marca como activa en edge y se marca como audiencia de flujo continuo.

Además, cada organización solo puede tener **uno** política de combinación activa en edge. Si una política de combinación está activa en Edge, puede utilizarse para otros sistemas en Edge, como Perfil de Edge, Segmentación de Edge y Destinos en Edge.

### Completar objeto de política de combinación

El objeto de política de combinación completo representa un conjunto de preferencias que controlan aspectos de la combinación de fragmentos de perfil.

**Objeto de política de combinación**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Propiedad | Descripción |
|---|---|
| `id` | El identificador único generado por el sistema asignado en el momento de la creación |
| `name` | Nombre descriptivo con el que se puede identificar la política de combinación en las vistas de lista. |
| `imsOrgId` | ID de organización al que pertenece esta política de combinación |
| `schema.name` | Parte de la [`schema`](#schema) objeto, el `name` Este campo contiene la clase de esquema XDM con la que se relaciona la política de combinación. Para obtener más información sobre esquemas y clases, lea la [Documentación de XDM](../../xdm/home.md). |
| `version` | [!DNL Platform] versión mantenida de la política de combinación. Este valor de solo lectura se incrementa cada vez que se actualiza una política de combinación. |
| `identityGraph` | [Gráfico de identidad](#identity-graph) objeto que indica el gráfico de identidad del que se obtendrán las identidades relacionadas. Se combinarán los fragmentos de perfil encontrados para todas las identidades relacionadas. |
| `attributeMerge` | [Combinación de atributos](#attribute-merge) objeto que indica la forma en que la política de combinación priorizará los atributos de perfil en caso de conflictos de datos. |
| `isActiveOnEdge` | Valor booleano que indica si esta política de combinación se puede utilizar en Edge. De forma predeterminada, este valor es `false`. |
| `default` | Valor booleano que indica si esta política de combinación es la predeterminada para el esquema especificado. |
| `updateEpoch` | Fecha de la última actualización de la política de combinación. |

**Ejemplo de política de combinación**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Gráfico de identidad {#identity-graph}

[Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md) administra los gráficos de identidad utilizados globalmente y para cada organización en [!DNL Experience Platform]. El `identityGraph` de la política de combinación define cómo determinar las identidades relacionadas de un usuario.

**objeto identityGraph**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Donde `{IDENTITY_GRAPH_TYPE}` es uno de los siguientes:

* **&quot;ninguno&quot;:** No realice ninguna vinculación de identidad.
* **&quot;pdg&quot;:** Realice la vinculación de identidad en función de su gráfico de identidad privada.

**Ejemplo`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Combinación de atributos {#attribute-merge}

Un fragmento de perfil es la información de perfil de una sola identidad de la lista de identidades que existen para un usuario en particular. Cuando el tipo de gráfico de identidad utilizado genera más de una identidad, existe la posibilidad de que haya conflictos entre los atributos de perfil y se debe especificar la prioridad. Uso de `attributeMerge`Además, puede especificar qué atributos de perfil priorizar en caso de un conflicto de combinación entre conjuntos de datos de tipo Valor clave (datos de registro).

**objeto attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Donde `{ATTRIBUTE_MERGE_TYPE}` es uno de los siguientes:

* **`timestampOrdered`**: (predeterminado) Dé prioridad al perfil que se actualizó en último lugar. Con este tipo de combinación, la variable `data` no es obligatorio.
* **`dataSetPrecedence`**: Dé prioridad a los fragmentos de perfil en función del conjunto de datos del que procedan. Esto se puede utilizar cuando se prefiere la información presente en un conjunto de datos o cuando se confía en ella sobre los datos de otro conjunto de datos. Al utilizar este tipo de combinación, la variable `order` es obligatorio, ya que enumera los conjuntos de datos en el orden de prioridad.
   * **`order`**: Cuando se utiliza &quot;dataSetPrecedence&quot;, una variable `order` La matriz debe proporcionarse con una lista de conjuntos de datos. No se combinarán los conjuntos de datos que no estén incluidos en la lista. En otras palabras, los conjuntos de datos deben enumerarse explícitamente para combinarse en un perfil. El `order` matriz enumera los ID de los conjuntos de datos en orden de prioridad.

#### Ejemplo `attributeMerge` objeto mediante `dataSetPrecedence` type

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Ejemplo `attributeMerge` objeto mediante `timestampOrdered` type

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Esquema {#schema}

El objeto de esquema especifica la clase de esquema del Modelo de datos de experiencia (XDM) para la que se crea esta política de combinación.

**`schema`objeto**

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

Para obtener más información sobre XDM y el trabajo con esquemas en Experience Platform, comience por leer el [Información general del sistema XDM](../../xdm/home.md).

## Acceso a políticas de combinación {#access-merge-policies}

Uso del [!DNL Real-Time Customer Profile] API, la `/config/mergePolicies` Un punto de conexión le permite realizar una solicitud de búsqueda para ver una política de combinación específica por su ID o acceder a todas las políticas de combinación de su organización, filtradas por criterios específicos. También puede utilizar la variable `/config/mergePolicies/bulk-get` punto final para recuperar varias políticas de combinación por sus ID. Los pasos para realizar cada una de estas llamadas se describen en las secciones siguientes.

### Acceso a una única política de combinación por ID

Puede acceder a una única política de combinación por su ID realizando una solicitud de GET al `/config/mergePolicies` punto final e incluir el `mergePolicyId` en la ruta de solicitud.

**Formato de API**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | El identificador de la política de combinación que desea eliminar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que componen una política de combinación.

### Recuperar varias políticas de combinación por sus ID

Puede recuperar varias políticas de combinación realizando una solicitud del POST a la variable `/config/mergePolicies/bulk-get` e incluir los ID de las políticas de combinación que desea recuperar en el cuerpo de la solicitud.

**Formato de API**

```http
POST /config/mergePolicies/bulk-get
```

**Solicitud**

El cuerpo de la solicitud incluye una matriz &quot;ids&quot; con objetos individuales que contienen el &quot;id&quot; para cada política de combinación cuyos detalles desea recuperar.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una respuesta correcta devuelve el estado HTTP 207 (varios estados) y los detalles de las políticas de combinación cuyos ID se proporcionaron en la solicitud del POST.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que componen una política de combinación.

### Enumerar varias políticas de combinación por criterios

Puede enumerar varias políticas de combinación dentro de su organización emitiendo una solicitud de GET a la `/config/mergePolicies` y utilizando parámetros de consulta opcionales para filtrar, ordenar y paginar la respuesta. Se pueden incluir varios parámetros, separados por el símbolo &quot;et&quot; (&amp;). Realizar una llamada a este extremo sin parámetros recuperará todas las políticas de combinación disponibles para su organización.

**Formato de API**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parámetro | Descripción |
|---|---|
| `default` | Un valor booleano que filtra los resultados dependiendo de si las políticas de combinación son o no las predeterminadas para una clase de esquema. |
| `limit` | Especifica el límite de tamaño de página para controlar el número de resultados que se incluyen en una página. Valor predeterminado: 20 |
| `orderBy` | Especifica el campo por el que ordenar los resultados como en `orderBy=name` o `orderBy=+name` para ordenar por nombre en orden ascendente, o `orderBy=-name`, para ordenar en orden descendente. Si se omite este valor, se ordenará de forma predeterminada `name` en orden ascendente. |
| `isActiveOnEdge` | Valores booleanos que filtran los resultados según si las políticas de combinación están activas o no en Edge. |
| `schema.name` | Nombre del esquema para el que se van a recuperar las políticas de combinación disponibles. |
| `identityGraph.type` | Filtra los resultados por tipo de gráfico de identidad. Los valores posibles incluyen &quot;none&quot; y &quot;pdg&quot; (gráfico privado). |
| `attributeMerge.type` | Filtra los resultados por el tipo de combinación de atributos utilizado. Los valores posibles incluyen &quot;timestampOrdered&quot; y &quot;dataSetPrecedence&quot;. |
| `start` | Desplazamiento de página: especifique el ID de inicio de los datos que se van a recuperar. Valor predeterminado: 0 |
| `version` | Especifique esto si desea utilizar una versión específica de la política de combinación. De forma predeterminada, se utiliza la versión más reciente. |

Para obtener más información sobre `schema.name`, `identityGraph.type`, y `attributeMerge.type`, consulte la [componentes de políticas de combinación](#components-of-merge-policies) sección proporcionada anteriormente en esta guía.


**Solicitud**

La siguiente solicitud enumera todas las políticas de combinación para un esquema determinado:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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

## Crear una política de combinación

Puede crear una nueva política de combinación para su organización realizando una solicitud de POST a `/config/mergePolicies` punto final.

**Formato de API**

```http
POST /config/mergePolicies
```

**Solicitud**
La siguiente solicitud crea una nueva política de combinación, que se configura con los valores de atributo proporcionados en la carga útil:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Propiedad | Descripción |
|---|---|
| `name` | Un nombre descriptivo mediante el cual se puede identificar la política de combinación en las vistas de lista. |
| `identityGraph.type` | El tipo de gráfico de identidad desde el que se obtienen las identidades relacionadas que se van a combinar. Valores posibles: &quot;none&quot; o &quot;pdg&quot; (gráfico privado). |
| `attributeMerge` | La forma en que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | La clase de esquema XDM asociada a la política de combinación. |
| `isActiveOnEdge` | Especifica si esta política de combinación está activa en Edge. |
| `default` | Especifica si esta política de combinación es la predeterminada para el esquema. |

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.

**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación recién creada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) al principio de este documento para obtener detalles sobre cada uno de los elementos individuales que componen una política de combinación.

## Actualizar una política de combinación {#update}

Puede modificar una política de combinación existente editando atributos individuales (PATCH) o sobrescribiendo toda la política de combinación con atributos nuevos (PUT). A continuación se muestran ejemplos de cada una de ellas.

### Editar campos de políticas de combinación individuales

Puede editar campos individuales para una política de combinación realizando una solicitud del PATCH a la variable `/config/mergePolicies/{mergePolicyId}` extremo:

**Formato de API**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | El identificador de la política de combinación que desea eliminar. |

**Solicitud**

La siguiente solicitud actualiza una política de combinación especificada cambiando el valor de su `default` propiedad a `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Especifica la operación que se va a realizar. Encontrará ejemplos de otras operaciones de PATCH en la [Documentación de parches de JSON](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | Ruta del campo que se va a actualizar. Los valores aceptados son: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | Valor en el que se establece el campo especificado. |

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.


**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación recién actualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### Sobrescribir una política de combinación

Otra forma de modificar una política de combinación es utilizar una solicitud de PUT, que sobrescribe toda la política de combinación.

**Formato de API**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | El identificador de la política de combinación que desea sobrescribir. |

**Solicitud**

La siguiente solicitud sobrescribe la política de combinación especificada y reemplaza sus valores de atributo por los proporcionados en la carga útil. Dado que esta solicitud reemplaza completamente una política de combinación existente, es necesario que proporcione todos los campos que fueron necesarios al definir originalmente la política de combinación. Sin embargo, esta vez proporciona valores actualizados para los campos que desea cambiar.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Propiedad | Descripción |
|---|---|
| `name` | Un nombre descriptivo mediante el cual se puede identificar la política de combinación en las vistas de lista. |
| `identityGraph` | Gráfico de identidad desde el que se obtienen identidades relacionadas para combinarlas. |
| `attributeMerge` | La forma en que se priorizan los valores de atributos de perfil en caso de conflictos de datos. |
| `schema` | La clase de esquema XDM asociada a la política de combinación. |
| `isActiveOnEdge` | Especifica si esta política de combinación está activa en Edge. |
| `default` | Especifica si esta política de combinación es la predeterminada para el esquema. |

Consulte la [componentes de políticas de combinación](#components-of-merge-policies) para obtener más información.

**Respuesta**

Una respuesta correcta devuelve los detalles de la política de combinación actualizada.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Eliminar una política de combinación

Se puede eliminar una política de combinación realizando una solicitud del DELETE a la `/config/mergePolicies` punto final e incluir el ID de la política de combinación que desea eliminar en la ruta de solicitud.

>[!NOTE]
>
>Si la política de combinación tiene `isActiveOnEdge` establecida como true, la política de combinación **no puede** se eliminarán. Utilice cualquiera de las [PATCH](#edit-individual-merge-policy-fields) o [PUT](#overwrite-a-merge-policy) puntos finales para actualizar la política de combinación antes de eliminarla.

**Formato de API**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parámetro | Descripción |
|---|---|
| `{mergePolicyId}` | El identificador de la política de combinación que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina una política de combinación.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una solicitud de eliminación correcta devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta vacío. Para confirmar que la eliminación se ha realizado correctamente, puede realizar una solicitud de GET para ver la política de combinación por su ID. Si se ha eliminado la política de combinación, recibirá un error de estado HTTP 404 (no encontrado).

## Pasos siguientes

Ahora que sabe cómo crear y configurar políticas de combinación para su organización, puede utilizarlas para ajustar la vista de perfiles de clientes dentro de Platform y para crear audiencias a partir de sus [!DNL Real-Time Customer Profile] datos.

Consulte la [Documentación del Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md) para empezar a definir y trabajar con audiencias.
