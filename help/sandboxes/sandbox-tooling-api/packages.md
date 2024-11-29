---
title: Punto final de API de paquetes de herramientas de zona protegida
description: El extremo /packages en la API de herramientas de espacio aislado le permite administrar paquetes mediante programación en Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 47e4616e5465ec97512647b9280f461c6971aa42
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 10%

---

# Extremo de paquetes

Las herramientas de espacio aislado permiten seleccionar diferentes artefactos (también conocidos como objetos) y exportarlos a un paquete. Un paquete puede constar de un solo artefacto o de varios artefactos (como conjuntos de datos o esquemas). Cualquier artefacto que se incluya en un paquete debe ser de la misma zona protegida.

El extremo `/packages` de la API de herramientas de zona protegida le permite administrar paquetes mediante programación en su organización, incluida la publicación de un paquete y la importación de un paquete en una zona protegida.

## Creación de un paquete {#create}

Puede crear un paquete de varios artefactos realizando una solicitud de POST al extremo `/packages` y proporcionando al mismo tiempo valores para el nombre y el tipo de paquete del paquete.

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
| `packageType` | El tipo de paquete es **PARTIAL** para indicar que se están incluyendo artefactos específicos en un paquete. | Cadena | SÍ |
| `sourceSandbox` | La zona protegida de origen del paquete. | Objeto | No |
| `expiry` | La marca de tiempo que define la fecha de caducidad del paquete. El valor predeterminado es de 90 días a partir de la fecha de creación. El campo de caducidad de la respuesta será la hora UTC epoch. | Cadena (formato de marca de hora UTC) | No |
| `artifacts` | Una lista de artefactos que se exportarán en el paquete. El valor `artifacts` debe ser **null** o **empty**, cuando `packageType` es `FULL`. | Matriz | No |

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

Puede actualizar un paquete realizando una solicitud de PUT al extremo `/packages`.

### Adición de artefactos a un paquete {#add-artifacts}

Para agregar artefactos a un paquete, debe proporcionar un `id` e incluir **ADD** para `action`.

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
| `action` | Para agregar artefactos al paquete, el valor de la acción debe ser **ADD**. Esta acción solo es compatible con los tipos de paquete **PARTIAL**. | Cadena | Sí |
| `artifacts` | Una lista de artefactos que se añadirán en el paquete. No habrá cambios en el paquete si la lista es **null** o **empty**. Los artefactos se deduplican antes de agregarse al paquete. Consulte la tabla siguiente para obtener una lista completa de los artefactos admitidos. | Matriz | No |
| `expiry` | La marca de tiempo que define la fecha de caducidad del paquete. El valor predeterminado es de 90 días desde la hora en que se llama a la API del PUT si no se especifica la caducidad en la carga útil. El campo de caducidad de la respuesta será la hora UTC epoch. | Cadena (formato de marca de hora UTC) | No |

Actualmente se admiten los siguientes tipos de artefactos.

|  Artefacto | Plataforma | Objeto | Flujo parcial | Espacio aislado completo |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Recorridos | Sí | No |
| `ID_NAMESPACE` | Plataforma de datos del cliente | Identidades | Sí | Sí |
| `REGISTRY_DATATYPE` | Plataforma de datos del cliente | Tipo de datos | Sí | Sí |
| `REGISTRY_CLASS` | Plataforma de datos del cliente | Clase | Sí | Sí |
| `REGISTRY_MIXIN` | Plataforma de datos del cliente | Grupo de campo | Sí | Sí |
| `REGISTRY_SCHEMA` | Plataforma de datos del cliente | Esquemas | Sí | Sí |
| `CATALOG_DATASET` | Plataforma de datos del cliente | Conjuntos de datos | Sí | Sí |
| `DULE_CONSENT_POLICY` | Plataforma de datos del cliente | Políticas de consentimiento y gobernanza | Sí | Sí |
| `PROFILE_SEGMENT` | Plataforma de datos del cliente | Públicos | Sí | Sí |
| `FLOW` | Plataforma de datos del cliente | Flujo de datos de fuentes | Sí | Sí |

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

Para eliminar artefactos de un paquete, debe proporcionar un `id` e incluir **DELETE** para `action`.

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
| `action` | Para eliminar artefactos de un paquete, el valor de la acción debe ser **DELETE**. Esta acción solo es compatible con los tipos de paquete **PARTIAL**. | Cadena | Sí |
| `artifacts` | Una lista de artefactos que se eliminarán del paquete. No habrá cambios en el paquete si la lista es **null** o **empty**. | Matriz | No |

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
>La acción **UPDATE** se usa para actualizar los campos de metadatos del paquete y **no se puede** usar para agregar o eliminar artefactos a un paquete.

