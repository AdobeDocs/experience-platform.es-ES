---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;habilitar conjunto de datos
title: Habilitar un conjunto de datos para el perfil y el servicio de identidad mediante API
type: Tutorial
description: Este tutorial muestra cómo habilitar un conjunto de datos para utilizarlo con el perfil del cliente en tiempo real y el servicio de identidad mediante las API de Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service] uso de API

Este tutorial cubre el proceso de habilitar un conjunto de datos para utilizarlo en [!DNL Real-Time Customer Profile] y [!DNL Identity Service], desglosado en los pasos siguientes:

1. Habilitar un conjunto de datos para utilizarlo en [!DNL Real-Time Customer Profile], utilizando una de las dos opciones:
   - [Crear un nuevo conjunto de datos](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar un conjunto de datos existente](#configure-an-existing-dataset)
1. [Ingesta de datos en el conjunto de datos](#ingest-data-into-the-dataset)
1. [Confirmar la ingesta de datos por el perfil del cliente en tiempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar ingesta de datos por servicio de identidad](#confirm-data-ingest-by-identity-service)

## Primeros pasos

Este tutorial requiere una comprensión práctica de varios servicios de Adobe Experience Platform implicados en la administración de conjuntos de datos con perfil habilitado. Antes de comenzar este tutorial, revise la documentación de estos temas relacionados [!DNL Platform] servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] uniendo identidades de diferentes fuentes de datos que se están ingiriendo en [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): una API RESTful que le permite crear conjuntos de datos y configurarlos para [!DNL Real-Time Customer Profile] y [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas correctamente a las API de Platform.

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un `Content-Type` encabezado. El valor correcto de este encabezado se muestra en las solicitudes de ejemplo cuando es necesario.

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un `x-sandbox-name` que especifica el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

## Crear un conjunto de datos habilitado para Perfil e identidad {#create-a-dataset-enabled-for-profile-and-identity}

Puede habilitar un conjunto de datos para el perfil del cliente en tiempo real y el servicio de identidad inmediatamente después de la creación o en cualquier momento después de la creación del conjunto de datos. Si desea habilitar un conjunto de datos que ya se haya creado, siga los pasos para lo siguiente [configuración de un conjunto de datos existente](#configure-an-existing-dataset) se encuentra más adelante en este documento.

>[!NOTE]
>
>Para crear un nuevo conjunto de datos habilitado para perfiles, debe conocer el ID de un esquema XDM existente que esté habilitado para el perfil. Para obtener información sobre cómo buscar o crear un esquema con perfil habilitado, consulte el tutorial sobre [creación de un esquema mediante la API de Registro de esquemas](../../xdm/tutorials/create-schema-api.md).

Para crear un conjunto de datos habilitado para el perfil, puede utilizar una solicitud del POST a `/dataSets` punto final.

**Formato de API**

```http
POST /dataSets
```

**Solicitud**

Incluyendo `unifiedProfile` y `unifiedIdentity` bajo `tags` en el cuerpo de la solicitud, el conjunto de datos se habilitará inmediatamente para [!DNL Profile] y [!DNL Identity Service], respectivamente. Los valores de estas etiquetas deben ser una matriz que contenga la cadena `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propiedad | Descripción |
|---|---|
| `schemaRef.id` | El ID del [!DNL Profile]Esquema habilitado para que se base el conjunto de datos. |
| `{TENANT_ID}` | El área de nombres dentro de [!DNL Schema Registry] que contiene recursos que pertenecen a su organización IMS. Consulte la [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la sección [!DNL Schema Registry] guía para desarrolladores para obtener más información. |

**Respuesta**

Una respuesta correcta muestra una matriz que contiene el ID del conjunto de datos recién creado en forma de `"@/dataSets/{DATASET_ID}"`. Una vez que haya creado y habilitado correctamente un conjunto de datos, siga los pasos para [carga de datos](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar un conjunto de datos existente {#configure-an-existing-dataset}

Los siguientes pasos explican cómo habilitar un conjunto de datos creado anteriormente para [!DNL Real-Time Customer Profile] y [!DNL Identity Service]. Si ya ha creado un conjunto de datos con perfil habilitado, siga los pasos para [ingesta de datos](#ingest-data-into-the-dataset).

### Compruebe si el conjunto de datos está habilitado {#check-if-the-dataset-is-enabled}

Uso del [!DNL Catalog] API, puede inspeccionar un conjunto de datos existente para determinar si está habilitado para su uso en [!DNL Real-Time Customer Profile] y [!DNL Identity Service]. La siguiente llamada recupera los detalles de un conjunto de datos por ID.

**Formato de API**

```http
GET /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | El ID del conjunto de datos que desea inspeccionar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
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
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
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

En el `tags` propiedad, puede ver que `unifiedProfile` y `unifiedIdentity` están presentes con el valor `enabled:true`. Por lo tanto, [!DNL Real-Time Customer Profile] y [!DNL Identity Service] están habilitados para este conjunto de datos, respectivamente.

### Habilitar el conjunto de datos {#enable-the-dataset}

Si el conjunto de datos existente no se ha habilitado para [!DNL Profile] o [!DNL Identity Service], puede habilitarlo realizando una solicitud de PATCH con el ID del conjunto de datos.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | El ID del conjunto de datos que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

El cuerpo de la solicitud incluye un `path` a dos tipos de etiquetas, `unifiedProfile` y `unifiedIdentity`. El `value` de cada son matrices que contienen la cadena `enabled:true`.

**Respuesta**
Una solicitud correcta del PATCH devuelve el estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. El `unifiedProfile` y `unifiedIdentity` ahora se han agregado etiquetas y el conjunto de datos está habilitado para su uso por los servicios de perfil e identidad.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingesta de datos en el conjunto de datos {#ingest-data-into-the-dataset}

Ambos [!DNL Real-Time Customer Profile] y [!DNL Identity Service] consumir datos XDM a medida que se incorporan a un conjunto de datos. Para obtener instrucciones sobre cómo cargar datos en un conjunto de datos, consulte el tutorial sobre [creación de un conjunto de datos mediante API](../../catalog/datasets/create.md). Al planificar qué datos enviar a su [!DNL Profile]Conjunto de datos habilitado para, tenga en cuenta las siguientes prácticas recomendadas:

- Incluya cualquier dato que desee utilizar como criterio de segmentación.
- Incluya tantos identificadores como pueda comprobar a partir de los datos de perfil para maximizar el gráfico de identidad. Esto permite [!DNL Identity Service] para vincular las identidades entre conjuntos de datos de forma más eficaz.

## Confirmar ingesta de datos por [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que implica un nuevo ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado según lo esperado. Uso del [!DNL Real-Time Customer Profile] Acceso a la API, puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Real-Time Customer Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplen con sus expectativas. Para obtener instrucciones detalladas sobre cómo utilizar el [!DNL Real-Time Customer Profile] API para acceder a [!DNL Profile] datos, consulte la [guía de extremo de entidades](../../profile/api/entities.md), también conocido como &quot;[!DNL Profile Access]&quot; API.

## Confirmar ingesta de datos por servicio de identidad {#confirm-data-ingest-by-identity-service}

Cada fragmento de datos introducido que contiene más de una identidad crea un vínculo en el gráfico de identidad privada. Para obtener más información sobre los gráficos de identidad y acceder a los datos de identidad, comience por leer el [Introducción al servicio de identidad](../../identity-service/home.md).
