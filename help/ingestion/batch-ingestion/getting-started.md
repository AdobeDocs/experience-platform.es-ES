---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API
title: Introducción a la API de ingesta de datos
type: Documentation
description: La guía de introducción a la API de ingesta de datos describe los conceptos clave y la funcionalidad básica que debe conocer antes de empezar a introducir datos en Experience Platform mediante API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 6%

---

# Introducción a la API de ingesta de datos {#getting-started}

Mediante los extremos de la API de ingesta de datos, puede realizar operaciones básicas de CRUD para introducir datos en Adobe Experience Platform.

El uso de las guías de la API requiere una comprensión práctica de varios servicios de Adobe Experience Platform implicados en el trabajo con datos. Antes de usar la API de ingesta de datos, revise la documentación de los siguientes servicios:

* [Ingesta por lotes](./overview.md): Permite la ingesta de datos en Adobe Experience Platform como archivos por lotes.
* [[!DNL Real-Time Customer Profile]](../home.md): proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para realizar llamadas exitosas a [!DNL Profile] extremos de API.

## Lectura de llamadas de API de muestra

La documentación de la API de ingesta de datos proporciona ejemplos de llamadas a la API para demostrar cómo dar formato adecuado a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Experience Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas POST, PUT y PATCH) deben incluir un encabezado `Content-Type`. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Las solicitudes a las API [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).
