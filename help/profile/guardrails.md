---
title: Protecciones predeterminadas para datos y segmentación del perfil del cliente en tiempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: Obtenga información acerca del rendimiento y las protecciones aplicadas por el sistema para los datos y la segmentación de perfiles a fin de garantizar un uso óptimo de la funcionalidad de Real-Time CDP.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2617'
ht-degree: 2%

---

# Protecciones predeterminadas para datos y segmentación de [!DNL Real-Time Customer Profile]

Adobe Experience Platform le permite ofrecer experiencias multicanal personalizadas en función de perspectivas de comportamiento y atributos del cliente en forma de perfiles del cliente en tiempo real. Para admitir este nuevo enfoque de los perfiles, Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos de perfil para obtener un rendimiento óptimo del sistema. Al revisar las siguientes barandillas, se supone que ha modelado los datos correctamente. Si tiene preguntas sobre cómo modelar sus datos, comuníquese con su servicio de atención al cliente representante.

>[!NOTE]
>
>La mayoría de los clientes no excede estos límites predeterminados. Si gustar obtener más información sobre los límites personalizados, póngase en contacto con su representante de atención al cliente.

## Introducción

Los siguientes servicios de Experience Platform están involucrados en el modelado de datos de perfil de cliente en tiempo real:

* [[!DNL Real-Time Customer Profile]](home.md): cree perfiles de consumidor unificados con datos de varios orígenes.
* [Identidades](../identity-service/home.md): identidades de Bridge de diferentes fuentes de datos a medida que se incorporan en Experience Platform.
* [Esquemas](../xdm/home.md): los esquemas XDM (Experience Data Model) son el marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Audiencias](../segmentation/home.md): El motor de segmentación de Experience Platform se usa para crear audiencias a partir de los perfiles de los clientes en función de los comportamientos y atributos de los clientes.

## Tipos de límite

Existen dos tipos de límites predeterminados en este documento:

| Tipo de protección | Descripción |
| -------------- | ----------- |
| **Protección de rendimiento (límite leve)** | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso. Al superar las barreras de rendimiento, puede experimentar una degradación y latencia del rendimiento. Adobe no es responsable de esta degradación del rendimiento. Los clientes que exceden de manera consistente una protección de rendimiento pueden optar por licenciar capacidad adicional para evitar la degradación del rendimiento. |
| **Protecciones impuestas por el sistema (límite estricto)** | La interfaz de usuario o la API de Real-Time CDP aplican las protecciones impuestas por el sistema. Estos son límites que no se pueden superar, ya que la IU y la API le bloquearán el acceso o devolverán un error. |

{style="table-layout:auto"}

>[!NOTE]
>
>Los límites descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones. Si le interesa conocer los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

## Límites del modelo de datos

