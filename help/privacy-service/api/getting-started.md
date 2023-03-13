---
title: Introducción a la API de Privacy Service
description: Obtenga información sobre cómo autenticarse en la API de Privacy Service y cómo interpretar las llamadas de API de ejemplo en la documentación.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# Introducción a la API de Privacy Service

Esta guía proporciona una introducción a los conceptos principales que necesita conocer antes de intentar realizar llamadas a la API de Adobe Experience Platform Privacy Service.

## Requisitos previos

Esta guía requiere una comprensión práctica de [Privacy Service](../home.md) y cómo le permite administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en las aplicaciones de Adobe Experience Cloud.

Para crear credenciales de acceso para la API, un administrador de su organización debe haber configurado previamente perfiles de producto para un Privacy Service en Adobe Admin Console. El perfil de producto que asigna a una integración de API determina qué permisos tiene la integración al acceder a las funciones de Privacy Service. Consulte la guía de [administración de permisos de Privacy Service](../permissions.md) para obtener más información.

## Recopilar valores para los encabezados obligatorios

Para realizar llamadas a la API de Privacy Service, primero debe recopilar las credenciales de acceso para utilizarlas en los encabezados obligatorios:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Estos valores se generan mediante [Consola de Adobe Developer](https://developer.adobe.com/console). Su `{ORG_ID}` y `{API_KEY}` solo debe generarse una vez y puede reutilizarse en futuras llamadas a la API. Sin embargo, su `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

### Configuración única

Vaya a la [consola de desarrollador de Adobe](https://developer.adobe.com/console) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de la consola de desarrollador.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Agregar al proyecto]** y elija **[!UICONTROL API]** en el menú desplegable.

![La opción API que se está seleccionando en la [!UICONTROL Agregar al proyecto] Menú desplegable de la página de detalles del proyecto en Developer Console](../images/api/getting-started/add-api-button.png)

#### Seleccione una API y genere un par de claves {#keypair}

Aparece la pantalla **[!UICONTROL Añadir una API]**. Seleccionar **[!UICONTROL Experience Cloud]** para reducir la lista de API disponibles y, a continuación, seleccione la tarjeta para **[!UICONTROL API de Privacy Service]** antes de seleccionar **[!UICONTROL Siguiente]**.

![La tarjeta de API de Privacy Service que se está seleccionando de la lista de API disponibles](../images/api/getting-started/add-privacy-service-api.png)

El **[!UICONTROL Configurar API]** aparece la pantalla. Seleccione la opción para **[!UICONTROL Generación de un par de claves]**, luego seleccione **[!UICONTROL Generar par de claves]**.

![El [!UICONTROL Generación de un par de claves] opción que se está seleccionando en la [!UICONTROL Configurar API] pantalla](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y el explorador descarga un archivo ZIP que contiene una clave privada y un certificado público (que se utilizará en un paso posterior). Haga clic en **[!UICONTROL Siguiente]** para continuar.

![El par de claves generado que se muestra en la interfaz de usuario, cuyos valores descarga automáticamente el explorador](../images/api/getting-started/key-pair-generated.png)

#### Asignación de permisos mediante perfiles de producto {#product-profiles}

El paso de configuración final es seleccionar los perfiles de producto desde los que heredará esta integración sus permisos. Si selecciona más de un perfil, sus conjuntos de permisos se combinarán para la integración.

>[!NOTE]
>
>Los administradores crean y administran los perfiles de producto y los permisos granulares que proporcionan a través de Adobe Admin Console. Consulte la guía de [Permisos de Privacy Service](../permissions.md) para obtener más información.

Cuando termine, seleccione **[!UICONTROL Guardar API configurada]**.

![Se está seleccionando un solo perfil de producto de la lista antes de guardar la configuración](../images/api/getting-started/select-product-profiles.png)

Una vez añadida la API al proyecto, la página del proyecto vuelve a aparecer en el **Información general de API de Privacy Service** página. Desde aquí, desplácese hacia abajo hasta el **[!UICONTROL Cuenta de servicio (JWT)]** , que proporciona las siguientes credenciales de acceso necesarias en todas las llamadas a la API de Privacy Service:

* **[!UICONTROL ID DE CLIENTE]**: el ID de cliente es el requerido `{API_KEY}` que debe proporcionarse en la variable `x-api-key` encabezado.
* **[!UICONTROL ID DE ORGANIZACIÓN]**: El ID de organización es el valor de `{ORG_ID}` que debe utilizarse en el encabezado de `x-gw-ims-org-id`.

![Los valores ID de cliente e ID de organización tal como aparecen en la página de información general del proyecto después de configurar la API](../images/api/getting-started/jwt-credentials.png)

### Autenticación para cada sesión

La credencial final necesaria que debe recopilar es su `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización. A diferencia de los valores para `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para seguir utilizando la API.

En general, hay dos métodos para generar un token de acceso:

* [Generar el token manualmente](#manual-token) para pruebas y desarrollo.
* [Automatización de la generación de tokens](#auto-token) para integraciones de API.

#### Generación manual de un token {#manual-token}

Para generar manualmente una nueva `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto situado junto a **[!UICONTROL Generar token de acceso]** antes de seleccionar **[!UICONTROL Generar token]**.

![El token de acceso generado anteriormente se pega en la página de información general del proyecto, con el [!UICONTROL Generar token] botón seleccionado después de](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado Autorización requerido y debe proporcionarse con el formato `Bearer {ACCESS_TOKEN}`.

![El token de acceso generado que se copia desde la interfaz de usuario](../images/api/getting-started/generated-access-token.png)

#### Automatización de la generación de tokens {#auto-token}

Puede generar nuevos tokens de acceso para procesos automatizados enviando un token web JSON (JWT) mediante una solicitud del POST al servicio Identity Management de Adobe (IMS). Consulte el documento de Developer Console sobre [Autenticación JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para ver los pasos detallados.

## Leer llamadas de API de muestra

Cada guía de extremo proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Platform.

## Pasos siguientes

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API de Privacy Service. Seleccione una de las guías de extremos para empezar:

* [Trabajos de privacidad](./privacy-jobs.md)
* [Consentimiento](./consent.md)
