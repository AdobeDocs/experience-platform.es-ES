---
keywords: Experience Platform;home;popular topics;offer management;Offer Management;Journey;customer journey;journey;decision events;decision event;Decision events
solution: Experience Platform
title: Offer Decisioning
topic: overview
description: El servicio de toma de decisiones permite crear experiencias personalizadas, optimizadas y orquestadas en aplicaciones que se ejecutan en Adobe Experience Platform. Con el servicio de toma de decisiones, puede determinar la mejor opción a partir de un conjunto de opciones disponibles. Estas opciones, también denominadas alternativas, pueden ser ofertas, recomendaciones de productos, componentes de contenido para una experiencia web, secuencias de comandos de conversación y acciones que se deben realizar.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---


# Visión general del servicio de decisiones

[!DNL Decisioning Service] proporciona la capacidad de crear experiencias personalizadas, optimizadas y orquestadas en aplicaciones que se ejecutan en Adobe Experience Platform. Con [!DNL Decisioning Service], puede determinar la mejor *opción* a partir de un conjunto de opciones disponibles. Estas opciones, también denominadas alternativas, pueden ser ofertas, recomendaciones de productos, componentes de contenido para una experiencia web, secuencias de comandos de conversación y acciones que se deben realizar. Actualmente se admite el caso de uso y el dominio de *Offer Decisioning* , donde las opciones de decisión se modelan específicamente como ofertas, con compatibilidad para más casos de uso en el futuro.

Con [!DNL Decisioning Service], los clientes pueden reutilizar la lógica empresarial y compartir un catálogo de opciones entre canales y aplicaciones. En lugar de administrar las opciones de decisión (y las estrategias para seleccionarlas) en profundidad dentro de una aplicación, ahora se pueden aprovechar independientemente de cuándo, cómo y en qué canal interactúa el usuario final de un cliente con una empresa u organización.

Las estrategias de toma de decisiones pueden influir en las muchas interacciones que ha tenido un cliente en muchos canales y aplicaciones. Por ejemplo: la actividad de la aplicación del centro de llamadas podría habilitar o suprimir un mensaje de marketing durante algún tiempo después de una queja, y ese mensaje en sí puede basarse en las compras realizadas y las revisiones anunciadas por el cliente.

[!DNL Decisioning Service] facilita la personalización de experiencias evolucionadas.

| Antes de la decisión de la experiencia | Después de la decisión de la experiencia |
| --- | --- |
| Personalice y optimice las experiencias de sus usuarios en un solo canal o en un pequeño conjunto de puntos de contacto de experiencia. | Las experiencias son respuestas orquestadas en todas las interacciones. |
| Las optimizaciones se centran en una fase única y generalmente corta del viaje del usuario final | Las decisiones se basan en todo el historial de interacción, desde los comportamientos detectados en el pasado hasta el contexto más reciente. |
| Las opciones y las estrategias para seleccionar qué presentar durante la experiencia de un cliente se codifican normalmente en profundidad dentro de una aplicación. | Las estrategias para seleccionar la mejor opción se definen fuera de las aplicaciones específicas del canal y se vuelven reutilizables. |
| Las experiencias de los clientes se personalizan y optimizan según un objetivo simplista, por ejemplo: aumentar el número de cierres de compra exitosos en una página web o la aceptación de una oferta presentada en una interacción con un representante. | Las experiencias de los clientes se optimizan en función de una comprensión holística de las necesidades actuales del cliente y se adaptan a todas las experiencias que el usuario tenga, buenas o malas. Por ejemplo: una campaña de mercadotecnia puede no ser apropiada para un cliente que recientemente ha presentado una queja sobre un producto o servicio. |

[!DNL Decisioning Service] traslada las funciones de personalización de la experiencia de la segmentación en un solo canal a determinar la fase general del ciclo vital de la participación de sus clientes con su marca, independientemente de los canales. Una etapa del ciclo vital es mucho más compleja que la pertenencia a un segmento y se basa casi siempre en flujos de eventos complejos, reglas comerciales y atributos predichos.

Otros términos utilizados por productos y servicios destinados a servir en casos de uso similares:

