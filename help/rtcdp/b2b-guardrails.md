---
keywords: perfil;perfil del cliente en tiempo real;solución de problemas;protecciones;directrices;límite;entidad;entidad principal;entidad de dimensión;RTCDP;CDP;edición B2B;Real-time Customer Data Platform;plataforma de datos del cliente en tiempo real;cdp en tiempo real;b2b;cdp;
title: Protecciones predeterminadas para Real-time Customer Data Platform B2B Edition
type: Documentation
description: Adobe Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional. Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos para obtener un rendimiento óptimo del sistema con Adobe Real-time Customer Data Platform B2B Edition.
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: f6cfe2de5f2f485cbd42c83b539fb458b505d260
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 2%

---

# Protecciones predeterminadas para Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Los límites descritos en este documento representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition le permite ofrecer experiencias multicanal personalizadas basadas en perspectivas de comportamiento y atributos del cliente en forma de Perfiles de cliente en tiempo real y Perfiles de cuenta. Para admitir este nuevo enfoque para los perfiles, Experience Platform utiliza un modelo de datos híbrido altamente desnormalizado que difiere del modelo de datos relacional tradicional.

Este documento proporciona límites predeterminados de uso y velocidad para ayudarle a modelar los datos para obtener un rendimiento óptimo del sistema. Al revisar las siguientes protecciones, se da por hecho que los datos se han modelado correctamente. Si tiene preguntas sobre cómo modelar los datos, póngase en contacto con su representante de servicio de atención al cliente.

>[!INFO]
>
>La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

## Tipos de límite

Existen dos tipos de límites predeterminados en este documento:

| Tipo de protección | Descripción |
| -------------- | ----------- |
| **Protección de rendimiento (límite suave)** | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso. Al superar las barreras de rendimiento, puede experimentar una degradación y latencia del rendimiento. El Adobe no es responsable de esta degradación del rendimiento. Los clientes que exceden de manera consistente una protección de rendimiento pueden optar por licenciar capacidad adicional para evitar la degradación del rendimiento. |
| **Protecciones reforzadas por el sistema (límite estricto)** | La interfaz de usuario o la API de Real-Time CDP aplican las protecciones impuestas por el sistema. Estos son límites que no se pueden superar, ya que la IU y la API le bloquearán el acceso o devolverán un error. |

>[!INFO]
>
>Los límites descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones. Si le interesa conocer los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.

## Límites del modelo de datos

