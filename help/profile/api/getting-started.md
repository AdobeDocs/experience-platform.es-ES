---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Introducción a la API de Perfil para clientes en tiempo real {#getting-started}

Mediante la API de Perfil de cliente en tiempo real, puede realizar operaciones CRUD básicas con recursos de Perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos de Perfil y la eliminación de conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en el trabajo con datos de Perfil. Antes de comenzar a trabajar con la API de Perfil del cliente en tiempo real, consulte la documentación de los siguientes servicios:

* [Perfil](../home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [Servicio](../../segmentation/home.md)de segmentación de Adobes Experience Platform: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [Simuladores](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a extremos de la API de Perfil con éxito.

## Leer llamadas de API de muestra

La documentación de la API de Perfil del cliente en tiempo real proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Encabezados requeridos

La documentación de la API también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a extremos de Platform. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados de Platform, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como las llamadas POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Perfil del cliente en tiempo real, seleccione una de las guías de punto final disponibles.