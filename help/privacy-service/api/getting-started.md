---
title: Introducción a la API de Privacy Service
description: Obtenga información sobre cómo autenticarse en la API de Privacy Service y cómo interpretar las llamadas de API de ejemplo en la documentación.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 6dcbf2df46ba35104abd9c4e6412799e77c9c49f
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 13%

---

# Introducción a la API de Privacy Service

Esta guía proporciona una introducción a los conceptos principales que debe conocer antes de intentar realizar llamadas a la API de Privacy Service.

## Requisitos previos

Esta guía requiere comprender las siguientes funciones:

* [Adobe Experience Platform Privacy Service](../home.md): Proporciona una API de RESTful y una interfaz de usuario que le permiten administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en todas las aplicaciones de Adobe Experience Cloud.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a la API de Privacy Service, primero debe recopilar las credenciales de acceso para utilizarlas en los encabezados necesarios:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Esto implica obtener permisos de desarrollador para Adobe Experience Platform en Adobe Admin Console y luego generar las credenciales en Adobe Developer Console.

### Obtener acceso de desarrollador a Experience Platform

Para obtener acceso de los desarrolladores a [!DNL Platform], siga los pasos iniciales en la [tutorial de autenticación de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Una vez que llegue al paso &quot;Generar credenciales de acceso en Adobe Developer Console&quot;, vuelva a este tutorial para generar las credenciales específicas del Privacy Service.

### Generar credenciales de acceso

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Su `{IMS_ORG}` y `{API_KEY}` solo debe generarse una vez y puede reutilizarse en futuras llamadas de API. Sin embargo, su `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

#### Configuración única

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial en [creación de un proyecto vacío](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Añadir API]** en el **[!UICONTROL Información general del proyecto]** en el Navegador.

![](../images/api/getting-started/add-api-button.png)

Aparece la pantalla **[!UICONTROL Añadir una API]**. Select **[!UICONTROL API de Privacy Service]** de la lista de API disponibles antes de seleccionar **[!UICONTROL Siguiente]**.

![](../images/api/getting-started/add-privacy-service-api.png)

La variable **[!UICONTROL Configuración de API]** se abre. Seleccione la opción para **[!UICONTROL Generación de un par de claves]** y, a continuación, seleccione **[!UICONTROL Generar par de teclas]** en la esquina inferior derecha.

![](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y se descarga un archivo ZIP que contiene una clave privada y un certificado público en el equipo local (para utilizarlo en un paso posterior). Select **[!UICONTROL Guardar la API configurada]** para completar la configuración.

![](../images/api/getting-started/key-pair-generated.png)

Una vez añadida la API al proyecto, la página del proyecto vuelve a aparecer en la página **Información general sobre la API de Privacy Service** página. Desde aquí, desplácese hacia abajo hasta el **[!UICONTROL Cuenta de servicio (JWT)]** , que proporciona las siguientes credenciales de acceso que son necesarias en todas las llamadas a la API de Privacy Service:

* **[!UICONTROL ID DE CLIENTE]**: El ID del cliente es el `{API_KEY}` para esto debe proporcionarse en el encabezado x-api-key.
* **[!UICONTROL ID DE ORGANIZACIÓN]**: El ID de organización es la variable `{IMS_ORG}` que debe utilizarse en el encabezado x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticación para cada sesión

La última credencial requerida que debe recopilar es su `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización . A diferencia de los valores de `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para seguir utilizando [!DNL Platform] API.

Para generar un nuevo `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto situado junto a **[!UICONTROL Generar token de acceso]** antes de seleccionar **[!UICONTROL Generar token]**.

![](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado de Autorización requerido y debe proporcionarse con el formato . `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/api-guide.md#sample-api) en la guía de introducción para las API de Platform.

## Pasos siguientes

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API de Privacy Service. Seleccione una de las guías de punto final para empezar:

* [Trabajos de privacidad](./privacy-jobs.md)
* [Consentimiento](./consent.md)
