---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía para desarrolladores de Privacy Service
description: Utilice la API de RESTful para administrar los datos personales de los sujetos de datos en todas las aplicaciones de Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# [!DNL Privacy Service] guía para desarrolladores

Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario que le permiten administrar (acceder y eliminar) los datos personales de sus usuarios (clientes) en todas las aplicaciones de Adobe Experience Cloud. [!DNL Privacy Service] también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que involucran [!DNL Experience Cloud] aplicaciones.

Esta guía explica cómo utilizar la [!DNL Privacy Service] API. Para obtener más información sobre cómo utilizar la interfaz de usuario, consulte la descripción general [de la interfaz de usuario del](../ui/overview.md)Privacy Service. Para obtener una lista completa de todos los extremos disponibles en la [!DNL Privacy Service] API, consulte la referencia [de la](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Primeros pasos {#getting-started}

Esta guía requiere una comprensión práctica de las siguientes [!DNL Experience Platform] funciones:

* [[!Privacy Service DNL]](../home.md): Proporciona una API de RESTful y una interfaz de usuario que le permiten administrar las solicitudes de acceso y eliminación de los temas de datos (clientes) en todas las aplicaciones de Adobe Experience Cloud.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a la API de Privacy Service.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

## Recopilar valores para encabezados necesarios

Para realizar llamadas a la [!DNL Privacy Service] API, primero debe recopilar sus credenciales de acceso para utilizarlas en los encabezados necesarios:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Esto implica obtener permisos de desarrollador para [!DNL Experience Platform] en Adobe Admin Console y, a continuación, generar las credenciales en Adobe Developer Console.

### Obtenga acceso de desarrollador a [!DNL Experience Platform]

Para obtener acceso de desarrollador a [!DNL Platform], siga los pasos iniciales en el tutorial [de autenticación de](../../tutorials/authentication.md)Experience Platform. Una vez que llegue al paso &quot;Generar credenciales de acceso en Adobe Developer Console&quot;, vuelva a este tutorial para generar las credenciales específicas de [!DNL Privacy Service].

### Generar credenciales de acceso

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Su `{IMS_ORG}` y `{API_KEY}` sólo debe generarse una vez y puede reutilizarse en futuras llamadas de API. Sin embargo, `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se explican detalladamente a continuación.

#### Configuración única

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vacío en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, haga clic en **[!UICONTROL Añadir API]** en la pantalla Información general **[!UICONTROL del]** proyecto.

![](../images/api/getting-started/add-api-button.png)

Aparece la pantalla **[!UICONTROL Añadir una API]** . Seleccione la API **[!UICONTROL de]** Privacy Service en la lista de las API disponibles antes de hacer clic en **[!UICONTROL Siguiente]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Aparece la pantalla **[!UICONTROL Configurar API]** . Seleccione la opción para **[!UICONTROL Generar un par]** de claves y, a continuación, haga clic en **[!UICONTROL Generar par]** de claves en la esquina inferior derecha.

![](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y se descarga un archivo ZIP con una clave privada y un certificado público en el equipo local (para utilizarlo en un paso posterior). Seleccione **[!UICONTROL Guardar API]** configurada para completar la configuración.

![](../images/api/getting-started/key-pair-generated.png)

Una vez que se ha agregado la API al proyecto, la página del proyecto vuelve a aparecer en la página de información general **de la API de** Privacy Service. Desde aquí, desplácese hacia abajo hasta la sección Cuenta **[!UICONTROL de servicio (JWT)]** , que proporciona las siguientes credenciales de acceso requeridas en todas las llamadas a la [!DNL Privacy Service] API:

* **[!UICONTROL ID]** DEL CLIENTE: El ID de cliente es el requerido `{API_KEY}` para ello debe proporcionarse en el encabezado x-api-key.
* **[!UICONTROL ID]** DE ORGANIZACIÓN: El identificador de organización es el `{IMS_ORG}` valor que debe utilizarse en el encabezado x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticación para cada sesión

La credencial requerida final que debe recopilar es la suya `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización. A diferencia de los valores para `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando [!DNL Platform] API.

Para generar una clave nueva `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto situado junto a **[!UICONTROL Generar token de acceso]** antes de hacer clic en **[!UICONTROL Generar token]**.

![](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado de autorización requerido y debe proporcionarse en el formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Pasos siguientes

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la [!DNL Privacy Service] API. El documento sobre trabajos [de](privacy-jobs.md) privacidad recorre las distintas llamadas de API que puede realizar mediante la [!DNL Privacy Service] API. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.
