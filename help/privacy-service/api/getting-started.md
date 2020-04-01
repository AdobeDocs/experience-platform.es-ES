---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de Privacy Service
description: Utilice la API de RESTful para administrar los datos personales de los sujetos de datos en las aplicaciones de Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a28ad2725094e0748e2860276ab2e7581d790ac

---


# Guía para desarrolladores de Privacy Service

Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario que le permiten administrar (acceder y eliminar) los datos personales de los usuarios (clientes) en todas las aplicaciones de Adobe Experience Cloud. Privacy Service también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que involucran aplicaciones de Experience Cloud.

Esta guía explica cómo utilizar la API de Privacy Service. Para obtener más información sobre cómo utilizar la interfaz de usuario, consulte la descripción general [de la interfaz de usuario de](../ui/overview.md)Privacy Service. Para obtener una lista completa de todos los extremos disponibles en la API de Privacy Service, consulte la referencia [de la](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Primeros pasos

Esta guía requiere un conocimiento práctico de las siguientes funciones de la plataforma de experiencias:

* [Privacy Service](../home.md): Proporciona una API de RESTful y una interfaz de usuario que le permiten administrar las solicitudes de acceso y eliminación de los temas de datos (clientes) en todas las aplicaciones de Adobe Experience Cloud.

Las siguientes secciones proporcionan información adicional que debe conocer para realizar llamadas exitosas a la API de Privacy Service.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](https://www.adobe.io/apis/experienceplatform/home/services/troubleshooting.html#!api-specification/markdown/narrative/technical_overview/platform_faq_and_troubleshooting/platform_faq_and_troubleshooting.md) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API de Privacy Service. El documento sobre trabajos [de](privacy-jobs.md) privacidad recorre las distintas llamadas de API que puede realizar mediante la API de Privacy Service. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.
