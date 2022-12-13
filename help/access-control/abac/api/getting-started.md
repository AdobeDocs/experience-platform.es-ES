---
keywords: Experience Platform;inicio;temas populares;Control de acceso basado en atributos;control de acceso basado en atributos
title: Introducción a la API de control de acceso basada en atributos
description: La API de control de acceso basado en atributos permite administrar mediante programación las funciones y las políticas de acceso en Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 54e15234d1b1050ea2cdb8b7d37c79a133a339f1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# Introducción a la API de control de acceso basada en atributos

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de control de acceso basada en atributos para administrar funciones, productos, categorías de permisos y conjuntos de permisos en Adobe Experience Platform, e incluye ejemplos de llamadas de API para realizar diversas operaciones.

## Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Esta guía requiere que haya completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en) para realizar llamadas correctamente a las API de Platform. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* `Content-Type: application/json`

## Pasos siguientes

Ahora que ha reunido las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante con respecto a sus extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.

Consulte los siguientes tutoriales de API para empezar a realizar llamadas a la API de control de acceso basada en atributos:

* [Punto de conexión de roles](./roles.md)
* [Punto final del producto](./products.md)
