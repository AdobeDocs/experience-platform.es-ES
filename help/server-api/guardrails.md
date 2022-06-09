---
title: Protecciones de rendimiento
description: Aprenda a utilizar la API del servidor dentro de protecciones de rendimiento óptimas
keywords: recopilación de datos;recopilación;red perimetral;api;sla;slt;niveles de servicio
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 6f0eb81f9709cf4fcaea94334449117c4ed76107
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---

# Protecciones de rendimiento

## Información general {#overview}

Las protecciones de rendimiento definen los límites de uso relacionados con los casos de uso de la API del servidor. Si se exceden las limitaciones de rendimiento indicadas en este artículo, el rendimiento podría degradarse.

El Adobe no es responsable de la degradación del rendimiento causada por los límites de uso excedidos. Los clientes que superen de manera consistente las barreras de rendimiento pueden solicitar capacidad de procesamiento adicional para evitar la degradación del rendimiento.

## Definiciones

* **Disponibilidad** se calcula para cada intervalo de cinco minutos como el porcentaje de solicitudes procesadas por la red perimetral del Experience Platform que no fallan con errores y están relacionadas únicamente con las API de red perimetral aprovisionadas. Si un inquilino no realizó ninguna solicitud en un intervalo de cinco minutos determinado, se considera que ese intervalo está disponible al 100%.
* **Porcentaje de tiempo activo mensual** para una región determinada se calcula como el promedio de disponibilidad para los intervalos de cinco minutos en un mes.
* Un **Upstream** es un servicio detrás de la red perimetral, habilitado para un conjunto de datos específico, como el reenvío del lado del servidor de Adobe, la segmentación de Adobe Edge o Adobe Target.
* A **unidad de solicitud** corresponde a un fragmento de 8 KB de una solicitud y a un fragmento ascendente configurado para un conjunto de datos.
* A **solicitud** es un único mensaje que envía una aplicación propiedad del cliente a la variable [!DNL Server API]. Una solicitud puede contener una o más unidades de solicitud.
* Un **error** es cualquier solicitud que falla debido a una red perimetral [error de servicio interno](error-handling.md).

## Límites de servicio

Todos los conjuntos de datos aplican ciertos límites de uso, que principalmente controlan cuántos eventos se pueden enviar simultáneamente, su tamaño y la cantidad de servicios de subida a los que se dirigen esas solicitudes.

### Solicitar unidades

Todos los límites se aplican y normalizan a lo largo de un **unidad de solicitud (RU)**, definido como **Fragmento de 8 KB** de una solicitud que va a un servicio ascendente configurado en un conjunto de datos.

#### Ejemplos

| Transmisiones configuradas por conjunto de datos | Tamaño promedio de la solicitud | Solicitar unidades |
| --- | --- | --- |
| 1 (Plataforma de Adobe) | 8 KB (1 fragmento) | 1 |
| 2 (Plataforma de Adobe, Adobe Target) | 8 KB (1 fragmento) | 2 |
| 2 (Plataforma de Adobe, Adobe Target) | 16 KB (2 fragmentos) | 4 |
| 2 (Plataforma de Adobe, Adobe Target) | 64 KB (8 fragmentos) | 16 |

### Límites de unidades de solicitud

La tabla siguiente muestra los valores de límite predeterminados. Si necesita límites de unidades de solicitud más altos, póngase en contacto con el representante de cuentas.

| Punto final | Solicitudes de unidades por segundo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Límite de tamaño de solicitud HTTP

| Formato de carga útil | Tamaño máximo de una solicitud | Máximo de fragmentos de solicitud de 8 KB |
| --- | --- | --- |
| Texto sin formato JSON | 64 kB | 8 |


>[!NOTE]
>
>Dependiendo de la carga útil en sí, los formatos binarios generalmente son entre un 20 y un 40% más compactos, lo que le permite insertar más datos de los que tendría en el JSON de texto sin formato. Póngase en contacto con su representante del Servicio de atención al cliente si necesita una mayor capacidad para sus conjuntos de datos.
