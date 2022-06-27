---
title: Información general sobre la API de Edge Network Server
description: Descubra qué es la API del servidor de red perimetral y cómo puede utilizarla.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: recopilación de datos;recopilación;Adobe Experience Platform Edge Network;api de servidor;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# Información general sobre la API de Edge Network Server {#overview}

La red perimetral de Adobe Experience Platform ofrece una forma optimizada para que los clientes interactúen con cualquier servicio Adobe Experience Cloud o Adobe Experience Platform Edge.

La variable [!DNL Edge Network Server API] se puede utilizar para una gran variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing. La variable [!DNL Server API] se puede usar en servidores, [!DNL IoT] dispositivos, cuadros superiores y otros dispositivos.

Dado que la variable [!DNL Server API] no depende de ninguna biblioteca para cargar, proporciona una forma rápida de interactuar con la red Adobe Experience Platform Edge y las soluciones compatibles.

Los beneficios de [!DNL Server API] la arquitectura incluye:

* Se ha reducido el tiempo de carga de las páginas
* Latencia mejorada
* Recopilación de datos de origen
* Comunicación optimizada del lado del servidor entre servicios

La variable [!DNL Server API] admite la recopilación de datos interactiva y por lotes mediante dos extremos dedicados:

1. El punto final interactivo admite la comunicación con los servicios de Adobe Experience Platform y Adobe Experience Cloud que admiten segmentación avanzada, personalización y otros casos de uso de marketing.
2. El extremo de lote permitirá que las solicitudes se envíen en lote cuando los datos deban ser incorporados sin recibir una respuesta de las aplicaciones a las que se llama.

La variable [!DNL Server API] admite el siguiente tipo de solicitudes:

* Solicitudes autenticadas mediante [Adobe I/O](https://developer.adobe.com/), utilizando el nuevo `server.adobedc.net` punto final.
* Solicitudes no autenticadas a través de la variable `edge.adobedc.net` punto final.

Esto permite casos de uso que permiten una recopilación segura y autenticada de datos confidenciales, según las políticas de privacidad de su organización. Además de la autenticación, la API del servidor admite el marcado de conjuntos de datos para aceptar solo la comunicación autenticada a través de la API.

Vea el siguiente vídeo para obtener una descripción general de la API del servidor.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
