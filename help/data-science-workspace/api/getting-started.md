---
keywords: Experience Platform;guía para desarrolladores;punto final;Data Science Workspace;temas populares;espacio de trabajo de ciencia de datos;ciencia de datos
solution: Experience Platform
title: Guía de API de aprendizaje automático de Sensei
description: La API de aprendizaje automático de Sensei permite a los desarrolladores realizar operaciones de CRUD en varios recursos de Data Science Workspace. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---

# Guía de la API de [!DNL Sensei Machine Learning]

La variable [!DNL Sensei Machine Learning] La API proporciona un mecanismo para que los científicos de datos organicen y gestionen los servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación de servicios.

Esta guía para desarrolladores proporciona los pasos para ayudarle a empezar a usar el [API de aprendizaje automático de Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)y muestra las llamadas de API para realizar operaciones de CRUD en varios recursos de Data Science Workspace.

## Primeros pasos

Debe completar la [autenticación](https://www.adobe.com/go/platform-api-authentication-en) para tener acceso a los siguientes encabezados de solicitud para realizar llamadas a [!DNL Adobe Experience Platform] API:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Una vez que haya recopilado las credenciales de autenticación necesarias, puede continuar con las secciones siguientes de esta guía para desarrolladores para ver llamadas de API de ejemplo a los siguientes grupos de puntos de conexión:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Insights](./insights.md)
* [Instancias MLI (Fórmulas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apéndice](./appendix.md)
