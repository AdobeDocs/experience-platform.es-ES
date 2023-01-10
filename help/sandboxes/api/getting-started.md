---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de entornos limitados
solution: Experience Platform
title: Introducción a la API de Sandbox
description: La API de espacio aislado permite a los desarrolladores administrar mediante programación entornos limitados en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 5%

---

# Introducción a la API de Sandbox

Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno de producción.

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de espacio aislado para administrar entornos limitados en Experience Platform, e incluye llamadas de API de muestra para realizar diversas operaciones.

## Requisitos previos

Para administrar entornos limitados para su organización de IMS, debe tener permisos de administración de entornos limitados. Los usuarios sin permisos de acceso solo pueden usar la variable [punto final de entornos limitados disponibles](./available.md) para mostrar los entornos limitados activos para el usuario actual. Consulte la [información general sobre el control de acceso](../../access-control/home.md) para obtener más información sobre cómo asignar permisos de simulación de pruebas para Experience Platform.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Ahora que ha reunido las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante con respecto a sus extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
