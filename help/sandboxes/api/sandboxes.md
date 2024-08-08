---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de espacios aislados
solution: Experience Platform
title: Punto final de API de administración de zona protegida
description: El extremo /sandboxes de la API de espacio aislado le permite administrar mediante programación los espacios aislados en Adobe Experience Platform.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: c15b24990835746a51a50a3e7e7b6a85701c0eb9
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 4%

---

# Extremo de administración de zona protegida

Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno de producción. El extremo `/sandboxes` de la API [!DNL Sandbox] le permite administrar mediante programación las zonas protegidas en Platform.

## Introducción

El extremo de API utilizado en esta guía forma parte de la [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de zonas protegidas {#list}

Puede enumerar todas las zonas protegidas que pertenecen a su organización (activas o de otro tipo), realizando una solicitud de GET al extremo `/sandboxes`.

**Formato de API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la sección sobre [parámetros de consulta](./appendix.md#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de zonas protegidas que pertenecen a su organización, incluidos detalles como `name`, `title`, `state` y `type`.

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
| `name` | Nombre de la zona protegida. Esta propiedad se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | El nombre para mostrar de la zona protegida. |
| `state` | El estado de procesamiento actual de la zona protegida. El estado de una zona protegida puede ser cualquiera de los siguientes: <br/><ul><li>`creating`: se ha creado la zona protegida, pero el sistema aún la está aprovisionando.</li><li>`active`: la zona protegida se ha creado y está activa.</li><li>`failed`: debido a un error, el sistema no pudo aprovisionar la zona protegida y está deshabilitada.</li><li>`deleted`: la zona protegida se ha deshabilitado manualmente.</li></ul> |
| `type` | El tipo de zona protegida. Los tipos de zona protegida admitidos actualmente incluyen `development` y `production`. |
| `isDefault` | Una propiedad booleana que indica si esta zona protegida es la zona protegida de producción predeterminada para la organización. |
| `eTag` | Identificador de una versión específica de la zona protegida. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en la zona protegida. |

## Búsqueda de una zona protegida {#lookup}

Puede buscar una zona protegida individual realizando una solicitud de GET que incluya la propiedad `name` de la zona protegida en la ruta de solicitud.

**Formato de API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` de la zona protegida que desea buscar. |

**Solicitud**

La siguiente solicitud recupera una zona protegida llamada &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la zona protegida, incluidos sus `name`, `title`, `state` y `type`.

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
| `name` | Nombre de la zona protegida. Esta propiedad se utiliza con fines de búsqueda en llamadas a la API. |
| `title` | El nombre para mostrar de la zona protegida. |
| `state` | El estado de procesamiento actual de la zona protegida. El estado de una zona protegida puede ser cualquiera de los siguientes: <ul><li>**creando**: la zona protegida se ha creado, pero el sistema la sigue aprovisionando.</li><li>**activo**: la zona protegida se ha creado y está activa.</li><li>**error**: debido a un error, el sistema no pudo aprovisionar la zona protegida y está deshabilitada.</li><li>**eliminado**: la zona protegida se ha deshabilitado manualmente.</li></ul> |
| `type` | El tipo de zona protegida. Los tipos de zona protegida admitidos actualmente incluyen: `development` y `production`. |
| `isDefault` | Una propiedad booleana que indica si esta zona protegida es la predeterminada para la organización. Normalmente, esta es la zona protegida de producción. |
| `eTag` | Identificador de una versión específica de la zona protegida. Este valor, que se utiliza para el control de versiones y la eficacia del almacenamiento en caché, se actualiza cada vez que se realiza un cambio en la zona protegida. |

## Creación de una zona protegida {#create}

>[!NOTE]
>
>Cuando se cree una nueva zona protegida, primero debe agregarla al perfil del producto en [Adobe Admin Console](https://adminconsole.adobe.com/) para poder empezar a usarla. Consulte la documentación sobre [administración de permisos para un perfil de producto](../../access-control/ui/permissions.md) para obtener información sobre cómo aprovisionar una zona protegida en un perfil de producto.

Puede crear una nueva zona protegida de desarrollo o producción realizando una solicitud de POST al extremo `/sandboxes`.

### Creación de una zona protegida de desarrollo

Para crear una zona protegida de desarrollo, debe proporcionar un atributo `type` con un valor de `development` en la carga de la solicitud.

**Formato de API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea una nueva zona protegida de desarrollo denominada &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El identificador que se utilizará para acceder a la zona protegida en solicitudes futuras. Este valor debe ser único, y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible en lenguaje natural que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de zona protegida que se va a crear. Para una zona protegida que no sea de producción, este valor debe ser `development`. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la zona protegida recién creada, que muestran que su `state` está &quot;creando&quot;.

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
>El sistema tarda aproximadamente 30 segundos en aprovisionar las zonas protegidas, después de lo cual su `state` se volverá &quot;activo&quot; o &quot;fallido&quot;.

### Creación de una zona protegida de producción

Para crear una zona protegida de producción, debe proporcionar un atributo `type` con un valor de `production` en la carga de la solicitud.

**Formato de API**

```http
POST /sandboxes
```

**Solicitud**

La siguiente solicitud crea una nueva zona protegida de producción denominada &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | El identificador que se utilizará para acceder a la zona protegida en solicitudes futuras. Este valor debe ser único, y se recomienda hacerlo lo más descriptivo posible. Este valor no puede contener espacios ni caracteres especiales. |
| `title` | Un nombre legible en lenguaje natural que se utiliza con fines de visualización en la interfaz de usuario de Platform. |
| `type` | Tipo de zona protegida que se va a crear. Para una zona protegida de producción, este valor debe ser `production`. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la zona protegida recién creada, que muestran que su `state` está &quot;creando&quot;.

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
>El sistema tarda aproximadamente 30 segundos en aprovisionar las zonas protegidas, después de lo cual su `state` se volverá &quot;activo&quot; o &quot;fallido&quot;.

## Actualización de una zona protegida {#put}

Puede actualizar uno o varios campos de una zona protegida realizando una solicitud al PATCH que incluya `name` de la zona protegida en la ruta de solicitud y la propiedad que se actualizará en la carga útil de la solicitud.

>[!NOTE]
>
>Actualmente solo se puede actualizar la propiedad `title` de una zona protegida.

**Formato de API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` de la zona protegida que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza la propiedad `title` de la zona protegida denominada &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) con los detalles de la zona protegida recién actualizada.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Restablecer una zona protegida {#reset}

Las zonas protegidas tienen una función de &quot;restablecimiento de fábrica&quot; que elimina todos los recursos no predeterminados de una zona protegida. Puede restablecer una zona protegida realizando una solicitud de PUT que incluya la zona protegida `name` en la ruta de solicitud.

**Formato de API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` de la zona protegida que desea restablecer. |
| `validationOnly` | Un parámetro opcional que le permite realizar una comprobación previa al vuelo en la operación de restablecimiento de la zona protegida sin realizar la solicitud real. Establezca este parámetro en `validationOnly=true` para comprobar si la zona protegida que va a restablecer contiene datos de uso compartido de Adobe Analytics, Adobe Audience Manager o segmentos. |

**Solicitud**

La siguiente solicitud restablece una zona protegida llamada &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `action` | Este parámetro debe proporcionarse en la carga útil de la solicitud con el valor &quot;reset&quot; para restablecer la zona protegida. |

**Respuesta**

>[!NOTE]
>
>Una vez restablecida una zona protegida, el sistema tarda aproximadamente 30 segundos en aprovisionarla.

Una respuesta correcta devuelve los detalles de la zona protegida actualizada, lo que muestra que su `state` se está &quot;restableciendo&quot;.

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

La zona protegida de producción predeterminada y las creadas por el usuario no se pueden restablecer si Adobe Analytics también está usando el gráfico de identidades alojado en ella para la característica [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=es) o si Adobe Audience Manager también está usando el gráfico de identidades alojado en ella para la característica [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=es).

A continuación se muestra una lista de posibles excepciones que podrían impedir que se restablezca una zona protegida:

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

Puede restablecer una zona protegida de producción que se use para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service] agregando el parámetro `ignoreWarnings` a su solicitud.

**Formato de API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | La propiedad `name` de la zona protegida que desea restablecer. |
| `ignoreWarnings` | Un parámetro opcional que le permite omitir la comprobación de validación y forzar el restablecimiento de una zona protegida de producción que se utiliza para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service]. Este parámetro no se puede aplicar a una zona protegida de producción predeterminada. |

**Solicitud**

La siguiente solicitud restablece una zona protegida de producción denominada &quot;acme&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la zona protegida actualizada, lo que muestra que su `state` se está &quot;restableciendo&quot;.

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

## Eliminación de una zona protegida {#delete}

>[!IMPORTANT]
>
>No se puede eliminar la zona protegida de producción predeterminada.

Puede eliminar una zona protegida realizando una solicitud de DELETE que incluya la zona protegida `name` en la ruta de solicitud.

>[!NOTE]
>
>Al realizar esta llamada de API, se actualiza la propiedad `status` de la zona protegida a &quot;eliminada&quot; y se desactiva. Las solicitudes de GET aún pueden recuperar los detalles de la zona protegida después de eliminarla.

**Formato de API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{SANDBOX_NAME}` | `name` de la zona protegida que desea eliminar. |
| `validationOnly` | Un parámetro opcional que le permite realizar una comprobación previa al vuelo en la operación de eliminación de la zona protegida sin realizar la solicitud real. Establezca este parámetro en `validationOnly=true` para comprobar si la zona protegida que va a restablecer contiene datos de uso compartido de Adobe Analytics, Adobe Audience Manager o segmentos. |
| `ignoreWarnings` | Un parámetro opcional que le permite omitir la comprobación de validación y forzar la eliminación de una zona protegida de producción creada por el usuario que se utiliza para compartir segmentos bidireccionales con [!DNL Audience Manager] o [!DNL Audience Core Service]. Este parámetro no se puede aplicar a una zona protegida de producción predeterminada. |

**Solicitud**

La siguiente solicitud elimina una zona protegida de producción denominada &quot;acme&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actualizados de la zona protegida, lo que muestra que su `state` se ha &quot;eliminado&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
