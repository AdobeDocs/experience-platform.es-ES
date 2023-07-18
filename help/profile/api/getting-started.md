---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Introducción a la API del perfil del cliente en tiempo real
type: Documentation
description: La guía de introducción a la API de perfil describe los conceptos clave y la funcionalidad básica que necesita conocer para utilizar los puntos finales de la API de perfil del cliente en tiempo real para realizar operaciones básicas de CRUD con datos de perfil.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Introducción a la [!DNL Real-Time Customer Profile] API {#getting-started}

Con los extremos de la API del perfil del cliente en tiempo real, puede realizar operaciones básicas de CRUD con datos de perfil, como configurar atributos calculados, acceder a entidades, exportar datos de perfil y eliminar conjuntos de datos o lotes innecesarios.

El uso de la guía para desarrolladores requiere una comprensión práctica de los distintos servicios de Adobe Experience Platform implicados en trabajar con [!DNL Profile] datos. Antes de comenzar a trabajar con [!DNL Real-Time Customer Profile] API, consulte la documentación de los siguientes servicios:

* [[!DNL Real-Time Customer Profile]](../home.md): Proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): obtenga una mejor vista de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permite crear audiencias a partir de los datos del perfil del cliente en tiempo real.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para poder realizar llamadas correctamente a [!DNL Profile] Extremos de API.

## Leer llamadas de API de muestra

El [!DNL Real-Time Customer Profile] La documentación de la API proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes correctamente. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

## Encabezados obligatorios

La documentación de la API también requiere que haya completado la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a [!DNL Platform] puntos finales. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

Todas las solicitudes con una carga útil en el cuerpo de la solicitud (como llamadas de POST, PUT y PATCH) deben incluir un `Content-Type` encabezado. Los valores aceptados específicos de cada llamada se proporcionan en los parámetros de llamada.

## Pasos siguientes

Para empezar a realizar llamadas utilizando [!DNL Real-Time Customer Profile] API, seleccione una de las guías de extremos disponibles.
