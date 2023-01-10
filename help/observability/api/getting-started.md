---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
solution: Experience Platform
title: Introducción a la API de Observability Insights
description: La API de Observability Insights permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Introducción a [!DNL Observability Insights] API

La variable [!DNL Observability Insights] La API le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas al [!DNL Observability Insights] API.

## Leer llamadas de API de ejemplo

La variable [!DNL Observability Insights] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre cómo leer llamadas de API de ejemplo en la sección [Guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

## Encabezados requeridos

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Observability Insights] API, vaya a [guía de extremo de métricas](./metrics.md).
