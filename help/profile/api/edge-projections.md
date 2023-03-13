---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Extremos de API de proyección de Edge
type: Documentation
description: Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y personalizadas para sus clientes en varios canales en tiempo real, haciendo que los datos adecuados estén disponibles y se actualicen continuamente a medida que se produzcan cambios. Esto se lleva a cabo mediante el uso de perímetros, un servidor colocado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# Configuraciones de proyección de Edge y extremos de destinos

Para impulsar experiencias coordinadas, coherentes y personalizadas para sus clientes en varios canales en tiempo real, los datos adecuados deben estar disponibles y actualizarse continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como perímetros. Un perímetro es un servidor ubicado geográficamente que almacena datos y hace que sea fácilmente accesible para las aplicaciones. Por ejemplo, las aplicaciones de Adobe como Adobe Target y Adobe Campaign utilizan Edge de para ofrecer experiencias del cliente personalizadas en tiempo real. Los datos se enrutan a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde. Esta guía proporciona instrucciones detalladas para utilizar el [!DNL Real-Time Customer Profile] API para trabajar con proyecciones de Edge, incluidos destinos y configuraciones.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte la [guía de introducción](getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier [!DNL Experience Platform] API.

>[!NOTE]
>
>Las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un `Content-Type` encabezado. Más de uno `Content-Type` en este documento. Preste especial atención a los encabezados de las llamadas de ejemplo para asegurarse de que está utilizando el `Content-Type` para cada solicitud.

## Destinos de proyección

Una proyección se puede enrutar a uno o más bordes especificando las ubicaciones a las que se enviarán los datos. Cada destino de proyección que se crea tiene un ID único que se utiliza para crear la configuración de proyección.

### Enumerar todos los destinos

Puede enumerar los destinos de Edge que ya se han creado para su organización realizando una solicitud de GET a `/config/destinations` punto final.

**Formato de API**

```http
GET /config/destinations
```

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye una `projectionDestinations` matriz con los detalles de cada destino mostrado como un objeto individual dentro de la matriz. Si no se han configurado proyecciones, la variable `projectionDestinations` la matriz devuelve empty.

>[!NOTE]
>
>Esta respuesta se ha abreviado para el espacio y muestra solo dos destinos.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Propiedad | Descripción |
|---|---|
| `_links.self.href` | En el nivel superior, coincide con la ruta utilizada para realizar la solicitud de GET. Dentro de cada objeto de destino individual, esta ruta se puede utilizar en una solicitud de GET para buscar directamente los detalles de un destino específico. |
| `id` | Dentro de cada objeto de destino, la variable `"id"` muestra el ID único de solo lectura generado por el sistema para el destino. Este ID se utiliza al hacer referencia a un destino específico y al crear configuraciones de proyección. |

Para obtener más información sobre los atributos de un destino individual, consulte la sección sobre [creación de un destino](#create-a-destination) que sigue.

### Crear un destino {#create-a-destination}

Si el destino que necesita no existe todavía, puede crear un nuevo destino de proyección realizando una solicitud de POST al `/config/destinations` punto final.

**Formato de API**

```http
POST /config/destinations
```

**Solicitud**

La siguiente solicitud crea un nuevo destino de Edge.

>[!NOTE]
>
>La solicitud del POST para crear un destino requiere un específico `Content-Type` encabezado, como se muestra a continuación. Uso de un incorrecto `Content-Type` da como resultado un error de estado HTTP 415 (Tipo de medio no compatible).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| Propiedad | Descripción |
|---|---|
| `type` **(Obligatorio)** | Tipo de destino que se va a crear. El único valor aceptado, &quot;EDGE&quot;, crea un destino de Edge. |
| `dataCenters` **(Obligatorio)** | Matriz de cadenas que enumera los bordes hacia los que se deben enrutar las proyecciones. Puede contener uno o más de los siguientes valores: &quot;OR1&quot; (oeste de Estados Unidos), &quot;VA5&quot; (este de Estados Unidos), &quot;NLD1&quot; (EMEA). |
| `ttl` **(Obligatorio)** | Especifica la caducidad de la proyección. Intervalo de valores aceptado: de 600 a 604800. Valor predeterminado: 3600. |
| `replicationPolicy` **(Obligatorio)** | Define el comportamiento de la duplicación de datos desde el concentrador hasta los extremos.  Valores admitidos: PROACTIVO, REACTIVO. Valor predeterminado: REACTIVE. |

**Respuesta**

Una respuesta correcta devuelve los detalles del destino perimetral recién creado, incluido el ID único de solo lectura generado por el sistema (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Propiedad | Descripción |
|---|---|
| `self.href` | Esta ruta se utiliza para buscar (GET) el destino directamente y también se puede utilizar para actualizar (PUT) o eliminar (DELETE) el destino. |
| `id` | El ID único de solo lectura generado por el sistema para el destino. Este ID se utiliza para hacer referencia al destino directamente y al crear configuraciones de proyección. |
| `version` | Este valor de solo lectura muestra la versión actual del destino. Cuando se actualiza un destino, el número de versión se incrementa automáticamente. |

### Ver un destino

Si conoce el ID único de un destino de proyección, puede realizar una solicitud de consulta para ver sus detalles. Esto se hace realizando una solicitud de GET a la `/config/destinations` e incluir el ID del destino en la ruta de solicitud.

**Formato de API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | El ID único del destino de proyección que desea ver. |

**Solicitud**

La siguiente solicitud realiza una búsqueda (GET) para ver el destino del ID proporcionado en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response muestra los detalles del destino de la proyección. El `id` debe coincidir con el ID del destino de proyección proporcionado en la solicitud.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Actualización de un destino

Se puede actualizar un destino existente realizando una solicitud de PUT a `/config/destinations` punto final e incluye el ID del destino que se va a actualizar en la ruta de solicitud. Esta operación esencialmente reescribe el destino, por lo tanto, se deben proporcionar los mismos atributos en el cuerpo de la solicitud que se proporcionan al crear un nuevo destino.

>[!CAUTION]
>
>La respuesta de la API a la solicitud de actualización es inmediata, pero los cambios en las proyecciones se aplican de forma asíncrona. En otras palabras, existe una diferencia horaria entre el momento en que se realiza la actualización de la definición del destino y el momento en que se aplica.

**Formato de API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | El ID único del destino de la proyección que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza el destino existente para incluir una segunda ubicación (`dataCenters`).

>[!IMPORTANT]
>
>La solicitud del PUT requiere un específico `Content-Type` encabezado, como se muestra a continuación. Uso de un incorrecto `Content-Type` da como resultado un error de estado HTTP 415 (Tipo de medio no compatible).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Propiedad | Descripción |
|---|---|
| `currentVersion` | La versión actual del destino existente. El valor del `version` al realizar una solicitud de consulta para el destino. |

**Respuesta**

La respuesta incluye los detalles actualizados del destino, incluido su ID y el nuevo `version` del destino.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Eliminar un destino

Si su organización ya no requiere un destino de proyección, se puede eliminar realizando una solicitud de DELETE a `/config/destinations` e incluir el ID del destino que desea eliminar en la ruta de solicitud.

>[!CAUTION]
>
>La respuesta de la API a la solicitud de eliminación es inmediata, pero los cambios reales en los datos de los extremos se producen de forma asíncrona. En otras palabras, los datos de perfil se eliminan de todos los extremos (la variable `dataCenters` especificado en la proyección (destino), pero el proceso tardará en completarse.

**Formato de API**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | El ID único del destino de la proyección que desea eliminar. |


**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La solicitud de eliminación devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Puede confirmar que la eliminación se ha realizado correctamente realizando una solicitud de búsqueda para el destino por su ID. La búsqueda debe devolver el estado HTTP 404 (no encontrado).

## Configuraciones de proyección

Las configuraciones de proyección proporcionan información sobre qué datos deben estar disponibles en cada perímetro. En lugar de proyectar una [!DNL Experience Data Model] (XDM) al perímetro, una proyección solo proporciona datos específicos, o campos, del esquema. Su organización puede definir varias configuraciones de proyección para cada esquema XDM.

### Enumerar todas las configuraciones de proyección

Puede enumerar todas las configuraciones de proyección que se han creado para su organización realizando una solicitud de GET a `/config/projections` punto final. También se pueden añadir parámetros opcionales a la ruta de solicitud para acceder a las configuraciones de proyección de un esquema determinado o buscar una proyección individual por su nombre.

**Formato de API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parámetro | Descripción |
|---|---|
| `{SCHEMA_NAME}` | El nombre de la clase de esquema asociada con la configuración de proyección a la que desea acceder. |
| `{PROJECTION_NAME}` | Nombre de la configuración de proyección a la que desea acceder. |

>[!NOTE]
>
>`schemaName` es necesario al utilizar el `name` , ya que un nombre de configuración de proyección solo es único en el contexto de una clase de esquema.

**Solicitud**

La siguiente solicitud enumera todas las configuraciones de proyección asociadas con la variable [!DNL Experience Data Model] clase de esquema, [!DNL XDM Individual Profile]. Para obtener más información sobre XDM y su función dentro de [!DNL Platform], empiece por leer el [Información general del sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de configuraciones de proyección dentro de la raíz `_embedded` atributo, contenido en `projectionConfigs` matriz. Si no se han realizado configuraciones de proyección para su organización, la variable `projectionConfigs` la matriz estará vacía.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Creación de una configuración de proyección

Puede crear (POST) una nueva configuración de proyección que dictará qué campos XDM están disponibles en los bordes.

**Formato de API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parámetro | Descripción |
|---|---|
| `{SCHEMA_NAME}` | El nombre de la clase de esquema asociada con la configuración de proyección a la que desea acceder. |

**Solicitud**

>[!NOTE]
>
>La solicitud del POST para crear una configuración de requiere un específico `Content-Type` encabezado, como se muestra a continuación. Uso de un incorrecto `Content-Type` da como resultado un error de estado HTTP 415 (Tipo de medio no compatible).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Propiedad | Descripción |
|---|---|
| `selector` | Cadena que contiene una lista de propiedades dentro del esquema que se van a replicar en los extremos. Las prácticas recomendadas para trabajar con selectores están disponibles en la [Selectores](#selectors) de este documento. |
| `name` | Un nombre descriptivo para la nueva configuración de proyección. |
| `destinationId` | El identificador del destino de Edge al que se proyectarán los datos. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la configuración de proyección recién creada.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Selectores {#selectors}

Un selector es una lista de nombres de campo XDM separados por comas. En una configuración de proyección, el selector designa las propiedades que se deben incluir en las proyecciones. El formato del `selector` El valor del parámetro se basa de forma flexible en la sintaxis XPath. A continuación se resume la sintaxis admitida, con ejemplos adicionales que se proporcionan como referencia.

### Sintaxis admitida

* Utilice comas para seleccionar varios campos. No utilice espacios.
* Utilice la notación de puntos para seleccionar campos anidados.
   * Por ejemplo, para seleccionar un campo denominado `field` que se anida dentro de un campo denominado `foo`, utilice el selector `foo.field`.
* Al incluir un campo que contiene subcampos, todos los subcampos también se proyectan de forma predeterminada. Sin embargo, puede filtrar los subcampos devueltos mediante paréntesis `"( )"`.
   * Por ejemplo, `addresses(type,city.country)` devuelve únicamente el tipo de dirección y el país en el que se encuentra la ciudad de la dirección para cada uno `addresses` elemento de matriz.
   * El ejemplo anterior es equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>La notación con puntos y la notación entre paréntesis son compatibles con los subcampos de referencia. Sin embargo, se recomienda utilizar la notación de puntos porque es más concisa y proporciona una mejor ilustración de la jerarquía de campos.

* Cada campo del selector se especifica en relación con la raíz de la respuesta.
   * Si los datos son una colección de recursos, la proyección incluirá una matriz de recursos.
   * Si los datos son un solo recurso, la proyección incluirá campos relativos a ese recurso.
   * Si el campo seleccionado es (o forma parte) de una matriz, la proyección incluirá la parte seleccionada de todos los elementos de la matriz.

### Ejemplos del parámetro selector

Los siguientes ejemplos muestran un ejemplo `selector` parámetros, seguidos de los valores estructurados que representan.

**person.lastName**

Devuelve el `lastName` subcampo de la variable `person` en el recurso solicitado.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**direcciones**

Devuelve todos los elementos del `addresses` matriz, incluidos todos los campos de cada elemento, pero ningún otro campo.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,addresses**

Devuelve el `person.lastName` y todos los elementos del campo `addresses` matriz.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

Devuelve únicamente el campo de ciudad de todos los elementos de la matriz de direcciones.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>Siempre que se devuelve un campo anidado, la proyección incluye los objetos principales envolventes. Los campos principales no incluyen ningún otro campo secundario a menos que también se seleccionen explícitamente.

**direcciones(tipo,ciudad)**

Devuelve solo los valores de `type` y `city` campos para cada elemento de la `addresses` matriz. Todos los demás subcampos incluidos en cada `addresses` Los elementos de se filtran.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Pasos siguientes

Esta guía muestra los pasos necesarios para configurar las proyecciones y los destinos, incluido cómo dar formato correctamente a la variable `selector` parámetro. Ahora puede crear nuevos destinos de proyección y configuraciones específicas para las necesidades de su organización.
