---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;guía de api;servicio de consultas;cuentas de servicio de consultas;cuentas;
solution: Experience Platform
title: Extremo de API de cuentas
description: Puede crear una cuenta de servicio de consultas para persistentes
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---

# Extremo de cuentas

En Adobe Experience Platform Query Service, las cuentas se utilizan para crear credenciales que no caducan y las puede utilizar con clientes SQL externos. Puede usar el complemento `/accounts` en la API del servicio de consultas, lo que le permite crear, recuperar, editar y eliminar mediante programación sus cuentas de integración del servicio de consultas (también conocidas como cuentas técnicas).

## Introducción

Los extremos utilizados en esta guía forman parte de la API del servicio de consultas. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API de, incluidos los encabezados obligatorios y cómo leer llamadas de API de ejemplo.

## Crear una cuenta

Puede crear una cuenta de integración de Query Service realizando una solicitud de POST a `/accounts` punto final.

**Formato de API**

```http
POST /accounts
```

**Solicitud**

La siguiente solicitud creará una nueva cuenta de integración del servicio de consultas para su organización.

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
| `accountName` | **Requerido** Nombre de la cuenta de integración del servicio de consultas. |
| `assignedToUser` | **Requerido** La Adobe ID para la que se creará la cuenta de integración del servicio de consultas. |
| `credential` | *(Opcional)* La credencial utilizada para la integración del servicio de consultas. Si no se especifica, el sistema generará automáticamente una credencial. |
| `description` | *(Opcional)* Descripción de la cuenta de integración del servicio de consultas. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200, con detalles de la cuenta de integración del servicio de consultas recién creada. Puede utilizar estos detalles de la cuenta para conectar el servicio de consulta con clientes externos.

```json
{
    "technicalAccountName": "2428A037-D963-47C2-A14D-CD816EFB0AA3@TECHACCT.ADOBE.COM",
    "technicalAccountId": "E09A0DFB5FDB25D90A494012",
    "credential": "samplecredential"
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `technicalAccountName` | El nombre de su cuenta de integración del servicio de consultas. |
| `technicalAccountId` | El ID de su cuenta de integración del servicio de consultas. Esto, junto con la `credential`, redacta la contraseña de la cuenta. |
| `credential` | Las credenciales de su cuenta de integración del servicio de consultas. Esto, junto con la `technicalAccountId`, redacta la contraseña de la cuenta. |

## Actualizar una cuenta

Puede actualizar su cuenta de integración de Query Service realizando una solicitud de PUT a `/accounts` punto final.

**Formato de API**

```http
POST /accounts/{ACCOUNT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ACCOUNT_ID}` | El ID de la cuenta de integración del servicio de consultas que desea actualizar. |

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
| `accountName` | *(Opcional)* Nombre actualizado de la cuenta de integración del servicio de consultas. |
| `assignedToUser` | *(Opcional)* Adobe ID actualizado al que está vinculada la cuenta de integración de Query Service. |
| `credential` | *(Opcional)* Credencial actualizada para su cuenta del servicio de consultas. |
| `description` | *(Opcional)* Descripción actualizada de la cuenta de integración del servicio de consultas. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la cuenta de integración del servicio de consultas recién actualizada.

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

Puede recuperar una lista de todas las cuentas de integración de Query Service realizando una solicitud de GET a `/accounts` punto final.

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

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todas las cuentas de integración del servicio de consultas.

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

## Eliminación de una cuenta

Puede eliminar su cuenta de integración de Query Service realizando una solicitud de DELETE a `/accounts` punto final.

**Formato de API**

```http
DELETE /accounts/{ACCOUNT_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{ACCOUNT_ID}` | El ID de la cuenta de integración del servicio de consultas que desea eliminar. |

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
