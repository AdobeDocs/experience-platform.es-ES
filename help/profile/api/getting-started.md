---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Introducción a la API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Getting started with the [!DNL Real-time Customer Profile] API {#getting-started}

Con la API, puede realizar operaciones CRUD básicas con recursos de Perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos de Perfil y la eliminación de conjuntos de datos o lotes innecesarios. [!DNL Real-time Customer Profile]

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform que intervienen en el trabajo con [!DNL Profile] datos. Antes de comenzar a trabajar con la [!DNL Real-time Customer Profile] API, consulte la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):: Obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):: [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a los extremos de la [!DNL Profile] API de forma satisfactoria.

## Leer llamadas de API de muestra

La documentación de la [!DNL Real-time Customer Profile] API proporciona llamadas de la API de ejemplo para mostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

## Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar llamadas a [!DNL Platform] extremos correctamente. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas de POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## Pasos siguientes

Para empezar a realizar llamadas mediante la [!DNL Real-time Customer Profile] API, seleccione una de las guías de punto final disponibles.