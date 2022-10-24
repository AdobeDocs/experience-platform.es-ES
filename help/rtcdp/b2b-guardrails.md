---
keywords: perfil;perfil de cliente en tiempo real;solución de problemas;protecciones;directrices;límite;entidad;entidad principal;entidad de dimensión;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;plataforma de datos de clientes en tiempo real;cdp en tiempo real;b2b;cdp;
title: Protecciones predeterminadas para Real-time Customer Data Platform B2B Edition
type: Documentation
description: Adobe Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional. Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar sus datos para lograr un rendimiento óptimo del sistema mediante Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 2%

---

# Protecciones predeterminadas para Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Los límites descritos en este documento representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition le permite ofrecer experiencias personalizadas entre canales basadas en perspectivas de comportamiento y atributos del cliente en forma de perfiles del cliente en tiempo real y perfiles de cuenta. Para admitir este nuevo enfoque de los perfiles, el Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional.

Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar sus datos para un rendimiento óptimo del sistema. Al revisar las siguientes barreras, se da por hecho que ha modelado los datos correctamente. Si tiene alguna pregunta sobre cómo modelar sus datos, póngase en contacto con su representante de servicio al cliente.

>[!INFO]
>
>La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante de atención al cliente.

## Tipos de límite

Existen dos tipos de límites predeterminados dentro de este documento:

* **Límite leve:** Es posible ir más allá de un límite suave, aunque los límites blandos proporcionan una guía recomendada para el rendimiento del sistema.

* **Límite grave:** Un límite estricto proporciona un máximo absoluto.

>[!INFO]
>
>Los límites descritos en este documento se están mejorando constantemente. Vuelva regularmente para ver las actualizaciones. Si le interesa conocer los límites personalizados, póngase en contacto con su representante de atención al cliente.

## Límites del modelo de datos

