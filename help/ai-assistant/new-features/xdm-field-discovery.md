---
title: Descubrimiento de campos XDM con el asistente de IA
description: Lea este documento para aprender a utilizar el asistente de IA para la detección de campos del modelo de datos de experiencia (XDM).
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Descubrimiento de campos XDM para con el asistente de IA

>[!AVAILABILITY]
>
>Esta función está en Alpha y es posible que no esté disponible para su organización. Para participar en el programa de Alpha y acceder a esta función, póngase en contacto con el equipo de cuenta de Adobe.

Puede utilizar el Asistente de IA para buscar y descubrir campos del Modelo de datos de experiencia (XDM) que luego puede utilizar para crear audiencias segmentadas dentro de Experience Platform.

Lea la siguiente tabla para ver los patrones de consulta y solicitud admitidos para la detección de campos XDM en el Asistente de IA.

>[!TIP]
>
>Aunque los patrones de consulta y petición de datos pueden ser los mismos en diferentes casos de uso, la formulación exacta de una pregunta variará según los campos XDM y los esquemas utilizados para una zona protegida determinada.

| Tipo de consulta | Patrón de consulta/solicitud | Ejemplos |
| --- | --- | --- |
| Detección de campos XDM por dominio o área de datos | Mostrarme los campos XDM utilizados para representar {DATA_DOMAIN/AREA}. | <ul><li>Muéstreme los campos XDM utilizados para representar los datos de consentimiento.</li><li>Mostrarme los campos XDM utilizados para representar información sobre las suscripciones por correo electrónico.</li></ul> |
| Detección de campos XDM por nombre de campo general | <ul><li>Mostrar los campos XDM relacionados con {DATA_DOMAIN/AREA}.</li><li>Qué campos XDM contienen {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Mostrarme los campos XDM relacionados con los pedidos.</li><li>Mostrarme los campos XDM relacionados con los detalles de interacción.</li><li>¿Qué campo XDM contiene ID de visitante?</li><li>¿Qué campo XDM contiene categorías de productos?</li></ul> |
| Detección de campos XDM por linaje del modelo de datos | <ul><li>Mostrar todos los campos del {FIELD_GROUP/CLASS_NAME} que contienen {GENERAL_FIELD_NAME}.</li><li>¿Qué es el {FIELD_GROUP/CLASS_NAME} del campo XDM {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Mostrar todos los campos del grupo de campos que contienen datos de producto.</li><li>Mostrar todos los campos del grupo de campos que contiene datos de análisis.</li><li>¿Cuál es la clase del nombre del campo XDM?</li><li>¿Cuál es la clase de las suscripciones de correo electrónico del campo XDM?</li></ul> |
| Preguntar para obtener descripciones mejoradas junto con nombres de campo | {FIELD_DISCOVERY_QUERY}. Incluya también descripciones mejoradas. | <ul><li>Muéstreme los campos XDM utilizados para representar los datos de consentimiento. Incluya también la descripción mejorada del campo.</li><li>Mostrarme los campos XDM relacionados con los detalles de interacción. Incluya también la descripción mejorada del campo.</li></ul> |

{style="table-layout:auto"}