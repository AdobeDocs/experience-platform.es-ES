---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Introducción a la API del perfil del cliente en tiempo real
topic-legacy: guide
type: Documentation
description: La guía de introducción a la API de perfil describe los conceptos clave y la funcionalidad básica que debe conocer para utilizar los extremos de la API de perfil de cliente en tiempo real para realizar operaciones CRUD básicas con datos de perfil.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Introducción a [!DNL Real-Time Customer Profile] API {#getting-started}

Mediante los extremos de la API del perfil del cliente en tiempo real, puede realizar operaciones CRUD básicas con los datos del perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos del perfil y la eliminación de conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en el trabajo con [!DNL Profile] datos. Antes de comenzar a trabajar con [!DNL Real-Time Customer Profile] , consulte la documentación de los siguientes servicios:

* [[!DNL Real-Time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenga una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite generar segmentos de audiencia a partir de datos del perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas a [!DNL Profile] Puntos finales de API.

## Leer llamadas de API de ejemplo

La variable [!DNL Real-Time Customer Profile] La documentación de API proporciona llamadas de API de ejemplo para demostrar cómo dar formato correctamente a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados requeridos

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como las llamadas de POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada .

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Real-Time Customer Profile] , seleccione una de las guías de punto final disponibles.
