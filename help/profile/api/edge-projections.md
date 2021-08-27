---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Puntos finales de la API de proyección de Edge
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y personalizadas a sus clientes en varios canales en tiempo real, haciendo que los datos adecuados estén disponibles y se actualicen continuamente a medida que se produzcan cambios. Esto se hace mediante el uso de bordes, un servidor ubicado geográficamente que almacena datos y lo hace fácilmente accesible para las aplicaciones.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# Configuraciones de proyección de Edge y extremos de destinos

Para ofrecer experiencias coordinadas, coherentes y personalizadas a sus clientes en varios canales en tiempo real, es necesario disponer fácilmente de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante lo que se conoce como bordes. Un Edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Por ejemplo, las aplicaciones de Adobe como Adobe Target y Adobe Campaign utilizan perímetros para ofrecer experiencias personalizadas al cliente en tiempo real. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que se pondrá a disposición en el borde. Esta guía proporciona instrucciones detalladas para utilizar la API [!DNL Real-time Customer Profile] para trabajar con proyecciones avanzadas, incluidos destinos y configuraciones.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte la [guía de introducción](getting-started.md) para ver los vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas correctamente a cualquier API [!DNL Experience Platform].

>[!NOTE]
>
>Las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado `Content-Type`. En este documento se utiliza más de un `Content-Type`. Preste especial atención a los encabezados de las llamadas de ejemplo para asegurarse de que utiliza el `Content-Type` correcto para cada solicitud.

## Destinos de proyección

Una proyección se puede dirigir a uno o varios bordes especificando las ubicaciones a las que se enviarán los datos. Cada destino de proyección que se crea tiene un ID único que se utiliza para crear la configuración de la proyección.

### Enumerar todos los destinos

Puede enumerar los destinos Edge que ya se han creado para su organización realizando una solicitud de GET al extremo `/config/destinations` .

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye una matriz `projectionDestinations` con los detalles de cada destino mostrados como un objeto individual dentro de la matriz. Si no se han configurado proyecciones, la matriz `projectionDestinations` devuelve empty.

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
| `id` | Dentro de cada objeto de destino, el `"id"` muestra el ID único de solo lectura generado por el sistema para el destino. Este ID se utiliza al hacer referencia a un destino específico y al crear configuraciones de proyección. |

Para obtener más información sobre los atributos de un destino individual, consulte la sección sobre [creación de un destino](#create-a-destination) que se muestra a continuación.

### Crear un destino {#create-a-destination}

Si el destino que necesita no existe, puede crear un nuevo destino de proyección realizando una solicitud de POST al extremo `/config/destinations` .

**Formato de API**

```http
POST /config/destinations
```

**Solicitud**

La siguiente solicitud crea un nuevo destino perimetral.

>[!NOTE]
>
>La solicitud del POST para crear un destino requiere un encabezado `Content-Type` específico, como se muestra a continuación. El uso de un encabezado `Content-Type` incorrecto genera un error de estado HTTP 415 (tipo de medio no compatible).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `type` **(Obligatorio)** | Tipo de destino que se va a crear. El único valor aceptado, &quot;EDGE&quot;, crea un destino de borde. |
| `dataCenters` **(Obligatorio)** | Matriz de cadenas que enumera los bordes hacia los que se deben enrutar las proyecciones. Puede contener uno o más de los siguientes valores: &quot;OR1&quot; - Estados Unidos Occidental, &quot;VA5&quot; - Estados Unidos Oriental, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obligatorio)** | Especifica la caducidad de la proyección. Intervalo de valores aceptado: 600 a 604800. Valor predeterminado: 3600. |
| `replicationPolicy` **(Obligatorio)** | Define el comportamiento de la replicación de datos desde el concentrador hasta los bordes.  Valores compatibles: PROACTIVO, REACTIVO. Valor predeterminado: REACTIVO. |

**Respuesta**

Una respuesta correcta devuelve los detalles del destino perimetral recién creado, incluido el ID único generado por el sistema de solo lectura (`id`).

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
| `id` | ID único de solo lectura generado por el sistema para el destino. Este ID se utiliza para hacer referencia al destino directamente y al crear configuraciones de proyección. |
| `version` | Este valor de solo lectura muestra la versión actual del destino. Cuando se actualiza un destino, el número de versión aumenta automáticamente. |