Las siguientes protecciones proporcionan límites recomendados al modelar datos del perfil del cliente en tiempo real. Para obtener más información acerca de entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidad](#entity-types) en el Apéndice.

![Diagrama que muestra las diferentes protecciones para los datos de perfil en Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Protecciones de la entidad principal

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Conjuntos de datos de clase de perfil individual XDM | 20 | Protección de rendimiento | Se recomienda un máximo de 20 conjuntos de datos que impulsar la clase de perfil individual XDM. |
| Conjuntos de datos de la clase XDM ExperienceEvent | 20 | Barandilla de rendimiento | Se recomienda un máximo de 20 conjuntos de datos que impulsar la clase XDM ExperienceEvent. |
| Adobe Analytics grupo de informes conjuntos de datos habilitados para el perfil | 1 | Barandilla de rendimiento | Se debe habilitar un máximo de un (1) Analytics grupo de informes conjunto de datos para el perfil. Intentar habilitar varios conjuntos de datos de Analytics grupo de informes para Profile puede tener consecuencias no deseadas para la calidad de los datos. Para obtener más información, consulte la sección sobre [Adobe Analytics conjuntos](#aa-datasets) de datos en el Apéndice. |
| Relaciones entre varias entidades | 5 | Protección de rendimiento | Se recomienda un máximo de 5 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión. No se deben realizar asignaciones de relaciones adicionales hasta que se elimine o deshabilite una relación existente. |
| Profundidad de JSON para el campo de ID utilizado en la relación de varias entidades | 4 | Protección de rendimiento | La profundidad máxima de JSON recomendada para un campo de ID utilizado en relaciones de varias entidades es de 4. Esto significa que, en un esquema muy anidado, los campos anidados con más de 4 niveles de profundidad no deben utilizarse como campo de ID en una relación. |
| Cardinalidad de matriz en un fragmento de perfil | &lt;=500 | Protección de rendimiento | La cardinalidad óptima de la matriz en un fragmento de perfil (datos independientes del tiempo) es &lt;=500. |
| Cardinalidad de matriz en ExperienceEvent | &lt;=10 | Protección de rendimiento | La cardinalidad óptima de la matriz en un ExperienceEvent (datos de series temporales) es &lt;=10. |
| Recuento de identidades para el gráfico de identidades de perfil individual | 50 | Barandilla reforzada por el sistema | **El número máximo de identidades en un gráfico de identidad para una perfil individual es 50.** Todos los perfiles con más de 50 identidades se excluyen de las segmentación, exportaciones y búsquedas. Para obtener más información, lea el guía sobre [la lógica](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated) de eliminación de identidad. |

{style="table-layout:auto"}

### Dimension barandillas de la entidad

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| No se permiten datos de series temporales para entidades que no sean [!DNL XDM Individual Profile] | 0 | Protección impuesta por el sistema | No se permiten **datos de series temporales para entidades que no son [!DNL XDM Individual Profile] en el servicio de perfil.** Si un conjunto de datos de series temporales está asociado con un ID que no es [!DNL XDM Individual Profile], el conjunto de datos no debe estar habilitado para [!DNL Profile]. |
| No hay relaciones anidadas | 0 | Protección de rendimiento | No debe crear una relación entre dos esquemas que no sean [!DNL XDM Individual Profile]. No se recomienda crear relaciones para ningún esquema que no forme parte del esquema de unión [!DNL Profile]. |
| Profundidad de JSON para el campo de ID principal | 4 | Protección de rendimiento | La profundidad máxima de JSON recomendada para el campo de ID principal es 4. Esto significa que, en un esquema muy anidado, no debe seleccionar un campo como ID principal si está anidado a más de 4 niveles de profundidad. Un campo que se encuentra en el cuarto nivel anidado se puede utilizar como ID principal. |

{style="table-layout:auto"}

## Límites de tamaño de datos

Las siguientes protecciones hacen referencia al tamaño de los datos y proporcionan límites recomendados para los datos que se pueden ingerir, almacenar y consultar según lo previsto. Para obtener más información acerca de entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidad](#entity-types) en el Apéndice.

>[!NOTE]
>
>El tamaño de los datos se mide como datos sin comprimir en JSON en el momento de la ingesta.

### Protecciones de la entidad principal

| Barandilla | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Tamaño máximo del evento de experiencia | 10 KB | Barandilla reforzada por el sistema | **El tamaño máximo de una evento es de 10 KB.** La ingesta continuará, pero cualquier evento mayor de 10 KB se descartará. |
| Tamaño máximo perfil de registro | 100 KB | Protección impuesta por el sistema | **El tamaño máximo de un registro de perfil es de 100 KB.** La ingesta continuará, pero perfil registros mayores a 100 KB se descartarán. |
| Tamaño máximo del fragmento perfil | 50 MB | Barandilla reforzada por el sistema | **El tamaño máximo de un fragmento de perfil es de 50 MB.** La segmentación, las exportaciones y las búsquedas pueden dar error en cualquier [fragmento de perfil](#profile-fragments) que supere los 50 MB. |
| Tamaño máximo de almacenamiento de perfil | 50 MB | Protección de rendimiento | **El tamaño máximo de un perfil almacenado es de 50 MB.** Si agrega nuevos [fragmentos de perfil](#profile-fragments) a un perfil que supere los 50 MB, el rendimiento del sistema se verá afectado. Por ejemplo, un perfil puede contener un solo fragmento de 50 MB o varios fragmentos en varios conjuntos de datos con un tamaño total combinado de 50 MB. Si se intenta almacenar un perfil con un solo fragmento de más de 50 MB o con varios fragmentos de más de 50 MB de tamaño combinado, el rendimiento del sistema se verá afectado. |
| Número de lotes de Perfil o ExperienceEvent introducidos por día | 90 | Protección de rendimiento | **El número máximo de lotes de Perfil o ExperienceEvent ingeridos por día es 90.** Esto significa que el total combinado de lotes Profile y ExperienceEvent ingeridos cada día no puede superar los 90. La ingesta de lotes adicionales afectará al rendimiento del sistema. |
| Número de ExperienceEvents por registro de perfil | 5000 | Protección de rendimiento | **El número máximo de ExperienceEvents por registro de perfil es de 5000.** perfiles con más de 5000 ExperienceEvents **no** se tendrán en cuenta para la segmentación. |

{style="table-layout:auto"}

### Protecciones de entidad de Dimension

| Barandilla | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Tamaño total para todas las entidades dimensionales | 5GB | Protección de rendimiento | El tamaño total recomendado para todas las entidades dimensionales es de 5 GB. La ingesta de entidades de gran dimensión puede afectar al rendimiento del sistema. Por ejemplo, no se recomienda intentar cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Protección de rendimiento | Se recomienda un máximo de 5 conjuntos de datos asociados con cada esquema de entidad dimensional. Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos colaboradores, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Lotes de entidades de Dimension ingeridos por día | 4 por entidad | Protección de rendimiento | El número máximo recomendado de lotes de dimensión entidades ingeridos al día es de 4 por entidad. Por ejemplo, podría ingerir actualizaciones en un catálogo de productos hasta 4 veces al día. La ingesta de lotes de entidades dimensión adicionales para la misma entidad puede afectar al rendimiento del sistema. |

{style="table-layout:auto"}

## Barreras de segmentación {#segmentation-guardrails}

Las barreras de protección descritas en esta sección se refieren al número y la naturaleza de las audiencias que una organización puede crear dentro de Experience Platform, así como a la asignación y activación de audiencias a los destinos.

| Barandilla | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Audiences por sandbox | 4000 | Barandilla de rendimiento | Puede tener hasta 4000 **audiencias activas** por sandbox. Puede tener más de 4000 audiencias por organización, siempre y cuando haya menos de 4000 audiencias en cada **sandbox individual** . Esto incluye las audiencias por lotes, de streaming y de borde. Si se intenta crear audiencias adicionales, puede afectar al rendimiento del sistema. Obtenga más información sobre [cómo crear audiencias a través del generador de](/help/segmentation/ui/segment-builder.md) segmento. |
| Audiencias perimetrales por espacio aislado | 150 | Barandilla de rendimiento | Puede tener hasta 150 **audiencias activas** de Edge por espacio aislado. Puede tener más de 150 audiencias perimetrales por organización, siempre que haya menos de 150 audiencias perimetrales en cada **entorno limitado individual** . Si intenta crear audiencias perimetrales adicionales, puede afectar al rendimiento del sistema. Obtenga más información sobre [las audiencias periféricas](/help/segmentation/methods/edge-segmentation.md). |
| Rendimiento perimetral en todos los entornos de pruebas | 1500 RPS | Barandilla de rendimiento | El segmentación perimetral admite un valor máximo de 1500 eventos entrantes por segundo al entrar en la red de Adobe Experience Platform Edge. Los segmentación perimetrales pueden tardar hasta 350 milisegundos en procesar un evento entrante tras entrar en la red de Adobe Experience Platform Edge. Obtenga más información sobre [las audiencias periféricas](/help/segmentation/methods/edge-segmentation.md). |
| Audiencias de streaming por sandbox | 500 | Barandilla de rendimiento | Puede tener hasta 500 **audiencias de streaming activas** por zona protegida. Puede tener más de 500 audiencias de streaming por organización, siempre y cuando haya menos de 500 audiencias de streaming en cada zona protegida **individual**. Esto incluye tanto a las audiencias de streaming como a las de Edge. Si se intenta crear audiencias de flujo adicionales, el rendimiento del sistema puede verse afectado. Más información sobre [audiencias de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Rendimiento de streaming en todas las zonas protegidas | 1500 RPS | Protección de rendimiento | La segmentación por flujo continuo admite un valor máximo de 1500 eventos entrantes por segundo. La segmentación por streaming puede tardar hasta 5 minutos en calificar un perfil para el abono a un segmento. Más información sobre [audiencias de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Audiencias por lotes por zona protegida | 4000 | Protección de rendimiento | Puede tener hasta 4000 **audiencias por lotes activas** por zona protegida. Puede tener más de 4000 audiencias de lote por organización, siempre y cuando haya menos de 4000 audiencias de lote en cada zona protegida **individual**. Si intenta crear audiencias por lotes adicionales, el rendimiento del sistema puede verse afectado. |
| Audiencias de cuenta por zona protegida | 50 | Barandilla reforzada por el sistema | Puede crear un máximo de 50 audiencias cuenta en un entorno limitado. Una vez que alcanza las 50 audiencias en un espacio aislado, el control de audiencia **de Crear** se deshabilita cuando se intenta crear un nuevo audiencia de cuenta. Obtenga más información sobre [cuenta audiencias](/help/segmentation/types/account-audiences.md). |
| Composiciones publicadas por sandbox | 10 | Barandilla de rendimiento | Puede tener un máximo de 10 composiciones publicadas en una zona protegida. Obtenga más información sobre [composición de audiencias en la guía de la interfaz de usuario](/help/segmentation/ui/audience-composition.md). |
| Tamaño máximo audiencia | 30 por ciento | Barandilla de rendimiento | El abono máximo recomendado de una audiencia es del 30 por ciento del número total de perfiles en el sistema. Crear audiencias con más del 30% de los perfiles como miembros o múltiples audiencias grandes es posible, pero afectará el rendimiento del sistema. |
| Ejecución flexible audiencia de evaluación | 50 por año (espacio aislado de producción)<br/>100 por año (simulador de pruebas de desarrollo) | Barandilla reforzada por el sistema | Tiene un máximo de 50 ejecuciones de evaluación de audiencia flexibles al año por **sandbox de producción** . Tiene un máximo de 100 ejecuciones de evaluación de audiencia flexibles al año por **cada espacio aislado de desarrollo** . |
| Ejecución flexible audiencia de evaluación | 2 por día | Barandilla reforzada por el sistema | Tiene un máximo de 2 ejecuciones por día por sandbox. |
| Audiences por ejecución de evaluación de audiencia flexible | 20 | Barandilla reforzada por el sistema | Puede tener un máximo de 20 audiencias por cada ejecución de evaluación de audiencia flexible. |

{style="table-layout:auto"}

## Disponibilidad esperada

En la sección siguiente se describe la disponibilidad esperada **para las audiencias y las políticas de combinación en los servicios descendentes, como los** destinos CDP en tiempo real:

| Tipo de zona protegida | Fecha |
| ------------ | ---- |
| Sandboxes existentes | 1 hora |
| Nuevo sandboxes | 2 horas |
| Sandboxes recién restablecidos | 2 horas |

{style="table-layout:auto"}

## Apéndice

En esta sección se proporcionan detalles adicionales sobre los límites de este documento.

### Tipos de entidad

El [!DNL Profile] modelo de datos tienda consta de dos tipos de entidad principales: [entidades](#primary-entity) principales y [entidades](#dimension-entity) dimensión.

#### Entidad principal

Una entidad primaria, o entidad perfil, combina los datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan mediante lo que se conoce como &quot;vista unión&quot;. Una unión vista agrega los campos de todos los esquemas que implementar la misma clase en una sola unión esquema. La unión esquema es [!DNL Real-Time Customer Profile] un modelo de datos híbrido desnormalizado que actúa como contenedor para todos los atributos de perfil y eventos de comportamiento.

Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot;, se modelan utilizando [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot;, se modelan mediante [!DNL XDM ExperienceEvent]. A medida que se ingieren datos de registros y series temporales en Adobe Experience Platform, se activa [!DNL Real-Time Customer Profile] para comenzar a ingerir datos que se han habilitado para su uso. Cuantas más interacciones y detalles se ingieran, más sólidos serán los perfiles individuales.

![Una infografía que describe las diferencias entre los datos de registro y los datos de series temporales.](images/guardrails/profile-entity.png)

#### Dimension entity

Aunque el almacén de datos de perfil que mantiene los datos de perfil no es un almacén relacional, el perfil permite la integración con entidades de dimensión pequeñas para crear audiencias de una manera simplificada e intuitiva. Esta integración se conoce como [segmentación de varias entidades](../segmentation/tutorials/multi-entity-segmentation.md).

Su organización también puede definir clases XDM para describir cosas que no sean individuales, como tiendas, productos o propiedades. Estos esquemas, que se modelan con clases XDM distintas de la clase XDM Individual Profile, se denominan &quot;entidades de dimensión&quot; (también conocidas como &quot;entidades de búsqueda&quot;) y no contienen datos de series temporales. Los esquemas que representan entidades de dimensión se vinculan a entidades de perfil mediante el uso de [relaciones de esquema](../xdm/tutorials/relationship-ui.md).

Las entidades de Dimension proporcionan datos de búsqueda que ayudan y simplifican las definiciones de segmentos de varias entidades y deben ser lo suficientemente pequeñas como para que el motor de segmentación pueda cargar todo el conjunto de datos en la memoria para un procesamiento óptimo (búsqueda rápida de puntos).

![Infografía que muestra que una entidad de perfil está compuesta por entidades de dimensión.](images/guardrails/profile-and-dimension-entities.png)

### Fragmentos de perfil

En este documento, hay varias protecciones que hacen referencia a &quot;fragmentos de perfil&quot;. En Experience Platform, se combinan varios fragmentos de perfil para formar el perfil del cliente en tiempo real. Cada fragmento representa una identidad principal única y el registro correspondiente o el conjunto completo de datos de evento para ese ID dentro de un conjunto de datos determinado. Para obtener más información sobre los fragmentos de perfil, consulte [Información general del perfil](home.md#profile-fragments-vs-merged-profiles).

### Combinar políticas {#merge-policies}

Al unir datos de varias fuentes, las políticas de combinación son las reglas que utiliza Experience Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Experience Platform, se combinan para crear un único perfil para ese cliente. Cuando los datos de varias fuentes entran en conflicto, la política de combinación determina qué información se incluirá en el perfil de la persona. Se permite un máximo de cinco (5) políticas de combinación que utilizan el esquema `_xdm.context.profile` por zona protegida. Para obtener más información acerca de las políticas de combinación, lea la [descripción general de las políticas de combinación](merge-policies/overview.md).

### Conjuntos de datos de grupos de informes Adobe Analytics en Experience Platform {#aa-datasets}

Se pueden habilitar varios grupos de informes para el perfil siempre y cuando se resuelvan todos los conflictos de datos. Puede utilizar la funcionalidad Preparación de datos para resolver conflictos de datos entre eVars, listas y props. Para obtener más información acerca de cómo usar la funcionalidad de preparación de datos, lea la [guía de la interfaz de usuario del conector de Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=es#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Datos del cliente en tiempo real Platform (B2P: paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Datos del cliente en tiempo real Platform (B2B: paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