- Administración de la interacción en tiempo real (RTIM)
- Gestión de viajes
- Comercialización y personalización de Omni-canal
- Decisiones en tiempo real

## ¿Cómo [!DNL Decisioning Service] funciona?

Las experiencias se pueden personalizar [!DNL Decisioning Service] en tiempo real, ya que el cliente se relaciona con la marca a través de un canal de entrada, como el sitio o la aplicación móvil. La toma de decisiones también se puede utilizar para personalizar mensajes mediante canales salientes, como un correo electrónico o una notificación push.

Las decisiones se pueden tomar de muchas maneras. Un método consiste en eliminar las opciones sucesivamente hasta que sólo quede una o hasta que se hayan reducido las opciones y haya algún subconjunto restante o hasta que se elija al azar un ganador del conjunto reducido. Una variante de este enfoque para elegir la opción ganadora según una fórmula calculada. La clasificación de las opciones elegibles se realiza mediante una función. Para la toma de decisiones de oferta, esa función podría calcular el coste, el valor de la oferta para la empresa y utilizar una opción predefinida de la probabilidad de que el usuario final acepte la oferta. La puntuación resultante podría utilizarse para ordenar las ofertas.

Alternativamente o de manera adicional, una estrategia podría basarse en los resultados obtenidos de interacciones previas con clientes similares a los que se propusieron opciones similares. En esta estrategia, se aprende la función que calculó los valores de prioridad. El valor óptimo de los resultados está ligado a los objetivos de la actividad y el indicador de rendimiento de la predicción es la frecuencia con que se logró el resultado después de que se propuso la opción.

### Estrategia de decisión

Las estrategias de decisión se configuran mediante objetos llamados actividades. Cada estrategia de decisión es esencialmente un algoritmo o una función que toma las opciones N {o1, o2, ...oN} como entrada y produce una lista ordenada de opciones (o1, o2,...oK) según la cual la primera opción de la lista se considera la mejor según un criterio de optimización, la segunda opción de la lista de resultados se considera entonces la segunda mejor opción y así sucesivamente.

En cualquier momento dado durante el viaje de un cliente, la mejor opción para una actividad dada se vuelve a evaluar en función del conjunto más reciente de variables de contexto, reglas y restricciones. Las variables de contexto incluyen los registros almacenados en [!DNL Real Time Customer Profile]. Una entidad de registro central es el perfil de un cliente, pero otras entidades, como los datos comerciales operativos, están igualmente disponibles para la actividad.

El algoritmo o función que produce la lista de las opciones de K superior varía según el caso de uso. Los componentes internos de ese algoritmo son diferentes para casos de uso diferentes. Los componentes se definen en un repositorio en tiempo de diseño y se &quot;compilan&quot; en instrucciones para la estrategia de decisión específica del caso de uso.

![optimización de decisiones](./images/decisioning-optimization.png)

## Trabajar con [!DNL Decisioning Service]

El [!DNL Decisioning Service], al igual que otros [!DNL Platform] servicios, adopta una filosofía de primera calidad de la API. Esto significa que la API es la interfaz principal en la que todas las funciones, incluidas las funciones administrativas, están disponibles mediante API. También significa que otros [!DNL Platform] servicios, soluciones de Adobe e integraciones de terceros utilizan las mismas API.

Puede utilizar [!DNL Decisioning Service] en un modo de interacción sincrónico de solicitud-respuesta facilitado por una sencilla API HTTP REST. La llamada de API devuelve la mejor opción para un solo perfil. La selección de &quot;la mejor opción actual&quot; cambiará en función de las reglas y restricciones aplicadas a todas las opciones que una actividad determinada esté considerando. La API de REST permite obtener la siguiente mejor opción para varias actividades a la vez. Esto permite el arbitraje de opciones entre canales. Cuando las respuestas para varias actividades se obtienen juntas, se pueden aplicar reglas adicionales.

![decisioning-API](./images/decisioning-API.png)

### Integración con otros [!DNL Platform] flujos de trabajo

El uso de [!DNL Decisioning Service] es opcional y solo requiere unos pocos pasos además de los pasos típicos necesarios para crear [!DNL Profile] entidades y administrarlas.

