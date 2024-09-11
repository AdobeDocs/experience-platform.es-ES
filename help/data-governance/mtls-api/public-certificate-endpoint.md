---
title: Extremo de certificado público
description: Obtenga información sobre cómo recuperar los certificados públicos mediante el extremo /public-certificate de la API del servicio MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Extremo de certificado público

En esta guía se explica cómo utilizar el extremo de certificados públicos para recuperar de forma segura certificados públicos para las aplicaciones de Adobe de su organización. Incluye una llamada de API de ejemplo e instrucciones detalladas para ayudar a los desarrolladores a autenticarse y verificar los intercambios de datos.

## Introducción

Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Rutas de API {#paths}

La siguiente información son las rutas de API esenciales que necesitará para utilizar la API del servicio mTLS. Estas incluyen la dirección URL de la puerta de enlace de la plataforma, la ruta base para la API y un ejemplo de una ruta completa para recuperar un certificado público.

- URL de puerta de enlace de PLATFORM: `https://platform.adobe.io/`
- Ruta de acceso base para esta API: `/data/core/mtls`
- Ejemplo de ruta de acceso completa: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recuperación de certificados públicos {#list}

Puede recuperar los certificados públicos de cualquiera de las aplicaciones de Adobe de su organización realizando una solicitud de GET al extremo `/v1/certificate/public-certificate`.

**Formato de API**

```http
GET /v1/certificate/public-certificate
```

Los siguientes parámetros de consulta opcionales se pueden utilizar al recuperar los certificados públicos.

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `page` | Especifica desde qué página comenzarán los resultados de la solicitud. | `page=5` |
| `limit` | Número máximo de certificados públicos que desea recuperar por página. | `limit=20` |

{style="table-layout:auto"}

**Solicitud**

En la sección contraíble siguiente se muestra una solicitud de ejemplo para devolver los certificados públicos asociados a su organización.

+++Solicitud de ejemplo

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 y enumera los certificados públicos de su organización.

+++Una respuesta correcta de muestra

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Propiedad | Descripción |
| --- | --- |
| `certCommonName` | El nombre común (CN) del certificado, que suele representar el nombre o la identidad del servidor o entidad al que se emite el certificado. |
| `publicCertificate` | El certificado público real en formato de cadena, que se utiliza para autenticar y cifrar comunicaciones. |
| `expiryDate` | La fecha y hora en que caducará el certificado público, con formato ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Pasos siguientes

Después de leer esta guía, ahora sabe cómo recuperar los certificados públicos mediante la API de Adobe Experience Platform. Para obtener más información acerca de la administración de datos de clientes con el fin de garantizar el cumplimiento de las regulaciones y las políticas organizativas, consulte la [Información general sobre la administración de datos](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
