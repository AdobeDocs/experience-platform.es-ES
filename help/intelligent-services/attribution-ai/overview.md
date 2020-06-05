---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Información general de Atribución de IA
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Información general de Atribución de IA

La API de atribución, como parte de Servicios Inteligentes, es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados. Con la API de atribución, los especialistas en mercadotecnia pueden medir y optimizar el gasto en mercadotecnia y publicidad al comprender el impacto de cada interacción del cliente en cada fase de los viajes de los clientes.

## Explicación de la IA de atribución

La API de atribución se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en mercadotecnia pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de mercadotecnia individual en los viajes de los clientes. Algunos ejemplos de puntos de contacto son: impresiones de anuncios en pantalla, envíos de correo electrónico, aperturas de correo electrónico y clics de búsqueda paga.

Las salidas de la API de atribución se pueden separar en varias dimensiones y se pueden utilizar en diferentes etapas del viaje del cliente. Esto se logra sin necesidad de traducir las necesidades comerciales en problemas de aprendizaje automático, selección de algoritmos, capacitación o implementación de modelos.

Los datos de AI de atribución pueden provenir de Adobe (p. ej. [!DNL Analytics]) o fuentes de datos que no sean de Adobe.

La IA de atribución admite dos categorías de puntuaciones, algorítmica y basada en reglas. Las puntuaciones algorítmicas incluyen puntuaciones incrementales e influenciadas. Las puntuaciones basadas en reglas incluyen Primer toque, Último toque, Lineal, en forma de U y Decadencia de tiempo.

El siguiente vídeo está diseñado para admitir su comprensión de la Atribución de IA.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Puntuaciones algorítmicas de la IA de atribución

La IA de atribución admite dos categorías de puntuaciones de atribución, las puntuaciones algorítmicas y las basadas en reglas.

La IA de atribución produce dos tipos diferentes de puntuaciones algorítmicas, incrementales e influenciadas. Una puntuación influida es la fracción de conversión de la que es responsable cada punto de contacto de marketing. Una puntuación incremental es la cantidad de impacto marginal causado directamente por el punto de contacto de marketing. La principal diferencia entre la puntuación incremental y la puntuación influida es que la puntuación incremental tiene en cuenta el efecto basal. No supone que una conversión se deba únicamente a los puntos de contacto de marketing anteriores.

Consulte la tabla siguiente para obtener más detalles sobre cada una de estas puntuaciones de atribución:

| Puntuaciones de atribución | Descripción |
| ----- | ----------- |
| Primer contacto | Puntuación de atribución basada en reglas que asigna todos los créditos al punto de contacto inicial en una ruta de conversión. |
| Último contacto | Puntuación de atribución basada en reglas que asigna todo el crédito al punto de contacto más cercano a la conversión. |
| Lineal | Puntuación de atribución basada en reglas que asigna el mismo crédito a cada punto de contacto de una ruta de conversión. |
| Forma de U | Puntuación de atribución basada en reglas que asigna el 40 % del crédito al primer punto de contacto y el 40 % del crédito al último punto de contacto, mientras que los demás puntos de contacto dividen el 20 % restante de forma equitativa. |
| Deterioro de tiempo | Puntuación de atribución basada en reglas donde los puntos de contacto más cercanos a la conversión reciben más crédito que los puntos de contacto más alejados en el tiempo de la conversión. |
| Influenciado (algorítmico) | La puntuación influida es la fracción de conversión de la que es responsable cada punto de contacto de marketing. |
| Incremental (algorítmico) | La puntuación incremental es la cantidad de impacto marginal causado directamente por un punto de contacto de marketing. |

## Ejemplos de casos de uso comercial

La API de atribución se puede utilizar para ayudar en los siguientes casos de uso de ejemplo:

- **sistema de informes** Ejecutivo: Permita que los ejecutivos entiendan el verdadero impacto incremental de la mercadotecnia, tanto en su conjunto como por canal, región, SKU, etc.
- **Asignación** presupuestaria: Informe las decisiones de asignación presupuestaria en todos los canales de marketing.
- **Optimización** de Campaña: En cada canal, comprenda qué campañas, elementos creativos y palabras clave funcionan mejor para qué SKU o términos. Esto le permite mirar cada canal para que el equipo de mercadotecnia pueda optimizar sus tácticas.
- **Atribución** de canal completo: Comprender el impacto de la mercadotecnia en todo el viaje del cliente. Por ejemplo, el inicio de sesión con cuenta gratuita en la conversión paga y más allá.
- **Evaluaciones** de socios: Evaluar la eficacia de los organismos y asociados sobre la base de los resultados de la atribución.

### Funciones adicionales

La API de atribución también oferta la integración con otras soluciones de Adobe como [!DNL Adobe Analytics]. Esto le permite utilizar estas soluciones para utilizar el modelo algorítmico personalizable para evaluar el rendimiento de los medios y proporcionar perspectivas analíticas.

## Pasos siguientes

Puede empezar por seguir la guía de [introducción](./getting-started.md) . Esta guía lo acompaña durante la configuración de todas las solicitudes previas requeridas para la API de atribución. Si ya tiene las credenciales y los datos listos, visite la guía del usuario de [Atribución de AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia y enviarla para capacitación y puntuación.