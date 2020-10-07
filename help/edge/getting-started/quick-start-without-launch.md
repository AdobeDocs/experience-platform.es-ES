---
title: Inicio rápido con javascript sin formato
seo-title: 'inicio rápido del SDK web de Adobe Experience Platform '
description: Guía de inicio rápido para utilizar el SDK web de Experience Platform para recopilar datos
seo-description: Guía de inicio rápido para utilizar el SDK web de Experience Platform para recopilar datos
keywords: 1st-party domain;CNAME;schema;create schema;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;install sdk;install web sdk;configure;configure web sdk;
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%

---


# Guía de inicio rápido de Adobe Experience Platform Web SDK JavaScript

Esta guía le guiará por las diferentes formas de configurar el SDK web de Adobe Experience Platform. Para utilizar esta función, debe estar en la lista de permitidos. Si desea entrar en la lista de espera, póngase en contacto con su administrador de software certificado (CSM).

- Habilite un dominio de [origen (CNAME)](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html) . Si ya tiene un CNAME para Analytics, debe utilizarlo. La prueba en desarrollo funciona sin un CNAME, pero se necesita uno antes de ir a producción.
- Tener derecho a Adobe Experience Platform.  Si no ha adquirido Platform, Adobe le proporcionará Experience Platform Data Services Foundation para que lo utilice de forma limitada con el SDK sin cargo adicional.
- Utilice la versión más reciente del servicio de ID de Visitante.

## Preparación de un Esquema

El [!DNL Experience Platform Edge Network] toma los datos como XDM. XDM es un formato de datos que permite definir esquemas. El esquema define cómo [!DNL Edge Network] espera que se formatee la información. Para enviar datos, debe definir el esquema.

- [Crear un esquema](../../xdm/tutorials/create-schema-ui.md)
- Añadir la mezcla de Adobe Experience Platform [!DNL Web SDK] en el esquema creado

El siguiente vídeo está diseñado para ayudarle a crear un conector de esquema, conjunto de datos y origen de flujo continuo para sus [!DNL Web SDK] datos.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Crear un ID de configuración

Puede crear un ID de configuración con la herramienta [de configuración](../fundamentals/edge-configuration.md) Edge en Inicio de Adobe, aunque no utilice las funciones de administración de etiquetas. Esto le permite habilitar el [!DNL Edge Network] envío de datos a las distintas soluciones. Los detalles de cómo encontrar cada opción se encuentran en la página Herramienta [de configuración de](../fundamentals/edge-configuration.md) Edge.

>[!NOTE]
>
>Su organización debe estar en la lista de permitidos de la función. Póngase en contacto con su CSM para ponerse en la lista de permitidos.

## Instalación del SDK

Para instalar el SDK, copie y pegue el siguiente &quot;código base&quot; lo más alto posible en la `<head>` etiqueta de su HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js" async></script>
```

Para obtener más información sobre las distintas opciones para realizar esto, consulte [Instalación del SDK](../fundamentals/installing-the-sdk.md).

## Configuración del SDK

A continuación, proporcione la configuración al SDK. Esto se realiza mediante el `configure` comando. Debe ser el primer comando llamado en cada página.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Aquí puede proporcionar la ID de configuración que ha creado anteriormente, así como la ID de organización. Estos son los únicos dos campos obligatorios. Sin embargo, hay muchas otras opciones [de configuración](../fundamentals/configuring-the-sdk.md).

## Envío de un evento

Después de llamar al comando configure, podrá usar los eventos de seguimiento de inicio.

```javascript
alloy("sendEvent", {});
```

Normalmente, se envían eventos con algunos datos. Puede enviar datos XDM de este modo. Los datos que envía deben estar en el esquema que ha creado en XDM.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Para obtener más información sobre cómo rastrear eventos, consulte [Seguimiento de Eventos](../fundamentals/tracking-events.md).

## Pasos siguientes

Una vez que haya datos fluidos, puede hacer lo siguiente:

- [Cree su esquema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html)
- [Más información sobre la depuración](../fundamentals/debugging.md)
- Aprenda a [personalizar la experiencia](../fundamentals/rendering-personalization-content.md)
- Obtenga información sobre cómo enviar datos a varias soluciones
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
