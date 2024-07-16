---
keywords: Experience Platform;inicio;temas populares;preparación de datos;guía de api;datos de ejemplo;
solution: Experience Platform
title: Punto final de API de datos de ejemplo
description: Puede utilizar el extremo /samples en la API de Adobe Experience Platform para recuperar, crear, actualizar y validar mediante programación los datos de ejemplo de asignación.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 6%

---


# Extremo de datos de muestra

Se pueden utilizar datos de muestra al crear un esquema para el conjunto de asignaciones. Puede usar el extremo `/samples` en la API de preparación de datos para recuperar, crear y actualizar datos de ejemplo mediante programación.

## Enumerar datos de muestra

Puede recuperar una lista de todos los datos de ejemplo de asignación para su organización realizando una solicitud de GET al extremo `/samples`.

**Formato de API**

El extremo `/samples` admite varios parámetros de consulta para filtrar los resultados. Actualmente, debe incluir los parámetros `start` y `limit` como parte de la solicitud.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{LIMIT}` | **Requerido**. Especifica el número de datos de ejemplo de asignación devueltos. |
| `{START}` | **Requerido**. Especifica el desplazamiento de las páginas de resultados. Para obtener la primera página de resultados, establezca el valor en `start=0`. |

**Solicitud**

La siguiente solicitud recuperará los dos últimos datos de ejemplo de asignación dentro de su organización.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre los dos últimos objetos de asignación de datos de ejemplo.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sampleData` | |
| `sampleType` | |

## Crear datos de ejemplo

Puede crear datos de ejemplo realizando una solicitud de POST al extremo `/samples`.

```http
POST /samples
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre los datos de ejemplo recién creados.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Creación de datos de ejemplo cargando un archivo

Puede crear datos de ejemplo utilizando un archivo realizando una solicitud de POST al extremo `/samples/upload`.

**Formato de API**

```http
POST /samples/upload
```

**Solicitud**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre los datos de ejemplo recién creados.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Buscar un objeto de datos de ejemplo específico

Puede buscar un objeto específico de datos de ejemplo proporcionando su ID en la ruta de una solicitud de GET al extremo `/samples`.

**Formato de API**

```http
GET /samples/{SAMPLE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SAMPLE_ID}` | El ID del objeto de datos de ejemplo que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información del objeto de datos de ejemplo que desea recuperar.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Actualizar datos de ejemplo

Puede actualizar un objeto de datos de ejemplo específico proporcionando su ID en la ruta de una solicitud del PUT al extremo `/samples`.

**Formato de API**

```http
PUT /samples/{SAMPLE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SAMPLE_ID}` | El ID del objeto de datos de ejemplo que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los datos de ejemplo especificados. En concreto, actualiza el apellido de &quot;Smith&quot; a &quot;Lee&quot;.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre los datos de ejemplo actualizados.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
