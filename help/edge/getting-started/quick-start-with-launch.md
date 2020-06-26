---
title: inicio rápido con Launch
seo-title: inicio rápido del SDK web de Adobe Experience Platform con Launch
description: Guía de inicio rápido para usar la extensión del SDK web Experience Platform para recopilar datos
seo-description: Guía de inicio rápido para usar la extensión del SDK web Experience Platform para recopilar datos
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 5%

---


# Bienvenido

Esta guía le guiará por los diferentes pasos para configurar el SDK web de Adobe Experience Platform en Adobe Launch. Debe tener permisos y estar en la lista de permitidos para utilizar esta función. Si desea subirse a la lista de espera, póngase en contacto con su CSM. Además, para utilizar esta función, debe:

- Habilite un dominio de [origen (CNAME)](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html) . Si ya tiene un CNAME para Adobe Analytics, debe utilizarlo. La prueba en desarrollo funcionará sin un CNAME, pero necesitará uno antes de ir a producción
- Utilizar la versión más reciente del servicio de ID de Visitante

## Crear un ID de configuración

Puede crear un ID de configuración con la herramienta [de configuración](../fundamentals/edge-configuration.md) Edge en Adobe Launch. Esto le permitirá habilitar la red perimetral para enviar datos a las distintas soluciones. Consulte la página Herramienta [de configuración de](../fundamentals/edge-configuration.md) Edge para obtener más información sobre cómo encontrar cada opción.

>[!NOTE]
>
>Su organización debe estar en la lista de permitidos para la función. Póngase en contacto con su CSM para agregar a la lista de permitidos.

## Preparación de un Esquema

La red perimetral Experience Platform toma los datos como XDM. XDM es un formato de datos que permite definir esquemas. El esquema define cómo espera la red de Edge que se formateen los datos. Para enviar datos, deberá definir su esquema. Asegúrese de completar lo siguiente:

- [Crear un esquema](../../xdm/tutorials/create-schema-ui.md)
- Añadir la mezcla de SDK web de Adobe Experience Platform en el esquema que ha creado

## Instalación del SDK en Adobe Launch

Inicie sesión en Adobe Launch e instale la `AEP Web SDK` extensión. Como parte de la instalación del SDK, se le pedirá que configure la extensión. Introduzca el ID de configuración que ha solicitado anteriormente. La extensión rellena automáticamente el identificador de organización.

Para obtener más información sobre las distintas opciones de configuración, consulte [Configuración del SDK](../fundamentals/configuring-the-sdk.md).

## Crear un elemento de datos en base a su Esquema

En Adobe Launch, cree un elemento de datos que haga referencia al esquema cambiando la extensión a AEP Web SDK y estableciendo el tipo en XDM Object. Esto cargará el esquema y le permitirá asignar elementos de datos a diferentes partes del esquema.

![Elemento Fecha En Inicio](../../assets/edge_data_element.png)

## Envío de un evento

Una vez instalada la extensión, inicio el envío de eventos agregando una acción &quot;sendEvent&quot; de la extensión del SDK web de AEP a una regla. Asegúrese de agregar el elemento de datos que acaba de crear al evento como datos XDM. Le recomendamos que envíe al menos un evento cada vez que cargue una página.

Para obtener más información sobre cómo rastrear eventos, consulte [Seguimiento de Eventos](../fundamentals/tracking-events.md).

## Pasos siguientes

Una vez que tenga datos fluidos, puede hacer lo siguiente:

- [Cree su esquema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html)
- [Más información sobre la depuración](../fundamentals/debugging.md)
- Aprenda a [personalizar la experiencia](../fundamentals/rendering-personalization-content.md)
- Obtenga información sobre cómo enviar datos a varias soluciones
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
