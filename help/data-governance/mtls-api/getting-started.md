---
title: Introducción a la API del servicio MTLS
description: Este documento proporciona información adicional que necesita conocer para trabajar correctamente con la API de MTLS.
role: Developer
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 7%

---

# Introducción a la API del servicio MTLS {#getting-started}

La API del servicio MTLS le permite recuperar y comprobar de forma segura los certificados públicos emitidos por el Adobe.

Las secciones siguientes proporcionan información adicional que deberá conocer para trabajar correctamente con la API del servicio MTLS.

## Lectura de llamadas de API de muestra

La documentación de la API del servicio MTLS proporciona una llamada de API de ejemplo para demostrar cómo dar formato a las solicitudes. Esto incluye la ruta, los encabezados obligatorios y la carga útil de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para poder realizar llamadas a los extremos de Platform correctamente. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas de API de Experience Platform, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## Pasos siguientes

Para realizar llamadas mediante la API del servicio MTLS, seleccione las guías de extremos mediante la navegación izquierda o en la [descripción general de la guía para desarrolladores](./overview.md)
