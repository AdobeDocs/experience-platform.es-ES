---
title: Introducción a las fuentes de autoservicio (Streaming SDK)
description: Este documento proporciona una introducción a la información sobre los requisitos previos que debe conocer antes de intentar crear una nueva fuente mediante fuentes de autoservicio (SDK de streaming).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 12%

---

# Introducción a las fuentes de autoservicio (Streaming SDK)

>[!NOTE]
>
>El SDK de flujo de fuentes de autoservicio está en versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Las fuentes de autoservicio (SDK de streaming) le permiten integrar su propia fuente para llevar los datos de streaming a Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en Experience Platform:

### Integración

* [Cree una nueva especificación de conexión para el SDK de transmisión por secuencias](create.md).
* [Actualice la especificación de flujo de flujo de flujo de flujo con su nuevo identificador de especificación de conexión](update-flow-specs.md).
* [Prueba y envía tu fuente de streaming](submit.md).

### Documentación

* Para empezar a documentar el origen, lea la [descripción general sobre la creación de documentación para orígenes de autoservicio](../documentation/doc-overview.md).
* Lea la guía de [uso de la interfaz web de GitHub](../documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub.
* Lea la guía de [uso de un editor de texto](../documentation/text-editor.md) para ver los pasos sobre cómo crear documentación con su equipo local.
* [Use la plantilla de documentación de la API del SDK de transmisión para documentar el origen en la API](streaming-template-api.md).
* [Use la plantilla de documentación de la IU del SDK de transmisión para documentar el origen en la IU](streaming-template-ui.md).

También puede descargar las plantillas de documentación a continuación:

* [Plantilla de documentación de API](../assets/streaming/streaming-template-api.zip)
* [Plantilla de documentación de IU](../assets/streaming/streaming-template-ui.zip)

## Requisitos previos

>[!IMPORTANT]
>
>El origen que integra con Experience Platform debe poder admitir un webhook al que se pueda suscribir un extremo para enviar actualizaciones.

Para utilizar fuentes de autoservicio (SDK de streaming), debe asegurarse de tener acceso a una organización de zona protegida aprovisionada con fuentes de Adobe Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Lectura de llamadas de API de muestra

La documentación de fuentes de autoservicio (Streaming SDK) y la API [!DNL Flow Service] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en Platform, consulte la [documentación sobre las zonas protegidas](../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes

Para empezar a crear una nueva fuente con orígenes de autoservicio (SDK de streaming), consulta el tutorial de [creación de una nueva fuente](./create.md).
