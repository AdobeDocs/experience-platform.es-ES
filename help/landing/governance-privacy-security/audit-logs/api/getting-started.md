---
title: Introducción a la API de consulta de auditoría
description: La API de consulta de auditoría le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de consulta de auditoría.
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 11%

---

# Introducción a la API de consulta de auditoría

Adobe Experience Platform permite auditar la actividad del usuario para varios servicios y funcionalidades en forma de registros de eventos de auditoría. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

La API de consulta de auditoría le permite auditar la actividad del usuario para varios servicios y funcionalidades en forma de registros de eventos de auditoría. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de consulta de auditoría.

## Requisitos previos

Para administrar eventos de auditoría, debe contar con el permiso de control de acceso **[!UICONTROL Ver registro de actividad de usuario]** concedido (que se encuentra en la categoría [!UICONTROL Control de datos]). Para obtener información sobre cómo administrar permisos individuales para funciones de Experience Platform, consulte la [documentación de control de acceso](../../../../access-control/home.md).

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de Experience Platform.

### Recopilación de valores para los encabezados obligatorios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para poder realizar correctamente llamadas a las API de Experience Platform. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Para empezar a realizar llamadas mediante la API [!DNL Audit Query], consulte la [guía de extremo de eventos](./events.md) y la [guía de extremo de exportación](./export.md).
