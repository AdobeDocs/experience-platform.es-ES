---
keywords: Experience Platform;inicio;temas populares;control de acceso;api;introducción
solution: Experience Platform
title: Guía de API de control de acceso
description: El control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para varias funcionalidades de Platform mediante Adobe Admin Console. Las secciones siguientes proporcionan información adicional que los desarrolladores deben conocer para realizar llamadas correctamente a la API de Registro de esquemas.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# Guía de la API de [!DNL Access Control]

[!DNL Access control] para [!DNL Experience Platform] se administra a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [información general de control de acceso](../home.md) para obtener más información.

Esta guía para desarrolladores proporciona información sobre cómo dar formato a las solicitudes en [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)y abarca las siguientes operaciones:

- [Nombres de lista de permisos y tipos de recursos](./permissions-and-resource-types.md)
- [Ver directivas de acceso efectivas para el usuario actual](./effective-policies.md)

## Primeros pasos

Las secciones siguientes proporcionan información adicional que deberá conocer para poder realizar llamadas correctamente a [!DNL Access Control] API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre sus puntos de conexión y muestra llamadas de API de ejemplo para realizar operaciones de CRUD. Cada llamada a incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y las cargas útiles con el formato adecuado, así como una respuesta de ejemplo para una llamada correcta.
