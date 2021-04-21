---
keywords: Experience Platform;inicio;temas populares;DULE;programación
solution: Experience Platform
title: Introducción a la API del servicio de directivas
topic-legacy: developer guide
description: La API del servicio de directivas le permite crear y administrar varios recursos relacionados con el control de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API del servicio de directivas.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Introducción a la API [!DNL Policy Service]

La API [!DNL Policy Service] le permite crear y administrar varios recursos relacionados con Adobe Experience Platform [!DNL Data Governance]. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API [!DNL Policy Service].

## Requisitos previos

El uso de la guía para desarrolladores requiere comprender bien los distintos servicios [!DNL Experience Platform] que intervienen en el trabajo con las funcionalidades de control de datos. Antes de comenzar a trabajar con [!DNL Policy Service API], revise la documentación de los siguientes servicios:

* [[!DNL Data Governance]](../home.md): El marco mediante el cual se  [!DNL Experience Platform] aplica el cumplimiento de las normas de uso de datos.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores para pruebas](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Leer llamadas de API de ejemplo

La documentación de la API [!DNL Policy Service] proporciona ejemplos de llamadas de API para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] llamadas a la API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Data Governance], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Recursos principales vs. recursos personalizados

Dentro de la API [!DNL Policy Service], todas las políticas y acciones de marketing se denominan `core` o `custom` recursos.

`core` los recursos son los definidos y mantenidos por el Adobe, mientras que los  `custom` recursos son los creados y mantenidos por su organización y, por lo tanto, son únicos y visibles únicamente para su organización de IMS. De este modo, las operaciones de listado y búsqueda (`GET`) son las únicas operaciones permitidas en los recursos `core`, mientras que las operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH` y `DELETE`) están disponibles para los recursos `custom`.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de directivas, seleccione una de las guías de punto final disponibles.
