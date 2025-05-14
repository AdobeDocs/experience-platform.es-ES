---
title: Extremo de certificado público
description: Obtenga información sobre cómo recuperar los certificados públicos mediante el extremo /public-certificate de la API del servicio MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# Extremo de certificado público

>[!NOTE]
>
>Adobe ya no admite la descarga estática de certificados mTLS públicos. Utilice esta API para recuperar certificados válidos para sus integraciones. Ahora se requiere la recuperación automatizada para evitar interrupciones en el servicio.

En esta guía se explica cómo utilizar el extremo de certificados públicos para recuperar de forma segura certificados públicos para las aplicaciones de Adobe de su organización. Incluye una llamada de API de ejemplo e instrucciones detalladas para ayudar a los desarrolladores a autenticarse y verificar los intercambios de datos.

## Introducción

Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener detalles importantes acerca de los encabezados requeridos y cómo interpretar las llamadas de API de ejemplo.

## Rutas de API {#paths}

La siguiente información son las rutas de API esenciales que necesitará para utilizar la API del servicio mTLS. Estas incluyen la dirección URL de la puerta de enlace de la plataforma, la ruta base para la API y un ejemplo de una ruta completa para recuperar un certificado público.

- URL de puerta de enlace de PLATFORM: `https://platform.adobe.io/`
- Ruta de acceso base para esta API: `/data/core/mtls`
- Ejemplo de ruta de acceso completa: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recuperación de certificados públicos {#list}

Realice una petición GET al extremo `/v1/certificate/public-certificate` para recuperar los certificados públicos de cualquiera de las aplicaciones Adobe de su organización.

**Formato de API**

```http
GET /v1/certificate/public-certificate
```

Los siguientes parámetros de consulta opcionales se pueden utilizar al recuperar los certificados públicos.

| Parámetros de consulta | Descripción | Ejemplo |
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

## Automatización del ciclo vital de certificados {#certificate-lifecycle-automation}

Adobe automatiza el ciclo de vida de los certificados mTLS públicos para garantizar la continuidad y reducir las interrupciones del servicio.

- Los certificados se vuelven a emitir 60 días antes del vencimiento.
- Los certificados se revocan 30 días antes de la caducidad.

>[!NOTE]
>
>Estas escalas de tiempo se acortarán con el tiempo de acuerdo con las [directrices del foro CA/B](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), cuyo objetivo es reducir la duración del certificado a un máximo de 47 días.

Debe actualizar las integraciones para que admitan la recuperación automatizada a través de la API. No confíe en las descargas manuales de certificados ni en las copias estáticas, ya que pueden dar lugar a certificados caducados o revocados.

## Pasos siguientes

Después de recuperar los certificados públicos mediante la API, actualice las integraciones para llamar regularmente a este punto de conexión antes de que los certificados caduquen. Para probar esta llamada de forma interactiva, visite la [página de referencia de la API MTLS](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Para obtener instrucciones más amplias sobre las integraciones basadas en certificados, consulte [Información general sobre el cifrado de datos en Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) o [Información general sobre el control de datos](../home.md).
