---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;protecciones;directrices;límite;entidad;entidad principal;entidad de dimensión;
title: Protecciones predeterminadas para los datos de perfil del cliente en tiempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional. Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos de perfil para obtener un rendimiento óptimo del sistema.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 6%

---

# Protecciones predeterminadas para [!DNL Real-Time Customer Profile] data

Adobe Experience Platform le permite ofrecer experiencias personalizadas entre canales basadas en perspectivas de comportamiento y atributos del cliente en forma de perfiles del cliente en tiempo real. Para admitir este nuevo enfoque de los perfiles, el Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional.

Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos de perfil para obtener un rendimiento óptimo del sistema. Al revisar las siguientes barreras, se da por hecho que ha modelado los datos correctamente. Si tiene alguna pregunta sobre cómo modelar sus datos, póngase en contacto con su representante de servicio al cliente.

>[!NOTE]
>
>La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante de atención al cliente.

## Primeros pasos

Los siguientes servicios de Experience Platform participan en el modelado de datos del perfil del cliente en tiempo real:

* [[!DNL Real-Time Customer Profile]](home.md): Cree perfiles de cliente unificados con datos de varias fuentes.
* [Identidades](../identity-service/home.md): Puente identidades de fuentes de datos dispares a medida que se incorporan en Platform.
* [Esquemas](../xdm/home.md): Los esquemas del Modelo de datos de experiencia (XDM) son el marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
* [Segmentos](../segmentation/home.md): El motor de segmentación de Platform se utiliza para crear segmentos a partir de los perfiles de los clientes en función de sus comportamientos y atributos.

## Tipos de límite

Existen dos tipos de límites predeterminados dentro de este documento:

* **Límite leve:** Es posible ir más allá de un límite suave, aunque los límites blandos proporcionan una guía recomendada para el rendimiento del sistema.

* **Límite grave:** Un límite estricto proporciona un máximo absoluto.

>[!NOTE]
>
>Los límites descritos en este documento se están mejorando constantemente. Vuelva regularmente para ver las actualizaciones. Si le interesa conocer los límites personalizados, póngase en contacto con su representante de atención al cliente.

## Límites del modelo de datos