Para actualizar los campos de metadatos de un paquete, debe proporcionar un `id` e incluir **UPDATE** para el `action`.

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
| `action` | Para actualizar los campos de metadatos de un paquete, el valor de la acción debe ser **UPDATE**. Esta acción solo es compatible con los tipos de paquete **PARTIAL**. | Cadena | Sí |
| `name` | El nombre actualizado del paquete. No se permiten nombres de paquetes duplicados. | Matriz | Sí |
| `sourceSandbox` | La zona protegida de Source debe pertenecer a la misma organización que se especifica en el encabezado de la solicitud. | Objeto | Sí |

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

Para eliminar un paquete, realice una solicitud de DELETE al extremo `/packages` y especifique el identificador del paquete que desea eliminar.

**Formato de API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina el paquete con el identificador {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve un motivo que muestra el ID del paquete eliminado.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish un paquete {#publish}

Para habilitar la importación de un paquete en una zona protegida, debe publicarlo. Realice una solicitud de GET al extremo `/packages` mientras especifica el identificador del paquete que desea publicar.

**Formato de API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete que desea publicar. |

**Solicitud**

La siguiente solicitud publica el paquete con el identificador {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Propiedad | Descripción | Tipo | Obligatorio |
| --- | --- | --- | --- |
| `expiryPeriod` | Este período de tiempo especificado por el usuario define la fecha de caducidad del paquete (en días) desde el momento en que se publicó. Este valor no debe ser negativo.<br> Si no se especifica ningún valor, el valor predeterminado se calculará en 90 (días) desde la fecha de publicación. | Entero | No |

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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Búsqueda de un paquete {#look-up-package}

Puede buscar un paquete individual realizando una solicitud de GET al extremo `/packages` que incluya el ID correspondiente del paquete en la ruta de solicitud.

**Formato de API**

```http
GET /packages/{PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete que desea buscar. |

**Solicitud**

La siguiente solicitud recupera información para {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

Puede enumerar todos los paquetes de su organización realizando una solicitud de GET al extremo `/packages`.

**Formato de API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la sección sobre [parámetros de consulta](./appendix.md) para obtener más información. |

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
| `{PACKAGE_ID}` | El ID del paquete que desea buscar. |

**Solicitud**

La siguiente solicitud importa {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Se devuelven conflictos en la respuesta. La respuesta muestra el paquete original más el fragmento `alternatives` como una matriz ordenada por clasificación.

+++Ver respuesta

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

Puede enviar una importación para un paquete una vez que haya revisado los conflictos y proporcionado las sustituciones realizando una solicitud de POST al extremo `/packages`. El resultado se proporciona como carga útil, que inicia el trabajo de importación para la zona protegida de destino según se especifica en la carga útil.

La carga útil también acepta el nombre y la descripción del trabajo especificados por el usuario para el trabajo de importación. Si el nombre y la descripción especificados por el usuario no están disponibles, se utilizan el nombre y la descripción del paquete para el nombre y la descripción del trabajo.

**Formato de API**

```http
POST /packages/import
```

**Solicitud**

La siguiente solicitud recupera los paquetes que se van a importar. La carga útil es un mapa de sustituciones en el que, si existe una entrada, la clave es `artifactId` proporcionada por el paquete y la alternativa es el valor. Si el mapa o la carga útil están **vacíos**, no se realizarán sustituciones.

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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Mostrar todos los objetos dependientes {#dependent-objects}

Enumere todos los objetos dependientes para los objetos exportados en un paquete realizando una solicitud de POST al extremo `/packages` mientras especifica el identificador del paquete.

**Formato de API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete. |

**Solicitud**

La siguiente solicitud enumera todos los objetos dependientes de {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

Puede comprobar si tiene permisos para importar artefactos del paquete realizando una solicitud de GET al extremo `/packages` mientras especifica el ID del paquete y el nombre de la zona protegida de destino.

**Formato de API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete que desea importar. |

**Solicitud**

La siguiente solicitud comprueba sus permisos para {PACKAGE_ID} y la zona protegida.

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

+++Ver respuesta

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

Puede enumerar los trabajos de exportación e importación actuales realizando una solicitud de GET al extremo `/packages`.

**Formato de API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales por los que filtrar los resultados. Consulte la sección sobre [parámetros de consulta](./appendix.md) para obtener más información. |

**Solicitud**

La siguiente solicitud enumera todos los trabajos de importación correctos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

## Uso compartido de paquetes entre organizaciones {#org-linking}

El extremo `/handshake` de la API de herramientas de zona protegida le permite asociarse con otras organizaciones para compartir paquetes.

### Envío de una solicitud de uso compartido {#send-request}

Envíe una solicitud a una organización asociada de destino para compartir la aprobación realizando una solicitud de POST al extremo `/handshake/bulkCreate`. Esto es necesario para poder compartir paquetes privados.

**Formato de API**

```http
POST /handshake/bulkCreate
```

**Solicitud**

La siguiente solicitud inicia la aprobación del uso compartido entre una organización asociada de destino y la organización de origen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | Una lista de organizaciones de destino a las que enviar una solicitud de uso compartido. | Matriz | Sí |
| `sourceIMSDetails` | Detalles sobre la organización de origen. | Objeto | Sí |

**Respuesta**

Una respuesta correcta devuelve detalles sobre la solicitud de uso compartido.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKIND_ID}"
        }
    },
    "failedRequests": {}
}
```

### Aprobación de solicitudes de uso compartido recibidas {#approve-requests}

Apruebe solicitudes compartidas de organizaciones asociadas de destino realizando una solicitud de POST al extremo `/handshake/action`. Después de la aprobación, las organizaciones asociadas de origen pueden compartir paquetes privados.

**Formato de API**

```http
POST /handshake/action
```

**Solicitudes**

La siguiente solicitud aprueba una solicitud de uso compartido de una organización asociada de destino.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `linkingID` | El ID de la solicitud compartida a la que está respondiendo. | Cadena | Sí |
| `status` | Acción que se está realizando en la solicitud de uso compartido. Los valores aceptables son `APPROVED` o `REJECTED`. | Cadena | Sí |
| `reason` | El motivo por el que se realiza la acción. | Cadena | Sí |
| `targetIMSOrgDetails` | Detalles acerca de la organización de destino donde el valor de id debe ser **ID** de la organización de destino, el valor de name debe ser **NAME** de la organización de destino y el valor de region debe ser las organizaciones de destino **REGION**. | Objeto | Sí |

**Respuesta**

Una respuesta correcta devuelve detalles sobre la solicitud de uso compartido aprobada.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Enumerar solicitudes de recursos compartidos salientes/entrantes {#outgoing-and-incoming-requests}

Enumerar solicitudes de recursos compartidos entrantes y salientes realizando una solicitud de GET al extremo `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`.

**Formato de API**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Parámetro | Valores aceptados/predeterminados |
| --- | --- |
| `property` | Especifica la propiedad por la que filtrar, como el estado. Los valores aceptables para el estado son: `APPROVED`, `REJECTED` y `IN_PROGRESS`. |
| `start` | El valor predeterminado de inicio es `0`. |
| `limit` | El valor predeterminado de limit es `20`. |
| `orderBy` | Ordena los registros en orden ascendente o descendente. |
| `requestType` | Acepta `INCOMING` o `OUTGOING`. |

**Solicitud**

La siguiente solicitud devuelve una lista de todas las solicitudes compartidas entrantes y salientes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de las solicitudes de uso compartido salientes y entrantes y sus detalles.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Transferir paquetes

Use el extremo `/transfer` en la API de herramientas de zona protegida para recuperar y crear nuevas solicitudes de uso compartido de paquetes.

### Nueva solicitud de uso compartido {#share-request}

Recupere el paquete de una organización de origen publicada y compártalo con una organización de destino realizando una solicitud de POST al extremo `/transfer` al mismo tiempo que proporciona el ID del paquete y el ID de la organización de destino.

**Formato de API**

```http
POST /transfer
```

**Solicitud**

La siguiente solicitud recupera un paquete de organizaciones de origen y lo comparte con una organización de destino.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `packageId` | El ID del paquete que desea compartir. | Cadena | Sí |
| `targets` | Una lista de organizaciones para compartir con las que empaquetar. | Matriz | Sí |

**Respuesta**

Una respuesta correcta devuelve los detalles del paquete solicitado y su estado compartido.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### Obtener una solicitud de uso compartido por ID {#fetch-transfer-by-id}

Recupere los detalles de una solicitud de uso compartido realizando una solicitud de GET al extremo `/transfer/{TRANSFER_ID}` mientras proporciona el ID de transferencia.

**Formato de API**

```http
GET /transfer/{TRANSFER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TRANSFER_ID}` | El ID de la transferencia que desea recuperar. |

**Solicitud**

La siguiente solicitud obtiene una transferencia con el ID de {TRANSFER_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de una solicitud de uso compartido.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### Buscar lista de recursos compartidos {#transfers-list}

Busque una lista de solicitudes de transferencia realizando una solicitud de GET al extremo `/transfer/list?{QUERY_PARAMETERS}`, cambiando los parámetros de la misma según sea necesario.

**Formato de API**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Parámetro | Valores aceptados/predeterminados |
| --- | --- |
| `property` | Especifica la propiedad por la que filtrar, como el estado. Los valores aceptables para el estado son: `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`. |
| `start` | El valor predeterminado de inicio es `0`. |
| `limit` | El valor predeterminado de limit es `20`. |
| `orderBy` | El pedido solo acepta el campo `createdDate`. |

**Solicitud**

La siguiente solicitud recupera una lista de solicitudes de transferencia a partir de los parámetros de búsqueda proporcionados.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de todas las solicitudes de transferencia de los parámetros de búsqueda proporcionados.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Actualización de la disponibilidad del paquete de privado a público {#update-availability}

Cambie un paquete de privado a público realizando una solicitud de GET al extremo `/packages/update`. De forma predeterminada, se crea un paquete con disponibilidad privada.

**Formato de API**

```http
PUT `/packages/update`
```

**Solicitud**

La siguiente solicitud cambia la disponibilidad de los paquetes de privada a pública.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `id` | El ID del paquete que se va a actualizar. | Cadena | Sí |
| `action` | Para actualizar la visibilidad al público, el valor de la acción debe ser **UPDATE**. | Cadena | Sí |
| `packageVisbility` | Para actualizar la visibilidad, el valor packageVisibility debe ser **PUBLIC**. | Cadena | Sí |

**Respuesta**

Una respuesta correcta devuelve detalles sobre un paquete y su visibilidad.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Solicitud para importar un paquete público {#pull-public-package}

Importe un paquete desde una organización de origen con disponibilidad pública realizando una solicitud de POST al extremo `/transfer/pullRequest`.

**Formato de API**

```http
POST /transfer/pullRequest
```

**Solicitud**

La siguiente solicitud importará un paquete y establecerá su disponibilidad en pública.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `imsOrgId` | El ID de la organización de origen del paquete. | Cadena | Sí |
| `packageId` | El ID del paquete que se va a importar. | Cadena | Sí |

**Respuesta**

Una respuesta correcta devuelve detalles sobre el paquete público importado.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Enumeración de paquetes públicos {#list-public-packages}

Obtenga una lista de paquetes con visibilidad pública realizando una solicitud de GET al extremo `/transfer/list?{QUERY_PARAMS}`.

**Formato de API**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Parámetro | Valores aceptados/predeterminados |
| --- | --- |
| `property` | Especifica la propiedad por la que filtrar, como el estado. Los valores aceptables para el estado son: `COMPLETED` y `FAILED`. |
| `start` | El valor predeterminado de inicio es `0`. |
| `limit` | El valor predeterminado de limit es `20`. |
| `orderBy` | El pedido solo acepta el campo `createdDate`. |
| `requestType` | Acepta `PUBLIC` o `PRIVATE`. |

**Solicitud**

La siguiente solicitud recupera una lista de paquetes con disponibilidad pública.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de paquetes públicos y sus detalles.

+++Ver respuesta

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Copiar carga útil del paquete (#package-payload)

Puede copiar la carga útil de un paquete público realizando una solicitud de GET al extremo `/packages/payload` que incluya el ID correspondiente del paquete en la ruta de solicitud.

**Formato de API**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{PACKAGE_ID}` | El ID del paquete que desea copiar. |

**Solicitud**

La siguiente solicitud recupera la carga útil de un paquete con el ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| Propiedad | Descripción | Tipo | Requerido |
| --- | --- | --- | --- |
| `imsOrdId` | El ID de la organización a la que pertenece el paquete. | Cadena | Sí |
| `packageId` | El ID del paquete que carga útil que solicita. | Cadena | Sí |

**Respuesta**

Una respuesta correcta devuelve la carga útil del paquete.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```
