---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de simuladores de pruebas
solution: Experience Platform
title: Guía para desarrolladores de la API de Simulador para pruebas
topic: developer guide
description: Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de Simulador para pruebas para administrar entornos limitados en Experience Platform, e incluye ejemplos de llamadas a la API para realizar diversas operaciones.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Guía para desarrolladores de la API de Simulador para pruebas

Los Simuladores para pruebas de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno de producción.

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de Simulador para pruebas para administrar entornos limitados en Experience Platform, e incluye ejemplos de llamadas a la API para realizar diversas operaciones.

## Introducción a la API de Simulador para pruebas

Para administrar los entornos limitados de su organización de IMS, debe tener permisos de administración de Simuladores para pruebas. Los usuarios sin permisos de acceso solo pueden usar el extremo para [enumerar los entornos limitados activos para el usuario actual](./list-active-sandboxes.md). Consulte la [información general de control de acceso](../../access-control/home.md) para obtener más información sobre cómo asignar permisos de simulación de pruebas para Experience Platform.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de plataforma. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre los extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.