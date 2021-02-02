---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Introducción a la API de Perfil para clientes en tiempo real
topic: guide
type: Documentation
description: La guía de introducción a la API de Perfil describe los conceptos clave y la funcionalidad básica que necesita conocer para utilizar los extremos de la API de Perfil de cliente en tiempo real para realizar operaciones CRUD básicas con datos de Perfil.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Introducción a la API [!DNL Real-time Customer Profile] {#getting-started}

Mediante los extremos de la API de Perfil del cliente en tiempo real, puede realizar operaciones CRUD básicas con datos de Perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos de Perfil y la eliminación de conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere una comprensión práctica de los diversos servicios de Adobe Experience Platform que intervienen en el trabajo con datos [!DNL Profile]. Antes de comenzar a trabajar con la API [!DNL Real-time Customer Profile], consulte la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../home.md):: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):: Obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md):: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md)::  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a [!DNL Profile] extremos de API de forma satisfactoria.

## Leer llamadas de API de muestra

La documentación de la API [!DNL Real-time Customer Profile] proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas a [!DNL Platform] extremos de forma satisfactoria. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en las llamadas de API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas de POST, PUT y PATCH) deben incluir un encabezado `Content-Type`. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Real-time Customer Profile], seleccione una de las guías de punto final disponibles.