---
keywords: Experience Platform;inicio;temas populares;control de acceso;API;introducción
solution: Experience Platform
title: Guía de API de control de acceso
topic: developer guide
description: Control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funciones de la plataforma mediante Adobe Admin Console. Las siguientes secciones proporcionan información adicional que los desarrolladores necesitarán conocer para realizar llamadas exitosas a la API del Registro de Esquema.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---


# [!DNL Access Control] Guía de API

[!DNL Access control] for  [!DNL Experience Platform] se administra a través del  [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en el Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [información general del control de acceso](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona información sobre cómo dar formato a las solicitudes a [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) y abarca las siguientes operaciones:

- [Nombres de lista de permisos y tipos de recursos](./permissions-and-resource-types.md)
- [Directivas eficaces de vista para el usuario actual](./effective-policies.md)

## Primeros pasos

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a la API [!DNL Schema Registry].

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre los extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados y las cargas útiles con el formato adecuado, y una respuesta de ejemplo para una llamada correcta.
