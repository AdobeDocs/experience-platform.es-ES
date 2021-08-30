---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Guía de API del Privacy Service
description: La API de Privacy Service permite a los desarrolladores crear y administrar solicitudes de clientes para acceder a sus datos personales o eliminarlos en todas las aplicaciones de Experience Cloud, de conformidad con las normas legales de privacidad. Siga esta guía para aprender a realizar operaciones clave con la API.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 16%

---

# Guía de la API de [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario que le permiten administrar (acceder y eliminar) los datos personales de sus interesados (clientes) en todas las aplicaciones de Adobe Experience Cloud. [!DNL Privacy Service] también proporciona un mecanismo central de auditoría y registro que le permite acceder al estado y los resultados de los trabajos que implican  [!DNL Experience Cloud] aplicaciones.

Esta guía explica cómo utilizar la API [!DNL Privacy Service]. Para obtener más información sobre cómo utilizar la IU, consulte la [descripción general de la IU del Privacy Service](../ui/overview.md). Para obtener una lista completa de todos los extremos disponibles en la API [!DNL Privacy Service], consulte la [referencia de API](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Primeros pasos {#getting-started}

Esta guía requiere comprender bien las siguientes funciones de [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../home.md): Proporciona una API de RESTful y una interfaz de usuario que le permiten administrar las solicitudes de acceso y eliminación de sus interesados (clientes) en todas las aplicaciones de Adobe Experience Cloud.

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas correctamente a la API de Privacy Service.

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md) en la guía de solución de problemas [!DNL Experience Platform].

## Recopilar valores para encabezados necesarios

Para realizar llamadas a la API [!DNL Privacy Service] , primero debe recopilar sus credenciales de acceso para utilizarlas en los encabezados necesarios:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Esto implica obtener permisos de desarrollador para [!DNL Experience Platform] en Adobe Admin Console y luego generar las credenciales en Adobe Developer Console.

### Obtener acceso del desarrollador a [!DNL Experience Platform]

Para obtener acceso del desarrollador a [!DNL Platform], siga los pasos iniciales en el [tutorial de autenticación del Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Una vez que llegue al paso &quot;Generar credenciales de acceso en Adobe Developer Console&quot;, vuelva a este tutorial para generar las credenciales específicas de [!DNL Privacy Service].

### Generar credenciales de acceso

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Los `{IMS_ORG}` y `{API_KEY}` solo deben generarse una vez y pueden reutilizarse en futuras llamadas de API. Sin embargo, el `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

#### Configuración única

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Agregar API]** en la pantalla **[!UICONTROL Información general del proyecto]**.

![](../images/api/getting-started/add-api-button.png)

Aparece la pantalla **[!UICONTROL Añadir una API]**. Seleccione **[!UICONTROL API de Privacy Service]** de la lista de API disponibles antes de seleccionar **[!UICONTROL Siguiente]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Aparece la pantalla **[!UICONTROL Configure API]**. Seleccione la opción **[!UICONTROL Generate a key pair]** y, a continuación, seleccione **[!UICONTROL Generate keypair]** en la esquina inferior derecha.

![](../images/api/getting-started/generate-key-pair.png)

El par de claves se genera automáticamente y se descarga un archivo ZIP que contiene una clave privada y un certificado público en el equipo local (para utilizarlo en un paso posterior). Seleccione **[!UICONTROL Guardar API configurada]** para completar la configuración.

![](../images/api/getting-started/key-pair-generated.png)

Una vez añadida la API al proyecto, la página del proyecto vuelve a aparecer en la página **información general de la API del Privacy Service**. Desde aquí, desplácese hacia abajo hasta la sección **[!UICONTROL Cuenta de servicio (JWT)]**, que proporciona las siguientes credenciales de acceso necesarias en todas las llamadas a la API de [!DNL Privacy Service]

* **[!UICONTROL ID]** DE CLIENTE: El ID de cliente es el necesario  `{API_KEY}` para el que debe proporcionarse en el encabezado x-api-key.
* **[!UICONTROL ID DE ORGANIZACIÓN]**: El ID de organización es el  `{IMS_ORG}` valor que debe utilizarse en el encabezado x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticación para cada sesión

La credencial requerida final que debe recopilar es su `{ACCESS_TOKEN}`, que se utiliza en el encabezado Autorización. A diferencia de los valores de `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando las API [!DNL Platform].

Para generar un nuevo `{ACCESS_TOKEN}`, abra la clave privada descargada anteriormente y pegue su contenido en el cuadro de texto junto a **[!UICONTROL Generate access token]** antes de seleccionar **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado de Autorización requerido y debe proporcionarse con el formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Pasos siguientes

Ahora que comprende qué encabezados utilizar, está listo para empezar a realizar llamadas a la API [!DNL Privacy Service]. El documento sobre [trabajos de privacidad](privacy-jobs.md) analiza las distintas llamadas de API que puede realizar mediante la API [!DNL Privacy Service]. Cada llamada de ejemplo incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.
