---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentos;segmento;segmento;segmentos;segmentos
solution: Experience Platform
title: Información general del servicio de segmentación
topic-legacy: overview
description: Obtenga información sobre el servicio de segmentación de Adobe Experience Platform y la función que desempeña en el ecosistema de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 52197a6c009fb5b0b6037a4fef3c98ad7c327e2e
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 0%

---

# Información general del [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados de forma centralizada y se mantienen en [!DNL Platform], y son fácilmente accesibles para cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y la función que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Es importante comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: Dividir un grupo grande de personas (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que compartan características similares y que respondan de manera similar a las estrategias de marketing.
- **Definición del segmento**: Conjunto de reglas utilizado para describir características clave o el comportamiento de una audiencia de destino. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia cualificados para un segmento.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que quiera una audiencia de todos los usuarios que buscaron zapatillas en los últimos 30 días, pero que no completaron una compra.

Una vez definido conceptualmente un segmento, se integra en [!DNL Experience Platform]. Normalmente, los segmentos los crea el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que los cree su departamento de marketing, en colaboración con sus analistas de datos. Tras revisar los datos que se envían a [!DNL Platform], el analista de datos compone la definición del segmento seleccionando qué campos y valores se utilizarán para crear las reglas o condiciones del segmento. Esto se realiza mediante la interfaz de usuario o la API.

## Creación de segmentos

Si se crea mediante la API o utilizando la variable [!DNL Segment Builder], los segmentos se definen usando [!DNL Profile Query Language] (PQL). Aquí es donde la definición del segmento conceptual se describe en el idioma creado para recuperar perfiles que cumplen los criterios. Para obtener más información, consulte la [Información general de PQL](./pql/overview.md).

