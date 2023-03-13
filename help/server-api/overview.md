---
title: Información general de API de servidor de red perimetral
description: Descubra qué es la API del servidor de red perimetral y cómo puede utilizarla.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: recopilación de datos;recopilación;Adobe Experience Platform Edge Network;api de servidor;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# Información general de API de servidor de red perimetral {#overview}

Adobe Experience Platform Edge Network ofrece una forma optimizada para que los clientes interactúen con cualquier servicio Adobe Experience Cloud o Adobe Experience Platform Edge.

El [!DNL Edge Network Server API] se puede utilizar para una variedad de casos de uso de recopilación de datos, personalización, publicidad y marketing. El [!DNL Server API] se puede utilizar en servidores de, [!DNL IoT] dispositivos, decodificadores y una variedad de otros dispositivos.

Dado que la variable [!DNL Server API] no depende de ninguna biblioteca para cargar, proporciona una forma rápida de interactuar con Adobe Experience Platform Edge Network y las soluciones compatibles.

Las ventajas de la [!DNL Server API] La arquitectura de incluye:

* Tiempo de carga de página reducido
* Latencia mejorada
* Recopilación de datos de origen
* Comunicación optimizada del lado del servidor entre servicios

El [!DNL Server API] admite la recopilación de datos interactiva y por lotes a través de dos extremos dedicados:

1. El extremo interactivo admite la comunicación con los servicios de Adobe Experience Platform y Adobe Experience Cloud, que admiten segmentación avanzada, personalización y otros casos de uso de marketing.
2. El extremo por lotes permitirá que las solicitudes se envíen por lotes cuando sea necesario incorporar datos sin recibir una respuesta de las aplicaciones a las que se llama.

El [!DNL Server API] admite el siguiente tipo de solicitudes:

* Solicitudes autenticadas mediante [Adobe I/O](https://developer.adobe.com/), utilizando el nuevo `server.adobedc.net` punto final.
* Solicitudes no autenticadas a través de `edge.adobedc.net` punto final.

Esto habilita casos de uso que permiten una recopilación segura y autenticada de datos confidenciales, según las políticas de privacidad de su organización. Además de la autenticación, la API de servidor admite el marcado de flujos de datos para aceptar solo la comunicación autenticada a través de la API.

Vea el siguiente vídeo para obtener una descripción general optimizada de la API de servidor.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