>[!NOTE]
>
>Para sacar el máximo partido de la [!DNL Real-time Customer Profile], el [!DNL Decisioning Service] centro se integra directamente con la tienda de perfiles. Las llamadas de API solo necesitan indicar una de las identidades de un perfil determinado.

La secuencia típica de pasos inicios con la generación de perfiles:

- Autenticar a [!DNL Experience Platform].
- Defina un esquema en función de la clase de perfil y, opcionalmente, defina un esquema en función de la clase de evento de experiencia.
- Configure un conjunto de datos para cargar datos de registros y series temporales en [!DNL Customer Profile].
- Añada datos a través del conjunto de datos configurado en el paso anterior o los datos de instancia de flujo a través de Pipeline.
- Transfiera eventos de experiencia al [!DNL Platform] para enriquecer el perfil con datos de comportamiento.

Además, para utilizar [!DNL Decisioning Service], siga estos pasos:

- Defina los componentes de decisión mediante las API de repositorio. Estas son las entidades lógicas del negocio que conforman la estrategia de decisión. Los componentes de decisión se compilarán automáticamente en un formato utilizado por el [!DNL Decision Service Runtime]. Las API del repositorio se ilustran en la parte izquierda del diagrama siguiente.
- Invoque la API de tiempo de ejecución para obtener la mejor opción según la lógica empresarial definida en el paso anterior. Las [!DNL Decision Service Runtime] API se ilustran a la derecha en el diagrama siguiente.

![decisioning-API1](./images/decisioning-API1.png)

La activación de las entidades lógicas del negocio se produce de manera automática y continua. Tan pronto como se guarde una nueva opción en el repositorio y se marque como &quot;aprobada&quot;, será un candidato para su inclusión en el conjunto de opciones disponibles. Tan pronto como se actualice una regla de decisión, el conjunto de reglas se volverá a montar y se preparará para la ejecución en tiempo de ejecución. En este paso de activación automática, se evaluarán todas las restricciones definidas por la lógica empresarial que no dependan del contexto de tiempo de ejecución. Los resultados de este paso de activación se envían a una caché en la que están disponibles para el motor de ejecución [!DNL Decisioning Service] . Esto se ilustra en el diagrama siguiente.

![decisioning-API2](./images/decisioning-API2.png)

Una vez que se activan los conjuntos de opciones, los conjuntos de reglas y las restricciones y se han insertado en [!DNL Decisioning Service] los nodos, se utiliza una API sencilla para publicar una solicitud de decisión. Normalmente, la API es invocada por un servicio de envío que luego toma la opción propuesta (por ejemplo, la siguiente mejor acción o la siguiente mejor oferta) y ensambla la experiencia o ejecuta la acción. Si la propuesta es una oferta, se busca el contenido que representa esa oferta y se inserta en una experiencia que se envía al usuario final. Esto se ilustra en el diagrama siguiente.

![decisioning-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] ensambla datos para la solicitud de decisión. Determina la ID de la entidad perfil para la que se decide la mejor opción. También ensambla cualquier dato de contexto que no esté almacenado en [!DNL Customer Profile] pero que pueda ser utilizado por la lógica de decisión.

La lógica de decisión está organizada por actividades, cada una de las cuales especifica un filtro para el subconjunto de opciones que deben considerarse para esta actividad, junto con una única opción de reserva.

Cada decisión se toma aplicando primero restricciones para reducir el número de opciones y luego clasificando las opciones restantes. Aunque la mayor parte de la lógica se evalúa dentro [!DNL Decisioning Service], se utilizan varios servicios auxiliares para ayudar con estos dos aspectos. Por ejemplo, un servicio de límite administra los límites superiores para determinar con qué frecuencia se puede utilizar una opción en cualquier decisión, y otro servicio puede alojar un modelo de aprendizaje automático que se utiliza para calcular las puntuaciones de un perfil y una opción.

Para obtener más información sobre el uso de las API de repositorio, consulte el tutorial sobre [Administración de entidades de decisiones y reglas mediante API](./tutorials/entities.md)

Para obtener más información sobre el uso del [!DNL Decisioning Service] motor de ejecución, consulte el tutorial sobre [Uso del tiempo de ejecución del servicio de decisiones mediante API](./tutorials/runtime.md)