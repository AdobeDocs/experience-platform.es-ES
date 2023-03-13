---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
solution: Experience Platform
title: Introducción a la API de Observability Insights
description: La API de Observability Insights le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Introducción a la [!DNL Observability Insights] API

El [!DNL Observability Insights] La API de le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a [!DNL Observability Insights] API.

## Leer llamadas de API de muestra

El [!DNL Observability Insights] La documentación de la API proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre cómo leer llamadas de API de ejemplo en la [guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

## Encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Pasos siguientes

Para empezar a realizar llamadas utilizando [!DNL Observability Insights] API, continúe con la [guía de extremo de métricas](./metrics.md).
