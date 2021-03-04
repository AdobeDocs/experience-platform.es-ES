---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API
title: Introducción a la API del perfil del cliente en tiempo real
topic: guía
type: Documentación
description: La guía de introducción a la API de perfil describe los conceptos clave y la funcionalidad básica que debe conocer para utilizar los extremos de la API de perfil de cliente en tiempo real para realizar operaciones CRUD básicas con datos de perfil.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Introducción a la API [!DNL Real-time Customer Profile] {#getting-started}

Mediante los extremos de la API del perfil del cliente en tiempo real, puede realizar operaciones CRUD básicas con los datos del perfil, como la configuración de atributos calculados, el acceso a entidades, la exportación de datos del perfil y la eliminación de conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere conocer los distintos servicios de Adobe Experience Platform que intervienen en el trabajo con datos [!DNL Profile]. Antes de comenzar a trabajar con la API [!DNL Real-time Customer Profile] , revise la documentación de los siguientes servicios:

* [[!DNL Real-time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenga una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite generar segmentos de audiencia a partir de datos del perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente a [!DNL Profile] extremos de API.

## Leer llamadas de API de ejemplo

La documentación de la API [!DNL Real-time Customer Profile] proporciona ejemplos de llamadas de API para demostrar cómo dar formato adecuado a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

## Encabezados requeridos

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a [!DNL Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] llamadas a la API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Las solicitudes para las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como las llamadas POST, PUT y PATCH) deben incluir un encabezado `Content-Type`. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada .

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Real-time Customer Profile], seleccione una de las guías de punto final disponibles.