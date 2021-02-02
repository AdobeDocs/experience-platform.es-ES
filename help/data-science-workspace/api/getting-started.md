---
keywords: Experience Platform;guía para desarrolladores;punto final;Área de trabajo de ciencia de datos;temas populares;área de trabajo de ciencia de datos;ciencia de datos
solution: Experience Platform
title: Guía para desarrolladores de la API de aprendizaje automático de Sensei
topic: Developer guide
description: En esta guía para desarrolladores se proporcionan pasos para ayudarle en el inicio del uso de la API de aprendizaje automático Sensei y se muestran las llamadas de API para realizar operaciones de CRUD en varios recursos del área de trabajo de ciencias de datos.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] Guía para desarrolladores de API

La API [!DNL Sensei Machine Learning] proporciona un mecanismo para que los científicos de datos organicen y administren servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación de servicios.

Esta guía para desarrolladores proporciona pasos para ayudarle a realizar inicios mediante la [API de aprendizaje automático de Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), y muestra las llamadas de API para realizar operaciones de CRUD en varios recursos del área de trabajo de ciencias de datos.

## Primeros pasos

Debe haber completado el tutorial [authentication](https://www.adobe.com/go/platform-api-authentication-en) para tener acceso a los siguientes encabezados de solicitud para realizar llamadas a [!DNL Adobe Experience Platform] API:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

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