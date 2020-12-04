---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Guía para desarrolladores de la API de aprendizaje automático de Sensei
topic: Developer guide
description: En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio del uso de la API de aprendizaje automático Sensei y se muestran las llamadas de API para realizar operaciones de CRUD en varios recursos de Área de trabajo de ciencias de datos.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] Guía para desarrolladores de API

La [!DNL Sensei Machine Learning] API proporciona un mecanismo para que los científicos de datos organicen y gestionen los servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación de servicios.

En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio con el uso de la API [de aprendizaje automático de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei y se muestran las llamadas de API para realizar operaciones de CRUD en varios recursos del área de trabajo de ciencias de datos.

## Primeros pasos

Debe haber completado el tutorial de [autenticación](../../tutorials/authentication.md) para tener acceso a los siguientes encabezados de solicitud para realizar llamadas a [!DNL Adobe Experience Platform] las API:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

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