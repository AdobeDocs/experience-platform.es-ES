---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentos;segmento;segmento;segmento;segmentos;segmentos;segmentos
solution: Experience Platform
title: Resumen del servicio de segmentación
description: Obtenga información acerca del servicio de segmentación de Adobe Experience Platform y la función que desempeña en el ecosistema de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# Información general del [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de [!DNL Real-Time Customer Profile] datos. Estos segmentos se configuran de forma centralizada y se mantienen en [!DNL Platform]y son fácilmente accesibles desde cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y el papel que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Es importante comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: divide un gran grupo de individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que comparten características similares y que responderán de manera similar a las estrategias de marketing.
- **Definición del segmento**: Conjunto de reglas utilizado para describir las características clave o el comportamiento de una audiencia objetivo. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia aptos para un segmento.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Se olvidó de comprar sus zapatillas de deporte?&quot;, es posible que desee una audiencia de todos los usuarios que buscaron zapatillas de running en los últimos 30 días, pero que no completaron una compra.

Una vez definido conceptualmente un segmento, se integra en [!DNL Experience Platform]. Normalmente, los segmentos los crea el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que los cree su departamento de marketing en colaboración con los analistas de datos. Al revisar los datos que se envían a [!DNL Platform], el analista de datos crea la definición del segmento seleccionando qué campos y valores se utilizarán para crear las reglas o condiciones del segmento. Esto se realiza mediante la interfaz de usuario o la API.

## Creación de segmentos

Si se crea mediante la API o mediante [!DNL Segment Builder], los segmentos se definen finalmente mediante [!DNL Profile Query Language] (PQL). Aquí es donde se describe la definición del segmento conceptual en el lenguaje creado para recuperar perfiles que cumplan los criterios. Para obtener más información, consulte la [Información general de PQL](./pql/overview.md).

