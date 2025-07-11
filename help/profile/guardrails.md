---
title: Protecciones predeterminadas para datos y segmentación del perfil del cliente en tiempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: Obtenga información acerca del rendimiento y las protecciones aplicadas por el sistema para los datos y la segmentación de perfiles a fin de garantizar un uso óptimo de la funcionalidad de Real-Time CDP.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: cfc221250a9c8f91b16aa1d4572263ecaf4eeccc
workflow-type: tm+mt
source-wordcount: '2622'
ht-degree: 2%

---

# Protecciones predeterminadas para datos y segmentación de [!DNL Real-Time Customer Profile]

Adobe Experience Platform le permite ofrecer experiencias multicanal personalizadas en función de perspectivas de comportamiento y atributos del cliente en forma de perfiles del cliente en tiempo real. Para admitir este nuevo enfoque de los perfiles, Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos de perfil para obtener un rendimiento óptimo del sistema. Al revisar las siguientes protecciones, se da por hecho que los datos se han modelado correctamente. Si tiene preguntas sobre cómo modelar los datos, póngase en contacto con su representante de servicio de atención al cliente.

>[!NOTE]
>
>La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

## Introducción

Los siguientes servicios de Experience Platform están relacionados con el modelado de datos del perfil del cliente en tiempo real:

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
| Conjuntos de datos de clase de perfil individual XDM | 20 | Protección de rendimiento | Se recomienda un máximo de 20 conjuntos de datos que aprovechen la clase de perfil individual XDM. |
| Conjuntos de datos de clase XDM ExperienceEvent | 20 | Protección de rendimiento | Se recomienda un máximo de 20 conjuntos de datos que aprovechen la clase XDM ExperienceEvent. |
| Conjuntos de datos de grupos de informes de Adobe Analytics habilitados para Perfil | 1 | Protección de rendimiento | Se debe habilitar un máximo de un (1) conjunto de datos de grupo de informes de Analytics para el perfil. El intento de habilitar varios conjuntos de datos de grupos de informes de Analytics para el perfil puede tener consecuencias no deseadas para la calidad de los datos. Para obtener más información, consulte la sección sobre [conjuntos de datos de Adobe Analytics](#aa-datasets) en el Apéndice. |
| Relaciones entre varias entidades | 5 | Protección de rendimiento | Se recomienda un máximo de 5 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión. No se deben realizar asignaciones de relaciones adicionales hasta que se elimine o deshabilite una relación existente. |
| Profundidad de JSON para el campo de ID utilizado en la relación de varias entidades | 4 | Protección de rendimiento | La profundidad máxima de JSON recomendada para un campo de ID utilizado en relaciones de varias entidades es de 4. Esto significa que, en un esquema muy anidado, los campos anidados con más de 4 niveles de profundidad no deben utilizarse como campo de ID en una relación. |
| Cardinalidad de matriz en un fragmento de perfil | &lt;=500 | Protección de rendimiento | La cardinalidad óptima de la matriz en un fragmento de perfil (datos independientes del tiempo) es &lt;=500. |
| Cardinalidad de matriz en ExperienceEvent | &lt;=10 | Protección de rendimiento | La cardinalidad óptima de la matriz en un ExperienceEvent (datos de series temporales) es &lt;=10. |
| Recuento de identidades para el gráfico de identidades de perfil individual | 50 | Protección impuesta por el sistema | **El número máximo de identidades en un gráfico de identidad para un perfil individual es 50.**: todos los perfiles con más de 50 identidades se excluyen de la segmentación, las exportaciones y las búsquedas. Para obtener más información, lea la guía sobre [comprensión de la lógica de eliminación de identidades](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). |

{style="table-layout:auto"}

### Protecciones de entidad de Dimension

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

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Tamaño máximo de ExperienceEvent | 10 KB | Protección impuesta por el sistema | **El tamaño máximo de un evento es de 10 KB.** La ingesta continuará, pero se perderán todos los eventos de más de 10 KB. |
| Tamaño máximo de registro de perfil | 100 KB | Protección impuesta por el sistema | **El tamaño máximo de un registro de perfil es de 100 KB.** La ingesta continuará, pero se perderán los registros de perfil que superen los 100 KB. |
| Tamaño máximo del fragmento de perfil | 50 MB | Protección impuesta por el sistema | **El tamaño máximo de un solo fragmento de perfil es de 50 MB.** La segmentación, las exportaciones y las búsquedas pueden dar error en cualquier [fragmento de perfil](#profile-fragments) que supere los 50 MB. |
| Tamaño máximo de almacenamiento de perfil | 50 MB | Protección de rendimiento | **El tamaño máximo de un perfil almacenado es de 50 MB.** Si agrega nuevos [fragmentos de perfil](#profile-fragments) a un perfil que supere los 50 MB, el rendimiento del sistema se verá afectado. Por ejemplo, un perfil puede contener un solo fragmento de 50 MB o varios fragmentos en varios conjuntos de datos con un tamaño total combinado de 50 MB. Si se intenta almacenar un perfil con un solo fragmento de más de 50 MB o con varios fragmentos de más de 50 MB de tamaño combinado, el rendimiento del sistema se verá afectado. |
| Número de lotes de Perfil o ExperienceEvent introducidos por día | 90 | Protección de rendimiento | **El número máximo de lotes de Perfil o ExperienceEvent ingeridos por día es 90.** Esto significa que el total combinado de lotes Profile y ExperienceEvent ingeridos cada día no puede superar los 90. La ingesta de lotes adicionales afectará al rendimiento del sistema. |
| Número de ExperienceEvents por registro de perfil | 5000 | Protección de rendimiento | **El número máximo de ExperienceEvents por registro de perfil es de 5000.** perfiles con más de 5000 ExperienceEvents solo usarán los **últimos** 5000 ExperienceEvents cuando se usen con la segmentación. |

{style="table-layout:auto"}

### Protecciones de entidad de Dimension

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Tamaño total para todas las entidades dimensionales | 5GB | Protección de rendimiento | El tamaño total recomendado para todas las entidades dimensionales es de 5 GB. La ingesta de entidades de gran dimensión puede afectar al rendimiento del sistema. Por ejemplo, no se recomienda intentar cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Protección de rendimiento | Se recomienda un máximo de 5 conjuntos de datos asociados con cada esquema de entidad dimensional. Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos colaboradores, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Lotes de entidades de Dimension ingeridos por día | 4 por entidad | Protección de rendimiento | El número máximo recomendado de lotes de entidades de dimensión introducidos por día es de 4 por entidad. Por ejemplo, puede introducir actualizaciones en un catálogo de productos hasta cuatro veces al día. La ingesta de lotes de entidades de dimensión adicionales para la misma entidad puede afectar al rendimiento del sistema. |

{style="table-layout:auto"}

## Protecciones de segmentación {#segmentation-guardrails}

Las protecciones descritas en esta sección se refieren al número y la naturaleza de las audiencias que una organización puede crear dentro de Experience Platform, así como a la asignación y activación de audiencias a destinos.

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Audiencias por zona protegida | 4000 | Protección de rendimiento | Puede tener hasta 4000 **audiencias activas** por zona protegida. Puede tener más de 4000 audiencias por organización, siempre y cuando haya menos de 4000 audiencias en cada zona protegida **individual**. Esto incluye audiencias por lotes, de streaming y de Edge. Si se intenta crear audiencias adicionales, el rendimiento del sistema puede verse afectado. Obtenga más información sobre [la creación de audiencias](/help/segmentation/ui/segment-builder.md) a través del generador de segmentos. |
| Audiencias de Edge por zona protegida | 150 | Protección de rendimiento | Puede tener hasta 150 **audiencias de Edge activas** por zona protegida. Puede tener más de 150 audiencias de Edge por organización, siempre y cuando haya menos de 150 audiencias de Edge en cada zona protegida **individual**. Si se intentan crear audiencias perimetrales adicionales, el rendimiento del sistema puede verse afectado. Más información sobre [audiencias de Edge](/help/segmentation/methods/edge-segmentation.md). |
| Rendimiento de Edge en todas las zonas protegidas | 1500 RPS | Protección de rendimiento | La segmentación de Edge admite un valor máximo de 1500 eventos entrantes por segundo al entrar en Adobe Experience Platform Edge Network. La segmentación de Edge puede tardar hasta 350 milisegundos en procesar un evento entrante después de que entre en Adobe Experience Platform Edge Network. Más información sobre [audiencias de Edge](/help/segmentation/methods/edge-segmentation.md). |
| Audiencias de streaming por zona protegida | 500 | Protección de rendimiento | Puede tener hasta 500 **audiencias de streaming activas** por zona protegida. Puede tener más de 500 audiencias de streaming por organización, siempre y cuando haya menos de 500 audiencias de streaming en cada zona protegida **individual**. Esto incluye tanto a las audiencias de streaming como a las de Edge. Si se intenta crear audiencias de flujo adicionales, el rendimiento del sistema puede verse afectado. Más información sobre [audiencias de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Rendimiento de streaming en todas las zonas protegidas | 1500 RPS | Protección de rendimiento | La segmentación por flujo continuo admite un valor máximo de 1500 eventos entrantes por segundo. La segmentación por streaming puede tardar hasta 5 minutos en calificar un perfil para el abono a un segmento. Más información sobre [audiencias de streaming](/help/segmentation/methods/streaming-segmentation.md). |
| Audiencias por lotes por zona protegida | 4000 | Protección de rendimiento | Puede tener hasta 4000 **audiencias por lotes activas** por zona protegida. Puede tener más de 4000 audiencias de lote por organización, siempre y cuando haya menos de 4000 audiencias de lote en cada zona protegida **individual**. Si intenta crear audiencias por lotes adicionales, el rendimiento del sistema puede verse afectado. |
| Audiencias de cuenta por zona protegida | 50 | Protección impuesta por el sistema | Puede crear un máximo de 50 audiencias de cuenta en una zona protegida. Después de llegar a 50 audiencias en una zona protegida, el control **[!UICONTROL Crear audiencia]** se deshabilita al intentar crear una nueva audiencia de cuenta. Más información sobre [audiencias de la cuenta](/help/segmentation/types/account-audiences.md). |
| Composiciones publicadas por zona protegida | 10 | Protección de rendimiento | Puede tener un máximo de 10 composiciones publicadas en una zona protegida. Obtenga más información sobre [composición de audiencias en la guía de la interfaz de usuario](/help/segmentation/ui/audience-composition.md). |
| Tamaño máximo de audiencia | 30 por ciento | Protección de rendimiento | La pertenencia máxima recomendada de una audiencia es del 30 % del número total de perfiles en el sistema. Es posible crear audiencias con más del 30 % de los perfiles como miembros o varias audiencias grandes, pero esto afectará al rendimiento del sistema. |
| Ejecuciones flexibles de evaluación de audiencias | 50 por año (zona protegida de producción)<br/>100 por año (zona protegida de desarrollo) | Protección impuesta por el sistema | Tiene un máximo de 50 ejecuciones de evaluación de audiencia flexibles por año por cada zona protegida de **producción**. Tiene un máximo de 100 ejecuciones de evaluación de audiencia flexibles por año por cada zona protegida de **desarrollo**. |
| Ejecuciones flexibles de evaluación de audiencias | 2 al día | Protección impuesta por el sistema | Tiene un máximo de 2 ejecuciones por día por zona protegida. |
| Audiencias por ejecución flexible de evaluación de audiencias | 20 | Protección impuesta por el sistema | Puede tener un máximo de 20 audiencias por ejecución de evaluación de audiencia flexible. |

{style="table-layout:auto"}

## Disponibilidad esperada

En la siguiente sección se describe la disponibilidad de **expected** para audiencias y políticas de combinación en servicios descendentes como destinos de Real-Time CDP:

| Tipo de zona protegida | Fecha |
| ------------ | ---- |
| Zonas protegidas existentes | 1 hora |
| Nuevas zonas protegidas | 2 horas |
| Zonas protegidas recién restablecidas | 2 horas |

{style="table-layout:auto"}

## Apéndice

En esta sección se proporcionan detalles adicionales sobre los límites de este documento.

### Tipos de entidad

El modelo de datos de almacén [!DNL Profile] consta de dos tipos de entidades principales: [entidades principales](#primary-entity) y [entidades de dimensión](#dimension-entity).

#### Entidad principal

Una entidad principal, o entidad de perfil, combina datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan mediante lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un único esquema de unión. El esquema de unión de [!DNL Real-Time Customer Profile] es un modelo de datos híbrido desnormalizado que actúa como contenedor para todos los atributos de perfil y eventos de comportamiento.

Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot; se modelan con [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot; se modelan con [!DNL XDM ExperienceEvent]. A medida que los datos de registros y series temporales se incorporan en Adobe Experience Platform, se establece el déclencheur de [!DNL Real-Time Customer Profile] para que comiencen a ingerir datos que se han habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más sólidos se volverán los perfiles individuales.

![Infografía que describe las diferencias entre los datos de los registros y los datos de las series temporales.](images/guardrails/profile-entity.png)

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
* [Real-Time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