Para aprender a crear y utilizar segmentos en la variable [!DNL Segment Builder] (la implementación de la interfaz de usuario de [!DNL Segmentation Service]), consulte la [Guía del Generador de segmentos](./ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos de audiencia mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En caso de que se amplíe un esquema, todas las cargas futuras deben actualizar los campos recién añadidos en consecuencia. Para obtener más información sobre la personalización [!DNL Experience Data Model] (XDM), visite el [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Además, si el tiempo de vida (TTL) está habilitado en el conjunto de datos, esto podría afectar a la pertenencia del segmento creado. Para obtener más información sobre TTL y cómo puede afectar a la segmentación, lea la [Guía de TTL del servicio de perfil](../profile/apply-ttl.md).

## Evaluar segmentos {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Métodos de evaluación"
>abstract="Actualmente, Platform admite tres métodos de evaluación de segmentos: segmentación de flujo continuo, segmentación por lotes y segmentación perimetral."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Evaluación de flujos"
>abstract="La segmentación por transmisión es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Evaluar eventos en tiempo casi real con segmentación de flujo continuo"

Actualmente, Platform admite tres métodos de evaluación de segmentos: segmentación de flujo continuo, segmentación por lotes y segmentación perimetral.

### Segmentación por transmisión {#streaming}

La segmentación por transmisión es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario. Una vez que se ha creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destino siga siendo relevante.

Para obtener más información sobre la segmentación de flujo continuo, lea la [documentación de segmentación por secuencias](./api/streaming-segmentation.md).

### Segmentación por lotes {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Evaluación por lotes"
>abstract="Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, el segmento se guarda y se almacena para que pueda exportarlo para utilizarlo."

Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y se almacena para que pueda exportarlo para utilizarlo.

Los segmentos por lotes se evalúan automáticamente cada 24 horas. Si desea evaluar un segmento de lote bajo demanda, puede utilizar un trabajo de segmento. Para obtener más información sobre los trabajos de segmentos, lea la [documentación de trabajos de segmentos](./api/segment-jobs.md).

### Segmentación de Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Evaluación de Edge"
>abstract="La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en Experience Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente página."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Guía de la interfaz de usuario de segmentación de Edge"

La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea [en Experience Edge](../edge/home.md), habilitando casos de uso de personalización de la misma página y de la siguiente página.

Para obtener más información sobre la segmentación de Edge, lea cualquiera de las [Documentación de API](./api/edge-segmentation.md) o [Documentación de la interfaz de usuario](./ui/edge-segmentation.md).

## Acceso a los resultados de segmentación

Para obtener información sobre cómo acceder a un segmento exportado, consulte la [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

## Metadatos del segmento

Los metadatos de segmento facilitan la indexación en caso de que se reutilice o combine cualquiera de los segmentos.

Composición de segmentos (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre de segmento y una política de combinación.

### Nombres de segmentos

Al crear un segmento nuevo, debe proporcionar un nombre de segmento. El nombre del segmento se utiliza para identificar un segmento concreto de la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de los segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar un segmento, recuerde que se puede hacer referencia a los segmentos desde cualquier otro segmento y combinarlos con él. Al seleccionar un nombre, tenga en cuenta la posibilidad de que el segmento contenga partes reutilizables.

### Combinar directivas

Las directivas de combinación son reglas que usa [!DNL Profile] para determinar cómo se priorizarán los datos y cómo se combinarán en una vista unificada bajo ciertas condiciones.
Si no se define una directiva de combinación, el valor predeterminado es [!DNL Platform] se utiliza la directiva de combinación. Si prefiere usar una directiva de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Puede encontrar más información sobre las políticas de combinación en la sección [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación de los tamaños de audiencia se basa en la política de combinación de perfiles predeterminada de la organización.

### Otros metadatos de segmentos

Además del nombre del segmento y la directiva de combinación, [!DNL Segment Builder] le ofrece un campo de metadatos &quot;descripción del segmento&quot; adicional donde puede resumir el propósito de su definición del segmento.

## Funciones de segmentación avanzada

Los segmentos se pueden configurar para que generen una audiencia de forma continua combinando [ingesta de datos de flujo continuo](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes funciones avanzadas de segmentación:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación de varias entidades](#multi-entity)

Estas funciones avanzadas se describen con más detalle en las secciones siguientes.

## Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es secuencial. Adobe Experience Platform le permite definir una serie ordenada de segmentos para que reflejen este recorrido y, por lo tanto, capturar secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado utilizando la cronología del evento visual en la variable [!DNL Segment Builder].

Un ejemplo de recorrido de un cliente que requeriría una segmentación secuencial sería vista de producto > adición de producto > cierre de compra > Sin compra.

## Segmentación dinámica {#dynamic}

La segmentación dinámica resuelve los problemas de escalabilidad que tradicionalmente enfrentan los especialistas en marketing al crear segmentos para campañas de marketing.

A diferencia de la segmentación estática, que requiere que capture explícita y repetidamente todos los casos de uso posibles, la segmentación dinámica utiliza variables para generar la lógica de reglas y expresar relaciones de forma dinámica.

### Caso de uso: Buscando clientes que realizan compras fuera del estado de origen

Para ilustrar el valor de esta característica de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un especialista en marketing para identificar a los clientes que realizaron compras fuera de su estado de origen.

**El problema**

La segmentación estática requiere que defina segmentos individuales con un atributo de estado principal único antes de filtrar por eventos de compra que no sean iguales al estado principal. Un segmento explícito de este tipo diría &quot;Estoy buscando personas de Utah donde el estado de su compra no es Utah&quot;. Para crear una audiencia con este método es necesario definir un segmento para cada estado de EE. UU., con un total de 50 segmentos.

Como resultado de las diferentes combinaciones de segmentos que inevitablemente surgen a medida que se escala, el proceso manual requerido para la segmentación estática toma más tiempo, lo que reduce su eficacia general.

**La solución**

Al asignar una variable al atributo de estado de compra, el segmento dinámico se simplifica para que &quot;encuentre una compra en la que el estado de dicha compra no sea igual al estado de origen del cliente&quot;. Al hacerlo, puede consolidar 50 segmentos estáticos en un único segmento dinámico.

## Segmentación de varias entidades {#multi-entity}

Con la función avanzada de segmentación multientidad, puede ampliar [!DNL Real-time Customer Profile] datos con datos adicionales basados en productos, tiendas u otras personas no personales, también conocidos como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento, como si fueran nativos de la variable [!DNL Profile] almacén de datos. La segmentación multientidad proporciona flexibilidad a la hora de identificar audiencias basándose en datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos los casos de uso y los flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite una variedad de tipos de datos simples y complejos. Encontrará información detallada, incluida una lista de los tipos de datos compatibles, en la [guía de tipos de datos compatibles](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado desde el que crear segmentos [!DNL Real-time Customer Profile] datos. En resumen:

- [!DNL Segmentation] es el proceso de definición de un subconjunto de perfiles del almacén de perfiles, que le permite caracterizar el comportamiento o los atributos de un grupo comercializable deseado. [!DNL Segmentation Service] hace posible este proceso.
- Al planificar un segmento, tenga en cuenta que se puede hacer referencia a un segmento desde cualquier otro segmento y combinarlo con él.
- Un segmento se puede crear a partir de reglas basadas en datos de perfil, datos de series temporales relacionadas o ambos.
- Los segmentos se pueden evaluar bajo demanda o de forma continua. Cuando se evalúan bajo demanda, todos los datos de perfil se pasan a través de las definiciones de segmento a la vez. Cuando se evalúan continuamente, los datos se transmiten a través de definiciones de segmento a medida que se introducen [!DNL Platform].

Para obtener información sobre cómo definir segmentos en la interfaz de usuario, consulte la [Guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos mediante la API](./tutorials/create-a-segment.md).