### Ver un destino

Si conoce el ID exclusivo de un destino de proyección, puede realizar una solicitud de consulta para ver sus detalles. Esto se realiza realizando una solicitud de GET al extremo `/config/destinations` e incluyendo el ID del destino en la ruta de solicitud.

**Formato de API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | ID exclusivo del destino de la proyección que desea ver. |

**Solicitud**

La siguiente solicitud realiza una búsqueda (GET) para ver el destino del ID proporcionado en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El objeto response muestra los detalles del destino de la proyección. El atributo `id` debe coincidir con el ID del destino de la proyección que se proporcionó en la solicitud.

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

### Actualizar un destino

Un destino existente se puede actualizar realizando una solicitud de PUT al extremo `/config/destinations` e incluyendo el ID del destino a actualizar en la ruta de solicitud. Esta operación está reescribiendo el destino, por lo que se deben proporcionar los mismos atributos en el cuerpo de la solicitud que se proporcionan al crear un nuevo destino.

>[!CAUTION]
>
>La respuesta de la API a la solicitud de actualización es inmediata, pero los cambios en las proyecciones se aplican asincrónicamente. En otras palabras, hay una diferencia de tiempo entre el momento en que se realiza la actualización a la definición del destino y el momento en que se aplica.

**Formato de API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | ID exclusivo del destino de la proyección que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza el destino existente para incluir una segunda ubicación (`dataCenters`).

>[!IMPORTANT]
>
>La solicitud del PUT requiere un encabezado `Content-Type` específico, como se muestra a continuación. El uso de un encabezado `Content-Type` incorrecto genera un error de estado HTTP 415 (tipo de medio no compatible).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | La versión actual del destino existente. El valor del atributo `version` al realizar una solicitud de búsqueda para el destino. |

**Respuesta**

La respuesta incluye los detalles actualizados para el destino, incluido su ID y el nuevo `version` del destino.

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

Si su organización ya no requiere un destino de proyección, se puede eliminar realizando una solicitud de DELETE al extremo `/config/destinations` e incluyendo el ID del destino que desea eliminar en la ruta de solicitud.

>[!CAUTION]
>
>La respuesta de la API a la solicitud de eliminación es inmediata, pero los cambios reales en los datos de los bordes se producen de forma asíncrona. En otras palabras, los datos de perfil se eliminarán de todos los bordes (el `dataCenters` especificado en el destino de la proyección), pero el proceso tardará un tiempo en completarse.

