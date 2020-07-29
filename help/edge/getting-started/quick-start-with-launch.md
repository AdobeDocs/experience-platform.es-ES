---
title: inicio rápido con Launch
seo-title: inicio rápido del SDK web de Adobe Experience Platform con Launch
description: Guía de inicio rápido para usar la extensión del SDK web Experience Platform para recopilar datos
seo-description: Guía de inicio rápido para usar la extensión del SDK web Experience Platform para recopilar datos
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%

---


# Bienvenido

Esta guía le guía por las diferentes formas de configurar el SDK web de Adobe Experience Platform en Launch. Para utilizar esta función debe tener una lista blanca. Si desea subirse a la lista de espera, póngase en contacto con su CSM.

- Habilite un dominio de [origen (CNAME)](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html) . Si ya tiene un CNAME para Analytics, debe utilizarlo. La prueba en desarrollo funciona sin un CNAME, pero se necesita uno antes de ir a producción.
- Tener derecho al Adobe Experience Platform. Si no ha adquirido Platform, Adobe le proporcionará Experience Platform Data Services Foundation para que lo utilice de forma limitada con el SDK sin cargo adicional.
- Utilice la versión más reciente del servicio de ID de Visitante.

## Preparación de un Esquema

La red perimetral Experience Platform toma los datos como XDM. XDM es un formato de datos que permite definir esquemas. El esquema define cómo espera la red de Edge que se formateen los datos. Para enviar datos, debe definir el esquema.

1. [Crear un esquema](../../xdm/tutorials/create-schema-ui.md)
2. Añada la mezcla de AEP [!DNL Web SDK ExperienceEvent] al esquema que ha creado.
3. Cree un conjunto de datos a partir del esquema que ha creado.

El siguiente vídeo está diseñado para ayudarle a crear un conector de esquema, conjunto de datos y origen de flujo continuo para sus [!DNL Web SDK] datos.

Inicie sesión para iniciar e instale la `AEP Web SDK` extensión. Cuando instale el SDK, se le pedirá que configure la extensión. Introduzca el ID de configuración que ha solicitado anteriormente. La extensión rellena automáticamente el identificador de organización.


Para obtener más información sobre las distintas opciones de configuración, consulte [Configuración del SDK](../fundamentals/configuring-the-sdk.md).

## Crear un ID de configuración

Puede crear un ID de configuración con la herramienta [de configuración](../fundamentals/edge-configuration.md) Edge en Launch. Esto le permite habilitar la red perimetral para enviar datos a las distintas soluciones. Los detalles de cómo encontrar cada opción se encuentran en la página Herramienta [de configuración de](../fundamentals/edge-configuration.md) Edge.

>[!NOTE]
>
>La organización debe estar en una lista blanca para esta función. Póngase en contacto con su CSM para que se le ponga en la lista para una eventual lista blanca.

## Crear un elemento de datos basado en su Esquema

En Iniciar, cree un elemento de datos que haga referencia al esquema cambiando la extensión al SDK web de AEP y estableciendo el tipo en `XDM Object`. Esto carga el esquema y le permite asignar elementos de datos a diferentes partes del esquema.

![Elemento Fecha En Inicio](../../assets/edge_data_element.png)

## Envío de un evento

Una vez instalada la extensión, inicio el envío de eventos agregando una acción de la extensión del SDK web de AEP a una regla `sendEvent` . Añada el elemento de datos que acaba de crear en el evento como datos XDM. Adobe recomienda que envíe al menos un evento cada vez que se cargue una página.

Para obtener más información sobre cómo rastrear eventos, consulte [Seguimiento de Eventos](../fundamentals/tracking-events.md).

## Pasos siguientes

Una vez que haya datos fluidos, puede hacer lo siguiente.

- [Cree su esquema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html)
- [Más información sobre la depuración](../fundamentals/debugging.md)
- Aprenda a [personalizar la experiencia](../fundamentals/rendering-personalization-content.md)
- Obtenga información sobre cómo enviar datos a varias soluciones
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
