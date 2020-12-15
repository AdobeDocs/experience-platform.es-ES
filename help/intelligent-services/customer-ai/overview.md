---
keywords: Experience Platform;overview;customer ai;popular topics;customer ai overview
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 'Información general sobre Customer AI '
topic: Customer AI overview
description: La AI del cliente se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.
landing-page-description: Customer AI is used to generate custom propensity scores such as churn and conversion for individual profiles at-scale.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 16%

---


# Información general sobre Customer AI 

La API del cliente, como parte de Servicios inteligentes, proporciona a los especialistas en marketing la capacidad de generar predicciones de clientes a nivel individual con explicaciones.

Con la ayuda de factores influyentes, la información sobre el cliente puede indicarle qué es lo que probablemente hará un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de la API del cliente para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados.

## Explicación de la AI del cliente

La AI del cliente se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

La API del cliente está diseñada para:

- Proporcione modelos de propensión del cliente de alta precisión para lograr una segmentación y un objetivo más sólidos.
- Ayudar a comprender los factores influyentes y la probabilidad que hay detrás de ciertos comportamientos del cliente.
- Proporcione opciones personalizables para los casos de uso y los datos únicos de su compañía.
- Mejore el Perfil de los clientes en tiempo real con puntuaciones de tendencia de los clientes como la conversión y la reproducción.
- Mejore los perfiles de los clientes con factores influyentes para las puntuaciones de tendencia.
- Cree segmentos de clientes basados en factores influyentes y puntuaciones de tendencia.

El cliente no está diseñado para:

- La API del cliente no debe utilizarse para predecir precios dinámicos ni el punto de precio en el que el cliente va a realizar una compra.
- La AI del cliente no puede determinar si la oferta aumentará la probabilidad de que el cliente compre un artículo. Aunque puede decidir enviar ofertas de descuento en función de las puntuaciones de tendencia, no es necesariamente la mejor forma de convertir a esos clientes.
- La API del cliente no es una herramienta de recomendaciones de productos. Si tiene miles de SKU, no utilice la API del cliente como proxy para una solución de recomendaciones de productos real como [!DNL Adobe Target].
- La AI del cliente no puede predecir en qué etapa del viaje de compra se encuentra el cliente, por ejemplo, si se encuentra en etapas de &quot;concienciación&quot;, &quot;consideración&quot;, &quot;compra&quot; o &quot;retención&quot;.
- No utilice la API del cliente para determinar los clientes que probablemente comprarán un producto en el futuro. Esto requiere que algunos eventos de éxito estén presentes en el pasado para que la API del cliente pueda entrenar correctamente el algoritmo de aprendizaje automático en los datos.

El siguiente vídeo está diseñado para ayudarle a comprender la información sobre la información de los clientes.

>[!VIDEO](https://video.tv.adobe.com/v/32664?learn=on&quality=12)

## ¿Cómo funciona?

La API del cliente funciona analizando los datos existentes del Evento de la experiencia del consumidor para predecir las puntuaciones de tendencia a la conversión o a la producción. Adobe se da cuenta de que la definición de generación y conversión no es uniforme en todos los casos de uso y, por este motivo, puede definir objetivos de destinatario personalizados como un conjunto de condiciones. Puede configurar el objetivo previsto siempre que el evento de interés esté presente en los datos de entrada de Evento de experiencias de consumo.

## Pasos siguientes

Puede empezar por seguir la guía de [introducción](./getting-started.md) . Esta guía lo acompaña durante la configuración de todos los requisitos previos necesarios para la API del cliente. Si ya tiene todas las credenciales y los datos listos, visite [Configuración de una instancia](./user-guide/configure.md)de AI de cliente. Proporciona los pasos para utilizar la API del cliente.