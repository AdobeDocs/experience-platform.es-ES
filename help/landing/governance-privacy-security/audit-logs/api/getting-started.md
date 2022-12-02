---
title: Introducción a la API de consulta de auditoría
description: La API de consulta de auditoría permite recuperar datos de métricas para varias funciones de Adobe Experience Platform. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de consulta de auditoría.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# Introducción a la API de consulta de auditoría

Adobe Experience Platform permite auditar la actividad de los usuarios para varios servicios y funciones en forma de registros de eventos de auditoría. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción.

La API de consulta de auditoría permite auditar la actividad del usuario para varios servicios y capacidades en forma de registros de eventos de auditoría. Este documento proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de consulta de auditoría.

## Requisitos previos

Para administrar los eventos de auditoría, debe tener la variable **[!UICONTROL Ver registro de actividades del usuario]** permiso de control de acceso concedido (encontrado en la sección [!UICONTROL Administración de datos] ). Para obtener información sobre cómo administrar permisos individuales para las funciones de Platform, consulte la [documentación de control de acceso](../../../../access-control/home.md).

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación. Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Para empezar a realizar llamadas con [!DNL Audit Query] API, consulte la [guía de extremo de eventos](./events.md) y [exportar guía de extremo](./export.md).
