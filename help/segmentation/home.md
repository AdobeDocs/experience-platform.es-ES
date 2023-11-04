---
solution: Experience Platform
title: Resumen del servicio de segmentación
description: Obtenga información acerca del servicio de segmentación de Adobe Experience Platform y la función que desempeña en el ecosistema de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 13%

---

# Información general del [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite crear audiencias a través de definiciones de segmentos u otras fuentes a partir de su [!DNL Real-Time Customer Profile] datos. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y el papel que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Debe comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: divide un gran grupo de individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que comparten características similares y que responderán de manera similar a las estrategias de marketing.
- **Audiencia**: una colección de personas que comparten comportamientos o características similares. Adobe Experience Platform puede generar esta colección de personas mediante definiciones de segmento (audiencia generada por Platform) o a partir de fuentes externas (audiencia generada externamente).
- **Definición del segmento**: el conjunto de reglas que utiliza Adobe Experience Platform para describir las características clave o el comportamiento de una audiencia objetivo.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Se olvidó de comprar sus zapatillas de deporte?&quot;, es posible que desee una audiencia de todos los usuarios que buscaron zapatillas de running en los últimos 30 días, pero que no completaron una compra.

Una vez que una audiencia se ha definido conceptualmente, se integra [!DNL Experience Platform]. Normalmente, las audiencias las crea el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que las cree su departamento de marketing en colaboración con los analistas de datos. Al revisar los datos que se envían a [!DNL Platform]Sin embargo, el analista de datos puede crear la audiencia de dos formas: creando una definición de segmento seleccionando qué campos y valores se utilizarán para crear las reglas o condiciones de la audiencia o componiendo una audiencia con la Composición de audiencia.

## Crear audiencias

Las audiencias se pueden crear de dos formas diferentes en Adobe Experience Platform: directamente compuestas como audiencias o a través de definiciones de segmentos derivadas de Platform.

### Composición de audiencia

Al componer directamente una audiencia en Platform, puede utilizar Composición de audiencia. Para aprender a utilizar la Composición de audiencia para crear una audiencia, lea la [Guía de composición de audiencias](./ui/audience-composition.md) para obtener más información.

### Definiciones de segmentos

Si se crea mediante la API o mediante [!DNL Segment Builder], las definiciones de segmentos se definen finalmente mediante [!DNL Profile Query Language] (PQL). Aquí es donde se describe la definición del segmento conceptual en el lenguaje creado para recuperar perfiles que cumplan los criterios. Para obtener más información, consulte la [Información general de PQL](./pql/overview.md).