Las siguientes protecciones proporcionan límites recomendados al modelar datos del perfil del cliente en tiempo real. Para obtener más información sobre entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidades](#entity-types) en el apéndice.

### Protecciones de entidades principales

>[!NOTE]
>
>Los límites del modelo de datos descritos en esta sección representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Conjuntos de datos de clase XDM estándar de Real-Time CDP B2B Edition | 60 | Leve | Se recomienda un máximo de 60 conjuntos de datos que aprovechen las clases estándar del Modelo de datos de experiencia (XDM) proporcionadas por Real-Time CDP B2B Edition. Para obtener una lista completa de las clases XDM estándar para casos de uso B2B, consulte la [esquemas en la documentación de Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Nota: Debido a la naturaleza del modelo de datos híbrido no normalizado de Experience Platform, la mayoría de los clientes no exceden este límite. Si tiene alguna duda sobre cómo modelar los datos o si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante de atención al cliente.* |
| Relaciones heredadas con varias entidades | 20 | Leve | Se recomienda un máximo de 20 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión. No se deben realizar asignaciones de relación adicionales hasta que se elimine o desactive una relación existente. |
| Relaciones &quot;varios a uno&quot; por clase XDM | 2 | Leve | Se recomienda un máximo de 2 relaciones &quot;varios a uno&quot; definidas por cada clase XDM. No se debe establecer una relación adicional hasta que se elimine o desactive una relación existente. Para ver los pasos sobre cómo crear una relación entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../xdm/tutorials/relationship-b2b.md). |

### Protecciones de entidades Dimension

>[!NOTE]
>
>Los límites del modelo de datos descritos en esta sección representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| No hay relaciones heredadas anidadas | 0 | Leve | No debe crear una relación entre dos[!DNL XDM Individual Profile] esquemas. No se recomienda la capacidad de crear relaciones para ningún esquema que no forme parte del [!DNL Profile] esquema de unión. |
| Solo los objetos B2B pueden participar en relaciones &quot;varios a uno&quot; | 0 | Grave | El sistema solo admite relaciones &quot;varios a uno&quot; entre objetos B2B. Para obtener más información sobre las relaciones &quot;varios a uno&quot;, consulte el tutorial sobre [definición de relaciones de esquema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profundidad máxima de las relaciones anidadas entre objetos B2B | 3 | Grave | La profundidad máxima de las relaciones anidadas entre objetos B2B es 3. Esto significa que en un esquema altamente anidado, no debe haber una relación entre los objetos B2B anidados con más de 3 niveles de profundidad. |

## Límites de tamaño de datos

Las siguientes protecciones hacen referencia al tamaño de los datos y proporcionan límites recomendados para los datos que se pueden introducir, almacenar y consultar según lo previsto. Para obtener más información sobre entidades principales y entidades de dimensión, consulte la sección sobre [tipos de entidades](#entity-types) en el apéndice.

>[!INFO]
>
>El tamaño de los datos se mide como datos sin comprimir en JSON en el momento de la ingesta.

### Protecciones de entidades principales

>[!NOTE]
>
>Los límites de tamaño de datos descritos en esta sección representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Lotes introducidos por clase XDM por día | 45 | Leve | El número total de lotes ingeridos cada día por clase XDM no debe superar los 45. La ingesta de lotes adicionales puede impedir un rendimiento óptimo. |

### Protecciones de entidades Dimension

>[!NOTE]
>
>Los límites de tamaño de datos descritos en esta sección representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño total para todas las entidades dimensionales | 5 GB | Leve | El tamaño total recomendado para todas las entidades dimensionales es de 5 GB. La ingesta de entidades de dimensión grandes puede afectar al rendimiento del sistema. Por ejemplo, no se recomienda cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Leve | Se recomienda un máximo de 5 conjuntos de datos asociados a cada esquema de entidad dimensional. Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos contribuyentes, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Lotes de entidad Dimension ingeridos por día | 4 por entidad | Leve | El número máximo recomendado de lotes de entidades de dimensión ingeridos por día es de 4 por entidad. Por ejemplo, puede ingerir actualizaciones en un catálogo de productos hasta 4 veces al día. La ingesta de lotes de entidades de dimensión adicionales para la misma entidad puede afectar al rendimiento del sistema. |

## Protecciones de segmentación

Las protecciones descritas en esta sección hacen referencia al número y la naturaleza de los segmentos que una organización puede crear dentro del Experience Platform, así como a la asignación y activación de segmentos a los destinos.

>[!NOTE]
>
>Los límites de segmentación descritos en esta sección representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Segmentos por simulador de pruebas B2B | 400 | Leve | Una organización puede tener más de 400 segmentos en total, siempre que haya menos de 400 segmentos en cada entorno limitado B2B individual. El intento de crear segmentos adicionales puede afectar al rendimiento del sistema. |

## Pasos siguientes

Los límites descritos en este documento representan los cambios activados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combine estos límites con los límites generales de Adobe Experience Platform descritos en la [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

## Apéndice

Esta sección proporciona detalles adicionales para los límites de este documento.

### Tipos de entidades

La variable [!DNL Profile] el modelo de datos de almacenamiento consta de dos tipos de entidades principales:

* **Entidad principal:** Una entidad principal, o entidad de perfil, combina los datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan con lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un esquema de unión único. El esquema de unión para [!DNL Real-time Customer Profile] es un modelo de datos híbrido no normalizado que actúa como contenedor de todos los atributos de perfil y eventos de comportamiento.

   Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot;, se modelan mediante [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot;, se modelan mediante [!DNL XDM ExperienceEvent]. A medida que los datos de registros y series temporales se incorporan en Adobe Experience Platform, se déclencheur [!DNL Real-time Customer Profile] para empezar a introducir datos que se hayan habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más robustos se vuelven los perfiles individuales.

   ![](../profile/images/guardrails/profile-entity.png)

* **entidad Dimension:** Aunque el almacén de datos de perfil que mantiene los datos de perfil no es un almacén relacional, Perfil permite la integración con entidades de dimensión pequeñas para crear segmentos de una forma simplificada e intuitiva. Esta integración se conoce como [segmentación multientidad](../segmentation/multi-entity-segmentation.md). Su organización también puede definir clases XDM para describir otras cosas que no sean individuos, como tiendas, productos o propiedades. Estos[!DNL XDM Individual Profile] los esquemas se conocen como &quot;entidades de dimensión&quot; y no contienen datos de series temporales. Las entidades de Dimension proporcionan datos de búsqueda que ayudan y simplifican las definiciones de segmentos de varias entidades y deben ser lo suficientemente pequeñas como para que el motor de segmentación pueda cargar todo el conjunto de datos en la memoria para un procesamiento óptimo (búsqueda de puntos rápidos).

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)
