---
title: Introducción a las fuentes de autoservicio (streaming de SDK)
description: Este documento proporciona una introducción a la información sobre requisitos previos que debe conocer antes de intentar crear una nueva fuente mediante fuentes de autoservicio (Streaming SDK).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 12%

---

# Introducción a las fuentes de autoservicio (streaming de SDK)

>[!NOTE]
>
>Fuentes de autoservicio Streaming SDK está en versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Las fuentes de autoservicio (Streaming SDK) le permiten integrar su propia fuente para llevar los datos de streaming a Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en Experience Platform:

### Integración

* [Cree una nueva especificación de conexión para Streaming SDK](create.md).
* [Actualice la especificación de flujo de flujo de flujo de flujo con su nuevo identificador de especificación de conexión](update-flow-specs.md).
* [Prueba y envía tu fuente de streaming](submit.md).

### Documentación

* Para empezar a documentar el origen, lea la [descripción general sobre la creación de documentación para orígenes de autoservicio](../documentation/doc-overview.md).
* Lea la guía de [uso de la interfaz web de GitHub](../documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub.
* Lea la guía de [uso de un editor de texto](../documentation/text-editor.md) para ver los pasos sobre cómo crear documentación con su equipo local.
* [Use la plantilla de documentación de la API de Streaming SDK para documentar su origen en la API](streaming-template-api.md).
* [Use la plantilla de documentación de la IU de Streaming SDK para documentar su origen en la IU](streaming-template-ui.md).

También puede descargar las plantillas de documentación a continuación:

* [Plantilla de documentación de API](../assets/streaming/streaming-template-api.zip)
* [Plantilla de documentación de IU](../assets/streaming/streaming-template-ui.zip)

## Requisitos previos

>[!IMPORTANT]
>
>La fuente que integre con Experience Platform debe poder admitir un webhook al que se pueda suscribir un punto final para enviar actualizaciones.

Para utilizar fuentes de autoservicio (Streaming de SDK), debe asegurarse de tener acceso a una organización de zona protegida aprovisionada con fuentes de Adobe Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Lectura de llamadas de API de muestra

La documentación de la API de fuentes de autoservicio (Streaming SDK) y [!DNL Flow Service] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de Experience Platform.

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

Para empezar a crear una nueva fuente con fuentes de autoservicio (Streaming SDK), consulta el tutorial de [creación de una nueva fuente](./create.md).
