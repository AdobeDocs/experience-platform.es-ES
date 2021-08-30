---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de entornos limitados
solution: Experience Platform
title: Punto final de la API de administración de entornos aislados
topic-legacy: developer guide
description: El extremo /sandboxes de la API de Sandbox le permite administrar entornos limitados en Adobe Experience Platform mediante programación.
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 3%

---

# Extremo de administración del Simulador para pruebas

Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno de producción. El extremo `/sandboxes` de la API [!DNL Sandbox] le permite administrar mediante programación entornos limitados en Platform.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, consulte la [guía de introducción](./getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios que se necesitan para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de entornos limitados {#list}

Puede enumerar todos los entornos limitados pertenecientes a su organización de IMS (activa o de otro tipo) realizando una solicitud de GET al extremo `/sandboxes` .

**Formato de API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales para filtrar los resultados por. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de entornos limitados que pertenecen a su organización, incluidos detalles como `name`, `title`, `state` y `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del simulador de pruebas. Esta propiedad se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | Nombre para mostrar del simulador para pruebas. |
| `state` | Estado de procesamiento actual del simulador de pruebas. El estado de un simulador para pruebas puede ser cualquiera de los siguientes: <br/><ul><li>`creating`: Se ha creado el simulador para pruebas, pero el sistema sigue aprovisionándolo.</li><li>`active`: El simulador para pruebas se crea y se activa.</li><li>`failed`: Debido a un error, el simulador de pruebas no pudo ser aprovisionado por el sistema y está deshabilitado.</li><li>`deleted`: El simulador para pruebas se ha desactivado manualmente.</li></ul> |
| `type` | El tipo de entorno limitado. Los tipos de entorno limitado admitidos actualmente son `development` y `production`. |
| `isDefault` | Una propiedad booleana que indica si este entorno limitado es el entorno limitado de producción predeterminado para la organización. |
| `eTag` | Identificador de una versión específica del simulador de pruebas. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en el simulador para pruebas. |

## Buscar un simulador para pruebas {#lookup}

Puede buscar un entorno limitado individual realizando una solicitud de GET que incluya la propiedad `name` del entorno limitado en la ruta de solicitud.

**Formato de API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador de pruebas que desea buscar. |

**Solicitud**

La siguiente solicitud recupera un entorno limitado denominado &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devolverá los detalles del entorno limitado, incluidos `name`, `title`, `state` y `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del simulador de pruebas. Esta propiedad se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | Nombre para mostrar del simulador para pruebas. |
| `state` | Estado de procesamiento actual del simulador de pruebas. El estado de un simulador para pruebas puede ser cualquiera de los siguientes: <ul><li>**crear**: Se ha creado el simulador para pruebas, pero el sistema sigue aprovisionándolo.</li><li>**activo**: El simulador para pruebas se crea y se activa.</li><li>**error**: Debido a un error, el simulador de pruebas no pudo ser aprovisionado por el sistema y está deshabilitado.</li><li>**eliminado**: El simulador para pruebas se ha desactivado manualmente.</li></ul> |
| `type` | El tipo de entorno limitado. Los tipos de entorno limitado admitidos actualmente son: `development` y `production`. |
| `isDefault` | Una propiedad booleana que indica si este entorno limitado es el entorno limitado predeterminado para la organización. Normalmente, este es el simulador para pruebas de producción. |
| `eTag` | Identificador de una versión específica del simulador de pruebas. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en el simulador para pruebas. |

## Creación de un simulador de pruebas {#create}

Puede crear un nuevo entorno limitado de desarrollo o producción realizando una solicitud de POST al extremo `/sandboxes` .

### Creación de un entorno limitado de desarrollo

Para crear un entorno limitado de desarrollo, debe proporcionar un atributo `type` con un valor de `development` en la carga útil de la solicitud.

**Formato de API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea un nuevo entorno limitado de desarrollo denominado &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en futuras solicitudes. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de simulador de pruebas que se va a crear. Para un entorno limitado que no es de producción, este valor debe ser `development`. |

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que su `state` está &quot;creando&quot;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Los entornos limitados tardan unos 30 segundos en aprovisionarse en el sistema, tras lo cual su `state` se convertirá en &quot;activo&quot; o &quot;fallido&quot;.

### Creación de un simulador para pruebas de producción

Para crear un entorno limitado de producción, debe proporcionar un atributo `type` con un valor de `production` en la carga útil de la solicitud.

**Formato de API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea un nuevo entorno limitado de producción denominado &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Identificador que se utilizará para acceder al simulador para pruebas en futuras solicitudes. Este valor debe ser único y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de simulador de pruebas que se va a crear. Para un entorno limitado de producción, este valor debe ser `production`. |

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado recién creado, mostrando que su `state` está &quot;creando&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Los entornos limitados tardan unos 30 segundos en aprovisionarse en el sistema, tras lo cual su `state` se convertirá en &quot;activo&quot; o &quot;fallido&quot;.

## Actualizar un simulador para pruebas {#put}

Puede actualizar uno o más campos de un simulador de pruebas realizando una solicitud de PATCH que incluya el `name` del simulador de pruebas en la ruta de solicitud y la propiedad que se va a actualizar en la carga útil de la solicitud.

>[!NOTE]
>
>Actualmente solo se puede actualizar la propiedad `title` de un entorno limitado.

**Formato de API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador de pruebas que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza la propiedad `title` del simulador de pruebas llamado &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) con los detalles del entorno limitado recién actualizado.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Restablecer un simulador para pruebas {#reset}

Los entornos limitados tienen una función de &quot;restablecimiento de fábrica&quot; que elimina todos los recursos no predeterminados de un entorno limitado. Puede restablecer un simulador para pruebas realizando una solicitud de PUT que incluya el `name` del simulador para pruebas en la ruta de solicitud.

**Formato de API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador de pruebas que desea restablecer. |
| `validationOnly` | Un parámetro opcional que permite realizar una comprobación previa de la operación de restablecimiento del simulador para pruebas sin realizar la solicitud real. Establezca este parámetro en `validationOnly=true` para comprobar si el simulador de pruebas que va a restablecer contiene datos de uso compartido de segmentos, Adobe Analytics o Adobe Audience Manager. |

**Solicitud**

La siguiente solicitud restablece un simulador de pruebas denominado &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `action` | Este parámetro debe proporcionarse en la carga útil de la solicitud con un valor de &quot;reset&quot; para restablecer el simulador para pruebas. |

**Respuesta**

>[!NOTE]
>
>Una vez que se restablece un simulador para pruebas, el sistema tarda unos 30 segundos en aprovisionar.

Una respuesta correcta devuelve los detalles del entorno limitado actualizado, mostrando que su `state` está &quot;restableciendo&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

El entorno limitado de producción predeterminado y los entornos limitados de producción creados por el usuario no se pueden restablecer si el gráfico de identidad alojado en él también está siendo utilizado por Adobe Analytics para la función [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) o si el gráfico de identidad alojado en él también está siendo utilizado por Adobe Audience Manager para la función [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).

A continuación se muestra una lista de posibles excepciones que podrían impedir que se restablezca un simulador para pruebas:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Puede restablecer un simulador para pruebas de producción que se utilice para el uso compartido de segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service] agregando el parámetro `ignoreWarnings` a su solicitud.

**Formato de API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` del simulador de pruebas que desea restablecer. |
| `ignoreWarnings` | Un parámetro opcional que le permite omitir la comprobación de validación y forzar el restablecimiento de un simulador para pruebas de producción que se utiliza para el uso compartido de segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service]. Este parámetro no se puede aplicar a un entorno limitado de producción predeterminado. |

**Solicitud**

La siguiente solicitud restablece un simulador de pruebas de producción denominado &quot;acme&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del entorno limitado actualizado, mostrando que su `state` está &quot;restableciendo&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Eliminación de un simulador para pruebas {#delete}

>[!IMPORTANT]
>
>No se puede eliminar el entorno limitado de producción predeterminado.

Puede eliminar un simulador para pruebas realizando una solicitud de DELETE que incluya el `name` del simulador para pruebas en la ruta de solicitud.

>[!NOTE]
>
>Al realizar esta llamada de API, se actualiza la propiedad `status` del entorno limitado a &quot;eliminado&quot; y se desactiva. Las solicitudes de GET aún pueden recuperar los detalles del entorno limitado una vez que se han eliminado.

**Formato de API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | El `name` del simulador de pruebas que desea eliminar. |
| `validationOnly` | Un parámetro opcional que permite realizar una comprobación previa de la operación de eliminación del simulador para pruebas sin realizar la solicitud real. Establezca este parámetro en `validationOnly=true` para comprobar si el simulador de pruebas que va a restablecer contiene datos de uso compartido de segmentos, Adobe Analytics o Adobe Audience Manager. |
| `ignoreWarnings` | Un parámetro opcional que le permite omitir la comprobación de validación y forzar la eliminación de un simulador para pruebas de producción creado por el usuario que se utiliza para el uso compartido de segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service]. Este parámetro no se puede aplicar a un entorno limitado de producción predeterminado. |

**Solicitud**

La siguiente solicitud elimina un simulador para pruebas de producción denominado &quot;acme&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actualizados del entorno limitado, mostrando que su `state` está &quot;eliminado&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
