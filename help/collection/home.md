---
keywords: Experience Platform;inicio;temas populares;recopilación de datos;launch;sdk web
solution: Experience Platform
title: Información general sobre la recopilación de datos
description: Obtenga información acerca de las distintas tecnologías relacionadas con la recopilación de datos sobre experiencias de los clientes en Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 998cc9a9c490124ff21fdbf5f3a7b91abef3e8b8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 8%

---

# Información general sobre la recopilación de datos

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente de fuentes del lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe en segundos.

La recopilación de datos es compatible con las siguientes fuentes del lado del cliente:

* Aplicaciones basadas en web
* Aplicaciones móviles nativas
* Aplicaciones OTT (Over-the-top)

La recopilación de datos se centra en la detección y accesibilidad de conjuntos de datos ingeridos, e incluye lo siguiente:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Etiquetas](../tags/home.md)
* [Corrientes de datos](../datastreams/overview.md)
* [Reenvío de eventos](../tags/ui/event-forwarding/overview.md)
* [SDK web de Adobe Experience Platform](../edge/home.md)
* [SDK móvil de Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/)
* [API del servidor de red perimetral](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=es)
* [Garantía del Experience Platform](../assurance/home.md)


Esta guía proporciona una introducción general a la recopilación de datos y a cómo funciona para enviar datos a productos de Adobe Experience Cloud y aplicaciones que no son de Adobe a través de Platform Edge Network.

## Etiquetas, SDK web y SDK móvil

El SDK web de Platform y el SDK móvil de Platform contraen y comprimen todas las bibliotecas de productos de Adobe en un único kit de desarrollo para plataformas web y móviles, respectivamente. Pueden implementarse mediante código sin procesar o utilizando [etiquetas](../tags/home.md) mediante la IU de recopilación de datos o la IU de Adobe Experience Platform.

La compresión de estas bibliotecas acelera la recopilación de datos y consolida las operaciones en un único flujo desde dispositivos del lado del cliente a la red perimetral de Platform.

![Etiquetas, SDK web, SDK móvil](./images/home/tags-sdks.png)

## Red perimetral de plataforma y flujos de datos {#edge}

Platform Edge Network es una red de servidores distribuidos globalmente, rápidos y fiables capaces de recibir y procesar datos a una escala tremenda. Con las etiquetas, puede configurar lo siguiente [flujos de datos](../datastreams/overview.md) para productos como Adobe Target, Adobe Audience Manager y Adobe Analytics, que le permiten activar estos productos en el servidor sin cambiar el código del lado del cliente.

Además, los flujos de datos están integrados con varias funciones de Platform que ayudan a garantizar que los datos confidenciales que envía se gestionen correctamente con respecto a las políticas organizativas y las regulaciones legales. Consulte la sección sobre [gestión de datos confidenciales](../datastreams/overview.md#sensitive) en la documentación de flujos de datos para obtener más información.

![Flujos de datos y soluciones de Adobe](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Para obtener una introducción de alto nivel a Platform Edge Network, consulte lo siguiente [recorrido interactivo del producto](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Reenvío de eventos

[Reenvío de eventos](../tags/ui/event-forwarding/overview.md) puede aprovechar cualquier conjunto de datos de Experience Platform, lo que le permite transformar, enriquecer y enviar datos a cualquier destino que no sea de Adobe con latencia baja extrema y sin agregar código de terceros al dispositivo cliente.

![Reenvío de eventos](./images/home/event-forwarding.png)

>[!NOTE]
>
>El reenvío de eventos es una función de pago que se incluye como parte de las ofertas de Adobe Real-time Customer Data Platform Connections, Prime o Ultimate.

## Pasos siguientes

Este documento proporciona una amplia descripción general de cómo funciona la recopilación de datos para automatizar el proceso de envío de los datos recopilados sobre la experiencia del cliente a productos de Adobe y destinos de terceros.

![Marco de recopilación de datos](./images/home/collection.png)

Para obtener más información sobre el flujo de trabajo general involucrado en el envío de datos de evento a través de la red perimetral, consulte la [información general de extremo a extremo](./e2e.md).
