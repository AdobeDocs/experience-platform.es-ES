---
title: inicio rápido con Launch
seo-title: inicio rápido del SDK web de Adobe Experience Platform con Launch
description: Guía de inicio rápido para usar la extensión del SDK web de la plataforma de experiencia para recopilar datos
seo-description: Guía de inicio rápido para usar la extensión del SDK web de la plataforma de experiencia para recopilar datos
translation-type: tm+mt
source-git-commit: e23b0ce9c20d5d2d770d1c1261fe08de5743325a

---


# Requisitos previos (Beta)

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Actualmente, el SDK web de Adobe Experience Platform solo admite el envío de datos a Adobe Experience Platform mediante XDM. Debe cumplir los siguientes requisitos previos.

- Habilite un dominio de [origen (CNAME)](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html) . Si ya tiene un CNAME para Analytics, debe utilizarlo.
- Tenga derecho a Adobe Experience Platform
- Utilizar la versión más reciente del servicio de ID de Visitante

## Preparar plataforma

Para poder enviar datos a Adobe Experience Platform, debe crear un esquema XDM y un conjunto de datos que utilicen ese esquema.

- [Cree un esquema](../../xdm/tutorials/create-schema-ui.md) con las siguientes mezclas:
   - Detalles de implementación de ExperienceEvent
   - Detalles del Entorno de ExperienceEvent
   - Detalles de la web de ExperienceEvent
- Añada la combinación del SDK web de la plataforma Adobe Experience Platform en el esquema que ha creado
- [Cree un conjunto de datos](https://platform.adobe.com/dataset/overview) con su esquema en el que desee que los datos aterricen

## Crear un ID de configuración

Puede crear un ID de configuración mediante la herramienta [de configuración](../fundamentals/edge-configuration.md) Edge durante el inicio.

>Nota: La organización debe estar en una lista blanca para la función. Póngase en contacto con su CSM para que se le ponga en la lista para una eventual lista blanca.

## Instalación del SDK en Launch

Inicie sesión para iniciar e instale la `AEP Web SDK` extensión. Como parte de la instalación del SDK, se le pedirá que configure la extensión. Introduzca el ID de configuración que ha solicitado anteriormente. La extensión rellena automáticamente el identificador de organización.

Para obtener más información sobre las distintas opciones de configuración, consulte [Configuración del SDK](../fundamentals/configuring-the-sdk.md).

## Envío de un evento

Una vez instalada la extensión, inicio el envío de eventos agregando una acción &quot;Send Beacon&quot; de la extensión AEP Web SDK. Se recomienda enviar al menos un evento cada vez que se cargue una página con la opción &quot;se produce en el inicio de una vista&quot; activada.

Para obtener más información sobre cómo rastrear eventos, consulte [Seguimiento de Eventos](../fundamentals/tracking-events.md).

## Enviar datos

Puede enviar datos que coincidan con el esquema creado anteriormente junto con sus eventos. Por ejemplo, si es propietario de un sitio comercial y agrega la mezcla comercial a su esquema, enviaría la siguiente estructura cuando alguien vista un producto.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
