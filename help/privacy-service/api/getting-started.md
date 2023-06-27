---
title: Autenticación y acceso a la API de Privacy Service
description: Obtenga información sobre cómo autenticarse en la API de Privacy Service y cómo interpretar las llamadas de API de ejemplo en la documentación.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 12%

---

# Autenticación y acceso a la API de Privacy Service

Esta guía proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de Adobe Experience Platform Privacy Service.

## Requisitos previos {#prerequisites}

Esta guía requiere una comprensión práctica de [Privacy Service](../home.md) y cómo le permite administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en las aplicaciones de Adobe Experience Cloud.

Para crear credenciales de acceso para la API, un administrador de su organización debe haber configurado previamente perfiles de producto para un Privacy Service en Adobe Admin Console. El perfil de producto que asigna a una integración de API determina qué permisos tiene la integración al acceder a las funciones de Privacy Service. Consulte la guía de [administración de permisos de Privacy Service](../permissions.md) para obtener más información.

## Recopilar valores para los encabezados obligatorios {#gather-values-required-headers}

Para realizar llamadas a la API de Privacy Service, primero debe recopilar las credenciales de acceso para utilizarlas en los encabezados obligatorios:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Estos valores se generan mediante [Consola de Adobe Developer](https://developer.adobe.com/console). Su `{ORG_ID}` y `{API_KEY}` solo debe generarse una vez y puede reutilizarse en futuras llamadas a la API. Sin embargo, su `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

### Configuración única {#one-time-setup}

Vaya a la [consola de desarrollador de Adobe](https://developer.adobe.com/console) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de la consola de desarrollador.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Agregar al proyecto]** y elija **[!UICONTROL API]** en el menú desplegable.

![La opción API que se está seleccionando en la [!UICONTROL Agregar al proyecto] Menú desplegable de la página de detalles del proyecto en Developer Console](../images/api/getting-started/add-api-button.png)

#### Seleccione la API de Privacy Service {#select-privacy-service-api}

Aparece la pantalla **[!UICONTROL Añadir una API]**. Seleccionar **[!UICONTROL Experience Cloud]** para reducir la lista de API disponibles y, a continuación, seleccione la tarjeta para **[!UICONTROL API de Privacy Service]** antes de seleccionar **[!UICONTROL Siguiente]**.

![La tarjeta de API de Privacy Service que se está seleccionando de la lista de API disponibles](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Seleccione el **[!UICONTROL Ver documentos]** opción para navegar en una ventana separada del explorador para completar el [Documentación de referencia de la API de Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

A continuación, seleccione el tipo de autenticación para generar tokens de acceso y acceder a la API de Privacy Service.

>[!IMPORTANT]
>
>Seleccione el **[!UICONTROL Servidor a servidor OAuth]** , ya que será el único método admitido a partir de ahora. El **[!UICONTROL Cuenta de servicio (JWT)]** El método está obsoleto. Aunque las integraciones que utilizan el método de autenticación JWT seguirán funcionando hasta el 1 de enero de 2025, Adobe recomienda migrar las integraciones existentes al nuevo método de servidor a servidor OAuth antes de esa fecha. Obtenga más información en la sección [!BADGE Obsoleto]{type=negative}[Generar un token web JSON (JWT)](/help/landing/api-authentication.md#jwt).

![Seleccione el método de autenticación de servidor a servidor Oauth.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Asignación de permisos mediante perfiles de producto {#product-profiles}

El paso de configuración final es seleccionar los perfiles de producto desde los que heredará esta integración sus permisos. Si selecciona más de un perfil, sus conjuntos de permisos se combinarán para la integración.

>[!NOTE]
>
Los administradores crean y administran los perfiles de producto y los permisos granulares que proporcionan a través de Adobe Admin Console. Consulte la guía de [Permisos de Privacy Service](../permissions.md) para obtener más información.

Cuando termine, seleccione **[!UICONTROL Guardar API configurada]**.

![Se está seleccionando un solo perfil de producto de la lista antes de guardar la configuración](../images/api/getting-started/select-product-profiles.png)

Una vez añadida la API al proyecto, la variable **[!UICONTROL API de Privacy Service]** Esta página del proyecto muestra las siguientes credenciales, necesarias en todas las llamadas a las API de Privacy Service:

* `{API_KEY}` ([!UICONTROL ID del cliente])
* `{ORG_ID}` ([!UICONTROL ID de organización])

![Información de integración después de agregar una API en Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Autenticación para cada sesión {#authentication-each-session}

La credencial final necesaria que debe recopilar es su `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización. A diferencia de los valores para `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para seguir utilizando la API.

En general, hay dos métodos para generar un token de acceso:

* [Generar el token manualmente](#manual-token) para pruebas y desarrollo.
* [Automatización de la generación de tokens](#auto-token) para integraciones de API.

#### Generación manual de un token {#manual-token}

Para generar manualmente una nueva `{ACCESS_TOKEN}`, vaya a **[!UICONTROL Credenciales]** > **[!UICONTROL Servidor a servidor OAuth]** y seleccione **[!UICONTROL Generar token de acceso]**, como se muestra a continuación.

![Grabación de pantalla de cómo se genera un token de acceso en la interfaz de usuario de Developer Console.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado [!DNL Authorization] requerido y debe proporcionarse con el formato `Bearer {ACCESS_TOKEN}`.

#### Automatización de la generación de tokens {#auto-token}

También puede utilizar un entorno y una colección de Postman para generar tokens de acceso. Para obtener más información, lea la sección sobre [uso de Postman para autenticar y probar llamadas a la API](/help/landing/api-authentication.md#use-postman) en la guía de autenticación de API de Experience Platform.

## Leer llamadas de API de muestra {#read-sample-api-calls}

Cada guía de extremo proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Platform.

## Pasos siguientes {#next-steps}

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API de Privacy Service. Seleccione una de las guías de extremos para empezar:

* [Trabajos de privacidad](./privacy-jobs.md)
* [Consentimiento](./consent.md)
