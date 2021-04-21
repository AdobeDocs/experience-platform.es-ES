---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
solution: Experience Platform
title: Introducción a la API de Observability Insights
topic-legacy: developer guide
description: La API de Observability Insights permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Introducción a la API [!DNL Observability Insights]

La API [!DNL Observability Insights] permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API [!DNL Observability Insights].

## Leer llamadas de API de ejemplo

La documentación de la API [!DNL Observability Insights] proporciona ejemplos de llamadas de API para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre cómo leer llamadas de API de ejemplo en la [guía de solución de problemas del Experience Platform](../../landing/troubleshooting.md).

## Encabezados requeridos

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Observability Insights], vaya a la [guía de extremo de métricas](./metrics.md).
