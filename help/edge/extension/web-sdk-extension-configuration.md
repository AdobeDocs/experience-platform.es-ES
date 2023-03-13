---
title: Configuración de la extensión SDK para web de Adobe Experience Platform
description: Configuración de la extensión de etiqueta SDK web de Adobe Experience Platform en la interfaz de usuario.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 7%

---

# Configuración de la extensión SDK para web de Adobe Experience Platform

La extensión de etiquetas SDK para web de Adobe Experience Platform envía datos a Adobe Experience Cloud desde las propiedades web a través de Adobe Experience Platform Edge Network. La extensión de le permite transmitir datos a Platform, sincronizar identidades, procesar señales de consentimiento de clientes y recopilar automáticamente datos de contexto.

Este documento explica cómo configurar la extensión en la interfaz de usuario de.

## Primeros pasos

Si la extensión del SDK web de Platform ya se ha instalado para una propiedad, abra la propiedad en la interfaz de usuario de y seleccione **[!UICONTROL Extensiones]** pestaña. En el SDK web de Platform, seleccione **[!UICONTROL Configurar]**.

![](../assets/extension/overview/configure.png)

Si aún no ha instalado la extensión, seleccione la **[!UICONTROL Catálogo]** pestaña. En la lista de extensiones disponibles, busque la extensión del SDK web de Platform y seleccione **[!UICONTROL Instalar]**.

![](../assets/extension/overview/install.png)

En ambos casos, se llega a la página de configuración del SDK web de Platform. Las secciones siguientes explican las opciones de configuración de la extensión.

![](../assets/extension/overview/config-screen.png)

## Opciones de configuración generales

Las opciones de configuración en la parte superior de la página indican a Adobe Experience Platform dónde enrutar los datos y qué configuraciones utilizar en el servidor.

### [!UICONTROL Nombre]

La extensión SDK para web de Adobe Experience Platform admite varias instancias en la página. El nombre se utiliza para enviar datos a varias organizaciones con una configuración de etiquetas.

El nombre de la extensión toma el valor predeterminado &quot;[!DNL alloy]&quot;. Sin embargo, puede cambiar el nombre de la instancia a cualquier nombre de objeto JavaScript válido.

### **[!UICONTROL ID de organización de IMS]**

El [!UICONTROL ID de organización IMS] es la organización a la que desea que se envíen los datos durante el Adobe. La mayoría de las veces, utilice el valor predeterminado que se rellena automáticamente. Cuando tenga varias instancias en la página, rellene este campo con el valor de la segunda organización a la que desee enviar datos.

### **[!UICONTROL Dominio de Edge]**

El [!UICONTROL Dominio de Edge] es el dominio desde el que la extensión de Adobe Experience Platform envía y recibe datos. El Adobe recomienda utilizar un dominio de origen (CNAME) para esta extensión. El dominio de terceros predeterminado funciona para entornos de desarrollo, pero no es adecuado para entornos de producción. Las instrucciones sobre cómo configurar un CNAME de origen se enumeran [aquí](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=es).

## [!UICONTROL Corrientes de datos]

Cuando se envía una solicitud a Adobe Experience Platform Edge Network, se utiliza un ID de secuencia de datos para hacer referencia a la configuración del lado del servidor. Puede actualizar la configuración sin tener que realizar cambios en el código del sitio web.

Consulte la guía de [flujos de datos](../datastreams/overview.md) para obtener más información.


## [!UICONTROL Privacidad]

![](../assets/extension/overview/privacy.png)

El [!UICONTROL Privacidad] le permite configurar cómo gestiona el SDK las señales de consentimiento de los usuarios desde su sitio web. En concreto, le permite seleccionar el nivel de consentimiento predeterminado que se supone de un usuario si no se ha proporcionado ninguna otra preferencia de consentimiento explícita. El nivel de consentimiento predeterminado no se guarda en el perfil del usuario. La siguiente tabla desglosa qué implica cada opción:

