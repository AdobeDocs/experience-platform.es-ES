---
title: Introducción a las fuentes de autoservicio (SDK de transmisión)
description: Este documento proporciona una introducción a la información necesaria antes de intentar crear un nuevo origen con fuentes de autoservicio (SDK de transmisión).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Introducción a las fuentes de autoservicio (SDK de transmisión)

Las fuentes de autoservicio (SDK de transmisión) le permiten integrar su propia fuente para llevar datos de flujo continuo a Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas al [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Proceso de alto nivel

A continuación se describe el proceso paso a paso para configurar el origen en el Experience Platform:

### Integración

* [Crear una nueva especificación de conexión para el SDK de transmisión](create.md).
* [Actualice la especificación del flujo de transmisión con su nuevo ID de especificación de conexión](update-flow-specs.md).
* [Prueba y envío de la fuente de flujo continuo](submit.md).

### Documentación

* Para empezar a documentar su fuente, lea la [información general sobre la creación de documentación para fuentes de autoservicio](../documentation/doc-overview.md).
* Lea la guía de [uso de la interfaz web de GitHub](../documentation/github.md) para ver los pasos sobre cómo crear documentación con GitHub.
* Lea la guía de [uso de un editor de texto](../documentation/text-editor.md) para ver los pasos sobre cómo crear documentación utilizando el equipo local.
* [Utilice la plantilla de documentación de la API del SDK de transmisión para documentar el origen en la API](streaming-template-api.md).
* [Utilice la plantilla de documentación de la interfaz de usuario del SDK de transmisión para documentar el origen en la interfaz de usuario](streaming-template-ui.md).

También puede descargar las plantillas de documentación siguientes:

* [Plantilla de documentación de API](../assets/streaming/streaming-template-api.zip)
* [Plantilla de documentación de la interfaz de usuario](../assets/streaming/streaming-template-ui.zip)

## Requisitos previos

>[!IMPORTANT]
>
>El origen que está integrando con Experience Platform debe ser capaz de soportar un weblink al que se pueda suscribir un punto final para enviar actualizaciones.

Para utilizar fuentes de autoservicio (SDK de transmisión), debe asegurarse de tener acceso a una organización de entorno limitado aprovisionada con fuentes de Adobe Experience Platform.

Esta guía también requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Leer llamadas de API de ejemplo

Las fuentes de autoservicio (SDK de transmisión) y [!DNL Flow Service] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de Platform, incluidos los que pertenecen a [!DNL Flow Service], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en Platform, consulte la [documentación de entorno limitado](../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes

Para empezar a crear un nuevo origen con orígenes de autoservicio (SDK de transmisión), consulte el tutorial sobre [crear un nuevo origen](./create.md).
