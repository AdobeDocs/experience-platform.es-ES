---
title: Información general sobre la extensión de SDK web de Adobe Experience Platform
description: Obtenga información sobre la extensión del SDK web de Adobe Experience Platform para Adobe Experience Platform Launch
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: b70fe5f3a4de2501730cc799125a7181b61186c0
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 19%

---

# Información general sobre la extensión de SDK web de Adobe Experience Platform

La extensión del SDK web de Adobe Experience Platform envía datos a Adobe Experience Cloud desde las propiedades web a través de Adobe Experience Platform Edge Network. La extensión le permite transmitir datos a Platform, sincronizar identidades, procesar señales de consentimiento del cliente y recopilar automáticamente datos de contexto.

Este documento explica cómo configurar la extensión en la interfaz de usuario de Adobe Experience Platform Launch.

## Configurar la extensión de

Si la extensión del SDK web de Platform ya se ha instalado para una propiedad, abra la propiedad en la interfaz de usuario de Platform launch y seleccione la pestaña **[!UICONTROL Extensions]** . En el SDK web de Platform, seleccione **[!UICONTROL Configure]**.

![](../images/extension/overview/configure.png)

Si todavía no ha instalado la extensión, seleccione la pestaña **[!UICONTROL Catalog]** . En la lista de extensiones disponibles, busque la extensión del SDK web de Platform y seleccione **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

En ambos casos, llega a la página de configuración del SDK web de Platform. Las secciones siguientes explican las opciones de configuración de la extensión.

![](../images/extension/overview/config-screen.png)

## Opciones de configuración generales

Las opciones de configuración en la parte superior de la página indican a Adobe Experience Platform dónde enrutar los datos y qué configuraciones utilizar en el servidor.

### [!UICONTROL Name]

La extensión del SDK web de Adobe Experience Platform admite varias instancias en la página. El nombre se utiliza para enviar datos a varias organizaciones con una sola configuración de Platform launch.

El nombre predeterminado de la extensión es &quot;[!DNL alloy]&quot;. Sin embargo, puede cambiar el nombre de la instancia a cualquier nombre de objeto JavaScript válido.

### **[!UICONTROL IMS Organization ID]**

El [!UICONTROL IMS Organization ID] indica la organización a la que desea que se envíen los datos en Adobe. La mayoría de las veces, utilice el valor predeterminado que se rellena automáticamente. Cuando tenga varias instancias en la página, rellene este campo con el valor de la segunda organización a la que desee enviar datos.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain] es el dominio desde el que la extensión de Adobe Experience Platform envía y recibe datos. La extensión requiere que utilice un CNAME de origen para el tráfico de producción. El dominio de terceros predeterminado funciona para entornos de desarrollo, pero no es adecuado para entornos de producción. Las instrucciones sobre cómo configurar un CNAME de origen se enumeran [aquí](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datastreams]

Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, se utiliza un ID de conjunto de datos para hacer referencia a la configuración del lado del servidor. Puede actualizar la configuración sin tener que realizar cambios de código en el sitio web.

Consulte la guía de [datastreams](../fundamentals/datastreams.md) para obtener más información.


## [!UICONTROL Privacy]

La sección [!UICONTROL Privacy] le permite configurar el modo en que el SDK gestiona las señales de consentimiento del usuario desde el sitio web. Específicamente, le permite seleccionar el nivel predeterminado de consentimiento que se asume de un usuario si no se ha proporcionado ninguna otra preferencia de consentimiento explícito. El nivel de consentimiento predeterminado no se guarda en el perfil del usuario. La tabla siguiente desglosa lo que implica cada opción:

| [!UICONTROL Default Consent Level] | Descripción |
| --- | --- |
| [!UICONTROL In] | Recopile eventos que se producen antes de que el usuario proporcione preferencias de consentimiento. |
| [!UICONTROL Out] | Descartar los eventos que se producen antes de que el usuario proporcione las preferencias de consentimiento. |
| [!UICONTROL Pending] | Eventos de cola que se producen antes de que el usuario proporcione las preferencias de consentimiento. Cuando se proporcionan las preferencias de consentimiento, los eventos se recopilan o descartan en función de las preferencias proporcionadas. |
| [!UICONTROL Provided by data element] | El nivel de consentimiento predeterminado está determinado por un elemento de datos independiente que usted defina. Al utilizar esta opción, debe especificar el elemento de datos mediante el menú desplegable proporcionado. |

Utilice Out o Pending si necesita consentimiento explícito del usuario para sus operaciones comerciales.
