---
title: inicio rápido con Launch
seo-title: inicio rápido del SDK web de Adobe Experience Platform con Launch
description: Guía de inicio rápido para usar la extensión del SDK web de la plataforma de experiencia para recopilar datos
seo-description: Guía de inicio rápido para usar la extensión del SDK web de la plataforma de experiencia para recopilar datos
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

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

## Solicitud de un ID de configuración

Debe tener un ID de configuración para utilizar el SDK. El ID de configuración garantiza que los datos se dirijan al lugar correcto. Puede obtener un ID de configuración de su consultor o a través de Client Care. Necesitarán la siguiente información:

- **ID de organización:** Puede encontrarlo siguiendo las instrucciones [aquí](https://docs.adobe.com/content/help/es-ES/core-services/interface/manage-users-and-products/organizations.html)
- **Id. de conjunto de datos:** Esto está disponible en la interfaz de usuario del conjunto de datos cuando hace clic en un conjunto de datos
- **ID de Esquema:** Esto está disponible en la dirección URL de la pantalla de creación de esquemas
- **Nombre práctico:** Es el nombre descriptivo que se utilizará en futuras IU para esta configuración

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
