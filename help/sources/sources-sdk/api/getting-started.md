---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Introducción a las fuentes de autoservicio (SDK por lotes)
description: Este documento proporciona una introducción a la información sobre requisitos previos que necesita conocer antes de intentar crear una nueva fuente mediante fuentes de autoservicio (SDK por lotes).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Introducción a las fuentes de autoservicio (SDK por lotes)

El SDK por lotes de fuentes de autoservicio le permite integrar su propia fuente basada en REST para llevar los datos por lotes a Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Requisitos previos

Para utilizar fuentes de autoservicio (SDK por lotes), debe asegurarse de tener acceso a una zona protegida de la organización aprovisionada con fuentes de Adobe Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Leer llamadas de API de muestra

Fuentes de autoservicio (SDK por lotes) y [!DNL Flow Service] La documentación de la API proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilar valores para los encabezados obligatorios

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de Platform, incluidos los que pertenecen a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de Platform, consulte la [documentación de zona protegida](../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes

Para empezar a crear una nueva fuente con fuentes de autoservicio (SDK por lotes), consulte el tutorial sobre [creación de una nueva fuente](./create.md).
