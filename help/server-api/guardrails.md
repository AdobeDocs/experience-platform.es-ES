---
title: Protecciones de rendimiento para la API del servidor de red perimetral
description: Aprenda a utilizar la API de servidor dentro de protecciones de rendimiento óptimas.
keywords: recopilación de datos;recopilación;red perimetral;api;sla;slt;niveles de servicio
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 0e609ce278af0c93503f05778887ad1bd881524a
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Protecciones de rendimiento para la API del servidor de red perimetral

## Información general {#overview}

Las protecciones de rendimiento definen los límites de uso relacionados con los casos de uso de la API de servidor. Si se superan las barreras de rendimiento descritas en este artículo, podría producirse una degradación del rendimiento.

El Adobe de no es responsable de la degradación del rendimiento causada por los límites de uso excedidos. Los clientes que superan de forma consistente las barreras de rendimiento pueden solicitar capacidad de procesamiento adicional para evitar una degradación del rendimiento.

## Definiciones

* **Disponibilidad** se calcula para cada intervalo de cinco minutos como el porcentaje de solicitudes procesadas por la red perimetral de Experience Platform que no fallan con errores y se relacionan únicamente con las API de red perimetral aprovisionadas. Si un inquilino no realizó ninguna solicitud en un intervalo determinado de cinco minutos, ese intervalo se considera disponible al 100 %.
* **Porcentaje de tiempo activo mensual** para una región determinada se calcula como el promedio de la disponibilidad para todos los intervalos de cinco minutos en un mes.
* Un **corriente arriba** es un servicio detrás de la red perimetral, habilitado para un conjunto de datos específico, como el reenvío del lado del servidor de Adobe, la segmentación de Adobe Edge o Adobe Target.
* A **unidad de solicitud** corresponde a un fragmento de 8 KB de una solicitud y a un flujo ascendente configurado para una secuencia de datos.
* A **solicitud** es un mensaje único enviado por una aplicación propiedad del cliente a [!DNL Server API]. Una solicitud puede contener una o más unidades de solicitud.
* Un **error** es cualquier solicitud que falla debido a una red perimetral [error de servicio interno](error-handling.md).

## Límites de servicio

Todos los flujos de datos aplican ciertos límites de uso, que controlan principalmente la cantidad de eventos que se pueden enviar simultáneamente, su tamaño y la cantidad de servicios de flujo ascendente a los que se dirigen esas solicitudes.

### Solicitar unidades

Todos los límites se aplican y normalizan sobre una **unidad de solicitud (RU)**, definido como **Fragmento de 8 KB** de una solicitud que va a un servicio ascendente configurado en una secuencia de datos.

#### Ejemplos

| Flujos ascendentes configurados por flujo de datos | Tamaño promedio de la solicitud | Solicitar unidades |
| --- | --- | --- |
| 1 (Plataforma de Adobe) | 8 KB (1 fragmento) | 1 |
| 2 (Plataforma de Adobe, Adobe Target) | 8 KB (1 fragmento) | 2 |
| 2 (Plataforma de Adobe, Adobe Target) | 16 KB (2 fragmentos) | 4 |
| 2 (Plataforma de Adobe, Adobe Target) | 64 KB (8 fragmentos) | 16 |

### Límites de unidades de solicitud

La tabla siguiente muestra los valores de límite predeterminados. Si necesita límites de unidades de solicitud más altos, póngase en contacto con el representante de la cuenta.

| Extremo | Unidades de solicitudes por segundo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Límite de tamaño de solicitud HTTP

| Formato de carga útil | Tamaño máximo de una solicitud | Fragmentos de solicitud máximos de 8 KB |
| --- | --- | --- |
| Texto sin formato JSON | 64 kB | 8 |


>[!NOTE]
>
>Según la carga útil en sí, los formatos binarios suelen ser entre un 20 y un 40 % más compactos, lo que le permite insertar más datos de los que haría en JSON de texto sin formato. Póngase en contacto con el representante del Servicio de atención al cliente si necesita una mayor capacidad para sus flujos de datos.

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-time Customer Data Platform (edición B2C - paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P: paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Paquetes B2B Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
