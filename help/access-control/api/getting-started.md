---
keywords: Experience Platform;inicio;temas populares;control de acceso;api;introducción
solution: Experience Platform
title: Guía de API de control de acceso
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para varias funciones de Experience Platform mediante Adobe Admin Console. Las secciones siguientes proporcionan información adicional que los desarrolladores deben conocer para realizar llamadas correctamente a la API de Registro de esquemas.
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 21%

---

# Guía de la API de [!DNL Access Control]

[!DNL Access control] para [!DNL Experience Platform] se administra mediante [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [descripción general del control de acceso](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona información sobre cómo dar formato a sus solicitudes para [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/) y cubre las siguientes operaciones:

- [Nombres de lista de permisos y tipos de recursos](./permissions-and-resource-types.md)
- [Ver directivas de acceso efectivas para el usuario actual](./effective-policies.md)

## Introducción

Las secciones siguientes proporcionan información adicional que necesitará conocer para poder realizar llamadas correctas a la API [!DNL Access Control].

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre sus puntos de conexión y muestra llamadas de API de ejemplo para realizar operaciones de CRUD. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, así como una respuesta de ejemplo para una llamada correcta.
