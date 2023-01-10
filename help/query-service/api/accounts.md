---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;guía de api;servicio de consulta;cuentas de servicio de consulta;cuentas;
solution: Experience Platform
title: Punto final de API de cuentas
description: Puede crear una cuenta de servicio de consulta para persistente .
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Punto de conexión de cuentas

En Adobe Experience Platform Query Service, las cuentas se utilizan para crear credenciales que no caducan y que puede utilizar con clientes SQL externos. Puede usar la variable `/accounts` en la API del servicio de consulta, que le permite crear, recuperar, editar y eliminar mediante programación sus cuentas de integración del servicio de consulta (también conocidas como cuenta técnica).

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la API del servicio de consulta. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Crear una cuenta

Puede crear una cuenta de integración del servicio de consulta realizando una solicitud de POST al `/accounts` punto final.

**Formato de API**

```http
POST /accounts
```

**Solicitud**

La siguiente solicitud creará una nueva cuenta de integración del servicio de consulta para su organización IMS.

```shell
curl -X POST https://platform.adobe.io/data/foundation/queryauth/accounts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "accountName": "sampleName",
    "assignedToUser": "sample@example.com",
    "credential": "samplecredential",
    "description": "Sample description"
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `accountName` | **Requerido** Nombre de la cuenta de integración del servicio de consulta. |
| `assignedToUser` | **Requerido** Adobe ID para el que se creará la cuenta de integración del servicio de consulta. |
| `credential` | *(Opcional)* Credenciales que se utilizan para la integración del servicio de consulta. Si no se especifica, el sistema generará automáticamente una credencial. |
| `description` | *(Opcional)* Descripción de la cuenta de integración del servicio de consulta. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200, con detalles de la cuenta de integración del servicio de consulta recién creada. Puede utilizar estos detalles de la cuenta para conectar el servicio de consulta con clientes externos.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `technicalAccountName` | El nombre de su cuenta de integración del servicio de consulta. |
| `technicalAccountId` | El ID de su cuenta de integración del servicio de consulta. Esto, junto con la variable `credential`, configura la contraseña de su cuenta. |
| `credential` | La credencial de su cuenta de integración del servicio de consulta. Esto, junto con la variable `technicalAccountId`, configura la contraseña de su cuenta. |

## Actualizar una cuenta

Puede actualizar su cuenta de integración del servicio de consulta realizando una solicitud de PUT al `/accounts` punto final.

**Formato de API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ACCOUNT_ID}` | El ID de la cuenta de integración del servicio de consulta que desea actualizar. |

**Solicitud**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
     "accountName": "Updated account name",
     "assignedToUser": "sampleuser2@adobe.com",
     "credential": "UpdatedCredential",
     "description": "Updated description"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `accountName` | *(Opcional)* El nombre actualizado de la cuenta de integración del servicio de consulta. |
| `assignedToUser` | *(Opcional)* El Adobe ID actualizado al que está vinculada la cuenta de integración del servicio de consulta. |
| `credential` | *(Opcional)* La credencial actualizada para su cuenta del servicio de consultas. |
| `description` | *(Opcional)* La descripción actualizada de la cuenta de integración del servicio de consulta. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la cuenta de integración del servicio de consulta recién actualizada.

```json
{
    "accountName": "Updated account name",
    "assignedToUser": "sampleuser2@adobe.com",
    "created": "2021-06-16T16:44:42.073Z",
    "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "credential": "UpdatedCredential",
    "description": "Updated description",
    "lastUpdated": "2021-08-03T23:47:46.588Z",
    "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012"
}
```

## Enumerar todas las cuentas

Puede recuperar una lista de todas las cuentas de integración del servicio de consulta realizando una solicitud de GET al `/accounts` punto final.

**Formato de API**

```http
GET /accounts
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/foundation/queryauth/accounts \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todas las cuentas de integración del servicio de consulta.

```json
{
    "accounts": [
        {
            "lastUpdated": "2021-06-16T18:07:49.581Z",
            "accountName": "Use for XQL testing of account creation",
            "description": "Local test",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "ADC7EB19-63B4-4B9F-A192-EBE3CD0C034E@TECHACCT.ADOBE.COM",
            "technicalAccountId": "38645A7360CA3DF30A49400F",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T18:07:49.581Z",
            "active": true
        },
        {
            "lastUpdated": "2021-06-16T16:44:42.073Z",
            "accountName": "Use for XQL testing of account creation",
            "description": " ",
            "assignedToUser": "platform-ui-automation@adobe.com",
            "technicalAccountName": "66E91FDD-4733-45E2-A312-D87580CFA55D@TECHACCT.ADOBE.COM",
            "technicalAccountId": "392202E060CA2A770A49420A",
            "lastUpdatedBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "createdBy": "3BF132EF5BC636C10A49400B@AdobeID",
            "created": "2021-06-16T16:44:42.073Z",
            "active": true
        }
    ],
    "_page": {
        "count": 2,
        "next": "2021-06-16T16:44:42.073Z",
        "orderby": "-created",
        "property": "active==true",
        "start": "2021-06-16T18:07:49.581Z"
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T16:44:42.073Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/queryauth/accounts?orderby=-created&property=active==true&start=2021-06-16T18:07:49.581Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

## Eliminar una cuenta

Puede eliminar su cuenta de integración del servicio de consulta realizando una solicitud de DELETE al `/accounts` punto final.

**Formato de API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ACCOUNT_ID}` | El ID de la cuenta de integración del servicio de consulta que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/accounts/E09A0DFB5FDB25D90A494012 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con un mensaje que indica que la cuenta se eliminó correctamente.

```json
{
    "result": "Success"
}
```
