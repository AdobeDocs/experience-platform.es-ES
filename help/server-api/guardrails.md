---
title: Protecciones de rendimiento para la API de servidor de Edge Network
description: Aprenda a utilizar la API de servidor dentro de protecciones de rendimiento óptimas.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# Protecciones de rendimiento para la API de servidor de Edge Network

## Información general {#overview}

Las protecciones de rendimiento definen los límites de uso relacionados con los casos de uso de la API de servidor. Si se superan las barreras de rendimiento descritas en este artículo, podría producirse una degradación del rendimiento.

Adobe no se responsabiliza de la degradación del rendimiento causada por los límites de uso excedidos. Los clientes que superan de forma consistente las barreras de rendimiento pueden solicitar capacidad de procesamiento adicional para evitar una degradación del rendimiento.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

Todas las protecciones de rendimiento descritas en esta página se aplican al nivel de organización de IMS. Para los usuarios con varias organizaciones de IMS configuradas, cada organización está sujeta individualmente a las protecciones de rendimiento que se indican a continuación. Consulte el [glosario de Experience Platform](../landing/glossary.md) para obtener más información sobre [!DNL IMS Organizations].

## Definiciones

* **Disponibilidad** se calcula para cada intervalo de cinco minutos como el porcentaje de solicitudes procesadas por Experience Platform Edge Network que no generan errores y que se relacionan únicamente con las API de Edge Network aprovisionadas. Si un inquilino no realizó ninguna solicitud en un intervalo determinado de cinco minutos, ese intervalo se considera disponible al 100 %.
* **El porcentaje de tiempo de actividad mensual** de una región determinada se calcula como el promedio de la disponibilidad para todos los intervalos de cinco minutos de un mes.
* Un **flujo ascendente** es un servicio detrás de Edge Network, habilitado para un conjunto de datos específico, como el reenvío del lado del servidor de Adobe, la segmentación de Adobe Edge o Adobe Target.
* Una **unidad de solicitud** corresponde a un fragmento de 8 KB de una solicitud y un flujo ascendente configurado para una secuencia de datos.
* Una **solicitud** es un solo mensaje enviado por una aplicación propiedad del cliente a [!DNL Server API]. Una solicitud puede contener una o más unidades de solicitud.
* Un **error** es cualquier solicitud que falla debido a un [error de servicio interno](error-handling.md) de Edge Network.

## Límites de servicio

Todos los flujos de datos aplican ciertos límites de uso, que controlan principalmente la cantidad de eventos que se pueden enviar simultáneamente, su tamaño y la cantidad de servicios de flujo ascendente a los que se dirigen esas solicitudes.

### Solicitar unidades

Todos los límites se aplican y normalizan en una **unidad de solicitud (RU)**, definida como un **fragmento de 8 KB** de una solicitud que va a un servicio ascendente configurado en una secuencia de datos.

#### Ejemplos

| Flujos ascendentes configurados por flujo de datos | Tamaño promedio de la solicitud | Solicitar unidades |
| --- | --- | --- |
| 1 (Adobe Experience Platform) | 8 KB (1 fragmento) | 1 |
| 2 (Adobe Experience Platform, Adobe Target) | 8 KB (1 fragmento) | 2 |
| 2 (Adobe Experience Platform, Adobe Target) | 16 KB (2 fragmentos) | 4 |
| 2 (Adobe Experience Platform, Adobe Target) | 64 KB (8 fragmentos) | 16 |

### Límites de unidades de solicitud

La tabla siguiente muestra los valores de límite predeterminados. Si necesita límites de unidades de solicitud más altos, póngase en contacto con el representante de la cuenta.

| Punto de conexión | Unidades de solicitudes por segundo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |

### Límite de tamaño de solicitud HTTP

| Formato de carga útil | Tamaño máximo de una solicitud | Fragmentos de solicitud máximos de 8 KB |
| --- | --- | --- |
| Texto sin formato JSON | 64 KB | 8 |


>[!NOTE]
>
>Según la carga útil en sí, los formatos binarios suelen ser entre un 20 y un 40 % más compactos, lo que le permite insertar más datos de los que haría en JSON de texto sin formato. Póngase en contacto con el representante del Servicio de atención al cliente si necesita una mayor capacidad para sus flujos de datos.

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