Las siguientes protecciones proporcionan límites recomendados al modelar datos del perfil del cliente en tiempo real. Para obtener más información sobre entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidades](#entity-types) en el apéndice.

### Protecciones de entidades principales

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Conjuntos de datos de clase de perfil individual XDM | 20 | Leve | Se recomienda un máximo de 20 conjuntos de datos que aprovechen la clase de Perfil individual XDM . |
| Conjuntos de datos de clase XDM ExperienceEvent | 20 | Leve | Se recomienda un máximo de 20 conjuntos de datos que aprovechen la clase XDM ExperienceEvent . |
| Conjuntos de datos de grupos de informes de Adobe Analytics habilitados para Perfil | 1 | Leve | Se debe habilitar un máximo de un (1) conjunto de datos de grupo de informes de Analytics para Perfil. Si intenta habilitar varios conjuntos de datos de grupos de informes de Analytics para Perfil, puede tener consecuencias no deseadas para la calidad de los datos. Para obtener más información, consulte la sección sobre [Conjuntos de datos de Adobe Analytics](#aa-datasets) en el apéndice. |
| Relaciones con varias entidades | 5 | Leve | Se recomienda un máximo de 5 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión. No se deben realizar asignaciones de relación adicionales hasta que se elimine o desactive una relación existente. |
| Profundidad de JSON para el campo de ID utilizado en la relación de varias entidades | 4 | Leve | La profundidad máxima recomendada de JSON para un campo de ID utilizado en relaciones entre varias entidades es 4. Esto significa que, en un esquema altamente anidado, los campos anidados con más de 4 niveles de profundidad no deben utilizarse como campo de ID en una relación. |
| Cardinalidad de matriz en un fragmento de perfil | &lt;=500 | Leve | La cardinalidad óptima de la matriz en un fragmento de perfil (datos independientes del tiempo) es &lt;=500. |
| Cardinalidad de matriz en ExperienceEvent | &lt;=10 | Leve | La cardinalidad óptima de la matriz en un ExperienceEvent (datos de series temporales) es &lt;=10. |
| Recuento de identidades para el gráfico de identidad de perfil individual | 50 | Grave | **El número máximo de identidades en un gráfico de identidad para un perfil individual es 50.** Los perfiles con más de 50 identidades se excluyen de la segmentación, las exportaciones y las búsquedas. |

{style=&quot;table-layout:auto&quot;}

### Protecciones de entidades Dimension

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| No se permiten datos de series temporales para[!DNL XDM Individual Profile] entities | 0 | Grave | **Los datos de series temporales no están permitidos para los[!DNL XDM Individual Profile] entidades en el servicio de perfil.** Si un conjunto de datos de series temporales está asociado a una[!DNL XDM Individual Profile] ID, el conjunto de datos no debe estar habilitado para [!DNL Profile]. |
| Sin relaciones anidadas | 0 | Leve | No debe crear una relación entre dos[!DNL XDM Individual Profile] esquemas. No se recomienda la capacidad de crear relaciones para ningún esquema que no forme parte del [!DNL Profile] esquema de unión. |
| Profundidad de JSON para el campo de ID principal | 4 | Leve | La profundidad máxima recomendada de JSON para el campo de ID principal es 4. Esto significa que en un esquema altamente anidado, no debe seleccionar un campo como ID principal si está anidado con más de 4 niveles de profundidad. Un campo del cuarto nivel anidado se puede utilizar como ID principal. |

{style=&quot;table-layout:auto&quot;}

## Límites de tamaño de datos

Las siguientes protecciones hacen referencia al tamaño de los datos y proporcionan límites recomendados para los datos que se pueden introducir, almacenar y consultar según lo previsto. Para obtener más información sobre entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidades](#entity-types) en el apéndice.

>[!NOTE]
>
>El tamaño de los datos se mide como datos sin comprimir en JSON en el momento de la ingesta.

### Protecciones de entidades principales

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño máximo de ExperienceEvent | 10 KB | Grave | **El tamaño máximo de un evento es de 10 KB.** La ingesta continuará, pero se perderán todos los eventos de más de 10 KB. |
| Tamaño máximo del registro de perfil | 100 KB | Grave | **El tamaño máximo de un registro de perfil es de 100 KB.** La ingesta continuará, pero se perderán los registros de perfil superiores a 100 KB. |
| Tamaño máximo del fragmento de perfil | 50MB | Grave | **El tamaño máximo de un fragmento de perfil único es de 50 MB.** La segmentación, las exportaciones y las búsquedas pueden fallar [fragmento de perfil](#profile-fragments) que es más de 50 MB. |
| Tamaño máximo de almacenamiento de perfiles | 50MB | Leve | **El tamaño máximo de un perfil almacenado es de 50 MB.** Adición de nuevas [fragmentos de perfil](#profile-fragments) en un perfil que tenga más de 50 MB, afectará el rendimiento del sistema. Por ejemplo, un perfil podría contener un solo fragmento de 50 MB o varios fragmentos en varios conjuntos de datos con un tamaño total combinado de 50 MB. Si se intenta almacenar un perfil con un solo fragmento de más de 50 MB, o con varios fragmentos que suman más de 50 MB en tamaño combinado, el rendimiento del sistema se verá afectado. |
| Número de lotes de Perfil o ExperienceEvent ingestados por día | 90 | Leve | **El número máximo de lotes de Perfil o ExperienceEvent ingestados por día es de 90.** Esto significa que el total combinado de lotes de Perfil y ExperienceEvent ingestados cada día no puede superar los 90. La ingesta de lotes adicionales afectará el rendimiento del sistema. |

{style=&quot;table-layout:auto&quot;}

### Protecciones de entidades Dimension

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño total para todas las entidades dimensionales | 5 GB | Leve | El tamaño total recomendado para todas las entidades dimensionales es de 5 GB. La ingesta de entidades de dimensión grandes puede afectar al rendimiento del sistema. Por ejemplo, no se recomienda cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Leve | Se recomienda un máximo de 5 conjuntos de datos asociados a cada esquema de entidad dimensional. Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos contribuyentes, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Lotes de entidad Dimension ingeridos por día | 4 por entidad | Leve | El número máximo recomendado de lotes de entidades de dimensión ingeridos por día es de 4 por entidad. Por ejemplo, puede ingerir actualizaciones en un catálogo de productos hasta 4 veces al día. La ingesta de lotes de entidades de dimensión adicionales para la misma entidad puede afectar al rendimiento del sistema. |

{style=&quot;table-layout:auto&quot;}

## Protecciones de segmentación

Las protecciones descritas en esta sección hacen referencia al número y la naturaleza de los segmentos que una organización puede crear dentro del Experience Platform, así como a la asignación y activación de segmentos a los destinos.

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Segmentos por simulador de pruebas | 4000 | Leve | Una organización puede tener más de 4000 segmentos en total, siempre que haya menos de 4000 segmentos en cada entorno limitado individual. El intento de crear segmentos adicionales puede afectar al rendimiento del sistema. |
| Segmentos de Edge por simulador de pruebas | 150 | Leve | Una organización puede tener más de 150 segmentos Edge en total, siempre que haya menos de 150 segmentos Edge en cada entorno limitado individual. El intento de crear segmentos Edge adicionales puede afectar al rendimiento del sistema. |
| Segmentos de flujo continuo por entorno limitado | 500 | Leve | Una organización puede tener más de 500 segmentos de flujo continuo en total, siempre que haya menos de 500 segmentos de flujo continuo en cada simulador de pruebas individual. El intento de crear segmentos de flujo continuo adicionales puede afectar al rendimiento del sistema. |
| Segmentos por lotes por simulador de pruebas | 4000 | Leve | Una organización puede tener más de 4000 segmentos de lote en total, siempre que haya menos de 4000 segmentos de lote en cada entorno limitado individual. El intento de crear segmentos de lote adicionales puede afectar al rendimiento del sistema. |

{style=&quot;table-layout:auto&quot;}

## Apéndice

Esta sección proporciona detalles adicionales para los límites de este documento.

### Tipos de entidades

La variable [!DNL Profile] el modelo de datos de almacenamiento consta de dos tipos de entidades principales:

* **Entidad principal:** Una entidad principal, o entidad de perfil, combina los datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan con lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un esquema de unión único. El esquema de unión para [!DNL Real-Time Customer Profile] es un modelo de datos híbrido no normalizado que actúa como contenedor de todos los atributos de perfil y eventos de comportamiento.

   Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot;, se modelan mediante [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot;, se modelan mediante [!DNL XDM ExperienceEvent]. A medida que los datos de registros y series temporales se incorporan en Adobe Experience Platform, se déclencheur [!DNL Real-Time Customer Profile] para empezar a introducir datos que se hayan habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más robustos se vuelven los perfiles individuales.

   ![Una infografía que describe las diferencias entre los datos de registro y los datos de series temporales.](images/guardrails/profile-entity.png)

* **entidad Dimension:** Aunque el almacén de datos de perfil que mantiene los datos de perfil no es un almacén relacional, Perfil permite la integración con entidades de dimensión pequeñas para crear segmentos de una forma simplificada e intuitiva. Esta integración se conoce como [segmentación multientidad](../segmentation/multi-entity-segmentation.md). Su organización también puede definir clases XDM para describir otras cosas que no sean individuos, como tiendas, productos o propiedades. Estos[!DNL XDM Individual Profile] los esquemas se conocen como &quot;entidades de dimensión&quot; y no contienen datos de series temporales. Las entidades de Dimension proporcionan datos de búsqueda que ayudan y simplifican las definiciones de segmentos de varias entidades y deben ser lo suficientemente pequeñas como para que el motor de segmentación pueda cargar todo el conjunto de datos en la memoria para un procesamiento óptimo (búsqueda de puntos rápidos).

   ![Una infografía que muestra que una entidad de perfil está compuesta por entidades de dimensión.](images/guardrails/profile-and-dimension-entities.png)

### Fragmentos de perfil

En este documento, existen varias protecciones que hacen referencia a &quot;fragmentos de perfil&quot;. En Experience Platform, se combinan varios fragmentos de perfil para formar el Perfil del cliente en tiempo real. Cada fragmento representa una identidad principal única y el registro o conjunto completo de datos de evento correspondiente para ese ID dentro de un conjunto de datos determinado. Para obtener más información sobre los fragmentos de perfil, consulte la [Información general del perfil](home.md#profile-fragments-vs-merged-profiles).

### Combinar directivas {#merge-policies}

Al reunir datos de varias fuentes, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente. Cuando los datos de varias fuentes entran en conflicto, la política de combinación determina qué información se incluirá en el perfil para el individuo. Se permite un máximo de cinco (5) políticas de combinación por organización. Para obtener más información sobre las políticas de combinación, lea la [información general sobre políticas de combinación](merge-policies/overview.md).

### Conjuntos de datos de grupos de informes de Adobe Analytics en Platform {#aa-datasets}

Se pueden habilitar varios grupos de informes para Perfil siempre y cuando se resuelvan todos los conflictos de datos. Puede utilizar la funcionalidad Preparación de datos para resolver conflictos de datos entre eVars, Listas y Props. Para obtener más información sobre cómo utilizar la funcionalidad de preparación de datos, lea la [Guía de la interfaz de usuario del conector de Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).
