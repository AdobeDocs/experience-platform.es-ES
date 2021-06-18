---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;protecciones;directrices;límite;entidad;entidad principal;entidad de dimensión;
title: Protecciones para datos de perfil del cliente en tiempo real
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform proporciona una serie de protecciones que le ayudan a evitar la creación de modelos de datos que el perfil del cliente en tiempo real no puede admitir. Este documento describe las prácticas recomendadas y restricciones que se deben tener en cuenta al modelar datos de perfil.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 441c2978b90a4703874787b3ed8b94c4a7779aa8
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 2%

---

# Protecciones para datos [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] proporciona perfiles individuales que le permiten ofrecer experiencias personalizadas entre canales basadas en perspectivas de comportamiento y atributos del cliente. Para lograr este objetivo, [!DNL Profile] y el motor de segmentación dentro de Adobe Experience Platform utilizan un modelo de datos híbrido altamente desnormalizado que ofrece un nuevo enfoque para el desarrollo de perfiles de clientes. El uso de este modelo de datos híbrido hace importante que los datos que se recopilen estén modelados correctamente. Aunque el [!DNL Profile] almacén de datos que mantiene los datos de perfil no es un almacén relacional, [!DNL Profile] permite la integración con entidades de dimensión pequeñas para crear segmentos de una manera simplificada e intuitiva. Esta integración se conoce como segmentación multientidad.

Adobe Experience Platform proporciona una serie de protecciones que le ayudan a evitar la creación de modelos de datos que [!DNL Real-time Customer Profile] no pueden admitir. Este documento describe estas protecciones y prácticas recomendadas y restricciones al usar datos de perfil para la segmentación.

>[!NOTE]
>
>Las barreras y límites descritos en este documento se están mejorando constantemente. Vuelva regularmente para ver las actualizaciones.

## Introducción

Se recomienda leer la siguiente documentación de servicios de Experience Platform antes de intentar crear modelos de datos para usarlos en [!DNL Real-time Customer Profile]. Para trabajar con modelos de datos y las barreras descritas en este documento, es necesario conocer los distintos servicios de Experience Platform involucrados en la administración de [!DNL Real-time Customer Profile] entidades:

* [[!DNL Real-time Customer Profile]](home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../identity-service/home.md): Admite la creación de una &quot;vista única del cliente&quot; al unir identidades de fuentes de datos dispares a medida que se incorporan en  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../xdm/schema/composition.md) del esquema: Introducción a los esquemas y el modelado de datos en Experience Platform.
* [Servicio de segmentación de Adobe Experience Platform](../segmentation/home.md): Motor de segmentación dentro de  [!DNL Platform] utilizado para crear segmentos de audiencia a partir de perfiles de clientes en función de los comportamientos y atributos de los clientes.
   * [Segmentación](../segmentation/multi-entity-segmentation.md) de varias entidades: Una guía para crear segmentos que integren entidades de dimensión con datos de perfil.

## Tipos de entidades

El modelo de datos de almacenamiento [!DNL Profile] consta de dos tipos de entidades principales:

* **Entidad principal:** una entidad principal, o entidad de perfil, combina los datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan con lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un esquema de unión único. El esquema de unión para [!DNL Real-time Customer Profile] es un modelo de datos híbrido no normalizado que actúa como contenedor de todos los atributos de perfil y eventos de comportamiento.

   Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot;, se modelan mediante [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot;, se modelan mediante [!DNL XDM ExperienceEvent]. A medida que los datos de registros y series temporales se incorporan en Adobe Experience Platform, se déclencheur [!DNL Real-time Customer Profile] comenzar a introducir datos que se hayan habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más robustos se vuelven los perfiles individuales.

   ![](images/guardrails/profile-entity.png)

* **Entidad de Dimension:** su organización también puede definir clases XDM para describir otras cosas que no sean individuos, como tiendas, productos o propiedades. Estos esquemas no [!DNL XDM Individual Profile] se conocen como &quot;entidades de dimensión&quot; y no contienen datos de series temporales. Las entidades de Dimension proporcionan datos de búsqueda que ayudan y simplifican las definiciones de segmentos de varias entidades y deben ser lo suficientemente pequeñas como para que el motor de segmentación pueda cargar todo el conjunto de datos en la memoria para un procesamiento óptimo (búsqueda de puntos rápidos).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Fragmentos de perfil

Hay varias protecciones en este documento que hacen referencia a &quot;fragmentos de perfil&quot;. El perfil del cliente en tiempo real está compuesto por varios fragmentos de perfil. Cada fragmento representa los datos de la identidad desde un conjunto de datos donde es la identidad principal. Esto significa que un fragmento puede contener un ID principal y datos de evento (serie temporal) en un conjunto de datos de ExperienceEvent de XDM o puede estar compuesto por un ID principal y datos de registro (atributos independientes del tiempo) en un conjunto de datos de Perfil individual de XDM.

## Tipos de límite

Al definir el modelo de datos, se recomienda permanecer dentro de los márgenes de protección proporcionados para garantizar un rendimiento adecuado y evitar errores en el sistema.

Las protecciones proporcionadas en este documento incluyen dos tipos de límite:

* **Límite leve:** un límite suave proporciona un máximo recomendado para un rendimiento óptimo del sistema. Es posible ir más allá de un límite suave sin romper el sistema ni recibir mensajes de error, sin embargo, ir más allá de un límite suave provocará una degradación del rendimiento. Se recomienda mantenerse dentro del límite suave para evitar disminuciones en el rendimiento general.

* **Límite estricto:** un límite estricto proporciona un máximo absoluto para el sistema. Si se supera un límite estricto, se producirán averías y errores, lo que impedirá que el sistema funcione según lo esperado.

## Protecciones del modelo de datos

Se recomienda adherirse a las siguientes protecciones al crear un modelo de datos para utilizarlo con [!DNL Real-time Customer Profile].

### Protecciones de entidades principales

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número de conjuntos de datos recomendados para contribuir al esquema de unión [!DNL Profile] | 20 | Leve | **Se recomienda un máximo de 20 conjuntos de datos  [!DNL Profile]habilitados.** Para habilitar otro conjunto de datos para  [!DNL Profile], primero se debe eliminar o deshabilitar un conjunto de datos existente. |
| Número de relaciones de varias entidades recomendadas | 5 | Leve | **Se recomienda un máximo de 5 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión.** No se deben realizar asignaciones de relación adicionales hasta que se elimine o desactive una relación existente. |
| Profundidad máxima de JSON para el campo de ID utilizado en la relación de varias entidades | 4 | Leve | **La profundidad máxima recomendada de JSON para un campo de ID utilizado en relaciones entre varias entidades es 4.** Esto significa que, en un esquema altamente anidado, los campos anidados con más de 4 niveles de profundidad no deben utilizarse como campo de ID en una relación. |
| Cardinalidad de matriz en un fragmento de perfil | &lt;=500 | Leve | **La cardinalidad óptima de la matriz en un fragmento de perfil (datos independientes del tiempo) es  &lt;>** |
| Cardinalidad de matriz en ExperienceEvent | &lt;=10 | Leve | **La cardinalidad óptima de la matriz en un ExperienceEvent (datos de series temporales) es  &lt;>** |

### Protecciones de entidades Dimension

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| No se permiten datos de series temporales para entidades que no sean [!DNL XDM Individual Profile] | 0 | Grave | **No se permiten datos de series temporales para [!DNL XDM Individual Profile] entidades que no estén en el servicio de perfil.** Si un conjunto de datos de series temporales está asociado con un [!DNL XDM Individual Profile] ID que no es de , el conjunto de datos no debe habilitarse para  [!DNL Profile]. |
| Sin relaciones anidadas | 0 | Leve | **No debe crear una relación entre dos [!DNL XDM Individual Profile] esquemas que no sean.** No se recomienda la capacidad de crear relaciones para ningún esquema que no forme parte del esquema de  [!DNL Profile] unión. |
| Profundidad máxima de JSON para el campo de ID principal | 4 | Leve | **La profundidad máxima recomendada de JSON para el campo de ID principal es 4.** Esto significa que en un esquema altamente anidado, no debe seleccionar un campo como ID principal si está anidado con más de 4 niveles de profundidad. Un campo del cuarto nivel anidado se puede utilizar como ID principal. |

## Protecciones de tamaño de datos

Las siguientes limitaciones hacen referencia al tamaño de los datos y se recomiendan para garantizar que los datos se puedan introducir, almacenar y consultar según lo previsto.

>[!NOTE]
>
>El tamaño de los datos se mide como datos sin comprimir en JSON en el momento de la ingesta.

### Protecciones de entidades principales

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño máximo de ExperienceEvent | 10 KB | Grave | **El tamaño máximo de un evento es de 10 KB.** La ingesta continuará, pero se perderán todos los eventos de más de 10 KB. |
| Tamaño máximo del registro de perfil | 100 KB | Grave | **El tamaño máximo de un registro de perfil es de 100 KB.** La ingesta continuará, pero se perderán los registros de perfil superiores a 100 KB. |
| Tamaño máximo del fragmento de perfil | 50 MB | Grave | **El tamaño máximo de un fragmento de perfil es de 50 MB.** La segmentación, las exportaciones y las búsquedas pueden fallar en cualquier  [fragmentación de ](#profile-fragments) perfil que supere los 50 MB. |
| Tamaño máximo de almacenamiento de perfiles | 50 MB | Leve | **El tamaño máximo de un perfil almacenado es de 50 MB.** Añadir nuevos  [fragmentos de ](#profile-fragments) perfil en un perfil de más de 50 MB afectará al rendimiento del sistema. |
| Número de lotes de Perfil o ExperienceEvent ingestados por día | 90 | Leve | **El número máximo de lotes de Perfil o ExperienceEvent ingestados por día es de 90.** Esto significa que el total combinado de lotes de Perfil y ExperienceEvent ingestados cada día no puede superar los 90. La ingesta de lotes adicionales afectará el rendimiento del sistema. |

### Protecciones de entidades Dimension

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño total máximo para todas las entidades dimensionales | 5 GB | Leve | **El tamaño total máximo recomendado para todas las entidades dimensionales es de 5 GB.** La ingesta de entidades de dimensión grandes resultará en un rendimiento del sistema degradado. Por ejemplo, no se recomienda cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Leve | **Se recomienda un máximo de 5 conjuntos de datos asociados a cada esquema de entidad dimensional.** Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos contribuyentes, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Número de lotes de entidades de dimensión introducidos por día | 4 por entidad | Leve | **El número máximo de lotes de entidades de dimensión ingeridos por día es de 4 por entidad.** Por ejemplo, puede ingerir actualizaciones en un catálogo de productos hasta 4 veces al día. La ingesta de lotes de entidades de dimensión adicionales para la misma entidad afectará al rendimiento del sistema. |

## Protecciones de segmentación

Las protecciones descritas en esta sección hacen referencia al número y la naturaleza de los segmentos que una organización puede crear dentro del Experience Platform, así como a la asignación y activación de segmentos a los destinos.

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de segmentos por simulador de pruebas | 10K | Leve | **El número máximo de segmentos que una organización puede crear es de 10 000 por simulador de pruebas.** Una organización puede tener más de 10 000 segmentos en total, siempre que haya menos de 10 000 segmentos en cada entorno limitado individual. Si intenta crear segmentos adicionales, el rendimiento del sistema se verá degradado. |
| Número máximo de segmentos de flujo continuo por simulador de pruebas | 500 | Leve | **El número máximo de segmentos de flujo continuo que puede crear una organización es de 500 por simulador de pruebas.** Una organización puede tener más de 500 segmentos de flujo continuo en total, siempre que haya menos de 500 segmentos de flujo continuo en cada simulador de pruebas individual. Si intenta crear segmentos de flujo adicionales, el rendimiento del sistema se verá degradado. |
| Número máximo de segmentos por lote por entorno limitado | 10K | Leve | **El número máximo de segmentos por lotes que una organización puede crear es de 10 000 por simulador de pruebas.** Una organización puede tener más de 10 000 segmentos de lote en total, siempre que haya menos de 10 000 segmentos de lote en cada entorno limitado individual. Si intenta crear segmentos de lote adicionales, el rendimiento del sistema se verá degradado. |
