---
title: Acuerdos y objetivos de nivel de servicio
description: Obtenga información sobre cómo configurar la autenticación para la API de servidor de red perimetral
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: recopilación de datos;recopilación;red perimetral;api;sla;slt;niveles de servicio
hide: true
hidefromtoc: true
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# Seguridad

## Información general {#overview}

El Adobe utilizará esfuerzos comercialmente razonables para hacer que la [!DNL Server API] disponible en un porcentaje mensual de tiempo activo de al menos el 99,9% para cada región, durante cualquier ciclo de facturación mensual.

## Definiciones

* **Disponibilidad** se calcula para cada intervalo de cinco minutos como el porcentaje de solicitudes procesadas por la red perimetral de Experience Adobe Experience Platform que no fallan con errores y están relacionadas únicamente con las API de red perimetral de Adobe Experience Platform aprovisionadas. Si un inquilino no realizó ninguna solicitud en un intervalo de cinco minutos determinado, se considera que ese intervalo está disponible al 100%.
* **Porcentaje de tiempo activo mensual** para una región determinada se calcula como el promedio de disponibilidad para los intervalos de cinco minutos en un mes.
* Un **Upstream** es un servicio detrás de Adobe Edge Network, habilitado para un conjunto de datos específico, como Adobe Server Side Forwarding, Adobe Edge Segmentation o Adobe Target.
* A **solicitud** enviado a la API de servidor se define como una o más unidades de solicitud.
* A **unidad de solicitud** corresponde a un fragmento de 8 KB de una solicitud y a un fragmento ascendente configurado para un conjunto de datos.
* Un **error** es cualquier solicitud que falle debido a una red perimetral de Adobe Experience Platform [error de servicio interno](error-handling.md).

## Objetivos internos

Los equipos de ingeniería de Adobe implementan procedimientos de telemetría, monitoreo y ampliación en tiempo real para garantizar los siguientes objetivos:

* Menos del 1% de las solicitudes HTTP devuelven `5xx` errores en los últimos cinco minutos
* Menos del 1 % de las conexiones de flujo ascendente devuelven un error en los últimos cinco minutos
* Cualquier capacidad de inquilino se duplica en menos de 10 minutos desde el momento en que se alcanza un límite.

## Exclusiones de acuerdos de nivel de servicio

La asignación de nivel de servicio descrita anteriormente no se aplica a ningún problema de falta de disponibilidad o rendimiento causado por los siguientes eventos:

* Factores fuera de nuestro control razonable, incluyendo acceso a Internet o problemas relacionados más allá de la infraestructura del Adobe.
* Cualquier uso indebido de [!DNL Server API], tal como se define en los límites descritos a continuación.

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

