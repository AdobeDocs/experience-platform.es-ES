---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API;habilitar conjunto de datos
title: Configuración de un conjunto de datos para Perfil y servicio de identidad mediante API
topic: tutorial
type: Tutorial
description: Este tutorial muestra cómo habilitar un conjunto de datos para su uso con el servicio de Perfil e identidad de clientes en tiempo real mediante las API de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 1%

---


# Configure un conjunto de datos para [!DNL Profile] y [!DNL Identity Service] mediante API

Este tutorial trata el proceso de habilitar un conjunto de datos para su uso en [!DNL Real-time Customer Profile] y [!DNL Identity Service], desglosado en los siguientes pasos:

1. Habilite un conjunto de datos para utilizarlo en [!DNL Real-time Customer Profile], utilizando una de las dos opciones:
   - [Crear un nuevo conjunto de datos](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar un conjunto de datos existente](#configure-an-existing-dataset)
1. [Ingesta de datos en el conjunto de datos](#ingest-data-into-the-dataset)
1. [Confirmar la ingesta de datos mediante el Perfil del cliente en tiempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar la ingesta de datos por servicio de identidad](#confirm-data-ingest-by-identity-service)

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos servicios de Adobe Experience Platform que participan en la administración de datasets habilitados para [!DNL Profile]. Antes de comenzar este tutorial, consulte la documentación de estos servicios [!DNL Platform] relacionados:

- [[!DNL Real-time Customer Profile]](../home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md):: Permite  [!DNL Real-time Customer Profile] el puente de identidades de orígenes de datos dispares que se están ingeriendo en  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md):: Una API RESTful que permite crear conjuntos de datos y configurarlos para  [!DNL Real-time Customer Profile] y  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Crear un conjunto de datos habilitado para [!DNL Profile] y [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Puede habilitar un conjunto de datos para [!DNL Real-time Customer Profile] y [!DNL Identity Service] inmediatamente después de la creación o en cualquier punto después de que se haya creado el conjunto de datos. Si desea habilitar un conjunto de datos que ya se ha creado, siga los pasos para [configurar un conjunto de datos existente](#configure-an-existing-dataset) que se encuentra más adelante en este documento. Para crear un nuevo conjunto de datos, debe conocer el ID de un esquema XDM existente que esté habilitado para el Perfil del cliente en tiempo real. Para obtener información sobre cómo buscar o crear un esquema con Perfil habilitado, consulte el tutorial sobre [creación de un esquema con la API del Registro de Esquema](../../xdm/tutorials/create-schema-api.md). La siguiente llamada a la API [!DNL Catalog] habilita un conjunto de datos para [!DNL Profile] y [!DNL Identity Service].

**Formato API**

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
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
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
| `schemaRef.id` | ID del esquema habilitado para [!DNL Profile] en el que se basará el conjunto de datos. |
| `{TENANT_ID}` | La Área de nombres dentro de [!DNL Schema Registry] que contiene recursos pertenecientes a su organización de IMS. Consulte la sección [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la guía para desarrolladores de [!DNL Schema Registry] para obtener más información. |

**Respuesta**

Una respuesta correcta muestra una matriz que contiene el ID del conjunto de datos recién creado en forma de `"@/dataSets/{DATASET_ID}"`. Una vez que haya creado y habilitado correctamente un conjunto de datos, continúe con los pasos para [cargar datos](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar un conjunto de datos existente {#configure-an-existing-dataset}

Los siguientes pasos explican cómo habilitar un conjunto de datos creado anteriormente para [!DNL Real-time Customer Profile] y [!DNL Identity Service]. Si ya ha creado un conjunto de datos habilitado para Perfil, continúe con los pasos para [ingesta de datos](#ingest-data-into-the-dataset).

### Compruebe si el conjunto de datos está habilitado {#check-if-the-dataset-is-enabled}

Mediante la API [!DNL Catalog], puede inspeccionar un conjunto de datos existente para determinar si está habilitado para su uso en [!DNL Real-time Customer Profile] y [!DNL Identity Service]. La siguiente llamada recupera los detalles de un conjunto de datos por ID.

**Formato API**

```http
GET /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | ID de un conjunto de datos que desea inspeccionar. |

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
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
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

Bajo la propiedad `tags`, puede ver que `unifiedProfile` y `unifiedIdentity` están presentes con el valor `enabled:true`. Por lo tanto, [!DNL Real-time Customer Profile] y [!DNL Identity Service] están habilitados para este conjunto de datos, respectivamente.

### Habilitar el conjunto de datos {#enable-the-dataset}

Si el conjunto de datos existente no se ha habilitado para [!DNL Profile] o [!DNL Identity Service], puede habilitarlo haciendo una solicitud de PATCH usando la ID del conjunto de datos.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DATASET_ID}` | ID de un conjunto de datos que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

El cuerpo de la solicitud incluye una propiedad `tags`, que contiene dos subpropiedades: `"unifiedProfile"` y `"unifiedIdentity"`. Los valores de estas subpropiedades son matrices que contienen la cadena `"enabled:true"`.

****
RespuestaUna solicitud de PATCH correcta devuelve Estado HTTP 200 (Aceptar) y una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH. Ahora se han agregado las etiquetas `"unifiedProfile"` y `"unifiedIdentity"` y el conjunto de datos está habilitado para su uso por Perfil y los servicios de identidad.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingresar datos en el conjunto de datos {#ingest-data-into-the-dataset}

Tanto [!DNL Real-time Customer Profile] como [!DNL Identity Service] consumen datos XDM a medida que se van ingeriendo en un conjunto de datos. Para obtener instrucciones sobre cómo cargar datos en un conjunto de datos, consulte el tutorial sobre [creación de un conjunto de datos mediante API](../../catalog/datasets/create.md). Al planificar qué datos enviar al conjunto de datos habilitado para [!DNL Profile], tenga en cuenta las siguientes optimizaciones:

- Incluya los datos que desee utilizar como criterios de segmentos de audiencia.
- Incluya tantos identificadores como pueda comprobar a partir de los datos de perfil para maximizar el gráfico de identidad. Esto permite [!DNL Identity Service] unir identidades entre conjuntos de datos de manera más efectiva.

## Confirmar la ingesta de datos por [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado según lo esperado. Mediante la API de acceso [!DNL Real-time Customer Profile], puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades que espera, es posible que el conjunto de datos no esté habilitado para [!DNL Real-time Customer Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato y los identificadores de los datos de origen admiten sus expectativas. Para obtener instrucciones detalladas sobre cómo utilizar la API [!DNL Real-time Customer Profile] para acceder a los datos [!DNL Profile], siga la [guía de extremo de entidades](../api/entities.md), también conocida como la API &quot;[!DNL Profile Access]&quot;.

## Confirmar la ingesta de datos por servicio de identidad {#confirm-data-ingest-by-identity-service}

Cada fragmento de datos ingerido que contiene más de una identidad crea un vínculo en el gráfico de identidad privada. Para obtener más información sobre los gráficos de identidad y los datos de identidad de acceso, lea la [información general del servicio de identidad](../../identity-service/home.md).