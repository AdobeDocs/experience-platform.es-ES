---
keywords: Experience Platform;inicio;temas populares;DULE;programar
solution: Experience Platform
title: Introducción a la API de servicio de directivas
topic: developer guide
description: La API de servicio de directivas le permite crear y administrar varios recursos relacionados con la administración de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de servicio de directivas.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Introducción a la API [!DNL Policy Service]

La API [!DNL Policy Service] le permite crear y administrar varios recursos relacionados con Adobe Experience Platform [!DNL Data Governance]. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API [!DNL Policy Service].

## Requisitos previos

El uso de la guía para desarrolladores requiere un conocimiento práctico de los diversos [!DNL Experience Platform] servicios que se involucran en el trabajo con las capacidades de administración de datos. Antes de comenzar a trabajar con [!DNL Policy Service API], consulte la documentación de los siguientes servicios:

* [[!DNL Data Governance]](../home.md):: Marco mediante el cual se  [!DNL Experience Platform] aplica el cumplimiento de la normativa de uso de datos.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Leer llamadas de API de muestra

La documentación de la API [!DNL Policy Service] proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas a [!DNL Platform] extremos de forma satisfactoria. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Data Governance], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Recursos principales vs. personalizados

Dentro de la API [!DNL Policy Service], todas las políticas y acciones de mercadotecnia se denominan `core` o `custom` recursos.

`core` los recursos son los definidos y mantenidos por Adobe, mientras que  `custom` los recursos son los creados y mantenidos por su organización, y por lo tanto son únicos y visibles únicamente para su organización de IMS. Por lo tanto, las operaciones de listado y búsqueda (`GET`) son las únicas operaciones permitidas en `core` recursos, mientras que las operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH` y `DELETE`) están disponibles para `custom` recursos.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de servicio de directivas, seleccione una de las guías de extremo disponibles.