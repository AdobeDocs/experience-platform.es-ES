---
keywords: Experience Platform;inicio;temas populares;recopilación de datos;launch;sdk web
solution: Experience Platform
title: Información general sobre la recopilación de datos
topic-legacy: overview
description: Obtenga información sobre las distintas tecnologías que intervienen en la recopilación de datos sobre las experiencias de los clientes en Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 6%

---

# Información general sobre la recopilación de datos

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente de fuentes del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe en segundos.

La recopilación de datos es compatible con las siguientes fuentes del lado del cliente:

* Aplicaciones basadas en la Web
* Aplicaciones móviles nativas
* Aplicaciones OTT

Las tecnologías de recopilación de datos proporcionadas por el Experience Platform se centran en la capacidad de detección y accesibilidad de los conjuntos de datos ingestados. Estas tecnologías comprenden lo siguiente:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Etiquetas](../tags/home.md)
* [Reenvío de eventos](../tags/ui/event-forwarding/overview.md)
* [SDK web de Adobe Experience Platform](../edge/home.md)
* [SDK móvil de Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Modelo de datos de experiencia (XDM)](../xdm/home.md)
* [Servicio de ID de Adobe Experience Platform](../identity-service/home.md)

<!-- (Outdated terminology)
![](./images/Collection.png)
-->

## Implementaciones más simples, rendimiento más rápido del lado del cliente

Los SDK web y móviles de Adobe Experience Platform contraen y comprimen todas las bibliotecas de productos de Adobe en un único kit de desarrollo para plataformas web o móviles. La compresión de estas bibliotecas acelera la recopilación de datos y consolida las operaciones en un único flujo desde dispositivos del lado del cliente a Adobe Experience Platform Edge Network.

## Proceso de conmutación para implementar la tecnología de Adobe {#edge}

Platform Edge Network es una red global de servidores distribuidos, rápidos y confiables que pueden recibir y procesar datos a una escala tremenda. Con las etiquetas, puede configurar [datastreams](../edge/fundamentals/datastreams.md) para productos como Adobe Target, Adobe Audience Manager y Adobe Analytics, que permiten activar estos productos en el servidor sin cambiar el código del lado del cliente.

<!-- (Outdated terminology)
![](./images/deploy.png)
-->

>[!NOTE]
>
>Para obtener una introducción de alto nivel a la red perimetral de plataforma, consulte lo siguiente [recorrido interactivo del producto](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Transformar, enriquecer y enviar datos de forma rápida y segura

[Reenvío de eventos en Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) puede aprovechar cualquier flujo de datos de Platform. Puede transformar, enriquecer y enviar datos a cualquier destino que no sea de Adobe con una latencia extrema y baja sin agregar código de terceros al dispositivo cliente, lo que permite una recopilación y distribución de datos más rápidas y seguras.

<!-- (Outdated terminology)
![](./images/launch.png)
-->