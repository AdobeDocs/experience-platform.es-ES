---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Introducción a la API de perspectivas de observación
topic: developer guide
description: La API de perspectivas de observación le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos básicos que debe conocer antes de intentar realizar llamadas a la API de perspectivas de la capacidad de observación.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

La [!DNL Observability Insights] API le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la [!DNL Observability Insights] API.

## Leer llamadas de API de muestra

La documentación de la [!DNL Observability Insights] API proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de muestra, consulte la sección sobre cómo leer llamadas de API de ejemplo en la guía de solución de problemas del [Experience Platform](../../landing/troubleshooting.md).

## Encabezados requeridos

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación. Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

* `x-sandbox-name: {SANDBOX_NAME}`

## Pasos siguientes

Para empezar a realizar llamadas mediante la [!DNL Observability Insights] API, vaya a la guía [de extremo de](./metrics.md)métricas.