| [!UICONTROL Nivel de consentimiento predeterminado] | Descripción |
| --- | --- |
| [!UICONTROL En] | Recopilar eventos que se producen antes de que el usuario proporcione preferencias de consentimiento. |
| [!UICONTROL Fuera] | Descartar los eventos que se producen antes de que el usuario proporcione preferencias de consentimiento. |
| [!UICONTROL Pendiente] | Eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento. Cuando se proporcionan las preferencias de consentimiento, los eventos se recopilan o descartan según las preferencias proporcionadas. |
| [!UICONTROL Proporcionado por el elemento de datos] | El nivel de consentimiento predeterminado está determinado por un elemento de datos independiente que usted defina. Al utilizar esta opción, debe especificar el elemento de datos mediante el menú desplegable proporcionado. |

Utilice Out o Pending si necesita el consentimiento explícito del usuario para sus operaciones comerciales.

## [!UICONTROL Identidad]

![](../assets/extension/overview/identity.png)

### [!UICONTROL Migrar ECID desde VisitorAPI]

Esta opción está habilitada de manera predeterminada. Cuando esta función está habilitada, el SDK puede leer las cookies AMCV y s_ecid y establecer la cookie AMCV utilizada por Visitor.js. Esta función es importante al migrar al SDK web de Adobe Experience Platform, ya que algunas páginas pueden seguir utilizando Visitor.js. Permite al SDK seguir utilizando el mismo ECID para que los usuarios no se identifiquen como dos usuarios independientes.

### [!UICONTROL Uso de cookies de terceros]

Esta opción permite al SDK intentar almacenar un identificador de usuario en una cookie de terceros. Si se realiza correctamente, el usuario se identifica como un solo usuario a medida que navega por varios dominios, en lugar de identificarse como un usuario independiente en cada dominio. Si esta opción está habilitada, es posible que el SDK aún no pueda almacenar el identificador de usuario en una cookie de terceros si el explorador no admite cookies de terceros o si el usuario lo ha configurado para no permitir cookies de terceros. En este caso, el SDK solo almacena el identificador en el dominio de origen.

## [!UICONTROL Personalización]

![](../assets/extension/overview/personalization.png)

Si desea ocultar determinadas partes si su sitio está cargado con contenido personalizado, puede especificar los elementos que desea ocultar en el editor de estilos de preocultación. A continuación, puede copiar el fragmento de ocultamiento previo predeterminado que se le ha proporcionado y pegarlo dentro de la variable `<head>`del sitio del HTML.

## [!UICONTROL Recopilación de datos]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL Función Callback]

La función de llamada de retorno proporcionada en la extensión también se denomina [`onBeforeEventSend` función](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=es) en la biblioteca. Esta función le permite modificar eventos globalmente antes de enviarlos a Adobe Edge Network. Encontrará información más detallada sobre cómo utilizar esta función [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Haga clic en recopilación de datos]

El SDK puede recopilar automáticamente información sobre clics en vínculos. Esta función está habilitada de forma predeterminada, pero se puede deshabilitar con esta opción. Los vínculos también se etiquetan como vínculos de descarga si contienen una de las expresiones de descarga enumeradas en la variable [!UICONTROL Cualificador de vínculo de descarga] cuadro de texto. El Adobe le proporciona algunos calificadores de vínculo de descarga predeterminados, pero se pueden editar en cualquier momento.

### [!UICONTROL Datos de contexto recopilados automáticamente]

De forma predeterminada, el SDK recopila determinados datos de contexto relacionados con el contexto del dispositivo, la web, el entorno y el lugar. Si desea ver una lista de los datos que recopila el Adobe de información, puede encontrarla [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Si no desea que se recopilen estos datos o solo desea que se recopilen determinadas categorías de datos, puede cambiar estas opciones.

## [!UICONTROL Configuración avanzada]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL Ruta base del borde]

Utilice este campo si necesita cambiar la ruta base que se utiliza para interactuar con Adobe Edge Network. Esto no debería requerir ninguna actualización, pero en caso de que participe en una versión beta o alfa, Adobe podría pedirle que cambie este campo.
