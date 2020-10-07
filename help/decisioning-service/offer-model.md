---
keywords: Experience Platform;home;popular topics;offer management;Offer Management
solution: Experience Platform
title: Modelo de dominio de Offer Decisioning
topic: overview
description: La toma de decisiones de ofertas es un caso de uso del servicio de decisiones en el que se formalizan y administran de forma centralizada las reglas y predicciones utilizadas para atraer clientes con ofertas.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '2640'
ht-degree: 0%

---


# Información general del modelo de dominio de Offer Decisioning

La toma de decisiones de oferta es un caso de uso en el [!DNL Decisioning Service] que se formalizan y administran de forma centralizada las reglas y predicciones utilizadas para atraer clientes con ofertas. La toma de decisiones de oferta se considera un tipo de decisiones de contenido. En este caso de uso, las opciones de decisión se denominan ofertas y se caracterizan como tales por el contenido que se les adjunta. Para obtener una introducción al modelo de objetos utilizado por el [!DNL Decisioning Service], consulte el Modelo [de dominio del servicio de](experience-model.md)decisiones.

El objetivo es presentar al usuario final una &quot;mejor Oferta&quot; en cualquier canal basado en criterios de objetivo, limitaciones de costo y frecuencia, así como en interacciones previas entre canales, incluidas Ofertas previas propuestas.

Al igual que con todos los casos de uso de decisiones, las opciones de decisión (ofertas) se administran en un repositorio compartido por cualquier número de aplicaciones. Las ofertas pueden ser creadas por diferentes departamentos de la organización o por socios, y esas ofertas pueden agregarse y eliminarse diariamente.

Las ofertas se colocan visualmente en experiencias más grandes mediante la aplicación que ofrece la experiencia. Las colocaciones, a veces denominadas zonas o ranuras, son componentes importantes para diseñar una estrategia. El diseño de una estrategia de oferta suele ser un inicio con la definición de esas colocaciones. Una oferta suele tener varias representaciones de contenido para que se pueda integrar correctamente en una variedad de experiencias, en las que cada una de ellas tiene diferentes limitaciones dimensionales o de otro tipo y requiere distintos formatos de medios.

Las ofertas suelen estar vinculadas a bienes o servicios físicos y se trata de un cálculo de los costos. Una organización debe poder limitar los recursos que consumen las ofertas y, por lo tanto, debe poder limitar el número total de veces que se puede proponer una oferta.

El valor previsto de una oferta aceptada para la organización es el criterio de optimización y se compara con el costo de realizar una oferta. El costo, la probabilidad de aceptación y el valor previsto se utilizan para clasificar las ofertas. La mejor Oferta es la que tiene el mayor impacto positivo previsto en los objetivos de sus actividades de oferta.

Offer Decisioning considera las interacciones que tuvo un usuario final en muchos canales y aplicaciones, y aprovecha los datos de evento de perfil y experiencia del usuario final. Por ejemplo, una aplicación de centro de llamadas puede utilizar Offer Decisioning para habilitar o suprimir una oferta en función de las compras realizadas y las revisiones publicadas por el usuario final; o una aplicación de administración de correo electrónico puede depender de Offer Decisioning para seleccionar la siguiente mejor Oferta en un boletín semanal basado en el historial de exploración de un sitio web.

Las ofertas tienen otras propiedades interesantes. Con frecuencia, existe una programación o un intervalo de fecha y hora definidos cuando la oferta es válida y cuando la oferta debe invalidarse.

Por último, el atractivo de una oferta se deteriora con la frecuencia con que se presenta. Una Oferta que no se acepta después de haber sido propuesta repetidamente es una oportunidad perdida porque se podría haber presentado una oferta diferente. Por este motivo, se debe gestionar la fatiga del usuario final.

## Estrategia de decisión de oferta con un vistazo

El enfoque general es reducir la selección de Ofertas hasta que se cumplan todas las restricciones, luego aplicar el modelo de clasificación a las opciones restantes y luego optimizar en varias actividades mediante Restricciones de límite (eliminación de duplicaciones y evitación de opciones de reserva).

| Componente de estrategia | Realizado como |
| --- | --- |
| Actividades de decisión | Actividades de oferta |
| Opciones de decisión | Oferta con representaciones de contenido |
| Opciones de reserva | Oferta de reserva con representaciones de contenido |
| Conjunto finito de opciones de decisión | Inventario de ofertas (también conocido como biblioteca de ofertas) |
| Categorías temáticas | Filtro de oferta basado en etiquetas e identificadores de oferta |
| Resultados de la decisión | Propuesta de una oferta por actividad, para múltiples actividades a la vez |
| Resultados de las decisiones | Evento de experiencia previsto en relación con la oferta, por ejemplo `eventType='opened'` |
| Algoritmo de decisión | Lógica de servicio interna, parametrizada |
| Restricciones | Restricciones de ubicación, restricciones de calendario, restricciones de límite globales y por usuario, restricciones de anulación de duplicación |
| Normas de decisión | Reglas de elegibilidad |
| Modelo para la utilidad *esperada* | Clasificación de oferta o prioridad |

