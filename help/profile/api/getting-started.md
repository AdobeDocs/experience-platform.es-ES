---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API
title: Introducción a la API del perfil del cliente en tiempo real
type: Documentation
description: La guía de introducción a la API de perfil describe los conceptos clave y la funcionalidad básica que necesita conocer para utilizar los puntos finales de la API de perfil del cliente en tiempo real para realizar operaciones básicas de CRUD con datos de perfil.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# Introducción a la API [!DNL Real-Time Customer Profile] {#getting-started}

Con los extremos de la API del perfil del cliente en tiempo real, puede realizar operaciones básicas de CRUD con datos de perfil, como configurar atributos calculados, acceder a entidades, exportar datos de perfil y eliminar conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en el trabajo con datos de [!DNL Profile]. Antes de comenzar a trabajar con la API [!DNL Real-Time Customer Profile], revise la documentación de los siguientes servicios:

* [[!DNL Real-Time Customer Profile]](../home.md): proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): permite crear audiencias a partir de los datos del perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para realizar llamadas exitosas a [!DNL Profile] extremos de API.

## Lectura de llamadas de API de muestra

La documentación de la API [!DNL Real-Time Customer Profile] proporciona ejemplos de llamadas a la API para mostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

## Encabezados obligatorios

La documentación de la API también requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Experience Platform] extremos. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Las solicitudes a las API [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas POST, PUT y PATCH) deben incluir un encabezado `Content-Type`. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Real-Time Customer Profile], seleccione una de las guías de extremos disponibles.
