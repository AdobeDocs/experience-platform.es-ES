---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Introducción a Content and Commerce AI
topic: Getting started
description: Content and Commerce AI utiliza las API de E/S de Adobe. Para realizar llamadas a las API de E/S de Adobe y a la integración de la consola de E/S, primero debe completar el tutorial de autenticación.
translation-type: tm+mt
source-git-commit: 2be04547b96e1a6c293cc63e782fe1b3259619ba
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Introducción a Content and Commerce AI

>[!NOTE]
>
>Content and Commerce AI está en versión beta. La documentación está sujeta a cambios.

[!DNL Content and Commerce AI] utiliza API de E/S de Adobe. Para realizar llamadas a las API de E/S de Adobe y a la integración de la consola de E/S, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación.

Sin embargo, cuando llega al paso **Añadir API** , la API se encuentra en Experience Cloud en lugar de Adobe Experience Platform, como se muestra en la siguiente captura de pantalla:

![adición de contenido y comercio AI](./images/add-api.png)

Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de E/S de Adobe, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Creación de un entorno Postman (opcional)

Una vez configurado el proyecto y la API en Adobe Developer Console, tiene la opción de descargar un archivo entorno para Postman. En **[!UICONTROL API]** , en el carril izquierdo del proyecto, seleccione **[!UICONTROL Contenido y comercio AI]**. Se abre una nueva ficha que contiene una tarjeta con la etiqueta &quot;[!DNL Try it out]&quot;. Seleccione **Descargar para Postman** para descargar un archivo JSON utilizado para configurar el entorno de postman.

![descargar para postman](./images/add-to-postman.png)

Una vez descargado el archivo, abra Postman y seleccione el icono **de** engranaje en la parte superior derecha para abrir el cuadro de diálogo **administrar entornos** .

![icono de engranaje](./images/select-gear-icon.png)

A continuación, seleccione **Importar** desde el cuadro de diálogo **Administrar entornos** .

![importar](./images/import.png)

Se le redirige y se le solicita que seleccione un archivo entorno del equipo. Seleccione el archivo JSON que descargó anteriormente y, a continuación, seleccione **Abrir** para cargar el entorno.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Se le redirige a la ficha *Administrar entornos* con un nuevo nombre de entorno relleno. Seleccione el nombre del entorno que desea vista y edite las variables disponibles en Postman. Aún necesita rellenar manualmente el `JWT_TOKEN` y `ACCESS_TOKEN`. Estos valores deberían haberse obtenido al completar el tutorial [](../../tutorials/authentication.md)de autenticación.

![](./images/re-direct.png)

Una vez completadas, las variables deben tener un aspecto similar al de la captura de pantalla de abajo. Seleccione **Actualizar** para finalizar la configuración del entorno.

![](./images/final-environment.png)

Ahora puede seleccionar el entorno en el menú desplegable de la esquina superior derecha y rellenar automáticamente los valores guardados. Simplemente vuelva a editar los valores en cualquier momento para actualizar todas las llamadas de API.

![ejemplo](./images/select-environment.png)

Para obtener más información sobre el trabajo con las API de E/S de Adobe mediante Postman, consulte la publicación Media sobre el [uso de Postman para la autenticación JWT en E/S](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)de Adobe.

## Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Pasos siguientes {#next-steps}

Una vez que tenga todas las credenciales, estará listo para configurar un programa de trabajo personalizado para [!DNL Content and Commerce AI]. Los siguientes documentos ayudan a comprender el marco de extensibilidad y la configuración del entorno.

Para obtener más información sobre el inicio de extensibilidad, lea la [introducción al documento de extensibilidad](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . Este documento describe los requisitos previos y los requisitos de aprovisionamiento.

Para obtener más información sobre la configuración de un entorno para [!DNL Content and Commerce AI], lea la guía para [configurar un entorno](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)para desarrolladores. Este documento proporciona instrucciones de configuración que le permiten desarrollar el servicio de Asset compute.