El número total de ofertas en el inventario de opciones suele ser bastante grande (en el orden de los 10.000) y cada actividad de oferta puede centrarse en ofertas que entran en una categoría diferente (tema). La estrategia de decisión de oferta permite adjuntar un filtro de oferta a una actividad de oferta. Se evaluarán las limitaciones adicionales en el momento en que se solicite la decisión.
Las siguientes secciones explican los componentes del dominio de Offer Decisioning en detalle.

## Ofertas generales

Las ofertas generales, también denominadas ofertas personalizadas, son las opciones centrales de las actividades de decisión de la oferta. Tienen atributos como nombre y estado. El atributo de estado indica si la entidad está lista para ser incluida en la lista de ofertas aprobadas activas. Las ofertas generales tendrán varias limitaciones. Más información sobre esto en la sección ‎ Restricciones [más abajo](#offer-constraints).

## Contenido en Ofertas

### Colocaciones de oferta

Las colocaciones definen las restricciones de contenido y se utilizan con una actividad para especificar el lugar en el que se entrega la mejor experiencia. Esto reduce aún más el número de opciones que se pueden considerar y es otra restricción impuesta por la actividad. Esto se denomina restricción de colocación. Solo se considerarán las opciones que tengan contenido que cumpla una restricción de colocación, como ofertas. Esto se evalúa en las primeras etapas de la estrategia de decisión. Cuando los objetos de opción cambian las restricciones de colocación de cada actividad se vuelven a evaluar y la opción puede considerarse o quedar fuera de ella para una o varias actividades.

No es responsabilidad del [!DNL Decisioning Service] grupo formalizar los detalles complejos de las dependencias de contenido. En su lugar, cada cliente identificará la lista de colocaciones en todos los canales y dará a esas colocaciones identificadores y nombres únicos. Al hacer referencia a una ubicación determinada, el diseñador afirma que el contenido determinado se ajustará a la ubicación.

Cuando se desarrolla el contenido, el especialista en marketing de oferta y el diseñador de contenido simplemente (tienen que) acordar un &quot;contrato implícito&quot; que se encuentra detrás del nombre &quot;Imagen principal de Página de inicio&quot; o &quot;Secuencia de comandos de apertura de llamada de servicio&quot;. El primero puede acordarse como una imagen de 600 px de ancho y 350 px de altura y el segundo puede estar restringiendo el contenido al texto en dos variantes de idioma que no sea más de 50 palabras en tres o cuatro frases con una estructura semántica. Ubicación para no almacenar todo el significado del contrato oculto.

### representaciones de la oferta

Para garantizar que una oferta se pueda presentar correctamente en los distintos parámetros de las colocaciones en los canales, se deben crear diferentes representaciones de esa oferta. El contenido que se adjunta a las ofertas se agrupa por colocaciones. Cada oferta puede tener una o varias representaciones en las que cada una de ellas haga referencia a una de las colocaciones definidas. Cada representación de una oferta debe utilizar una colocación diferente. Cuantas más representaciones tenga una oferta, más oportunidades habrá de utilizar la oferta en diferentes contextos de colocación.

Una colocación restringe el tipo de elementos de contenido que se pueden agregar a la representación.

## Ofertas de reserva

Las ofertas de reserva son opciones de decisión que no tienen restricciones adicionales excepto las reglas de colocación. Las ofertas de reserva tienen representaciones de contenido vinculadas a las colocaciones, como cualquier otra oferta.

Las ofertas de reserva se especifican en actividades para indicar una experiencia de contenido viable que se utilizará cuando las restricciones combinadas descalifiquen todas las opciones restringidas. Dado que no depende del contexto de tiempo de ejecución ni del perfil, la restricción de colocación se puede comprobar con antelación cuando se monta la actividad. Al utilizar ofertas de reserva, siempre hay una respuesta a la pregunta: ¿Cuál es actualmente la mejor oferta?

## Restricciones de oferta

### Restricciones del calendario

En el dominio de decisión de oferta, las ofertas tienen un período de validez. Esto significa que la oferta no puede proponerse antes de que haya pasado la fecha y hora de su inicio y no puede proponerse más tarde de la fecha y hora de finalización. La entidad oferta tiene una estructura simple que define esas restricciones de calendario.

Periódicamente, las Ofertas caducadas se eliminarán de la lista de opciones consideradas. Sin embargo, el filtro de calendario se aplica correctamente en el momento en que se solicita la decisión, de modo que las restricciones se apliquen con precisión.

### Restricciones de límite

Las ofertas pueden tener una restricción de límite opcional. Consiste en dos valores:

- El valor de límite global restringe la frecuencia con la que se puede proponer una oferta en todo el conjunto de perfiles (audiencia de objetivo).

- El límite por perfil y determina la frecuencia con la que se puede proponer esa Oferta al mismo perfil.

### Restricciones de duplicación

Cuando se solicita una decisión, el cliente puede solicitar propuestas de varias actividades a la vez. Este es un escenario típico en la toma de decisiones de contenido. Cada actividad aporta una o más opciones de contenido a la experiencia global. Debido al aspecto de la composición, las decisiones deben arbitrar entre actividades para evitar la duplicación, a menos que las actividades elijan un subconjunto desunido del inventario de opciones general. Es probable que una opción de alto rango ocupe un lugar alto en todas las actividades y sería una experiencia deficiente que todas las actividades propusieran la misma opción. Por otra parte, si un sistema de envío desea saber cuál es la Mejor Conversión Siguiente en todos los canales y no hay restricción de límite, puede que esté bien proponer la misma opción en diferentes actividades.

Actualmente, las restricciones de duplicación no se escriben en el repositorio de objetos comerciales. En su lugar, la desduplicación es la estrategia predeterminada en tiempo de ejecución. Un parámetro de solicitud puede anular el comportamiento predeterminado para suprimir el paso de anulación de duplicación.

### [!DNL Profile] restricciones: Reglas de elegibilidad

Hasta ahora, las limitaciones examinadas han sido aplicables independientemente de para quién se haya seleccionado la oferta. La toma de decisiones de experiencias también admite un caso de uso en el que la personalización de propuestas se basa en los eventos de registros y series temporales del cliente. Las reglas se evalúan por perfil para decidir si una oferta cumple los requisitos o debe suprimirse para ese usuario. Para ello, se puede asociar una regla de elegibilidad con cada oferta. Además de los eventos de perfil y experiencia de un usuario final, la regla de elegibilidad tendrá en cuenta los datos de contexto en tiempo real. Esos datos son proporcionados por el servicio de envío y pueden adoptar la forma de datos que no están relacionados con un perfil, como los niveles de inventario, las condiciones meteorológicas y los horarios de vuelo.

Es importante distinguir entre las reglas de segmentación y objetivo, y entre las reglas de elegibilidad y prioridad para la toma de decisiones. Para dirigir un conjunto de perfiles es el resultado (selección de audiencias) para la elegibilidad un conjunto de opciones (ofertas permitidas) es el resultado de la evaluación.

## Colecciones de oferta

El inventario es el conjunto general de opciones que se consideran para la toma de decisiones. El inventario puede dividirse en categorías o colecciones. Una colección de opciones se representa con una etiqueta común que tienen esas opciones. Los filtros se utilizan para comprobar si las ofertas entran en una determinada categoría o, más específicamente, si comparten la misma etiqueta o etiquetas.

### Etiquetas

Las etiquetas proporcionan una manera de expresar que un grupo de opciones pertenece a una categoría.

Una opción puede tener más de una etiqueta y, por lo tanto, puede estar en varias categorías al mismo tiempo. Las categorías también pueden superponerse o contener otra. Cuando una categoría &quot;S&quot; se define por ofertas con la etiqueta &quot;A&quot; y la categoría &quot;R&quot; se define por opciones con las etiquetas &quot;A&quot; y &quot;B&quot;, entonces &quot;S&quot; será un superconjunto de &quot;R&quot;.

### Filtros

Los filtros se utilizan para definir los criterios de un conjunto de opciones que pertenece a una categoría. Se puede considerar que los filtros son consultas del inventario de ofertas generales. Existen dos formas básicas de formar un filtro: al indicar que una oferta tiene una o varias etiquetas y seleccionar el conjunto de ofertas de forma explícita. El método anterior se puede configurar para indicar que una oferta de esa colección debe tener todas las etiquetas especificadas o que una opción se califica cuando tiene al menos una de las etiquetas especificadas.

Cuando las opciones se colocan explícitamente en una colección, su conjunto de etiquetas se ignora para esa colección.

## Actividades de oferta

Actividades configuran y controlan el proceso de toma de decisiones. Actualmente, la estrategia de decisión está predefinida, pero las futuras iteraciones del modelo de dominio de Offer Decisioning permitirán la selección de modelos, reglas adicionales y restricciones.

Una experiencia se puede montar usando muchas actividades simultáneamente. Actualmente, se pueden abordar hasta 30 actividades en una sola solicitud de decisión. Si se deben rellenar con contenido más de 30 actividades o ranuras en una experiencia, se pueden realizar varias solicitudes para el mismo perfil. Sin embargo, cuando se incluyan actividades en la misma solicitud de decisión, se eliminará la duplicación de propuestas de oferta entre esas actividades.

Si las actividades se definen de forma que seleccionan entre conjuntos de ofertas desunidos, no hay mucha diferencia en cuanto a si las actividades se combinan en la misma solicitud o se dividen en solicitudes independientes. Sin embargo, las restricciones de tiempo de respuesta y de red pueden requerir combinar actividades en la misma solicitud. Dado que diferentes solicitudes pueden enrutarse a diferentes nodos de servicio, es posible que sea necesario recuperar los mismos datos de perfil en diferentes nodos. Esto reduce el ancho de banda de E/S efectivo disponible para otras solicitudes.

Las actividades se utilizan para insertar contenido en una experiencia. Para facilitar (y no garantizar) que los elementos de contenido se &quot;ajusten&quot; correctamente, una actividad hace referencia a una sola colocación. Observe que una colocación no siempre es un lugar/ranura concreto sino más bien una abstracción de esos lugares/ranuras. Por ejemplo, en una página web con una cuadrícula de mosaicos, cada mosaico podría estar regido por la misma colocación, suponiendo que todos tengan una forma y un tamaño similares y que puedan tener contenido similar. Sin embargo, un mosaico individual normalmente se suministraría por su propia actividad.

La siguiente figura ilustra cómo las entidades comerciales están relacionadas entre sí:

![](./images/figure-10.png)

Cuando los clientes crean y vinculan el gráfico de objetos para tomar decisiones, normalmente habrá tres flujos de trabajo diferentes. Estos son los siguientes:

- Configuración de las entidades de soporte, como etiquetas y colocaciones. Estas entidades se utilizan para estructurar, filtrar y agrupar otras entidades. También se utilizan para proporcionar cierta coordinación entre el segundo y el tercer flujo de trabajo. Este flujo de trabajo constituye un trabajo inicial, pero en cualquier momento se pueden realizar mejoras en la configuración. Aunque las etiquetas son relativamente simples, las colocaciones requieren un poco más de planificación. Como mínimo, una empresa debe hacer un inventario de todos los lugares donde se presenta una decisión.

- Creación de ofertas con las distintas representaciones y reglas comerciales (restricciones). Este flujo de trabajo central proporciona las opciones entre las que debemos seleccionar las mejores. Las etiquetas del primer flujo de trabajo se utilizan para categorizar ofertas y las colocaciones para indicar qué opciones se pueden presentar y dónde.

   - Este flujo de trabajo también define restricciones absolutas para las ofertas. Son absolutos porque siempre se aplicarán y no solo afectan a la clasificación entre un conjunto de ofertas. Por ejemplo, cuando se establece una restricción de calendario, se fuerza que la oferta nunca se seleccione antes de la fecha y hora de inicio establecida y nunca después de la fecha y hora de finalización. Las restricciones que se establecerán en este flujo de trabajo son las restricciones [de](#calendar-constraints)calendario, las restricciones de [límite](#capping-constraints) y las restricciones [de](#profile-constraints---eligibility-rules)elegibilidad. Un subflujo de trabajo aquí es la definición de reglas adicionales que determinan quién puede recibir una oferta determinada.

      - Al mismo tiempo que se crean restricciones para una oferta, se seleccionan sus representaciones. Este flujo de trabajo supone que el contenido ya se ha creado en algún lugar y simplemente se carga en el repositorio de contenido y se selecciona de él. Aquí es donde entran en juego las colocaciones del primer flujo de trabajo. Una oferta puede elegir colocaciones y asociar el contenido de esa [colocación](#offer-placements).

      - La creación de ofertas de reserva adecuadas es el último paso de este flujo de trabajo. Una oferta de reserva se parece mucho a una oferta general sin restricciones.

- El último flujo de trabajo está relacionado con la creación de actividades. Sin embargo, este paso no se produce necesariamente de forma secuencial después del flujo de trabajo para crear ofertas. Ambos procesos están en curso y son concurrentes. Las actividades se utilizan para reducir el alcance de las opciones por tema y por lugar en que se presentan las decisiones. Una actividad hace referencia a una [colección](#offer-collections) y a una colocación. También debe especificar una oferta [de](#fallback-offers) reserva que se utilice en los casos en que no se pueda determinar una oferta cualificada.

