---
keywords: Experience Platform;guía para desarrolladores;punto final;Workspace de ciencia de datos;temas populares;espacio de trabajo de ciencia de datos;ciencia de datos
solution: Experience Platform
title: Guía de la API de aprendizaje automático de Sensei
description: La API de aprendizaje automático de Sensei permite a los desarrolladores realizar operaciones de CRUD en varios recursos de Workspace de ciencia de datos. Siga esta guía para aprender a realizar operaciones clave con la API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 14%

---

# Guía de la API de [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

La API [!DNL Sensei Machine Learning] proporciona un mecanismo para que los científicos de datos organicen y administren los servicios de aprendizaje automático, desde la incorporación del algoritmo hasta la experimentación y la implementación de servicios.

Esta guía para desarrolladores proporciona pasos que le ayudarán a empezar a utilizar la [API de aprendizaje automático de Sensei](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/), y muestra las llamadas a la API para realizar operaciones CRUD en varios recursos de Workspace de ciencia de datos.

## Introducción

Es necesario que haya completado el tutorial [authentication](https://www.adobe.com/go/platform-api-authentication-en) para tener acceso a los siguientes encabezados de solicitud y realizar llamadas a las API [!DNL Adobe Experience Platform]:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Pasos siguientes

Una vez que haya recopilado las credenciales de autenticación necesarias, puede continuar con las secciones siguientes de esta guía para desarrolladores para ver llamadas de API de ejemplo a los siguientes grupos de extremos:

* [Motores](./engines.md)
* [Experimentos](./experiments.md)
* [Información](./insights.md)
* [Instancias MLL (fórmulas)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelos](./models.md)
* [Apéndice](./appendix.md)
