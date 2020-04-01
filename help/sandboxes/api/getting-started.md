---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de la API de Simulador para pruebas
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# Guía para desarrolladores de la API de Simulador para pruebas

Los Simuladores para pruebas de Adobe Experience Platform proporcionan entornos de desarrollo aislados que le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno de producción.

Esta guía para desarrolladores proporciona pasos para ayudarle a utilizar la API de Simulador para pruebas para administrar entornos limitados en la plataforma de experiencia e incluye llamadas de API de ejemplo para realizar diversas operaciones.

## Introducción a la API de Simulador para pruebas

Para administrar los entornos limitados de su organización de IMS, debe tener permisos de administración de Simuladores para pruebas. Los usuarios sin permisos de acceso solo pueden usar el punto final para [enumerar los entornos limitados activos para el usuario](./list-active-sandboxes.md)actual. Consulte la descripción general [de](../../access-control/home.md) control de acceso para obtener más información sobre cómo asignar permisos de simulación de pruebas para la plataforma de experiencia.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Esta guía requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para realizar llamadas a las API de plataforma correctamente. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Además de los encabezados de autenticación, todas las solicitudes requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT y PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre los extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato **general de** API, una **solicitud** de muestra que muestra los encabezados y las cargas útiles con el formato adecuado, y una **respuesta** de ejemplo para una llamada correcta.