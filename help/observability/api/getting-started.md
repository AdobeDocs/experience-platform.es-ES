---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
solution: Experience Platform
title: Introducción a la API de Observability Insights
description: La API de Observability Insights le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---

# Introducción a la API [!DNL Observability Insights]

La API [!DNL Observability Insights] le permite recuperar datos de métricas para diversas funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API [!DNL Observability Insights].

## Lectura de llamadas de API de muestra

La documentación de la API [!DNL Observability Insights] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre cómo leer las llamadas de API de ejemplo en la [guía de solución de problemas de Experience Platform](../../landing/troubleshooting.md).

## Encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Pasos siguientes

Para empezar a realizar llamadas usando la API [!DNL Observability Insights], continúe con la [guía de extremo de métricas](./metrics.md).
