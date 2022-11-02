---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API;habilitar conjunto de datos
title: Habilitar un conjunto de datos para actualizaciones de perfil mediante API
type: Tutorial
description: Este tutorial le muestra cómo utilizar las API de Adobe Experience Platform para habilitar un conjunto de datos con capacidades de "actualización" para realizar actualizaciones en los datos del perfil del cliente en tiempo real.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 132407af947b97a1925799a1fb5e12caa2b0410c
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 2%

---

# Habilitar un conjunto de datos para actualizaciones de perfil mediante API

Este tutorial trata el proceso de activación de un conjunto de datos con capacidades de &quot;actualización&quot; para realizar actualizaciones en los datos del perfil del cliente en tiempo real. Esto incluye pasos para crear un nuevo conjunto de datos y configurar un conjunto de datos existente.

>[!NOTE]
>
>El flujo de trabajo de actualización solo funciona para la ingesta por lotes. La ingesta de transmisión es **not** compatible.

## Primeros pasos

Este tutorial requiere una comprensión práctica de varios servicios de Adobe Experience Platform involucrados en la administración de conjuntos de datos con perfil habilitado. Antes de comenzar este tutorial, revise la documentación de estas [!DNL Platform] servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Catalog Service]](../../catalog/home.md): Una API de RESTful que le permite crear conjuntos de datos y configurarlos para [!DNL Real-time Customer Profile] y [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.
- [Ingesta por lotes](../../ingestion/batch-ingestion/overview.md): La API de ingesta de lotes permite introducir datos en el Experience Platform como archivos por lotes.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente a las API de Platform.

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un `Content-Type` encabezado. El valor correcto de este encabezado se muestra en las solicitudes de muestra donde es necesario.

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un `x-sandbox-name` encabezado que especifica el nombre del simulador de pruebas en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

## Crear un conjunto de datos habilitado para las actualizaciones de perfil

Al crear un nuevo conjunto de datos, puede habilitar ese conjunto de datos para Perfil y habilitar las capacidades de actualización en el momento de la creación.

>[!NOTE]
>
>Para crear un nuevo conjunto de datos habilitado para Perfil, debe conocer el ID de un esquema XDM existente que esté habilitado para Perfil. Para obtener información sobre cómo buscar o crear un esquema habilitado para perfil, consulte el tutorial en [creación de un esquema mediante la API del Registro de esquemas](../../xdm/tutorials/create-schema-api.md).

Para crear un conjunto de datos habilitado para Perfil y actualizaciones, utilice una solicitud de POST para `/dataSets` punto final.

**Formato de API**

```http
POST /dataSets
```

**Solicitud**

Al incluir ambas `unifiedIdentity` y `unifiedProfile` under `tags` en el cuerpo de la solicitud, el conjunto de datos se habilitará para [!DNL Profile] al crearlo. Dentro de `unifiedProfile` matriz, adición `isUpsert:true` agregará la capacidad para que el conjunto de datos admita actualizaciones.

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
        "fields": [],
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
| `schemaRef.id` | El ID de la variable [!DNL Profile]esquema habilitado para , en el que se basará el conjunto de datos. |
| `{TENANT_ID}` | El espacio de nombres dentro de la variable [!DNL Schema Registry] que contiene recursos pertenecientes a su organización. Consulte la [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la sección [!DNL Schema Registry] guía para desarrolladores para obtener más información. |

**Respuesta**

Una respuesta correcta muestra una matriz que contiene el ID del conjunto de datos recién creado en forma de `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar un conjunto de datos existente {#configure-an-existing-dataset}

Los siguientes pasos tratan sobre cómo configurar un conjunto de datos habilitado para Perfil existente para la funcionalidad de actualización (actualización).

>[!NOTE]
>
>Para configurar un conjunto de datos habilitado para el perfil existente para la actualización, primero debe deshabilitar el conjunto de datos para el perfil y luego volver a habilitarlo junto con la variable `isUpsert` etiqueta. Si el conjunto de datos existente no está habilitado para Perfil, puede continuar directamente con los pasos de [activación del conjunto de datos para Perfil y actualizar](#enable-the-dataset). Si no está seguro, los siguientes pasos le muestran cómo comprobar si el conjunto de datos ya está habilitado.

### Comprobar si el conjunto de datos está habilitado para Perfil

Al usar la variable [!DNL Catalog] API, puede inspeccionar un conjunto de datos existente para determinar si está habilitado para usarse en [!DNL Real-time Customer Profile]. La siguiente llamada recupera los detalles de un conjunto de datos por ID.

**Formato de API**

```http
GET /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID de un conjunto de datos que desea inspeccionar. |

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
        "lastBatchId": "{BATCH_ID}",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

En el `tags` puede ver que `unifiedProfile` está presente con el valor `enabled:true`. Por lo tanto, [!DNL Real-time Customer Profile] está habilitado para este conjunto de datos.

### Deshabilitar el conjunto de datos para el perfil

Para configurar un conjunto de datos habilitado para perfiles para actualizaciones, primero debe deshabilitar la variable `unifiedProfile` y `unifiedIdentity` y vuelva a activarlas junto con la variable `isUpsert` etiqueta. Esto se realiza mediante dos solicitudes de PATCH, una para deshabilitar y otra para volver a habilitar.

>[!WARNING]
>
>Los datos introducidos en el conjunto de datos mientras está deshabilitado no se incorporarán en el Almacenamiento de perfiles. Debe evitar la ingesta de datos en el conjunto de datos hasta que se vuelva a habilitar para Perfil.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID del conjunto de datos que desea actualizar. |

**Solicitud**

El primer cuerpo de solicitud del PATCH incluye un `path` a `unifiedProfile` y `path` a `unifiedIdentity`, configurando la variable `value` a `enabled:false` para ambas rutas con el fin de deshabilitar las etiquetas.

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

Una solicitud de PATCH correcta devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. La variable `unifiedProfile` y `unifiedIdentity` las etiquetas de ahora se han desactivado.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Habilitar el conjunto de datos para Perfil y actualizar {#enable-the-dataset}

Se puede habilitar un conjunto de datos existente para las actualizaciones de perfiles y atributos mediante una única solicitud de PATCH.

>[!IMPORTANT]
>
>Al habilitar el conjunto de datos para Perfil, asegúrese de que el esquema al que está asociado el conjunto de datos sea **also** Habilitado para perfiles. Si el esquema no está habilitado para Perfil, el conjunto de datos **not** aparece como habilitado para perfiles en la interfaz de usuario de Platform.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{DATASET_ID}` | El ID de un conjunto de datos que desea actualizar. |

**Solicitud**

El cuerpo de la solicitud incluye un `path` a `unifiedProfile` configurar la variable `value` para incluir el `enabled` y `isUpsert` etiquetas, ambas configuradas como `true`y `path` a `unifiedIdentity` configurar la variable `value` para incluir el `enabled` etiqueta establecida en `true`.

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

Una solicitud de PATCH correcta devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. La variable `unifiedProfile` y `unifiedIdentity` ahora se han habilitado y configurado para las actualizaciones de atributos.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Pasos siguientes

Los flujos de trabajo de ingesta por lotes ahora pueden usar su conjunto de datos habilitado para perfiles y servidores para realizar actualizaciones en los datos de perfil. Para obtener más información sobre la ingesta de datos en Adobe Experience Platform, comience por leer la [información general sobre la ingesta de datos](../../ingestion/home.md).
