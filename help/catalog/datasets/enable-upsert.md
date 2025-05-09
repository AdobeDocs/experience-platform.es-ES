---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;habilitar conjunto de datos
title: Habilitar un conjunto de datos para actualizaciones de perfil mediante API
type: Tutorial
description: Este tutorial muestra cómo utilizar las API de Adobe Experience Platform para habilitar un conjunto de datos con funcionalidades de "actualización" y así poder realizar actualizaciones en los datos del perfil del cliente en tiempo real.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 7%

---

# Habilitar un conjunto de datos para actualizaciones de perfil mediante API

Este tutorial cubre el proceso de activación de un conjunto de datos con funciones de &quot;actualización&quot; para realizar actualizaciones de los datos del perfil del cliente en tiempo real. Esto incluye pasos para crear un nuevo conjunto de datos y configurar uno existente.

>[!NOTE]
>
>El flujo de trabajo descrito en este tutorial solo funciona para la ingesta por lotes. Para actualizaciones de ingesta de transmisión, consulte la guía sobre [envío de actualizaciones parciales de fila al perfil del cliente en tiempo real mediante la preparación de datos](../../data-prep/upserts.md).

## Introducción

Este tutorial requiere una comprensión práctica de varios servicios de Adobe Experience Platform implicados en la administración de conjuntos de datos con perfil habilitado. Antes de comenzar este tutorial, revise la documentación de estos servicios relacionados de [!DNL Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [[!DNL Catalog Service]](../../catalog/home.md): una API RESTful que le permite crear conjuntos de datos y configurarlos para [!DNL Real-Time Customer Profile] y [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
- [Ingesta por lotes](../../ingestion/batch-ingestion/overview.md): La API de ingesta por lotes le permite ingerir datos en Experience Platform como archivos por lotes.

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas correctamente a las API de Experience Platform.

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado `Content-Type` adicional. El valor correcto de este encabezado se muestra en las solicitudes de ejemplo cuando es necesario.

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API [!DNL Experience Platform] requieren un encabezado `x-sandbox-name` que especifica el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

## Crear un conjunto de datos habilitado para actualizaciones de perfil

Al crear un nuevo conjunto de datos, puede habilitar ese conjunto de datos para Perfil y habilitar las funcionalidades de actualización en el momento de la creación.

>[!NOTE]
>
>Para crear un nuevo conjunto de datos habilitado para perfiles, debe conocer el ID de un esquema XDM existente que esté habilitado para el perfil. Para obtener información sobre cómo buscar o crear un esquema habilitado para el perfil, vea el tutorial sobre [creación de un esquema mediante la API de Registro de esquemas](../../xdm/tutorials/create-schema-api.md).

Para crear un conjunto de datos habilitado para Perfil y actualizaciones, use una petición POST para el extremo `/dataSets`.

**Formato de API**

```http
POST /dataSets
```

**Solicitud**

Al incluir tanto `unifiedIdentity` como `unifiedProfile` en `tags` en el cuerpo de la solicitud, el conjunto de datos se habilitará para [!DNL Profile] tras la creación. Dentro de la matriz `unifiedProfile`, al agregar `isUpsert:true` se agregará la capacidad para que el conjunto de datos admita actualizaciones.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schemaRef.id` | El identificador del esquema habilitado para [!DNL Profile] en el que se basará el conjunto de datos. |
| `{TENANT_ID}` | El área de nombres dentro de [!DNL Schema Registry] que contiene recursos que pertenecen a su organización. Consulte la sección [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la guía para desarrolladores de [!DNL Schema Registry] para obtener más información. |

**Respuesta**

Una respuesta correcta muestra una matriz que contiene el ID del conjunto de datos recién creado en forma de `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar un conjunto de datos existente {#configure-an-existing-dataset}

Los siguientes pasos tratan sobre cómo configurar un conjunto de datos con perfil habilitado para la funcionalidad de actualización (actualización).

>[!NOTE]
>
>Para configurar un conjunto de datos con perfil habilitado para su actualización, primero debe deshabilitar el conjunto de datos para el perfil y, a continuación, volver a habilitarlo junto con la etiqueta `isUpsert`. Si el conjunto de datos existente no está habilitado para el perfil, puede continuar directamente con los pasos para [habilitar el conjunto de datos para el perfil y actualizar](#enable-the-dataset). Si no está seguro, los siguientes pasos le muestran cómo comprobar si el conjunto de datos ya está habilitado.

### Compruebe si el conjunto de datos está habilitado para el perfil

Con la API [!DNL Catalog], puede inspeccionar un conjunto de datos existente para determinar si está habilitado para usarse en [!DNL Real-Time Customer Profile]. La siguiente llamada recupera los detalles de un conjunto de datos por ID.

**Formato de API**

```http
GET /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID del conjunto de datos que desea inspeccionar. |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

En la propiedad `tags`, puede ver que `unifiedProfile` está presente con el valor `enabled:true`. Por lo tanto, [!DNL Real-Time Customer Profile] está habilitado para este conjunto de datos.

### Deshabilitar el conjunto de datos para el perfil

Para configurar un conjunto de datos con perfil habilitado para las actualizaciones, primero debe deshabilitar las etiquetas `unifiedProfile` y `unifiedIdentity` y luego volver a habilitarlas junto con la etiqueta `isUpsert`. Esto se realiza mediante dos solicitudes de PATCH, una para deshabilitar y otra para volver a habilitar.

>[!WARNING]
>
>Los datos introducidos en el conjunto de datos mientras está deshabilitado no se introducirán en el almacén de perfiles. Debe evitar la ingesta de datos en el conjunto de datos hasta que se haya vuelto a habilitar para el perfil.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID del conjunto de datos que desea actualizar. |

**Solicitud**

El primer cuerpo de solicitud de PATCH incluye un `path` para `unifiedProfile` y un `path` para `unifiedIdentity`, lo que establece `value` para `enabled:false` en ambas rutas de acceso para deshabilitar las etiquetas.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Respuesta**

Una solicitud correcta de PATCH devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH. Ahora se han deshabilitado las etiquetas `unifiedProfile` y `unifiedIdentity`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Habilitar el conjunto de datos para perfiles y actualizaciones {#enable-the-dataset}

Se puede habilitar un conjunto de datos existente para las actualizaciones de perfiles y atributos mediante una sola solicitud de PATCH.

>[!IMPORTANT]
>
>Al habilitar el conjunto de datos para el perfil, asegúrese de que el esquema con el que está asociado el conjunto de datos esté habilitado para el perfil **also**. Si el esquema no tiene habilitado el perfil, el conjunto de datos **no** aparecerá como habilitado para el perfil en la interfaz de usuario de Experience Platform.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID del conjunto de datos que desea actualizar. |

**Solicitud**

El cuerpo de la solicitud incluye un `path` para `unifiedProfile` que establece `value` para incluir las etiquetas `enabled` y `isUpsert`, ambas establecidas en `true`, y un `path` para `unifiedIdentity` que establece `value` para incluir la etiqueta `enabled` establecida en `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Respuesta**

Una solicitud correcta de PATCH devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH. La etiqueta `unifiedProfile` y la etiqueta `unifiedIdentity` se han habilitado y configurado para actualizaciones de atributos.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Pasos siguientes

Los flujos de trabajo de ingesta por lotes ahora pueden utilizar el perfil y el conjunto de datos habilitado para actualizar los datos del perfil. Para obtener más información acerca de la ingesta de datos en Adobe Experience Platform, comience por leer la [descripción general de la ingesta de datos](../../ingestion/home.md).
