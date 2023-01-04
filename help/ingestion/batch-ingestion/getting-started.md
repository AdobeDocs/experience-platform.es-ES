---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Introducción a la API de ingesta de datos
type: Documentation
description: La guía de introducción a la API de ingesta de datos describe los conceptos clave y la funcionalidad básica que debe conocer antes de empezar a introducir datos en Experience Platform mediante API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Introducción a la API de ingesta de datos {#getting-started}

Con los extremos de la API de ingesta de datos, puede realizar operaciones básicas de CRUD para introducir datos en Adobe Experience Platform.

El uso de las guías de API requiere comprender bien varios servicios de Adobe Experience Platform que participan en el trabajo con datos. Antes de utilizar la API de ingesta de datos, consulte la documentación de los siguientes servicios:

* [Ingesta por lotes](./overview.md): Permite introducir datos en Adobe Experience Platform como archivos por lotes.
* [[!DNL Real-Time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas a [!DNL Profile] Puntos finales de API.

## Leer llamadas de API de ejemplo

La documentación de la API de ingesta de datos proporciona llamadas de API de ejemplo para demostrar cómo dar formato correctamente a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados requeridos

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como las llamadas de POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada .

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).
