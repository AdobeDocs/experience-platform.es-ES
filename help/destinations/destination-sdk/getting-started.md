---
description: En esta página se describe cómo autenticarse y empezar a utilizar Adobe Experience Platform Destination SDK. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de zona protegida y el permiso de control de acceso de creación de destino.
title: Introducción a Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# Introducción

## Información general {#overview}

En esta página se describe cómo autenticarse y empezar a utilizar Adobe Experience Platform Destination SDK. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de zona protegida y el permiso de control de acceso de creación de destino.

## Terminología {#terminology}

Esta guía utiliza conceptos específicos de Experience Platform, como la organización y los entornos limitados. Consulte el [glosario de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=es) para ver las definiciones de estos términos. Consulte el [glosario de Destination SDK](/help/destinations/destination-sdk/glossary.md) para ver los términos relacionados directamente con esta funcionalidad.

## Obtener las credenciales de autenticación requeridas {#obtain-authentication-credentials}

Destination SDK usa la puerta de enlace [Adobe I/O](https://www.adobe.io/) para la autenticación. Para realizar llamadas de API a extremos de Destination SDK, debe proporcionar ciertos encabezados en las llamadas de API. Trabaje con el equipo de Adobe Exchange para configurar la autenticación en [Adobe Developer Console](https://developer.adobe.com/console).

Para realizar llamadas correctamente a los extremos de la API de Destination SDK, siga el [tutorial de autenticación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=es). Inicie el tutorial desde el paso &quot;[Generar una clave de API, ID de organización y secreto de cliente](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=es#api-ims-secret)&quot;. El equipo de Adobe Exchange se encargará de los pasos anteriores. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Destination SDK, como se muestra a continuación:

* `x-api-key: {API_KEY}`, también denominado ID de cliente
* `x-gw-ims-org-id: {ORG_ID}`, también denominado ID de organización
* `Authorization: Bearer {ACCESS_TOKEN}`. El token de acceso tiene un tiempo de caducidad de 24 horas, expresado en milisegundos, por lo que tendrá que actualizarlo. Para actualizar el token de acceso, repita los pasos descritos en el tutorial de autenticación.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propiedad del destino y zonas protegidas {#destination-ownership}

Todos los recursos de Experience Platform están aislados para zonas protegidas virtuales específicas. Las solicitudes a Destination SDK requieren encabezados que especifiquen el nombre de la zona protegida en la que se realiza la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

El equipo de Adobe Exchange le proporciona su nombre de zona protegida, que debe utilizar en las llamadas a los extremos de la API de Destination SDK.

## Control de acceso basado en roles (RBAC) {#rbac}

Para usar los extremos de la API de Destination SDK descritos en la [documentación de referencia](functionality/configuration-options.md), necesita el permiso de control de acceso de **[!UICONTROL Creación de destinos]**. Trabaje con el equipo de Adobe Exchange para que se le asigne este permiso en [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permiso de creación de destino](./assets/destination-authoring-permission.png)

Para obtener más información, lea los siguientes documentos de Control de acceso de Experience Platform:

* [Administración de permisos para un perfil de producto](/help/access-control/ui/permissions.md)
* [Permisos disponibles para Experience Platform](/help/access-control/home.md#permissions)
* [Documentación de Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html)

## Consideraciones adicionales {#additional-considerations}

* En el caso de los destinos públicos o de producción, Adobe debe revisar y aprobar cualquier cambio que realice en las configuraciones de destino, tanto si crea como si edita una configuración de destino. Los cambios se reflejarán en los destinos solo después de que se haya realizado la revisión. Esto no se aplica a destinos privados que solo están disponibles para usted.
* Solo los usuarios que pertenecen a la misma organización y tienen acceso a la zona protegida pueden editar la configuración de destino.

## Pasos siguientes {#next-steps}

Siguiendo los pasos de este artículo, ha obtenido credenciales de autenticación para Adobe I/O, un nombre de zona protegida y el permiso de control de acceso de creación de destino. A continuación, puede configurar un destino con Destination SDK.

* Lea las siguientes guías de configuración, según el tipo de destino:

   * [Usar Destination SDK para configurar un destino de flujo continuo](guides/configure-destination-instructions.md)
   * [Usar Destination SDK para configurar un destino basado en archivos](guides/configure-file-based-destination-instructions.md)

* Para todas las operaciones, consulte la [documentación de la API de creación de destino](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Use la [colección de Postman de la API de creación de destino](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) para configurar su destino mediante los extremos de la API de Destination SDK. Para empezar a usar Postman, vea los [pasos para importar entornos y colecciones](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) y una [guía de vídeo para crear el entorno de Postman](https://video.tv.adobe.com/v/31627?captions=spa).
