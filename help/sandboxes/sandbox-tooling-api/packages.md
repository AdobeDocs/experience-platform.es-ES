---
title: Punto final de API de paquetes de herramientas de zona protegida
description: El extremo /packages en la API de herramientas de espacio aislado le permite administrar paquetes mediante programación en Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 8ff9c50b4999a49413f8c45274815225ba58361c
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 7%

---

# Extremo de paquetes

Las herramientas de espacio aislado permiten seleccionar diferentes artefactos (también conocidos como objetos) y exportarlos a un paquete. Un paquete puede constar de un solo artefacto o de varios artefactos (como conjuntos de datos o esquemas). Cualquier artefacto que se incluya en un paquete debe ser de la misma zona protegida.

El `/packages` El extremo de la API de herramientas de entorno limitado le permite administrar paquetes de forma programada en su organización, incluida la publicación de un paquete y la importación de un paquete en un entorno limitado.

## Creación de un paquete {#create}

Puede crear un paquete de varios artefactos realizando una solicitud de POST a `/packages` proporciona valores para el nombre y el tipo de paquete del paquete.

**Formato de API**

```http
POST /packages/
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `name` | El nombre del paquete. | Cadena | Sí |
| `description` | Una descripción para proporcionar más información sobre el paquete. | Cadena | No |
| `packageType` | El tipo de paquete es **PARCIAL** para indicar que está incluyendo artefactos específicos en un paquete. | Cadena | SÍ |
| `sourceSandbox` | La zona protegida de origen del paquete. | Cadena | No |
| `expiry` | La marca de tiempo que define la fecha de caducidad del paquete. El valor predeterminado es de 90 días a partir de la fecha de creación. El campo de caducidad de la respuesta será la hora UTC epoch. | Cadena (formato de marca de hora UTC) | No |
| `artifacts` | Una lista de artefactos que se exportarán en el paquete. El `artifacts` el valor debe ser **null** o **vaciar**, cuando la variable `packageType` es `FULL`. | Matriz | No |

**Respuesta**

Una respuesta correcta devuelve el paquete recién creado. La respuesta incluye el ID de paquete correspondiente, así como información sobre su estado, caducidad y lista de artefactos.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Actualización de un paquete {#update}

Puede actualizar un paquete realizando una solicitud de PUT a `/packages` punto final.

### Adición de artefactos a un paquete {#add-artifacts}

Para añadir artefactos a un paquete, debe proporcionar un `id` e incluyen **AÑADIR** para el `action`.

**Formato de API**

```http
PUT /packages/
```

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `id` | El ID del paquete que se va a actualizar. | Cadena | Sí |
| `action` | Para añadir artefactos al paquete, el valor de acción debe ser **AÑADIR**. Esta acción solo es compatible para **PARCIAL** tipos de paquetes. | Cadena | Sí |
| `artifacts` | Una lista de artefactos que se añadirán en el paquete. No habrá cambios en el paquete si la lista es **null** o **vaciar**. Los artefactos se deduplican antes de agregarse al paquete. | Matriz | No |
| `expiry` | La marca de tiempo que define la fecha de caducidad del paquete. El valor predeterminado es de 90 días desde la hora en que se llama a la API del PUT si no se especifica la caducidad en la carga útil. El campo de caducidad de la respuesta será la hora UTC epoch. | Cadena (formato de marca de hora UTC) | No |

**Respuesta**

Una respuesta correcta devuelve el paquete actualizado. La respuesta incluye el ID de paquete correspondiente, así como información sobre su estado, caducidad y lista de artefactos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Eliminación de artefactos de un paquete {#delete-artifacts}

Para eliminar artefactos de un paquete, debe proporcionar un `id` e incluyen **DELETE** para el `action`.


**Formato de API**

```http
PUT /packages/
```

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `id` | El ID del paquete que se va a actualizar. | Cadena | Sí |
| `action` | Para eliminar artefactos de un paquete, el valor de la acción debe ser **DELETE**. Esta acción solo es compatible para **PARCIAL** tipos de paquetes. | Cadena | Sí |
| `artifacts` | Una lista de artefactos que se eliminarán del paquete. No habrá cambios en el paquete si la lista es **null** o **vaciar**. | Matriz | No |

**Respuesta**

Una respuesta correcta devuelve el paquete actualizado. La respuesta incluye el ID de paquete correspondiente, así como información sobre su estado, caducidad y lista de artefactos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Actualización de campos de metadatos en un paquete {#update-metadata}

>[!NOTE]
>
>El **ACTUALIZACIÓN** se utiliza para actualizar los campos de metadatos del paquete y **no puede** se puede utilizar para añadir o eliminar artefactos a un paquete.

Para actualizar los campos de metadatos en un paquete, debe proporcionar un `id` e incluyen **ACTUALIZACIÓN** para el `action`.

**Formato de API**

```http
PUT /packages/
```

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `id` | El ID del paquete que se va a actualizar. | Cadena | Sí |
| `action` | Para actualizar los campos de metadatos en un paquete, el valor de la acción debe ser **ACTUALIZACIÓN**. Esta acción solo es compatible para **PARCIAL** tipos de paquetes. | Cadena | Sí |
| `name` | El nombre actualizado del paquete. No se permiten nombres de paquetes duplicados. | Matriz | Sí |
| `sourceSandbox` | La zona protegida de origen debe pertenecer a la misma organización que se especifica en el encabezado de la solicitud. | Cadena | Sí |

**Respuesta**

Una respuesta correcta devuelve el paquete actualizado. La respuesta incluye el ID de paquete correspondiente, así como información sobre su descripción, estado, caducidad y lista de artefactos.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Eliminación de un paquete {#delete}

Para eliminar un paquete, realice una solicitud de DELETE al `/packages` y especifique el ID del paquete que desea eliminar.

**Formato de API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina el paquete con el ID de {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve un motivo que muestra el ID del paquete eliminado.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publicación de un paquete {#publish}

Para habilitar la importación de un paquete en una zona protegida, debe publicarlo. Realice una solicitud de GET a `/packages` punto final al especificar el ID del paquete que desea publicar.

**Formato de API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete que desea publicar. |

**Solicitud**

La siguiente solicitud publica el paquete con el ID de {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `expiryPeriod` | Este período de tiempo especificado por el usuario define la fecha de caducidad del paquete (en días) desde el momento en que se publicó. Este valor no debe ser negativo.<br> Si no se especifica ningún valor, el valor predeterminado se calculará en 90 (días) desde la fecha de publicación. | Número entero | No |

**Respuesta**

Una respuesta correcta devuelve el paquete publicado.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Búsqueda de un paquete {#look-up-package}

Puede buscar un paquete individual realizando una solicitud de GET al `/packages` punto final que incluye el ID correspondiente del paquete en la ruta de solicitud.

**Formato de API**

```http
GET /packages/{PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete que desea buscar. |

**Solicitud**

La siguiente solicitud recupera información para {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve detalles para el ID del paquete consultado. La respuesta incluye el nombre, la descripción, la fecha de publicación y la fecha de caducidad, la zona protegida de origen del paquete, así como una lista de artefactos.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Enumeración de paquetes {#list-packages}

Puede enumerar todos los paquetes de su organización realizando una solicitud de GET a `/packages` punto final.

**Formato de API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| {QUERY_PARAMS} | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la sección sobre [parámetros de consulta](./appendix.md) para obtener más información. |

**Solicitud**

La siguiente solicitud recupera información de los paquetes en función de {QUERY_PARAMS}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de paquetes que pertenecen a su organización, incluidos detalles como nombre, estado, caducidad y lista de artefactos.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Importar un paquete {#import}

Este extremo se utiliza para recuperar los objetos en conflicto de la zona protegida de destino especificada. Los objetos en conflicto representan objetos similares que ya están presentes en la zona protegida de destino.

**Formato de API**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete que desea buscar. |

**Solicitud**

La siguiente solicitud importa el {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Se devuelven conflictos en la respuesta. La respuesta muestra el paquete original más el `alternatives` fragmento como una matriz ordenada por clasificación.

Ver respuesta+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Envío de una importación {#submit-import}

>[!NOTE]
>
>Es inherente a la resolución de conflictos que el artefacto alternativo ya existe en la zona protegida de destino.

Puede enviar una importación para un paquete una vez que haya revisado los conflictos y proporcionado las sustituciones realizando una solicitud de POST a `/packages` punto final. El resultado se proporciona como carga útil, que inicia el trabajo de importación para la zona protegida de destino según se especifica en la carga útil.

La carga útil también acepta el nombre y la descripción del trabajo especificados por el usuario para el trabajo de importación. Si el nombre y la descripción especificados por el usuario no están disponibles, se utilizan el nombre y la descripción del paquete para el nombre y la descripción del trabajo.

**Formato de API**

```http
POST /packages/import
```

**Solicitud**

La siguiente solicitud recupera los paquetes que se van a importar. La carga útil es un mapa de sustituciones donde, si existe una entrada, la clave es `artifactId` proporcionado por el paquete y la alternativa es el valor. Si el mapa o la carga útil es **vaciar**, no se realizan sustituciones.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` representa la asignación de artefactos de zona protegida de origen a los artefactos de zona protegida de destino existentes. Como ya están allí, el trabajo de importación evita la creación de estos artefactos en la zona protegida de destino. | Cadena | No |

**Respuesta**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## Mostrar todos los objetos dependientes {#dependent-objects}

Enumerar todos los objetos dependientes para los objetos exportados en un paquete realizando una solicitud de POST a `/packages` al especificar el ID del paquete.

**Formato de API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete. |

**Solicitud**

La siguiente solicitud enumera todos los objetos dependientes de {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Respuesta**

Una respuesta correcta devuelve una lista de elementos secundarios para los objetos.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Compruebe los permisos basados en funciones para importar todos los artefactos del paquete {#role-based-permissions}

Puede comprobar si tiene permisos para importar artefactos de paquetes realizando una solicitud de GET a `/packages` al especificar el ID del paquete y el nombre de la zona protegida de destino.

**Formato de API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parámetro | Descripción |
| --- | --- |
| {PACKAGE_ID} | El ID del paquete que desea importar. |

**Solicitud**

La siguiente solicitud comprueba los permisos de para {PACKAGE_ID} y zona protegida.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve permisos de recurso para la zona protegida de destino, incluida una lista de permisos necesarios, permisos que faltan, tipo de artefacto y una decisión sobre si la creación está permitida.

Ver respuesta+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Enumerar trabajos de exportación/importación {#list-jobs}

Puede enumerar los trabajos de exportación e importación actuales realizando una solicitud de GET a `/packages` punto final.

**Formato de API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| {QUERY_PARAMS} | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la sección sobre [parámetros de consulta](./appendix.md) para obtener más información. |

**Solicitud**

La siguiente solicitud enumera todos los trabajos de importación correctos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve todos los trabajos de importación correctos.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
