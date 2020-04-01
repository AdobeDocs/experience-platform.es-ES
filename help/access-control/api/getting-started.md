---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de Control de acceso
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Guía para desarrolladores de Control de acceso

Control de acceso para la plataforma de experiencias se administra a través de la Consola de administración de [Adobe](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la descripción general [del](../home.md) control de acceso para obtener más información.

Esta guía para desarrolladores proporciona información sobre cómo dar formato a las solicitudes a la API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)Control de acceso y trata las siguientes operaciones:

- [Nombres de Lista de permisos y tipos de recursos](./permissions-and-resource-types.md)
- [Directivas eficaces de Vista para el usuario actual](./effective-policies.md)

## Primeros pasos

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas correctamente a la API del Registro de Esquema.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Pasos siguientes

Ahora que ha recopilado las credenciales necesarias, puede seguir leyendo el resto de la guía para desarrolladores. Cada sección proporciona información importante sobre los extremos y muestra ejemplos de llamadas de API para realizar operaciones de CRUD. Cada llamada incluye el formato **general de** API, una **solicitud** de muestra que muestra los encabezados y las cargas útiles con el formato adecuado, y una **respuesta** de ejemplo para una llamada correcta.