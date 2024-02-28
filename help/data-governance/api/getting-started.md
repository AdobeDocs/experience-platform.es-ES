---
keywords: Experience Platform;inicio;temas populares;DULE;dule
solution: Experience Platform
title: Introducción a la API del servicio de directivas
description: La API del servicio de políticas le permite crear y administrar varios recursos relacionados con la administración de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API del servicio de directivas.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 8%

---

# Introducción a la [!DNL Policy Service] API

El [!DNL Policy Service] La API de le permite crear y administrar varios recursos relacionados con la gobernanza de datos de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a [!DNL Policy Service] API.

## Requisitos previos

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Experience Platform] servicios implicados en el trabajo con capacidades de control de datos. Antes de comenzar a trabajar con [!DNL Policy Service API], consulte la documentación de los siguientes servicios:

* [Gobernanza de datos](../home.md): el marco mediante el cual [!DNL Experience Platform] aplica el cumplimiento de uso de datos.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Lectura de llamadas de API de muestra

El [!DNL Policy Service] La documentación de la API proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados obligatorios

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Platform] puntos finales. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las que pertenecen a la gobernanza de datos, están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Recursos principales y personalizados

Dentro de [!DNL Policy Service] API, todas las políticas y acciones de marketing se denominan `core` o `custom` recursos.

`core` los recursos son los definidos y mantenidos por el Adobe, mientras que `custom` los recursos son los que crea y mantiene su organización y, por lo tanto, son únicos y visibles únicamente para su organización. Como tal, las operaciones de listado y búsqueda (`GET`) son las únicas operaciones permitidas en `core` recursos, mientras que las operaciones de listado, búsqueda y actualización (`POST`, `PUT`, `PATCH`, y `DELETE`) están disponibles para `custom` recursos.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de directivas, seleccione una de las guías de extremos disponibles.
