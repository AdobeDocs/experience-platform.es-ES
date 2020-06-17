---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de Privacy Service
description: Utilice la API de RESTful para administrar los datos personales de los sujetos de datos en las aplicaciones de Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 6f93191defad6a79a3f6623da3492ab405787b5c
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Guía para desarrolladores de Privacy Service

Adobe Experience Platform Privacy Service proporciona una API RESTful y una interfaz de usuario que le permiten administrar (acceder y eliminar) los datos personales de los usuarios (clientes) en todas las aplicaciones de Adobe Experience Cloud. Privacy Service también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que involucran aplicaciones Experience Cloud.

Esta guía explica cómo utilizar la API de Privacy Service. Para obtener más información sobre cómo utilizar la interfaz de usuario, consulte la descripción general [de la interfaz de usuario del](../ui/overview.md)Privacy Service. Para obtener una lista completa de todos los extremos disponibles en la API de Privacy Service, consulte la referencia [de la](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Primeros pasos

Esta guía requiere una comprensión práctica de las siguientes funciones del Experience Platform:

* [Privacy Service](../home.md): Proporciona una API de RESTful y una interfaz de usuario que le permiten administrar las solicitudes de acceso y eliminación de los temas de datos (clientes) en todas las aplicaciones de Adobe Experience Cloud.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a la API de Privacy Service.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md) de API de ejemplo en la guía de solución de problemas del Experience Platform.

## Recopilar valores para encabezados necesarios

Para realizar llamadas a la API de Privacy Service, primero debe recopilar las credenciales de acceso para utilizarlas en los encabezados necesarios:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Esto implica obtener permisos de desarrollador para Experience Platform en Adobe Admin Console y, a continuación, generar las credenciales en Adobe Developer Console.

### Obtener acceso del desarrollador al Experience Platform

Para obtener acceso de desarrollador a Platform, siga los pasos iniciales en el tutorial [de autenticación de](../../tutorials/authentication.md)Experience Platform. Una vez que llegue al paso &quot;Generar credenciales de acceso en Adobe Developer Console&quot;, vuelva a este tutorial para generar las credenciales específicas de Privacy Service.

### Generar credenciales de acceso

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Su `{IMS_ORG}` y `{API_KEY}` sólo debe generarse una vez y puede reutilizarse en futuras llamadas de API. Sin embargo, `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se explican detalladamente a continuación.

#### Configuración única

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vacío en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, haga clic en **[!UICONTROL Añadir API]** en la pantalla Información general _[!UICONTROL del]_proyecto.

![](../images/api/getting-started/add-api-button.png)

Aparece la pantalla _[!UICONTROL Añadir una API]_. Seleccione la API**[!UICONTROL  de ]**Privacy Service en la lista de las API disponibles antes de hacer clic en**[!UICONTROL  Siguiente ]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Aparece la pantalla _[!UICONTROL Configurar API]_. Seleccione la opción para**[!UICONTROL  Generar un par ]**de claves y, a continuación, haga clic en**[!UICONTROL  Generar par ]**de claves en la esquina inferior derecha.

![](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y se descarga un archivo ZIP con una clave privada y un certificado público en el equipo local (para utilizarlo en un paso posterior). Seleccione **[!UICONTROL Guardar API]** configurada para completar la configuración.

![](../images/api/getting-started/key-pair-generated.png)

Una vez que se ha agregado la API al proyecto, la página del proyecto vuelve a aparecer en la página de información general _de la API de_ Privacy Service. Desde aquí, desplácese hacia abajo hasta la sección Cuenta _[!UICONTROL de servicio (JWT)]_, que proporciona las siguientes credenciales de acceso requeridas en todas las llamadas a la API de Privacy Service:

* **[!UICONTROL ID]** DEL CLIENTE: El ID de cliente es el requerido `{API_KEY}` para ello debe proporcionarse en el encabezado x-api-key.
* **[!UICONTROL ID]** DE ORGANIZACIÓN: El identificador de organización es el `{IMS_ORG}` valor que debe utilizarse en el encabezado x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticación para cada sesión

La credencial requerida final que debe recopilar es la suya `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización. A diferencia de los valores para `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando las API de Platform.

Para generar una clave nueva `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto situado junto a _[!UICONTROL Generar token de acceso]_antes de hacer clic en**[!UICONTROL  Generar token ]**.

![](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado de autorización requerido y debe proporcionarse en el formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Pasos siguientes

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API de Privacy Service. El documento sobre trabajos [de](privacy-jobs.md) privacidad recorre las distintas llamadas de API que puede realizar mediante la API de Privacy Service. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.
