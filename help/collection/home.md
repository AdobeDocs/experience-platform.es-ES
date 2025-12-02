---
solution: Experience Platform
title: Información general sobre la recopilación de datos
description: Obtenga información sobre cómo enviar datos a Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Información general sobre la recopilación de datos

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente de varias fuentes y enviarlos a Adobe Experience Platform Edge Network. Estos datos se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

Adobe es compatible con los siguientes lenguajes de código con bibliotecas específicas para la recopilación de datos:

* **JavaScript**: para sitios web y aplicaciones basadas en web
* **Kotlin**: Para dispositivos Android
* **Swift**: Para dispositivos iOS
* **Brightscript**: Para dispositivos Roku
* **Flutter**: Para aplicaciones de Android + iOS que usan Flutter
* **React Native**: para aplicaciones de Android + iOS que usan React Native

La IU de etiquetas de la recopilación de datos de Adobe Experience Platform incluye una extensión de Web SDK y Mobile SDK.

Si ninguno de los SDK anteriores se ajusta a las necesidades de su proyecto, puede usar la [API de Adobe Experience Platform Edge Network](https://developer.adobe.com/data-collection-apis/docs/) para enviar datos directamente a Adobe.

## Proceso de recopilación de datos

En lugar de instalar e implementar bibliotecas individuales independientes para cada producto de Adobe, puede implementar uno de los SDK o extensiones de etiquetas anteriores para acumular todos los datos deseados en una sola carga útil. Esa carga útil se enviará a un [conjunto de datos](/help/datastreams/overview.md) en Adobe Experience Platform Edge Network.

![Diagrama de recopilación de datos](assets/tags-sdks.png)

Adobe Experience Platform Edge Network es una red de servidores distribuidos globalmente, rápidos y fiables capaces de recibir y procesar datos a una escala tremenda. Cuando un flujo de datos recibe datos, los distribuye a cada solución de que haya configurado. Los datos se transmiten en un formato que cada producto individual comprende.

![Diagrama de soluciones de Adobe](assets/adobe-solutions.png)

También puede usar [reenvío de eventos](/help/tags/ui/event-forwarding/overview.md) para transformar, enriquecer y enviar datos a cualquier destino que no sea Adobe con baja latencia y sin ningún código de implementación del lado del cliente.

![Diagrama de reenvío de eventos](assets/event-forwarding.png)
