---
title: Información general sobre la API del cliente (alfa)
seo-title: Información general sobre la API del cliente (alfa)
description: Este documento proporciona información general sobre Sensei Insights - Customer AI (Alpha)
seo-description: Este documento proporciona información general sobre Sensei Insights - Customer AI (Alpha)
index: false
translation-type: tm+mt
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Información general sobre la API del cliente (alfa)

>[!NOTE]
>La funcionalidad de AI del cliente descrita en este documento está en alfa. La documentación y la funcionalidad están sujetas a cambios.

La API de cliente en Adobe Experience Platform proporciona a los especialistas en marketing la capacidad de aprovechar Adobe Sensei para anticipar lo que sus clientes harán a continuación mediante el aprendizaje automático.

## ¿Para qué se utiliza?

La API del cliente se utiliza para generar puntuaciones de tendencia personalizadas, como la conversión y la ignición, para perfiles individuales a escala. Esto se logra sin tener que transformar las necesidades comerciales en un problema de aprendizaje automático, eligiendo un algoritmo, capacitación o implementación.

La API del cliente está diseñada para:

- Mejore el perfil del cliente en tiempo real con puntuaciones de tendencia del cliente como la conversión y la reproducción.
- Mejore los perfiles del cliente con códigos de razón para las puntuaciones de tendencia.
- Cree segmentos de clientes basados en puntuaciones de tendencia y factores influyentes.

El cliente no está diseñado para:

- Prediga el precio de compra de los productos.
- Prediga qué productos comprados anteriormente estarán en el siguiente pedido del cliente.
- Generar recomendaciones de productos a escala.
- Dictar la etapa del viaje de compra en la que se encuentra el cliente
- Prediga el siguiente total de salida del cliente.

## ¿Cómo funciona?

La API del cliente funciona analizando los datos de eventos de experiencia del consumidor existentes para predecir las puntuaciones de tendencia de conversión o de ignición de conversión. Adobe se da cuenta de que la definición de conversión e ignición no es uniforme en todos los casos de uso y, por este motivo, puede definir objetivos personalizados como un conjunto de condiciones. Puede configurar el objetivo previsto siempre que el evento de interés esté presente en los datos del evento de experiencia del consumidor de entrada.

## ¿Qué debo hacer para comenzar?

Para empezar, siga el tutorial del documento [Predecir puntuaciones de tendencia del cliente mediante la API](./customer-ai-tutorial.md)del cliente. Proporciona los pasos para utilizar la API del cliente y muestra la creación de segmentos del cliente mediante puntuaciones de tendencia.