Para aprender a crear y utilizar segmentos en [!DNL Segment Builder] (la implementación de la IU de [!DNL Segmentation Service]), consulte la [Guía del Generador de segmentos](./ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos de audiencia mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En caso de que se amplíe un esquema, todas las cargas futuras deben actualizar los campos recién añadidos en consecuencia. Para obtener más información sobre la personalización [!DNL Experience Data Model] (XDM), visite la [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Además, si un valor de caducidad de Evento de experiencia está habilitado en el conjunto de datos, esto podría afectar a la pertenencia del segmento creado. Lea la guía de [Caducidad de Experience Event](../profile/event-expirations.md) para obtener más información sobre cómo esta función puede afectar a la segmentación.

## Evaluar segmentos {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Métodos de evaluación"
>abstract="Actualmente, Platform admite tres métodos para evaluar segmentos: segmentación de streaming, segmentación por lotes y segmentación de Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Evaluación de streaming"
>abstract="La segmentación por streaming es un proceso de selección de datos continuo que actualiza los segmentos en respuesta a la actividad del usuario."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Evaluar eventos en tiempo casi real con segmentación de flujo continuo"

Actualmente, Platform admite tres métodos para evaluar segmentos: segmentación de streaming, segmentación por lotes y segmentación de Edge.

### Segmentación de streaming {#streaming}

La segmentación por streaming es un proceso de selección de datos continuo que actualiza los segmentos en respuesta a la actividad del usuario. Una vez que se ha creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-Time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan regularmente, lo que garantiza que la audiencia de destino siga siendo relevante.

Para obtener más información acerca de la segmentación de flujo continuo, lea la [documentación de segmentación de streaming](./api/streaming-segmentation.md).

### Segmentación por lotes {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Evaluación por lotes"
>abstract="Como alternativa a un proceso de selección de datos en curso, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir audiencias correspondientes. Una vez creado, el segmento se guarda y almacena para que pueda exportarlo y utilizarlo."

Como alternativa a un proceso de selección de datos en curso, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir audiencias correspondientes. Una vez creado, este segmento se guarda y almacena para que pueda exportarlo y utilizarlo.

Los segmentos por lotes se evalúan automáticamente cada 24 horas. Si desea evaluar un segmento de lote bajo demanda, puede utilizar un trabajo de segmento. Para obtener más información sobre los trabajos de segmentos, lea la [documentación de trabajos de segmentos](./api/segment-jobs.md).

### Segmentación de Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Evaluación de Edge"
>abstract="La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea en Experience Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Guía de IU de segmentación de Edge"

La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea [en Experience Edge](../edge/home.md), habilitando casos de uso de personalización de la misma página y de la siguiente.

Para obtener más información acerca de la segmentación de Edge, lea cualquiera de las dos [Documentación de API](./api/edge-segmentation.md) o el [Documentación de IU](./ui/edge-segmentation.md).

## Acceso a resultados de segmentación

Para obtener información sobre cómo acceder a un segmento exportado, consulte la [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

## Metadatos de segmentos

Los metadatos del segmento facilitan la indexación en el caso de que cualquiera de sus segmentos se vaya a reutilizar o combinar.

Composición de segmentos (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre de segmento y una política de combinación.

### Nombres de segmentos

Al crear un segmento nuevo, debe proporcionar un nombre de segmento. El nombre del segmento se utiliza para identificar un segmento en particular entre la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de los segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar un segmento, recuerde que se puede hacer referencia a los segmentos desde cualquier otro segmento y combinarlos con él. Al seleccionar un nombre, considere la posibilidad de que el segmento pueda contener partes reutilizables.

### Políticas de combinación

Las políticas de combinación son reglas utilizadas por [!DNL Profile] para determinar cómo se priorizarán y combinarán los datos en una vista unificada en determinadas condiciones.
Si no se define una política de combinación, el valor predeterminado [!DNL Platform] se utiliza la política de combinación. Si prefiere utilizar una política de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación del tamaño de la audiencia se basa en la política de combinación de perfiles predeterminada de la organización.

### Otros metadatos del segmento

Además del nombre del segmento y la política de combinación, [!DNL Segment Builder] le ofrece un campo de metadatos adicional llamado &quot;descripción del segmento&quot; en el que puede resumir el propósito de la definición del segmento.

## Funciones de segmentación avanzada

Los segmentos se pueden configurar para generar continuamente una audiencia de forma continua combinando [ingesta de datos de streaming](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes funciones de segmentación avanzada:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación de varias entidades](#multi-entity)

Estas funciones avanzadas se analizan con más detalle en las siguientes secciones.

## Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es de naturaleza secuencial. Adobe Experience Platform le permite definir una serie ordenada de segmentos para reflejar este recorrido y, por lo tanto, capturar secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado utilizando la cronología de evento visual en [!DNL Segment Builder].

Un ejemplo de recorrido de cliente que requeriría segmentación secuencial sería vista de producto > adición de producto > cierre de compra > Sin compra.

## Segmentación dinámica {#dynamic}

La segmentación dinámica resuelve los problemas de escalabilidad a los que se enfrentan los especialistas en marketing tradicionalmente al crear segmentos para campañas de marketing.

A diferencia de la segmentación estática, que requiere que capture de forma explícita y repetida todos los casos de uso posibles, la segmentación dinámica utiliza variables para crear la lógica de regla y expresar relaciones de forma dinámica.

### Caso de uso: búsqueda de clientes que realizan compras fuera de su estado original

Para ilustrar el valor de esta función de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un experto en marketing para identificar a los clientes que realizaron compras fuera de su estado natal.

**El problema**

La segmentación estática requiere que defina segmentos individuales con un atributo de estado de inicio único antes de filtrar por eventos de compra que no sean iguales al estado de inicio. Un segmento explícito de este tipo diría &quot;Estoy buscando gente de Utah donde el estado de su compra no sea Utah&quot;. Para crear una audiencia con este método, es necesario definir un segmento para cada estado de EE. UU., con un total de 50 segmentos.

Como resultado de las diferentes combinaciones de segmentos que surgen inevitablemente a medida que se escala, el proceso manual necesario para la segmentación estática requiere más tiempo, lo que reduce su eficiencia general.

**La solución**

Al asignar una variable al atributo purchase state, el segmento dinámico simplifica el proceso de búsqueda de &quot;una compra cuyo estado no sea igual al estado de inicio del cliente&quot;. Al hacerlo, puede consolidar 50 segmentos estáticos en un único segmento dinámico.

## Segmentación de varias entidades {#multi-entity}

Con la función de segmentación avanzada de varias entidades, puede ampliar [!DNL Real-Time Customer Profile] datos con datos adicionales basados en productos, tiendas u otras entidades no personales, también conocidas como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento como si fueran nativos de [!DNL Profile] almacén de datos. La segmentación de varias entidades proporciona flexibilidad a la hora de identificar audiencias en función de datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos casos de uso y flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite diversos tipos de datos primitivos y complejos. Encontrará información detallada, incluida una lista de tipos de datos admitidos, en la [guía de tipos de datos admitidos](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado desde el que generar segmentos [!DNL Real-Time Customer Profile] datos. En resumen:

- [!DNL Segmentation] es el proceso de definir un subconjunto de perfiles del almacén de perfiles, lo que le permite caracterizar el comportamiento o los atributos de un grupo comercializable deseado. [!DNL Segmentation Service] hace posible este proceso.
- Al planificar un segmento, tenga en cuenta que se puede hacer referencia a un segmento desde cualquier otro segmento y combinarlo con él.
- Un segmento se puede crear a partir de reglas basadas en datos de perfil, datos de series temporales relacionados o ambos.
- Los segmentos se pueden evaluar bajo demanda o de forma continua. Cuando se evalúan bajo demanda, todos los datos de perfil se pasan a través de las definiciones de segmento a la vez. Cuando se evalúan continuamente, los datos fluyen a través de las definiciones de segmentos a medida que ingresan [!DNL Platform].

Para obtener información sobre cómo definir segmentos en la interfaz de usuario, consulte [Guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos mediante la API](./tutorials/create-a-segment.md).
