---
title: Información general del SDK web de Adobe Experience Platform
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para integrar las funcionalidades de Platform en su sitio web.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;iniciar
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Información general del SDK web de Adobe Experience Platform {#overview}

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios del [!DNL Experience Cloud] a través de Adobe Experience Platform Edge Network. Además de la biblioteca JavaScript, hay un [extensión de etiqueta](./extension/web-sdk-extension-configuration.md) para ayudarle con las configuraciones del SDK web.

Para obtener una guía paso a paso sobre la configuración del SDK web con etiquetas y el envío de datos a las soluciones, consulte nuestra [Tutorial de implementación de Adobe Experience Cloud con SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Este producto evoluciona constantemente y crece para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades y ver lo que admitimos actualmente, consulte la [página de casos de uso admitidos](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] forma parte de la colección que forma la [!DNL Adobe Experience Edge]. [!DNL Experience Edge] consta de las siguientes tecnologías:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** Un SDK de JavaScript y la extensión de etiquetas para simplificar considerablemente la implementación [!DNL Adobe] tecnologías.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Extensión del SDK móvil v5 para permitir a los clientes utilizar la nueva metodología de implementación
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Una red distribuida global de servidores que permiten una nueva metodología de implementación [!DNL Adobe] products

La variable [!DNL Adobe Experience Edge] es un nuevo marco para la recopilación de datos de baja latencia, la computación conectable y la activación rápida de datos en todos los canales a los que se puede dirigir.

[!DNL Adobe Experience Edge] proporciona un único SDK consolidado para cada canal (JavaScript, móvil, del lado del servidor), que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una única carga útil para el envío de datos y experiencias.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicios de plataforma común facilitan la incorporación e implementación de nuevas capacidades en este entorno informático en tiempo real.  Esta arquitectura:

* Reduce el tiempo de respuesta del cliente
* Finaliza la necesidad de integraciones &quot;puntuales&quot;
* Mejora el rendimiento en comparación con las bibliotecas antiguas
* Disminuye costes
* Aumenta la velocidad de la innovación
* Crea ventajas competitivas sostenidas para los clientes de Adobe

Un solo sistema Edge consolidado permite a los clientes administrar sus campañas de publicidad, marketing o personalización en todos los canales como una experiencia integrada. Permite [!DNL Adobe] para ofrecer servicios con un menor coste total de propiedad para los clientes.  También ayuda a aumentar la velocidad de innovación de los productos al hacer que el borde en tiempo real sea conectable y permitir [!DNL Adobe] y sus clientes para agregar más rápidamente nuevas funciones y lógica definida por el cliente a ese sistema en tiempo real.

## Información general del vídeo {#video}

El siguiente vídeo ofrece información general sobre Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas reemplazadas por el SDK web {#sdks}

El SDK web no es solo un envoltorio para bibliotecas existentes. Es una biblioteca completamente nueva, escrita desde cero para incorporar las funcionalidades de las bibliotecas existentes. Su objetivo es acabar con los desafíos, ya que las etiquetas deben activarse en el orden correcto, con incoherencia con los desafíos de versiones de las bibliotecas y con una mejor administración de dependencias. Es una nueva forma de implementar el [!DNL Experience Cloud] y es [código abierto](https://github.com/adobe/alloy).

El SDK web sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Además de una nueva biblioteca, existe un nuevo punto final que optimiza las solicitudes HTTP para las soluciones de Adobe. Antes, Visitor.js enviaba una llamada de bloqueo al servicio de ID de visitante, luego AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID y obtener un [!DNL Target] experiencia, enviar datos a [!DNL Audience Manager]y pasar los datos a Adobe Experience Platform en una sola llamada.

El siguiente vídeo muestra Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network] en acción. El ejemplo de vídeo utiliza una sola llamada al Adobe que envía datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migración de bibliotecas existentes a SDK web {#migrating-to-web-sdk}

Para simplificar la migración desde cualquiera de las [bibliotecas existentes](#sdks) al SDK web, Adobe ofrece una ruta de actualización optimizada que le permite migrar cada página individual de su sitio web al SDK web, sin necesidad de migrar todo su sitio web a la vez.

Esto significa que puede utilizar el SDK web en una página y dejar las bibliotecas existentes en las demás páginas, hasta que también pueda migrarlas.

### Consideraciones sobre la migración de at.js al SDK web {#considerations}

Antes de migrar páginas que utilicen [!DNL at.js] para el SDK web, asegúrese de habilitar las siguientes opciones de configuración del SDK web. Esto garantiza que el perfil del visitante se mantenga mientras se navega desde las páginas con [!DNL at.js ] a páginas que utilicen el SDK web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Las siguientes funciones de Target no son compatibles al migrar de at.js al SDK web:
> * [Ofertas de redireccionamiento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [Compatibilidad con CNAME y entre dominios](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


Después de migrar de at.js al SDK web, debe eliminar la variable `targetMigrationEnabled` de su configuración.



