---
keywords: Experience Platform;inicio;temas populares;guía para desarrolladores de espacios aislados
solution: Experience Platform
title: Introducción a la API de zona protegida
description: La API de zona protegida permite a los desarrolladores administrar mediante programación las zonas protegidas en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 15%

---

# Introducción a la API de zona protegida

Los entornos limitados de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno de producción.

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de zona protegida para administrar zonas protegidas en Experience Platform e incluye llamadas de API de ejemplo para realizar varias operaciones.

## Requisitos previos

Para administrar los entornos limitados de su organización, debe tener permisos de administración de entornos limitados. Los usuarios sin permisos de acceso solo pueden usar el [extremo de zonas protegidas disponible](./available.md) para enumerar las zonas protegidas activas del usuario actual. Consulte la [descripción general del control de acceso](../../access-control/home.md) para obtener más información sobre cómo asignar permisos de zona protegida para Experience Platform.

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilación de valores para los encabezados obligatorios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre sus puntos de conexión y muestra llamadas de API de ejemplo para realizar operaciones de CRUD. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, así como una respuesta de ejemplo para una llamada correcta.
