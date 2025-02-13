---
solution: Experience Platform
title: Comparación de Edge Network y hub
description: Obtenga información acerca de las diferentes rutas de procesamiento disponibles para usar en Adobe Experience Platform.
source-git-commit: 08a63fb854fe1c2aa83e7a7f74df4c02580e4d4c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---


# Comparación de Edge Network y hub

Adobe Experience Platform es el sistema más potente, flexible y abierto del mercado para crear y administrar soluciones completas que mejoren la experiencia del cliente. Puede utilizar Experience Platform para centralizar y estandarizar los datos y el contenido de los clientes de cualquier sistema y aplicar la ciencia de datos y el aprendizaje automático para mejorar en gran medida el diseño y el envío de las experiencias personalizadas enriquecidas. Como resultado, Platform tiene varias formas de procesar los datos, lo que le permite evaluarlos de la mejor manera posible.

## Tipos de servidor

En Platform, los datos se pueden procesar en dos rutas diferentes: Adobe Experience Platform hub para flujos de trabajo por lotes y de flujo continuo, y Edge Network para experiencias en tiempo real.

### concentrador de Adobe Experience Platform

Hub es un centro de datos principal que goza de una ubicación central y que contiene todos los datos históricos y el contexto de perfil enriquecido que se han recopilado en Adobe Experience Platform. Esto le permite enviar y recibir datos más sólidos y completos a sus servicios descendentes. Como resultado, hub debería usarse en escenarios donde la **minuciosidad** de los datos sea más importante.

Los servicios disponibles en hub incluyen los siguientes:

- Segmentación por lotes
- Segmentación de streaming
- Perfiles
- Destinos
- Gráfico de identidad
- Data Distiller: servicio de consultas
- Conectores de Source

### Experience Platform Edge Network

Edge Network es un servidor que se encuentra físicamente más cerca de diferentes ubicaciones geográficas. Estos centros de datos procesan todos los datos recopilados a través de las extensiones de SDK y las API de Edge Network. Los únicos datos que residen en Edge Network son las pertenencias a audiencias, las identidades de perfil y los atributos necesarios para la personalización.

Edge Network permite enviar y recibir datos a sus clientes más rápidamente debido a su mayor proximidad al usuario final. Además, puede utilizar Edge Network para procesar solicitudes de reenvío de eventos y solicitudes de administración de etiquetas. Sin embargo, Edge Network solo procesa los datos de **comportamiento**. Como resultado, Edge Network debería usarse en escenarios donde la **velocidad** de los datos sea más importante.

Los servicios disponibles en Edge Network son los siguientes:

- Segmentación de Edge
- Perfiles de Edge
- Destinos de Edge
- Recopilación de datos
- Extensiones de SDK

## Ubicaciones

En la siguiente sección se enumeran las ubicaciones de hub y Edge Network.

![Diagrama que enumera las diferentes ubicaciones para los servidores hub y Edge Network.](./images/servers/platform-server-locations.png)

**Hub**

- VA7 (Virginia, EE.UU.)
- NLD2 (Países Bajos)
- AUS5 (Australia)
- CAN2 (Canadá)
- GBR9 (Reino Unido)
- IND1 (India)

**Edge Network**

- OR2 (Oregón, Estados Unidos)
- VA6 (Virginia, EE. UU.)
- IRL1 (Irlanda)
- IND1 (India)
- SGP3 (Singapur)
- AUS3 (Australia)
- JPN3 (Japón)

Encontrará información más detallada sobre las ubicaciones de servidores disponibles en [descripción general de varias nubes](./multi-cloud.md#available-cloud-regions).

## Pasos siguientes

Después de leer esta descripción general, ahora comprende las diferencias entre procesar datos en Adobe Experience Platform hub y en Adobe Experience Platform Edge Network.

## Apéndice

En la siguiente sección se muestra información complementaria sobre el procesamiento de datos en Adobe Experience Platform.

### Preguntas frecuentes

En la siguiente sección se enumeran las preguntas más frecuentes sobre hub y Edge Network:

#### ¿Qué escenarios son los más adecuados para hub?

Hub es más adecuado en escenarios donde la **minuciosidad** de los datos es más importante. Por ejemplo, supongamos que desea crear una campaña de marketing dirigida a todos los clientes que han abandonado los carros de compras. En ese caso de uso, puede utilizar la segmentación por lotes creando una audiencia que coincida con los usuarios del carro de compras abandonados y exportándola a un destino por lotes.

#### ¿Qué escenarios son los más adecuados para Edge Network?

Edge Network es más adecuado para escenarios donde la **velocidad** de los datos es más importante. Por ejemplo, supongamos que necesita crear una venta flash limitada para dirigirse a un cliente que esté navegando por su sitio con un producto en el carro de compras. En ese caso de uso, puede utilizar la segmentación de Edge, lo que le permite establecer como objetivo y enviar inmediatamente una notificación personalizada a los usuarios con un producto en su carro de compras con una &quot;venta flash&quot;.

#### ¿Qué datos pasan de hub a Edge Network?

Solo los datos necesarios para ofrecer experiencias en tiempo real en el perímetro de se cargan de hub a Edge Network. Estos datos se envían automáticamente desde Hub a Edge Network para mantenerlos coherentes a largo plazo y solo se conservan durante un máximo de 14 días. Sin embargo, esto **no** significa que los datos se mantienen perfectamente sincronizados con los datos de hub. Como resultado, puede haber diferencias en los datos disponibles entre hub y Edge Network.
