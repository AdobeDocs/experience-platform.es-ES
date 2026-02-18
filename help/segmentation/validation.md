---
title: Validación de audiencia
description: Descubra cómo Experience Platform valida sus audiencias para asegurarse de que funcionan bien en el flujo descendente.
exl-id: 55877ad5-757f-4928-853c-3b211ece0a45
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---

# Validación de audiencia

Al escribir una definición de audiencia en Adobe Experience Platform, la validación de audiencias proporciona validaciones y protecciones integradas para garantizar que las audiencias no solo sean precisas, sino también estables y escalables.

Al cumplir las prácticas recomendadas de definición de audiencia, se garantiza que las audiencias puedan evaluarse más rápido, que la lógica sea eficiente incluso cuando el tamaño de la audiencia aumenta y que se reduzca el riesgo de errores de evaluación durante los períodos de alto tráfico. Las audiencias optimizadas también mejoran la velocidad de activación a los destinos, reducen la latencia de personalización en tiempo real y mantienen la estabilidad general de la zona protegida.

Experience Platform ejecuta estas validaciones en tiempo real a medida que crea su audiencia en el Generador de segmentos. Cuando agregue eventos o atributos que superen los umbrales de validación, recibirá comentarios inmediatos en la interfaz del Generador de segmentos.

## Tipos de validación {#validation-types}

Cuando la validación de audiencias se ejecuta en las audiencias, hay dos tipos diferentes de construcciones que se pueden infringir: construcciones de validación críticas y construcciones de optimización de rendimiento.

Si se infringe una construcción de validación crítica, el sistema impide guardar la audiencia para proteger la estabilidad de la zona protegida. Si se viola una construcción de optimización de rendimiento, podrá guardar su audiencia, pero es *muy recomendable* que actualice su definición de audiencia para evitar problemas de rendimiento.

## Comprobaciones de validación {#validation-checks}

Actualmente, se admiten las siguientes validaciones:

| Comprobación de validación | Tipo | Umbral |
| ---------------- | ---- | --------- |
| Complejidad lógica | Validación crítica | La definición de audiencia contiene demasiadas consultas, lo que resulta en una complejidad lógica innecesaria. |
| Eventos secuenciales | Validación crítica | Hay más de 6 eventos secuenciales dentro de una definición de audiencia. |
| Recuento agregado | Optimización del rendimiento | Hay más de tres funciones de agregación dentro de una definición de audiencia. |
| Datos anidados | Optimización del rendimiento | Hay más de dos niveles de profundidad de datos anidados (tipos de datos de matriz o mapa) dentro de una definición de audiencia. |
| Tamaño de público | Optimización del rendimiento | El tamaño de calificación de audiencia es superior al 30 % del número total de perfiles en la zona protegida. |

### [!BADGE Validación crítica]{type=Negative} Complejidad lógica {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Alerta de eficacia de consultas"
>abstract="La audiencia contiene demasiadas consultas, lo que resulta en una complejidad lógica innecesaria. Simplifique la definición de la audiencia antes de continuar."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Complejidad lógica"
>abstract="La audiencia contiene demasiadas consultas, lo que resulta en una complejidad lógica innecesaria. Simplifique la definición de la audiencia antes de continuar."

La validación de complejidad lógica analiza la estructura de las sentencias lógicas (Y, O, NO) dentro de la definición de audiencia. Específicamente, busca definiciones de audiencia que obliguen al sistema a realizar un número excesivo de comparaciones por perfil.

Si la definición de audiencia tiene un número excesivo de comparaciones por perfil, este aumento de la complejidad provoca una evaluación más lenta por perfil. Como resultado, esto aumenta el tiempo general empleado para la evaluación de audiencias.

Para evitar activar esta validación, simplifique la definición de la audiencia. Si no puede comprender su propia definición de audiencia, es demasiado complicado y Experience Platform puede tardar más en evaluarla.

**Ejemplo**

Supongamos que desea encontrar clientes que viven en determinados estados. Usted _podría_ escribir esto de manera ineficiente comprobando si el perfil tiene el valor para un estado que coincide con uno de los 45 valores enumerados, de la siguiente manera:

+++ Definición de audiencia ineficaz

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Sin embargo, si utiliza una comprobación de no, solo debe comprobar si el perfil no tiene uno de los 5 valores enumerados, lo que resulta en una consulta mucho más eficiente.

+++ Definición de audiencia eficiente

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Alternativamente, supongamos que desea encontrar clientes canadienses en su plan de prueba. Un enfoque menos eficiente sería buscar canadienses en su plan de prueba excluyendo manualmente todos los demás planes, uno por uno, y comprobando que el perfil no esté en ninguno de ellos.

+++ Definición de audiencia ineficaz

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

En su lugar, debe ser directo y segmentar el plan específico que desee incluir.

+++ Definición de audiencia eficiente

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Validación crítica]{type=Negative} Complejidad de evento secuencial {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Límite de secuencia de eventos"
>abstract="La audiencia contiene demasiados eventos secuenciales. Solo puede tener un máximo de 6 eventos secuenciales dentro de la definición de audiencia. Elimine algunos eventos secuenciales de su definición de audiencia antes de continuar."

La validación de la complejidad del evento secuencial limita el número de eventos secuenciales en una secuencia a 6 eventos.

La segmentación secuencial es una de las operaciones más complicadas desde el punto de vista informático dentro de Experience Platform, ya que el sistema necesita analizar todo el historial de eventos de experiencia de un cliente, ordenarlos por marca de tiempo y comprobar si el orden especificado coincide con la consulta. Como resultado, cuando la cadena crece, el número de permutaciones que el sistema necesita calcular aumenta drásticamente.

Para evitar activar esta validación, céntrese en los conceptos básicos de la cadena secuencial definiendo el principio, el medio y el final del recorrido. Los pasos inmediatos suelen estar implícitos dentro de la conversión final.

**Ejemplo**

Supongamos que desea dirigirse a usuarios que han visto un producto, que lo han agregado al carro de compras y que lo han comprado. Un enfoque menos eficiente comprobaría cada estado individual de la ruta del usuario. Por ejemplo, la siguiente consulta sigue esta secuencia de eventos: Inicia sesión en el sitio web -> Busca un producto -> Ve una página de producto -> Agrega al carro de compras -> Navega al cierre de compra -> Evento de compra

+++ Definición de audiencia ineficaz

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Sin embargo, al reducir la secuencia a su principio, medio y final, solo necesita tener una secuencia de eventos de 3 eventos, lo que resulta en una consulta más eficiente. Por ejemplo, la siguiente consulta pasa por esta secuencia de eventos: Ve una página de producto -> Agrega al carro de compras -> Evento de compra

+++ Definición de audiencia eficiente

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Optimización del rendimiento]{type=Caution} Recuento agregado {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Contar advertencia de filtro"
>abstract="La audiencia tiene demasiados eventos de agregación. Debe usar un máximo de 3 eventos de agregación dentro de la audiencia. Para evitar problemas de rendimiento, debe eliminar algunos eventos de agregación de la definición de audiencia."

La comprobación de recuento agregado limita el número de eventos de agregación utilizados en la audiencia a 3 condiciones.

Un evento estándar solo necesita encontrar un único evento coincidente para calificar a un usuario. Sin embargo, un evento de agregación necesita leer y analizar **todo el historial** de eventos de un usuario para poder tomar una decisión, lo que lleva a tiempos de procesamiento más lentos con más eventos de agregación utilizados.

Para evitar activar esta validación, utilice únicamente recuentos específicos cuando sea estrictamente necesario para la definición de la audiencia. Si solo necesita saber si un usuario ha participado una vez, por ejemplo, puede utilizar la lógica estándar &quot;Existe&quot;, en lugar de utilizar un evento &quot;Recuento > 0&quot;.

### [!BADGE Optimización del rendimiento]{type=Caution} Complejidad de datos anidados {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Advertencia de datos anidados"
>abstract="La audiencia tiene demasiadas capas de datos anidadas. Debe utilizar un máximo de dos capas de datos dentro de la audiencia. Para evitar problemas de rendimiento, debe aplanar la definición de audiencia."

La validación de la complejidad de los datos anidados limita el número de datos anidados dentro de una definición de audiencia a dos capas.

Aunque Experience Platform admite el uso de objetos de matriz y asignación para almacenar tipos de datos complejos, desempaquetar estructuras anidadas para encontrar un valor requiere una lógica de recorrido más compleja. Cuanto más profundos sean los datos anidados en una matriz, más tardará en recuperarse para la validación.

Si realiza la segmentación con frecuencia en un atributo profundamente anidado, es posible que deba ponerse en contacto con el equipo de ingeniería de datos para copiar el atributo en un nivel superior dentro del esquema del perfil y facilitar el acceso.

### [!BADGE Optimización de rendimiento]{type=Caution} Tamaño de audiencia {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Advertencia de tamaño de audiencia"
>abstract="Su audiencia está escrita de forma demasiado amplia. Evite escribir una definición de audiencia que clasifique más del 30 % del total de perfiles en la zona protegida. Para evitar problemas de rendimiento, debe ajustar la definición de audiencia."

La validación del tamaño de la audiencia comprueba si la definición de audiencia es tan amplia que más del 30 % de los perfiles totales de la zona protegida cumplen los requisitos de audiencia.

Aunque Experience Platform puede gestionar audiencias grandes, una definición de audiencia demasiado vaga (como Todos los clientes activos) puede aumentar el tiempo de evaluación y la latencia de activación.

Si necesita crear una audiencia que cumpla los requisitos de más del 30 % del almacén de perfiles, asegúrese de que la primera evaluación de la audiencia se realice mediante una evaluación de audiencia flexible. La evaluación de la audiencia con una evaluación bajo demanda puede reducir el impacto general de una audiencia grande en el trabajo de segmentación diario.

## Próximos pasos

Después de leer esta guía, tendrá una mejor comprensión de cómo ejecuta Experience Platform las validaciones automáticas para mejorar la evaluación, la estabilidad y la escalabilidad. Para obtener más información sobre cómo crear audiencias mediante la interfaz de usuario, lea la [documentación del Generador de segmentos](./ui/segment-builder.md).

## Apéndice

En el siguiente apéndice se enumeran las preguntas más frecuentes acerca de la validación de audiencias en Experience Platform.

### Preguntas frecuentes {#faq}

**¿Qué sucede si ignoro las advertencias y guardo la audiencia?**

+++ Respuesta

Para las advertencias de optimización de rendimiento, se guarda la audiencia y el sistema intenta evaluarla. Sin embargo, es posible que los tiempos de procesamiento sean considerablemente más lentos. En situaciones extremas, si el volumen de datos es lo suficientemente alto, el trabajo de segmentación puede fallar o agotar el tiempo de espera, lo que le obliga a rediseñar la audiencia.

En el caso de errores de validación graves, no podrá guardar la audiencia.

+++

**¿Puedo solicitar un aumento al límite de &quot;Evento secuencial&quot;?**

+++ Respuesta

No, no puedes. Se trata de una protección sólida diseñada para proteger la estabilidad de todo el entorno de Experience Platform. Si la secuencia requiere más de 6 pasos, es un buen indicador de que la lógica debe simplificarse o dividirse en dos audiencias diferentes (como una audiencia de &quot;participación&quot; y una audiencia de &quot;conversión&quot;).

+++

**¿Estas nuevas validaciones romperán mis audiencias existentes?**

+++ Respuesta

Estas validaciones se ejecutan en el momento de **crear**. Como resultado, las audiencias existentes seguirán ejecutándose tal cual. Sin embargo, si intenta editar una audiencia existente que infringe estas reglas, deberá optimizarla antes de guardar los cambios.

+++

**Tengo requisitos de datos complejos. ¿Cómo puedo evitar la advertencia &quot;Datos anidados&quot;?**

+++ Respuesta

La mejor solución para evitar la advertencia &quot;Datos anidados&quot; es usar la capa de modelado de datos. Algunas sugerencias incluyen trabajar con su equipo de ingeniería de datos para aplanar su esquema XDM y llevar atributos críticos (como `subscriptionStatus` y `loyaltyTier`) al nivel superior del perfil.

+++

**¿Se aplicarán estas comprobaciones tanto a las audiencias de borrador como a las publicadas?**

+++ Respuesta

Sí, estas comprobaciones se aplican a *todas* las audiencias evaluadas en Experience Platform.

+++
