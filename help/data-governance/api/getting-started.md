---
keywords: Experience Platform;inicio;temas populares;DULE;dule
solution: Experience Platform
title: Introducción a la API del servicio de directivas
description: La API del servicio de políticas le permite crear y administrar varios recursos relacionados con la administración de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API del servicio de directivas.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# Introducción a la API [!DNL Policy Service]

La API [!DNL Policy Service] le permite crear y administrar varios recursos relacionados con la administración de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API [!DNL Policy Service].

## Requisitos previos

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos servicios de [!DNL Experience Platform] implicados en el trabajo con las capacidades de control de datos. Antes de comenzar a trabajar con [!DNL Policy Service API], revise la documentación de los siguientes servicios:

* [Control de datos](../home.md): El marco por el cual [!DNL Experience Platform] aplica el cumplimiento del uso de datos.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Lectura de llamadas de API de muestra

La documentación de la API [!DNL Policy Service] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Experience Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a Control de datos, están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Recursos principales y personalizados

Dentro de la API [!DNL Policy Service], todas las políticas y acciones de marketing se denominan recursos `core` o `custom`.

`core` recursos son los definidos y mantenidos por Adobe, mientras que `custom` recursos son los creados y mantenidos por su organización y, por lo tanto, son únicos y visibles únicamente para su organización. De este modo, las operaciones de listado y búsqueda (`GET`) son las únicas permitidas en `core` recursos, mientras que las operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH` y `DELETE`) están disponibles para `custom` recursos.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de directivas, seleccione una de las guías de extremos disponibles.