Las siguientes protecciones proporcionan límites recomendados al modelar datos del perfil del cliente en tiempo real. Para obtener más información sobre las entidades principales y las entidades de dimensión, consulte la sección sobre [tipos de entidad](#entity-types) en el apéndice.

### Protecciones de la entidad principal

>[!NOTE]
>
>Los límites del modelo de datos descritos en esta sección representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Conjuntos de datos de clase XDM estándar de Real-Time CDP B2B Edition | 60 | Protección de rendimiento | Se recomienda un máximo de 60 conjuntos de datos que aprovechen las clases estándar del Modelo de datos de experiencia (XDM) proporcionadas por Real-Time CDP B2B Edition. Para obtener una lista completa de las clases XDM estándar para casos de uso B2B, consulte la [Esquemas en la documentación de Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Nota: Debido a la naturaleza del modelo de datos híbrido desnormalizado de Experience Platform, la mayoría de los clientes no superan este límite. Si tiene alguna pregunta sobre cómo modelar los datos o si desea obtener más información sobre los límites personalizados, póngase en contacto con el representante del servicio de atención al cliente.* |
| Recuento de identidad de una cuenta individual en un gráfico de identidad | 50 | Protección de rendimiento | El número máximo de identidades en un gráfico de identidad para una cuenta individual es 50. Cualquier perfil con más de 50 identidades se excluye de la segmentación, las exportaciones y las búsquedas. |
| Relaciones heredadas entre varias entidades | 20 | Protección de rendimiento | Se recomienda un máximo de 20 relaciones de varias entidades definidas entre entidades principales y entidades de dimensión. No se deben realizar asignaciones de relaciones adicionales hasta que se elimine o deshabilite una relación existente. |
| Relaciones varios a uno por clase XDM | 2 | Protección de rendimiento | Se recomienda un máximo de dos relaciones varios a uno definidas por clase XDM. No se debe establecer una relación adicional hasta que se elimine o deshabilite una relación existente. Para ver los pasos sobre cómo crear una relación entre dos esquemas, consulte el tutorial sobre [definición de relaciones de esquema B2B](../xdm/tutorials/relationship-b2b.md). |

### protecciones de entidad Dimension

>[!NOTE]
>
>Los límites del modelo de datos descritos en esta sección representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| No hay relaciones heredadas anidadas | 0 | Protección de rendimiento | No debe crear una relación entre dos variables que no sean[!DNL XDM Individual Profile] esquemas. La creación de relaciones es **no** recomendado para cualquier esquema que no forme parte de [!DNL Profile] esquema de unión. |
| Solo los objetos B2B pueden participar en relaciones varios a uno | 0 | Protección impuesta por el sistema | El sistema solo admite relaciones varios a uno entre objetos B2B. Para obtener más información sobre las relaciones varios a uno, consulte el tutorial sobre [definición de relaciones de esquema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profundidad máxima de relaciones anidadas entre objetos B2B | 3 | Protección impuesta por el sistema | La profundidad máxima de las relaciones anidadas entre objetos B2B es 3. Esto significa que, en un esquema muy anidado, no debe tener una relación entre objetos B2B anidados con más de 3 niveles de profundidad. |
| Esquema único para cada entidad de dimensión | 1 | Protección impuesta por el sistema | Cada entidad de dimensión debe tener un solo esquema. El intento de utilizar entidades de dimensión creadas a partir de más de un esquema puede afectar a los resultados de la segmentación. Se espera que las distintas entidades de dimensión tengan esquemas independientes. |

## Límites de tamaño de datos

Las siguientes protecciones hacen referencia al tamaño de los datos y proporcionan límites recomendados para los datos que se pueden ingerir, almacenar y consultar según lo previsto. Para obtener más información sobre las entidades principales y las entidades de dimensión, consulte la sección sobre [tipos de entidad](#entity-types) en el apéndice.

>[!INFO]
>
>El tamaño de los datos se mide como datos sin comprimir en JSON en el momento de la ingesta.

### Protecciones de la entidad principal

>[!NOTE]
>
>Los límites de tamaño de datos descritos en esta sección representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Lotes ingeridos por clase XDM por día | 45 | Protección de rendimiento | El número total de lotes introducidos cada día por clase XDM no debe superar los 45. La ingesta de lotes adicionales puede impedir un rendimiento óptimo. |

### protecciones de entidad Dimension

>[!NOTE]
>
>Los límites de tamaño de datos descritos en esta sección representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Tamaño total para todas las entidades dimensionales | 5GB | Protección de rendimiento | El tamaño total recomendado para todas las entidades dimensionales es de 5 GB. La ingesta de entidades de gran dimensión puede afectar al rendimiento del sistema. Por ejemplo, no se recomienda intentar cargar un catálogo de productos de 10 GB como entidad de dimensión. |
| Conjuntos de datos por esquema de entidad dimensional | 5 | Protección de rendimiento | Se recomienda un máximo de 5 conjuntos de datos asociados con cada esquema de entidad dimensional. Por ejemplo, si crea un esquema para &quot;productos&quot; y agrega cinco conjuntos de datos colaboradores, no debe crear un sexto conjunto de datos vinculado al esquema de productos. |
| Lotes de entidades Dimension introducidos por día | 4 por entidad | Protección de rendimiento | El número máximo recomendado de lotes de entidades de dimensión introducidos por día es de 4 por entidad. Por ejemplo, puede introducir actualizaciones en un catálogo de productos hasta cuatro veces al día. La ingesta de lotes de entidades de dimensión adicionales para la misma entidad puede afectar al rendimiento del sistema. |

## Protecciones de segmentación

Las protecciones descritas en esta sección hacen referencia al número y la naturaleza de los segmentos que una organización puede crear dentro de Experience Platform, así como a la asignación y activación de segmentos a destinos.

>[!NOTE]
>
>Los límites de segmentación descritos en esta sección representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --------- | ----- | ---------- | ----------- |
| Definiciones de segmentos por zona protegida B2B | 400 | Protección de rendimiento | Una organización puede tener más de 400 definiciones de segmentos en total, siempre y cuando haya menos de 400 definiciones de segmentos en cada zona protegida B2B individual. El intento de crear definiciones de segmento adicionales puede afectar al rendimiento del sistema. |

## Pasos siguientes

Los límites descritos en este documento representan los cambios habilitados por Real-time Customer Data Platform B2B Edition. Para obtener una lista completa de los límites predeterminados de Real-Time CDP B2B Edition, combínelos con los límites generales de Adobe Experience Platform descritos en la sección [protecciones para la documentación de datos del perfil del cliente en tiempo real](../profile/guardrails.md).

## Apéndice

En esta sección se proporcionan detalles adicionales sobre los límites de este documento.

### Tipos de entidad

El [!DNL Profile] el modelo de datos de tienda consta de dos tipos de entidades principales: [entidades principales](#primary-entity) y [entidades de dimensión](#dimension-entity).

#### Entidad principal

Una entidad principal, o entidad de perfil, combina datos para formar una &quot;única fuente de verdad&quot; para un individuo. Estos datos unificados se representan mediante lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un único esquema de unión. El esquema de unión para [!DNL Real-Time Customer Profile] es un modelo de datos híbrido desnormalizado que actúa como contenedor para todos los atributos de perfil y eventos de comportamiento.

Los atributos independientes del tiempo, también conocidos como &quot;datos de registro&quot;, se modelan utilizando [!DNL XDM Individual Profile], mientras que los datos de series temporales, también conocidos como &quot;datos de evento&quot;, se modelan mediante [!DNL XDM ExperienceEvent]. A medida que los datos de registros y series temporales se incorporan en Adobe Experience Platform, se producen déclencheur [!DNL Real-Time Customer Profile] para comenzar a ingerir datos que se hayan habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más sólidos se volverán los perfiles individuales.

![Una infografía que describe las diferencias entre los datos de registro y los datos de series temporales.](../profile/images/guardrails/profile-entity.png)

#### entidad Dimension

Aunque el almacén de datos de perfil que mantiene los datos de perfil no es un almacén relacional, el perfil permite la integración con entidades de dimensión pequeñas para crear segmentos de una manera simplificada e intuitiva. Esta integración se conoce como [segmentación de varias entidades](../segmentation/multi-entity-segmentation.md).

Su organización también puede definir clases XDM para describir cosas que no sean individuales, como tiendas, productos o propiedades. Estas no son[!DNL XDM Individual Profile] los esquemas se denominan &quot;entidades de dimensión&quot; (también conocidas como &quot;entidades de búsqueda&quot;) y no contienen datos de series temporales. Los esquemas que representan entidades de dimensión se vinculan a entidades de perfil mediante el uso de [relaciones de esquema](../xdm/tutorials/relationship-ui.md).

Las entidades Dimension proporcionan datos de búsqueda que ayudan y simplifican las definiciones de segmentos de varias entidades y deben ser lo suficientemente pequeñas como para que el motor de segmentación pueda cargar todo el conjunto de datos en la memoria para un procesamiento óptimo (búsqueda rápida de puntos).

![Infografía que muestra que una entidad de perfil está compuesta por entidades de dimensión.](../profile/images/guardrails/profile-and-dimension-entities.png)
