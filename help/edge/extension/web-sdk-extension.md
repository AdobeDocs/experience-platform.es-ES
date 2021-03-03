---
title: Extensión de SDK web de Adobe Experience Platform Información general
description: Obtenga información sobre la extensión del SDK web de Adobe Experience Platform para Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 14%

---


# Descripción general de la extensión web SDK de Adobe Experience Platform

La extensión web SDK de Adobe Experience Platform envía datos a Adobe Experience Cloud desde las propiedades web a través de Adobe Experience Platform Edge Network. La extensión le permite transmitir datos a Platform, sincronizar identidades, procesar señales de consentimiento del cliente y recopilar automáticamente datos de contexto.

Este documento explica cómo configurar la extensión en la interfaz de usuario de Adobe Experience Platform Launch.

## Configurar la extensión de

Si la extensión del SDK web de Platform ya se ha instalado para una propiedad, abra la propiedad en la interfaz de usuario de Platform Launch y seleccione la pestaña **[!UICONTROL Extensions]**. En el SDK web de Platform, seleccione **[!UICONTROL Configurar]**.

![](../images/extension/overview/configure.png)

Si todavía no ha instalado la extensión, seleccione la pestaña **[!UICONTROL Catalog]**. En la lista de extensiones disponibles, busque la extensión del SDK web de Platform y seleccione **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

En ambos casos, llega a la página de configuración del SDK web de Platform. Las secciones siguientes explican las opciones de configuración de la extensión.

![](../images/extension/overview/config-screen.png)

## Opciones de configuración generales

Las opciones de configuración en la parte superior de la página indican a Adobe Experience Platform dónde enrutar los datos y qué configuraciones utilizar en el servidor.

### [!UICONTROL Nombre]

La extensión web SDK de Adobe Experience Platform admite varias instancias en la página. El nombre se utiliza para enviar datos a varias organizaciones con una sola configuración de Platform Launch.

El nombre predeterminado de la extensión es &quot;[!DNL alloy]&quot;. Sin embargo, puede cambiar el nombre de la instancia a cualquier nombre de objeto JavaScript válido.

### **[!UICONTROL ID de organización de IMS]**

El [!UICONTROL IMS Organization ID] es la organización a la que desea que se envíen los datos en Adobe. La mayoría de las veces, utilice el valor predeterminado que se rellena automáticamente. Cuando tenga varias instancias en la página, rellene este campo con el valor de la segunda organización a la que desee enviar datos.

### **[!UICONTROL Dominio de Edge]**

El [!UICONTROL Dominio perimetral] es el dominio desde el cual la extensión de Adobe Experience Platform envía y recibe datos. La extensión requiere que utilice un CNAME de origen para el tráfico de producción. El dominio de terceros predeterminado funciona para entornos de desarrollo, pero no es adecuado para entornos de producción. Las instrucciones sobre cómo configurar un CNAME de origen se enumeran [aquí](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Configuraciones de Edge]

Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, se utiliza un ID de configuración perimetral para hacer referencia a la configuración del lado del servidor. Puede actualizar la configuración sin tener que realizar cambios de código en el sitio web.

Consulte la guía de [edge settings](../fundamentals/edge-configuration.md) para obtener más información.

## [!UICONTROL Privacidad]

La sección [!UICONTROL Privacidad] le permite configurar el modo en que el SDK gestiona las señales de consentimiento del cliente desde el sitio web. Específicamente, le permite seleccionar el nivel predeterminado de consentimiento que se presupone de un cliente si no se ha proporcionado ninguna otra preferencia de consentimiento explícito. La tabla siguiente desglosa lo que implica cada opción:

| [!UICONTROL Nivel de consentimiento predeterminado] | Descripción |
| --- | --- |
| [!UICONTROL En] | Inclusión. Utilice esta opción si asume el consentimiento del cliente de forma predeterminada y solo respeta las señales de exclusión. |
| [!UICONTROL Pendiente] | Los clientes con consentimiento &quot;pendiente&quot; se excluyen hasta que se envía una señal de inclusión. Utilice esta opción si necesita consentimiento explícito del cliente para sus operaciones comerciales. |
| [!UICONTROL Proporcionado por un elemento de datos] | El nivel de consentimiento predeterminado está determinado por un elemento de datos independiente que usted defina. Al utilizar esta opción, debe especificar el elemento de datos mediante el menú desplegable proporcionado. |