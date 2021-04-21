---
keywords: Experience Platform;inicio;temas populares;control de acceso;api;introducción
solution: Experience Platform
title: Guía de API de control de acceso
topic-legacy: developer guide
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funcionalidades de Platform mediante Adobe Admin Console. Las secciones siguientes proporcionan información adicional que los desarrolladores deberán conocer para realizar correctamente llamadas a la API del Registro de esquemas.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# [!DNL Access Control] Guía de API

[!DNL Access control] para  [!DNL Experience Platform] se administra a través de  [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [descripción general del control de acceso](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona información sobre cómo dar formato a las solicitudes a [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) y abarca las siguientes operaciones:

- [Nombres de lista de permisos y tipos de recursos](./permissions-and-resource-types.md)
- [Ver directivas efectivas para el usuario actual](./effective-policies.md)

## Primeros pasos

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente a la API [!DNL Schema Registry] .

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Pasos siguientes

Ahora que ha reunido las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante con respecto a sus extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
