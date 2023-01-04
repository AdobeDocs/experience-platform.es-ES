---
keywords: Experience Platform;inicio;temas populares;DULE;programación
solution: Experience Platform
title: Introducción a la API del servicio de directivas
topic-legacy: developer guide
description: La API del servicio de directivas le permite crear y administrar varios recursos relacionados con el control de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API del servicio de directivas.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Introducción a [!DNL Policy Service] API

La variable [!DNL Policy Service] La API le permite crear y administrar varios recursos relacionados con la Administración de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas al [!DNL Policy Service] API.

## Requisitos previos

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Experience Platform] servicios implicados en el trabajo con capacidades de control de datos. Antes de comenzar a trabajar con [!DNL Policy Service API], consulte la documentación de los siguientes servicios:

* [Administración de datos](../home.md): El marco por el cual [!DNL Experience Platform] exige el cumplimiento de las normas de uso de datos.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Leer llamadas de API de ejemplo

La variable [!DNL Policy Service] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados requeridos

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a Administración de datos, están aislados de entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Recursos principales vs. recursos personalizados

Dentro de [!DNL Policy Service] API, todas las políticas y acciones de marketing se denominan `core` o `custom` recursos.

`core` los recursos son los definidos y mantenidos por el Adobe, mientras que `custom` son los recursos creados y mantenidos por su organización y, por lo tanto, son únicos y visibles únicamente para su organización de IMS. Como tal, las operaciones de listado y búsqueda (`GET`) son las únicas operaciones permitidas en `core` recursos, mientras que operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH`y `DELETE`) están disponibles para `custom` recursos.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de directivas, seleccione una de las guías de punto final disponibles.
