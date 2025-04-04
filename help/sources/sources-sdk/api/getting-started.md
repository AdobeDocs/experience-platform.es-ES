---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
solution: Experience Platform
title: Introducción a las fuentes de autoservicio (SDK por lotes)
description: Este documento proporciona una introducción a la información sobre requisitos previos que necesita conocer antes de intentar crear una nueva fuente utilizando fuentes de autoservicio (SDK por lotes).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 16%

---

# Introducción a las fuentes de autoservicio (SDK por lotes)

Las fuentes de autoservicio (SDK por lotes) le permiten integrar su propia fuente basada en REST para llevar los datos por lotes a Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Requisitos previos

Para utilizar fuentes de autoservicio (SDK por lotes), debe asegurarse de tener acceso a una zona protegida de la organización aprovisionada con fuentes de Adobe Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Lectura de llamadas de API de muestra

La documentación de la API de fuentes de autoservicio (SDK por lotes) y [!DNL Flow Service] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de Experience Platform.

## Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a las API de Experience Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de Experience Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [documentación sobre las zonas protegidas](../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes

Para empezar a crear una nueva fuente con orígenes de autoservicio (SDK por lotes), vea el tutorial de [creación de una nueva fuente](./create.md).
