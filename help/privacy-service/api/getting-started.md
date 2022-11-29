---
title: Introducción a la API de Privacy Service
description: Obtenga información sobre cómo autenticarse en la API de Privacy Service y cómo interpretar las llamadas de API de ejemplo en la documentación.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# Introducción a la API de Privacy Service

Esta guía proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de Adobe Experience Platform Privacy Service.

## Requisitos previos

Esta guía requiere una comprensión práctica de [Privacy Service](../home.md) y cómo le permite administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en todas las aplicaciones de Adobe Experience Cloud.

Para crear credenciales de acceso para la API, un administrador de su organización debe haber configurado previamente perfiles de producto para el Privacy Service en Adobe Admin Console. El perfil de producto que asigna a una integración de API determina qué permisos tiene esa integración al acceder a las funcionalidades de Privacy Service. Consulte la guía de [administración de permisos de Privacy Service](../permissions.md) para obtener más información.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a la API de Privacy Service, primero debe recopilar las credenciales de acceso para utilizarlas en los encabezados necesarios:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Estos valores se generan mediante [Consola de Adobe Developer](https://developer.adobe.com/console). Su `{ORG_ID}` y `{API_KEY}` solo debe generarse una vez y puede reutilizarse en futuras llamadas de API. Sin embargo, su `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

### Configuración única

Vaya a la [consola de desarrollador de Adobe](https://developer.adobe.com/console) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de la consola de desarrollador.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Agregar a proyecto]** y elija **[!UICONTROL API]** en el menú desplegable.

![La opción API que se está seleccionando en la sección [!UICONTROL Agregar a proyecto] lista desplegable de la página de detalles del proyecto en Developer Console](../images/api/getting-started/add-api-button.png)

#### Seleccione una API y genere un par de claves {#keypair}

Aparece la pantalla **[!UICONTROL Añadir una API]**. Select **[!UICONTROL Experience Cloud]** para reducir la lista de API disponibles, seleccione la tarjeta para **[!UICONTROL API de Privacy Service]** antes de seleccionar **[!UICONTROL Siguiente]**.

![La tarjeta de API del Privacy Service que se selecciona en la lista de API disponibles](../images/api/getting-started/add-privacy-service-api.png)

La variable **[!UICONTROL Configuración de API]** se abre. Seleccione la opción para **[!UICONTROL Generación de un par de claves]** y, a continuación, seleccione **[!UICONTROL Generar par de teclas]**.

![La variable [!UICONTROL Generación de un par de claves] que se selecciona en la [!UICONTROL Configuración de API] pantalla](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y el explorador descarga un archivo ZIP que contiene una clave privada y un certificado público (para utilizarlo en un paso posterior). Haga clic en **[!UICONTROL Siguiente]** para continuar.

![El par de claves generado que se muestra en la interfaz de usuario, cuyos valores el explorador descarga automáticamente](../images/api/getting-started/key-pair-generated.png)

#### Asignación de permisos a través de perfiles de producto {#product-profiles}

El paso de configuración final es seleccionar los perfiles de producto de los que esta integración heredará sus permisos. Si selecciona más de un perfil, sus conjuntos de permisos se combinarán para la integración.

>[!NOTE]
>
>Los perfiles de producto y los permisos granulares que proporcionan los crean y administran los administradores a través de Adobe Admin Console. Consulte la guía de [Permisos del Privacy Service](../permissions.md) para obtener más información.

Cuando termine, seleccione **[!UICONTROL Guardar la API configurada]**.

![Un solo perfil de producto seleccionado de la lista antes de guardar la configuración](../images/api/getting-started/select-product-profiles.png)

Una vez añadida la API al proyecto, la página del proyecto vuelve a aparecer en la página **Información general sobre la API de Privacy Service** página. Desde aquí, desplácese hacia abajo hasta el **[!UICONTROL Cuenta de servicio (JWT)]** , que proporciona las siguientes credenciales de acceso que son necesarias en todas las llamadas a la API de Privacy Service:

* **[!UICONTROL ID DE CLIENTE]**: El ID del cliente es el `{API_KEY}` que debe incluirse en la `x-api-key` encabezado.
* **[!UICONTROL ID DE ORGANIZACIÓN]**: El ID de organización es el valor de `{ORG_ID}` que debe utilizarse en el encabezado de `x-gw-ims-org-id`.

![Los valores ID de cliente e ID de organización tal como aparecen en la página de información general del proyecto después de configurar la API](../images/api/getting-started/jwt-credentials.png)

### Autenticación para cada sesión

La última credencial requerida que debe recopilar es su `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización . A diferencia de los valores de `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para continuar usando la API.

En general, existen dos métodos para generar un token de acceso:

* [Generar el token manualmente](#manual-token) para pruebas y desarrollo.
* [Automatizar la generación de tokens](#auto-token) para integraciones de API.

#### Generación manual de un token {#manual-token}

Para generar manualmente un nuevo `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto situado junto a **[!UICONTROL Generar token de acceso]** antes de seleccionar **[!UICONTROL Generar token]**.

![El token de acceso generado anteriormente se pega en la página de información general del proyecto, con la variable [!UICONTROL Generar token] botón seleccionado después de](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado de Autorización requerido y debe proporcionarse con el formato . `Bearer {ACCESS_TOKEN}`.

![Token de acceso generado que se copia desde la interfaz de usuario](../images/api/getting-started/generated-access-token.png)

#### Automatizar la generación de tokens {#auto-token}

Puede generar nuevos tokens de acceso para procesos automatizados enviando un token web JSON (JWT) a través de una solicitud del POST al servicio de Identity Management de Adobe (IMS). Consulte el documento de Developer Console en [Autenticación JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para ver los pasos detallados.

## Leer llamadas de API de ejemplo

Cada guía de extremo proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Platform.

## Pasos siguientes

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API de Privacy Service. Seleccione una de las guías de punto final para empezar:

* [Trabajos de privacidad](./privacy-jobs.md)
* [Consentimiento](./consent.md)