**Formato de API**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DESTINATION_ID}` | ID exclusivo del destino de la proyección que desea eliminar. |


**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La solicitud de eliminación devuelve el estado HTTP 204 (sin contenido) y un cuerpo de respuesta vacío. Puede confirmar que la eliminación se haya realizado correctamente realizando una solicitud de búsqueda del destino por su ID. La búsqueda debe devolver el estado HTTP 404 (no encontrado).

## Configuraciones de proyección

Las configuraciones de proyección proporcionan información sobre qué datos deben estar disponibles en cada Edge. En lugar de proyectar un esquema [!DNL Experience Data Model] (XDM) completo al borde, una proyección proporciona solo datos o campos específicos del esquema. Su organización puede definir más de una configuración de proyección para cada esquema XDM.

### Enumerar todas las configuraciones de proyección

Puede enumerar todas las configuraciones de proyección creadas para su organización realizando una solicitud de GET al extremo `/config/projections` . También puede agregar parámetros opcionales a la ruta de solicitud para acceder a las configuraciones de proyección de un esquema en particular o buscar una proyección individual por su nombre.

**Formato de API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parámetro | Descripción |
|---|---|
| `{SCHEMA_NAME}` | Nombre de la clase de esquema asociada con la configuración de proyección a la que desea acceder. |
| `{PROJECTION_NAME}` | Nombre de la configuración de proyección a la que desea acceder. |

>[!NOTE]
>
>`schemaName` es necesario cuando se utiliza el  `name` parámetro , ya que el nombre de configuración de la proyección solo es único en el contexto de una clase de esquema.

**Solicitud**

La siguiente solicitud enumera todas las configuraciones de proyección asociadas con la clase de esquema [!DNL Experience Data Model], [!DNL XDM Individual Profile]. Para obtener más información sobre XDM y su función dentro de [!DNL Platform], comience leyendo la [información general del sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de configuraciones de proyección dentro del atributo `_embedded` raíz, contenido en la matriz `projectionConfigs`. Si no se han realizado configuraciones de proyección para su organización, la matriz `projectionConfigs` estará vacía.

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

### Crear una configuración de proyección

Puede crear (POST) una nueva configuración de proyección que dicte qué campos XDM están disponibles en los bordes.

**Formato de API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parámetro | Descripción |
|---|---|
| `{SCHEMA_NAME}` | Nombre de la clase de esquema asociada con la configuración de proyección a la que desea acceder. |

**Solicitud**

>[!NOTE]
>
>La solicitud del POST para crear una configuración requiere un encabezado `Content-Type` específico, como se muestra a continuación. El uso de un encabezado `Content-Type` incorrecto genera un error de estado HTTP 415 (tipo de medio no compatible).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `selector` | Cadena que contiene una lista de propiedades dentro del esquema que se van a replicar en los bordes. Las prácticas recomendadas para trabajar con selectores están disponibles en la sección [Selectores](#selectors) de este documento. |
| `name` | Un nombre descriptivo para la nueva configuración de proyección. |
| `destinationId` | Identificador del destino de borde al que se proyectarán los datos. |

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

Un selector es una lista de nombres de campo XDM separados por comas. En una configuración de proyección, el selector designa las propiedades que se incluyen en las proyecciones. El formato del valor del parámetro `selector` se basa de forma flexible en la sintaxis XPath. La sintaxis admitida se resume a continuación y se proporcionan ejemplos adicionales como referencia.

### Sintaxis compatible

* Utilice comas para seleccionar varios campos. No utilice espacios.
* Utilice la notación de puntos para seleccionar campos anidados.
   * Por ejemplo, para seleccionar un campo denominado `field` que está anidado dentro de un campo denominado `foo`, utilice el selector `foo.field`.
* Al incluir un campo que contiene subcampos, todos los subcampos también se proyectan de forma predeterminada. Sin embargo, puede filtrar los subcampos devueltos utilizando los paréntesis `"( )"`.
   * Por ejemplo, `addresses(type,city.country)` devuelve solo el tipo de dirección y el país en el que se ubica la ciudad de dirección para cada elemento de matriz `addresses`.
   * El ejemplo anterior es equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Tanto la notación de puntos como la notación entre paréntesis son compatibles para hacer referencia a subcampos. Sin embargo, se recomienda utilizar la notación de puntos porque es más concisa y proporciona una mejor ilustración de la jerarquía de campos.

* Cada campo de un selector se especifica en relación con la raíz de la respuesta.
   * Si los datos son una colección de recursos, la proyección incluirá una matriz de recursos.
   * Si los datos son un solo recurso, la proyección incluirá campos relativos a ese recurso.
   * Si el campo seleccionado es (o forma parte de) una matriz, la proyección incluirá la parte seleccionada de todos los elementos de la matriz.

### Ejemplos del parámetro del selector

Los siguientes ejemplos muestran parámetros `selector` de muestra, seguidos de los valores estructurados que representan.

**person.lastName**

Devuelve el subcampo `lastName` del objeto `person` en el recurso solicitado.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**direcciones**

Devuelve todos los elementos de la matriz `addresses`, incluidos todos los campos de cada elemento, pero no otros campos.

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

Devuelve el campo `person.lastName` y todos los elementos de la matriz `addresses`.

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

Devuelve solo el campo de ciudad para todos los elementos de la matriz de direcciones.

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
>Siempre que se devuelve un campo anidado, la proyección incluye los objetos principales que lo rodean. Los campos principales no incluyen ningún otro campo secundario a menos que también estén seleccionados explícitamente.

**addresses(type,city)**

Devuelve solo los valores de los campos `type` y `city` para cada elemento de la matriz `addresses`. Todos los demás subcampos contenidos en cada elemento `addresses` se filtran hacia fuera.

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

Esta guía le muestra los pasos necesarios para configurar proyecciones y destinos, incluido cómo dar formato adecuado al parámetro `selector`. Ahora puede crear nuevos destinos de proyección y configuraciones específicas de las necesidades de su organización.
