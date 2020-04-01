---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Guía para desarrolladores de la API de aprendizaje automático de Sensei
topic: Developer guide
translation-type: tm+mt
source-git-commit: b0b44f4aaf365f58086cfa17d27fbba6ed2a2a97

---


# Guía para desarrolladores de la API de aprendizaje automático de Sensei

La API de aprendizaje automático de Sensei proporciona un mecanismo para que los científicos de datos organicen y gestionen los servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación del servicio.

En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio con el uso de la API [de aprendizaje automático de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei y se muestran las llamadas de API para realizar operaciones de CRUD en varios recursos del área de trabajo de ciencias de datos.

## Primeros pasos

Debe haber completado el tutorial de [autenticación](../../tutorials/authentication.md) para tener acceso a los siguientes encabezados de solicitud para realizar llamadas a las API de Adobe Experience Platform:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Una vez recopiladas las credenciales de autenticación necesarias, puede pasar a las secciones siguientes de esta guía para desarrolladores para ver las llamadas de API de ejemplo a los siguientes grupos de extremos:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Perspectivas](./insights.md)
* [Instancias MLI (Fórmulas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apéndice](./appendix.md)