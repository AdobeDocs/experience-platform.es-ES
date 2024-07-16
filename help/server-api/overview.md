---
title: Información general sobre API de Edge Network Server
description: Descubra qué es la API del servidor de red perimetral y cómo puede utilizarla.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---

# Información general sobre API de Edge Network Server {#overview}

El Edge Network de Adobe Experience Platform ofrece una forma optimizada para que los clientes interactúen con cualquier servicio de Adobe Experience Cloud o Adobe Experience Platform Edge.

[!DNL Edge Network Server API] se puede usar para varios casos de uso de recopilación de datos, personalización, publicidad y marketing. [!DNL Server API] se puede usar en servidores, [!DNL IoT] dispositivos, descodificadores y otros dispositivos.

Dado que [!DNL Server API] no depende de ninguna biblioteca para cargarse, ofrece una forma rápida de interactuar con el Edge Network de Adobe Experience Platform y las soluciones compatibles.

Entre las ventajas de la arquitectura [!DNL Server API] se incluyen:

* Tiempo de carga de página reducido
* Latencia mejorada
* Recopilación de datos de origen
* Comunicación optimizada del lado del servidor entre servicios

[!DNL Server API] admite la recopilación de datos interactiva y por lotes, a través de dos extremos dedicados:

1. El extremo interactivo admite la comunicación con los servicios de Adobe Experience Platform y Adobe Experience Cloud que admiten la segmentación avanzada, la personalización y otros casos de uso de marketing.
2. El extremo por lotes permite enviar solicitudes en lote cuando se deben incorporar datos sin recibir una respuesta de las aplicaciones a las que se llama.

[!DNL Server API] admite el siguiente tipo de solicitudes:

* Solicitudes autenticadas a través de [Adobe Developer](https://developer.adobe.com/), usando el extremo `server.adobedc.net`.
* Solicitudes no autenticadas a través del extremo `edge.adobedc.net`.

Esto habilita casos de uso que permiten la recopilación segura y autenticada de datos confidenciales, según las políticas de privacidad de su organización. Además de la autenticación, la API de servidor admite el marcado de flujos de datos para aceptar solo la comunicación autenticada a través de la API.

Vea el siguiente vídeo para obtener una descripción general optimizada de la API de servidor.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
