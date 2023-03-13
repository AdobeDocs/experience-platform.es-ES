---
title: Introducción a la API de consulta de auditoría
description: La API de consulta de auditoría le permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de consulta de auditoría.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Introducción a la API de consulta de auditoría

Adobe Experience Platform permite auditar la actividad del usuario para varios servicios y funcionalidades en forma de registros de eventos de auditoría. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

La API de consulta de auditoría le permite auditar la actividad del usuario para varios servicios y funcionalidades en forma de registros de eventos de auditoría. Este documento proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de consulta de auditoría.

## Requisitos previos

Para administrar eventos de auditoría, debe tener **[!UICONTROL Ver registro de actividades de usuario]** permiso de control de acceso concedido (se encuentra en la sección [!UICONTROL Gobernanza de datos] categoría). Para obtener información sobre cómo administrar permisos individuales para funciones de Platform, consulte la [documentación de control de acceso](../../../../access-control/home.md).

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para los encabezados obligatorios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación. Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Para empezar a realizar llamadas utilizando [!DNL Audit Query] API, consulte la [guía de extremo de eventos](./events.md) y el [guía de extremo de exportación](./export.md).
