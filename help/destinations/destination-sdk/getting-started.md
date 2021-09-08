---
description: En esta página se describe cómo autenticarse y empezar a utilizar el SDK de destino de Adobe Experience Platform. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino.
title: Introducción al SDK de destino
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Primeros pasos

## Información general {#overview}

En esta página se describe cómo autenticarse y empezar a utilizar el SDK de destino de Adobe Experience Platform. Incluye instrucciones sobre cómo obtener las credenciales de autenticación de Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino.

## Terminología {#terminology}

Esta guía utiliza conceptos específicos de la plataforma, como organización de IMS y entornos limitados. Consulte el [glosario del Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) para ver las definiciones de estos y otros términos.

## Obtenga las credenciales de autenticación necesarias {#obtain-authentication-credentials}

El SDK de destino utiliza la puerta de enlace [Adobe I/O](https://www.adobe.io/) para la autenticación. Para realizar llamadas de API a puntos finales de SDK de destino, debe proporcionar ciertos encabezados en las llamadas de API. Trabaje con el equipo de Adobe Exchange para configurar la autenticación en la [Consola del desarrollador de Adobe](http://console.adobe.io/).

Para realizar llamadas correctamente a puntos finales de API de SDK de destino, siga el [tutorial de autenticación de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Inicie el tutorial desde el paso &quot;[Generate an API key, IMS Org ID y client secret](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. El equipo de Adobe Exchange se encargará de los pasos anteriores. Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API del SDK de destino, como se muestra a continuación:

* `x-api-key: {API_KEY}`, también denominado ID de cliente
* `x-gw-ims-org-id: {IMS_ORG}`, también denominado ID de organización
* `Authorization: Bearer {ACCESS_TOKEN}`. El token de acceso tiene una caducidad de 24 horas, expresada en milisegundos, por lo que tendrá que actualizarlo. Para actualizar el token de acceso, repita los pasos descritos en el tutorial de autenticación.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propiedad de destino y entornos limitados {#destination-ownership}

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Las solicitudes al SDK de destino requieren encabezados que especifican el nombre del simulador para pruebas en el que se realiza la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

El equipo de Adobe Exchange le proporciona su nombre de simulador de pruebas, que debe utilizar en llamadas a los extremos de la API del SDK de destino.

## Control de acceso basado en roles (RBAC) {#rbac}

Para utilizar los extremos de la API del SDK de destino descritos en la [documentación de referencia](./configuration-options.md), necesita el permiso de control de acceso **[!UICONTROL Destination Authoring]**. Trabaje con el equipo de Adobe Exchange para obtener este permiso asignado en [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permiso de creación de destino](./assets/destination-authoring-permission.png)

Para obtener más información, lea los siguientes documentos de Control de acceso del Experience Platform:

* [Administrar permisos para un perfil de producto](/help/access-control/ui/permissions.md)
* [Permisos disponibles para el Experience Platform](/help/access-control/home.md#permissions)
* [Documentación de Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html)

## Consideraciones adicionales {#additional-considerations}

* Cualquier cambio que realice en las configuraciones de destino, tanto si crea como si edita una configuración de destino, debe revisarse y aprobarse por Adobe. Los cambios solo se reflejan en los destinos una vez que se haya realizado la revisión.
* Solo los usuarios que pertenecen a la misma organización y tienen acceso al simulador para pruebas pueden editar la configuración de destino.

## Pasos siguientes {#next-steps}

Al seguir los pasos de este artículo, obtuvo las credenciales de autenticación en Adobe I/O, un nombre de simulador de pruebas y el permiso de control de acceso de creación de destino. A continuación, puede configurar un destino mediante el SDK de destino. Lea [Use el SDK de destino para configurar su destino](./configure-destination-instructions.md) para los pasos siguientes.
