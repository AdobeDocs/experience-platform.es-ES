---
keywords: Experience Platform;introducción;ai de contenido;ai de comercio;ai de contenido y comercio
solution: Experience Platform
title: Introducción a Content and Commerce AI
description: La API de contenido y comercio utiliza API de Adobe I/O. Para realizar llamadas a las API de Adobe I/O y a la integración de la consola de E/S, primero debe completar el tutorial de autenticación.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Introducción a Content and Commerce AI

>[!NOTE]
>
>La API de contenido y comercio está en fase beta. La documentación está sujeta a cambios.

[!DNL Content and Commerce AI] utiliza las API de Adobe I/O. Para realizar llamadas a las API de Adobe I/O y a la integración de la consola de E/S, primero debe completar la [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

Sin embargo, cuando llegue al **Añadir API** , la API se encuentra en Experience Cloud en lugar de en Adobe Experience Platform, como se muestra en la siguiente captura de pantalla:

![adición de contenido y Commerce AI](./images/add-api.png)

Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Adobe I/O, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Crear un entorno de Postman (opcional)

Una vez configurado el proyecto y la API en la consola de Adobe Developer, tiene la opción de descargar un archivo de entorno para Postman. En **[!UICONTROL API]** en el carril izquierdo del proyecto, seleccione **[!UICONTROL AI de contenido y comercio]**. Se abre una nueva pestaña que contiene una tarjeta etiquetada como &quot;[!DNL Try it out]&quot;. Select **Descargar para Postman** para descargar un archivo JSON utilizado para configurar el entorno de postman.

![descargar para postman](./images/add-to-postman.png)

Una vez descargado el archivo, abra Postman y seleccione la opción **icono de engranaje** en la parte superior derecha para abrir el **administrar entornos** diálogo.

![icono de engranaje](./images/select-gear-icon.png)

A continuación, seleccione **Importar** desde el **Administrar entornos** diálogo.

![importar](./images/import.png)

Se le redirige y se le pide que seleccione un archivo de entorno del equipo. Seleccione el archivo JSON que descargó anteriormente y, a continuación, seleccione **Apertura** para cargar el entorno.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Se le redirige de nuevo a la función *Administrar entornos* con un nuevo nombre de entorno rellenado. Seleccione el nombre del entorno para ver y editar las variables disponibles en Postman. Sigue siendo necesario rellenar manualmente la variable `JWT_TOKEN` y `ACCESS_TOKEN`. Estos valores deberían haberse obtenido al completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Una vez completadas, las variables deberían tener un aspecto similar a la captura de pantalla siguiente. Select **Actualizar** para finalizar la configuración de su entorno.

![](./images/final-environment.png)

Ahora puede seleccionar su entorno en el menú desplegable de la esquina superior derecha y rellenar automáticamente los valores guardados. Simplemente vuelva a editar los valores en cualquier momento para actualizar todas las llamadas de API.

![ejemplo](./images/select-environment.png)

Para obtener más información sobre cómo trabajar con las API de Adobe I/O mediante Postman, consulte la publicación Media en [uso de Postman para la autenticación JWT en el Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas del Experience Platform.

## Pasos siguientes {#next-steps}

Una vez que tenga todas las credenciales, estará listo para configurar un programa de trabajo personalizado para [!DNL Content and Commerce AI]. Los siguientes documentos ayudan a comprender el marco de extensibilidad y la configuración del entorno.

Para obtener más información sobre el marco de extensibilidad, comience leyendo el [introducción a la extensibilidad](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) documento. Este documento describe los requisitos previos y los requisitos de aprovisionamiento.

Para obtener más información sobre la configuración de un entorno para [!DNL Content and Commerce AI], comience leyendo la guía de [configuración de un entorno de desarrollador](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Este documento proporciona instrucciones de configuración que le permiten desarrollar para el servicio de Asset compute.