Para aprender a crear y utilizar segmentos en [!DNL Segment Builder] (la implementación de la IU de [!DNL Segmentation Service]), consulte la [Guía del Generador de segmentos](./ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de definiciones de segmentos mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En caso de que se amplíe un esquema, todas las cargas futuras deben actualizar los campos recién añadidos en consecuencia. Para obtener más información sobre la personalización [!DNL Experience Data Model] (XDM), visite la [Tutorial del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Además, si un valor de caducidad de Evento de experiencia está habilitado en el conjunto de datos, esto podría afectar al abono de la definición de segmento creada. Lea la guía de [Caducidad de Experience Event](../profile/event-expirations.md) para obtener más información sobre cómo esta función puede afectar a la segmentación.

## Evaluar públicos {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Métodos de evaluación"
>abstract="Actualmente, Platform admite tres métodos de evaluación de públicos: segmentación de streaming, segmentación por lotes y segmentación de Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Evaluación de streaming"
>abstract="La segmentación de streaming es un proceso continuo de selección de datos que actualiza las audiencias en respuesta a la actividad de los usuarios."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=es" text="Evaluar eventos en tiempo casi real con segmentación de streaming"

Actualmente, Platform admite tres métodos de evaluación de públicos: segmentación de streaming, segmentación por lotes y segmentación de Edge.

### Segmentación de streaming {#streaming}

La segmentación de streaming es un proceso continuo de selección de datos que actualiza las audiencias en respuesta a la actividad de los usuarios. Una vez que se ha creado y guardado una audiencia, la definición del segmento se aplica a los datos entrantes a [!DNL Real-Time Customer Profile]. Las adiciones y eliminaciones a la audiencia se procesan regularmente, lo que garantiza que la audiencia de destino siga siendo relevante.

Para obtener más información acerca de la segmentación de flujo continuo, lea la [documentación de segmentación de streaming](./api/streaming-segmentation.md).

### Segmentación por lotes {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Evaluación por lotes"
>abstract="Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, el público se guarda y se almacena para que pueda exportarlo para utilizarlo."

Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creada, la audiencia resultante se guarda y almacena para que pueda exportarla y utilizarla.

Las audiencias por lotes se evalúan automáticamente cada 24 horas. Si desea evaluar una audiencia por lotes bajo demanda, puede utilizar un trabajo de segmentación. Para obtener más información sobre los trabajos de segmentos, lea la [documentación de trabajos de segmentos](./api/segment-jobs.md).

### Segmentación de Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Evaluación de Edge"
>abstract="La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en la red de Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente página."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es" text="Guía de la interfaz de usuario de segmentación de Edge"

La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea [en la red perimetral](../edge/home.md), habilitando casos de uso de personalización de la misma página y de la siguiente.

Para obtener más información acerca de la segmentación de Edge, lea cualquiera de las dos [Documentación de API](./api/edge-segmentation.md) o el [Documentación de IU](./ui/edge-segmentation.md).

## Acceso a resultados de segmentación

Para obtener información sobre cómo acceder a una audiencia exportada, consulte la [tutorial de evaluación de definición de segmentos](./tutorials/evaluate-a-segment.md).

## Metadatos de definición de segmento

Los metadatos de definición de segmentos facilitan la indexación en el caso de que alguna de sus audiencias se vaya a reutilizar o combinar.

La composición de una definición de segmento (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre y una política de combinación.

### Nombres de definición de segmento

Al crear una nueva definición de segmento, es necesario proporcionar un nombre. El nombre de la definición del segmento se utiliza para identificar una definición de segmento concreta entre la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de las definiciones de segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar una definición de segmento, recuerde que se puede hacer referencia a las definiciones de segmento desde cualquier otra definición de segmento y combinarlas con ella. Al seleccionar un nombre, considere la posibilidad de que la definición del segmento contenga partes reutilizables.

### Políticas de combinación

Las políticas de combinación son reglas utilizadas por [!DNL Profile] para determinar cómo se priorizarán y combinarán los datos en una vista unificada en determinadas condiciones.

Si no se define una política de combinación, el valor predeterminado [!DNL Platform] se utiliza la política de combinación. Si prefiere utilizar una política de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación del tamaño de la audiencia se basa en la política de combinación de perfiles predeterminada de la organización.

### Otros metadatos de definición de segmento

Además de las políticas de nomenclatura y combinación, [!DNL Segment Builder] le ofrece un campo de metadatos de descripción adicional donde puede resumir el propósito de la definición del segmento.

## Funciones de segmentación avanzada

Las definiciones de segmentos se pueden configurar para generar continuamente una audiencia de forma continua combinando [ingesta de datos de streaming](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes funciones de segmentación avanzada:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación de varias entidades](#multi-entity)

Estas funciones avanzadas se analizan con más detalle en las siguientes secciones.

### Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es de naturaleza secuencial. Adobe Experience Platform le permite definir una serie ordenada de audiencias para reflejar este recorrido y, por lo tanto, capturar secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado utilizando la cronología de evento visual en [!DNL Segment Builder].

Un ejemplo de recorrido de cliente que requeriría segmentación secuencial sería vista de producto > adición de producto > cierre de compra > Sin compra.

### Segmentación dinámica {#dynamic}

La segmentación dinámica resuelve los problemas de escalabilidad a los que se enfrentan los especialistas en marketing tradicionalmente al crear audiencias para campañas de marketing.

A diferencia de la segmentación estática, que requiere que capture de forma explícita y repetida todos los casos de uso posibles, la segmentación dinámica utiliza variables para crear la lógica de regla y expresar relaciones de forma dinámica.

Para ilustrar el valor de esta función de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un experto en marketing para identificar a los clientes que realizaron compras fuera de su estado natal.

La segmentación estática requiere que defina segmentos individuales con un atributo de estado de inicio único antes de filtrar por eventos de compra que no sean iguales al estado de inicio. Una definición explícita de segmento de este tipo diría &quot;Busco personas de Utah donde el estado de su compra no sea Utah&quot;. La creación de una audiencia con este método requiere que defina una definición de segmento para cada estado de EE. UU., para un total de 50 segmentos.

Como resultado de las diferentes combinaciones de definiciones de segmentos que surgen inevitablemente a medida que se escala, el proceso manual necesario para la segmentación estática requiere más tiempo, lo que reduce su eficiencia general.

Al asignar una variable al atributo de estado de compra, la definición del segmento dinámico se simplifica a &quot;buscarme una compra en la que el estado de esa compra no sea igual al estado de inicio del cliente&quot;. Al hacerlo, puede consolidar 50 segmentos estáticos en una sola definición de segmento dinámico.

### Segmentación de varias entidades {#multi-entity}

Con la función de segmentación avanzada de varias entidades, puede ampliar [!DNL Real-Time Customer Profile] datos con datos adicionales basados en productos, tiendas u otras entidades no personales, también conocidas como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento como si fueran nativos de [!DNL Profile] almacén de datos. La segmentación de varias entidades proporciona flexibilidad a la hora de identificar audiencias en función de datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos casos de uso y flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite diversos tipos de datos primitivos y complejos. Encontrará información detallada, incluida una lista de tipos de datos admitidos, en la [guía de tipos de datos admitidos](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado desde el que crear audiencias [!DNL Real-Time Customer Profile] datos.

Para obtener más información sobre el uso de la interfaz de usuario del servicio de segmentación, lea la [Resumen de IU del servicio de segmentación](./ui/overview.md).

Para aprender a componer audiencias en la interfaz de usuario, lea la [Guía de composición de audiencias](./ui/audience-composition.md). Para obtener información sobre cómo definir definiciones de segmentos en la interfaz de usuario, consulte la [Guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de definiciones de segmentos mediante la API](./tutorials/create-a-segment.md).
