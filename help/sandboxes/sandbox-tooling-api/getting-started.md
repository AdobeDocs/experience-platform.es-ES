---
title: Introducción a la API de herramientas de espacio aislado
description: Utilice la API de herramientas de entorno limitado para examinar artefactos, exportar e importar una instantánea de las configuraciones de los entornos limitados entre entornos limitados. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 15%

---

# Introducción a la API de herramientas de zona protegida {#getting-started}

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de herramientas de entorno limitado para administrar paquetes y herramientas en Adobe Experience Platform, e incluye llamadas de API de ejemplo para realizar varias operaciones.

## Lectura de llamadas de API de muestra {#api-calls}

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporcionan los datos JSON de muestra devueltos a la respuesta de la API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilación de valores para los encabezados obligatorios {#headers}

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar correctamente llamadas a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes {#next-steps}

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre sus puntos de conexión y muestra llamadas de API de ejemplo para realizar operaciones de CRUD. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, así como una respuesta de ejemplo para una llamada correcta.

Consulte los siguientes tutoriales de API para empezar a realizar llamadas a la API de herramientas de zona protegida:

* [Extremo de paquetes](./packages.md)
* [Extremo de herramientas](./tools.md)
