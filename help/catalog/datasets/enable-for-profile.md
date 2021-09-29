---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API;habilitar conjunto de datos
title: Habilitar un conjunto de datos para perfil y servicio de identidad mediante API
type: Tutorial
description: Este tutorial le muestra cómo habilitar un conjunto de datos para utilizarlo con el perfil del cliente en tiempo real y el servicio de identidad mediante las API de Adobe Experience Platform.
source-git-commit: 244e09835cec4b15d6a96e7d615321513fa3b5aa
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# Habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service] mediante API

Este tutorial trata el proceso de activación de un conjunto de datos para su uso en [!DNL Real-time Customer Profile] y [!DNL Identity Service], dividido en los siguientes pasos:

1. Habilite un conjunto de datos para utilizarlo en [!DNL Real-time Customer Profile], utilizando una de estas dos opciones:
   - [Crear un nuevo conjunto de datos](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar un conjunto de datos existente](#configure-an-existing-dataset)
1. [Ingesta de datos en el conjunto de datos](#ingest-data-into-the-dataset)
1. [Confirmar la ingesta de datos por Perfil del cliente en tiempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar la ingesta de datos por el servicio de identidad](#confirm-data-ingest-by-identity-service)

## Primeros pasos

Este tutorial requiere una comprensión práctica de varios servicios de Adobe Experience Platform involucrados en la administración de conjuntos de datos con perfil habilitado. Antes de comenzar este tutorial, revise la documentación de estos servicios de plataforma DNL relacionados:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Permite  [!DNL Real-time Customer Profile] al unir identidades de fuentes de datos dispares que se están incorporando en  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Una API de RESTful que permite crear conjuntos de datos y configurarlos para  [!DNL Real-time Customer Profile] y  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente a las API de Platform.

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado `Content-Type` adicional. El valor correcto de este encabezado se muestra en las solicitudes de muestra donde es necesario.

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado `x-sandbox-name` que especifique el nombre del simulador para pruebas en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

## Crear un conjunto de datos habilitado para Perfil e Identidad {#create-a-dataset-enabled-for-profile-and-identity}

Puede habilitar un conjunto de datos para Perfil del cliente en tiempo real y Servicio de identidad inmediatamente después de la creación o en cualquier momento después de crear el conjunto de datos. Si desea habilitar un conjunto de datos que ya se ha creado, siga los pasos para [configurar un conjunto de datos existente](#configure-an-existing-dataset) que se encuentra más adelante en este documento.

>[!NOTE]
>
>Para crear un nuevo conjunto de datos habilitado para Perfil, debe conocer el ID de un esquema XDM existente que esté habilitado para Perfil. Para obtener información sobre cómo buscar o crear un esquema habilitado para perfil, consulte el tutorial sobre la [creación de un esquema mediante la API del Registro de esquemas](../../xdm/tutorials/create-schema-api.md).

Para crear un conjunto de datos habilitado para Perfil, puede utilizar una solicitud de POST al extremo `/dataSets` .

**Formato de API**

```http
POST /dataSets
```

**Solicitud**

Al incluir `unifiedProfile` y `unifiedIdentity` en `tags` en el cuerpo de la solicitud, el conjunto de datos se habilitará inmediatamente para [!DNL Profile] y [!DNL Identity Service], respectivamente. Los valores de estas etiquetas deben ser una matriz que contenga la cadena `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propiedad | Descripción |
|---|---|
| `schemaRef.id` | El ID del esquema habilitado para [!DNL Profile] en el que se basará el conjunto de datos. |
| `{TENANT_ID}` | El espacio de nombres dentro de [!DNL Schema Registry] que contiene recursos pertenecientes a su organización de IMS. Consulte la sección [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la guía para desarrolladores de [!DNL Schema Registry] para obtener más información. |

**Respuesta**

Una respuesta correcta muestra una matriz que contiene el ID del conjunto de datos recién creado en forma de `"@/dataSets/{DATASET_ID}"`. Una vez que haya creado y habilitado correctamente un conjunto de datos, siga los pasos para [cargar datos](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar un conjunto de datos existente {#configure-an-existing-dataset}

Los siguientes pasos tratan sobre cómo habilitar un conjunto de datos creado anteriormente para [!DNL Real-time Customer Profile] y [!DNL Identity Service]. Si ya ha creado un conjunto de datos habilitado para el perfil, siga los pasos para [ingesta de datos](#ingest-data-into-the-dataset).

### Compruebe si el conjunto de datos está habilitado {#check-if-the-dataset-is-enabled}

Con la API [!DNL Catalog], puede inspeccionar un conjunto de datos existente para determinar si está habilitado para su uso en [!DNL Real-time Customer Profile] y [!DNL Identity Service]. La siguiente llamada recupera los detalles de un conjunto de datos por ID.

**Formato de API**

```http
GET /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | El ID de un conjunto de datos que desea inspeccionar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
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
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

En la propiedad `tags` puede ver que `unifiedProfile` y `unifiedIdentity` están presentes con el valor `enabled:true`. Por lo tanto, [!DNL Real-time Customer Profile] y [!DNL Identity Service] están habilitados para este conjunto de datos, respectivamente.

### Habilitar el conjunto de datos {#enable-the-dataset}

Si el conjunto de datos existente no se ha habilitado para [!DNL Profile] o [!DNL Identity Service], puede habilitarlo haciendo una solicitud de PATCH usando el ID del conjunto de datos.

**Formato de API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | El ID de un conjunto de datos que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

El cuerpo de la solicitud incluye de `path` a dos tipos de etiquetas, `unifiedProfile` y `unifiedIdentity`. Los `value` de cada son matrices que contienen la cadena `enabled:true`.

****
RespuestaUna solicitud correcta del PATCH devuelve el Estado HTTP 200 (OK) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud del PATCH. Ahora se han agregado las etiquetas `unifiedProfile` y `unifiedIdentity` y el conjunto de datos está habilitado para su uso por los servicios de Perfil e identidad.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingesta de datos en el conjunto de datos {#ingest-data-into-the-dataset}

Tanto [!DNL Real-time Customer Profile] como [!DNL Identity Service] consumen datos XDM a medida que se incorporan en un conjunto de datos. Para obtener instrucciones sobre cómo cargar datos en un conjunto de datos, consulte el tutorial sobre la [creación de un conjunto de datos mediante API](../../catalog/datasets/create.md). Al planificar qué datos enviar a su conjunto de datos habilitado para [!DNL Profile], tenga en cuenta las siguientes prácticas recomendadas:

- Incluya los datos que desee utilizar como criterios de segmentación.
- Incluya tantos identificadores como pueda comprobar a partir de los datos de perfil para maximizar el gráfico de identidad. Esto permite a [!DNL Identity Service] unir identidades entre conjuntos de datos de forma más eficaz.

## Confirmar la ingesta de datos por [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado según lo esperado. Con la API de acceso [!DNL Real-time Customer Profile], puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Real-time Customer Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplan con sus expectativas. Para obtener instrucciones detalladas sobre cómo utilizar la API [!DNL Real-time Customer Profile] para acceder a los datos [!DNL Profile], consulte la [guía de extremo de entidades](../../profile/api/entities.md), también conocida como la API &quot;[!DNL Profile Access]&quot;.

## Confirmar la ingesta de datos por el servicio de identidad {#confirm-data-ingest-by-identity-service}

Cada fragmento de datos introducido que contiene más de una identidad crea un vínculo en el gráfico de identidad privada. Para obtener más información sobre los gráficos de identidad y los datos de identidad de acceso, comience por leer la [información general del servicio de identidad](../../identity-service/home.md).
