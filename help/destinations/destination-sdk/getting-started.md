---
description: En esta página se describe cómo autenticarse y empezar a utilizar Adobe Experience Platform Destination SDK. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino.
title: Introducción a Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# Primeros pasos

## Información general {#overview}

En esta página se describe cómo autenticarse y empezar a utilizar Adobe Experience Platform Destination SDK. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino.

## Terminología {#terminology}

Esta guía utiliza conceptos específicos de la plataforma, como organización y entornos limitados. Consulte la [glosario del Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=es) para las definiciones de estos y otros términos.

## Obtenga las credenciales de autenticación necesarias {#obtain-authentication-credentials}

El Destination SDK utiliza la variable [Adobe I/O](https://www.adobe.io/) puerta de enlace para la autenticación. Para realizar llamadas de API a extremos de Destination SDK, debe proporcionar ciertos encabezados en las llamadas de API. Trabaje con el equipo de Adobe Exchange para configurar la autenticación para usted en el [Consola de Adobe Developer](https://developer.adobe.com/console).

Para realizar llamadas correctamente a puntos finales de API de Destination SDK, siga la [tutorial de autenticación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Inicie el tutorial desde el &quot;[Generar una clave de API, un ID de organización y un secreto de cliente](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. El equipo de Adobe Exchange se encargará de los pasos anteriores. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Destination SDK, como se muestra a continuación:

* `x-api-key: {API_KEY}`, también denominado ID de cliente
* `x-gw-ims-org-id: {ORG_ID}`, también denominado ID de organización
* `Authorization: Bearer {ACCESS_TOKEN}`. El token de acceso tiene una caducidad de 24 horas, expresada en milisegundos, por lo que tendrá que actualizarlo. Para actualizar el token de acceso, repita los pasos descritos en el tutorial de autenticación.

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

## Propiedad de destino y entornos limitados {#destination-ownership}

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Las solicitudes al Destination SDK requieren encabezados que especifiquen el nombre del simulador para pruebas en el que se realiza la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

El equipo de Adobe Exchange le proporciona su nombre de simulador de pruebas, que debe usar en las llamadas a los extremos de la API del Destination SDK.

## Control de acceso basado en roles (RBAC) {#rbac}

Para utilizar los extremos de API del Destination SDK descritos en la sección [documentación de referencia](functionality/configuration-options.md), necesita el **[!UICONTROL Creación de destinos]** permiso de control de acceso. Trabaje con el equipo de Adobe Exchange para obtener este permiso asignado en [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permiso de creación de destino](./assets/destination-authoring-permission.png)

Para obtener más información, lea los siguientes documentos de Control de acceso del Experience Platform:

* [Administrar permisos para un perfil de producto](/help/access-control/ui/permissions.md)
* [Permisos disponibles para el Experience Platform](/help/access-control/home.md#permissions)
* [Documentación de Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html)

## Consideraciones adicionales {#additional-considerations}

* En el caso de los destinos públicos o productivos, cualquier cambio que realice en las configuraciones de destino, tanto si crea como si edita una configuración de destino, deberá revisarse y aprobarse por Adobe. Los cambios solo se reflejan en los destinos una vez que se haya realizado la revisión. Esto no se aplica a los destinos privados que solo están disponibles para usted.
* Solo los usuarios que pertenecen a la misma organización y tienen acceso al simulador para pruebas pueden editar la configuración de destino.

## Pasos siguientes {#next-steps}

Al seguir los pasos de este artículo, obtuvo las credenciales de autenticación en Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino. A continuación, puede configurar un destino mediante Destination SDK.

* Lea las siguientes guías de configuración, según el tipo de destino:

   * [Usar Destination SDK para configurar un destino de flujo continuo](guides/configure-destination-instructions.md)
   * [Usar Destination SDK para configurar un destino basado en archivos](guides/configure-file-based-destination-instructions.md)

* Para todas las operaciones, consulte la [Documentación de la API de creación de destino](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Utilice la variable [Recopilación de Postman de la API de creación de destino](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) para configurar el destino mediante los extremos de la API de Destination SDK. Para empezar a usar Postman, consulte la [pasos para importar entornos y colecciones](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) y [guía de vídeo para crear el entorno de Postman](https://video.tv.adobe.com/v/28832).
