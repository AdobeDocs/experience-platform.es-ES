---
solution: Experience Platform
title: Resumen del servicio de segmentación
description: Obtenga información acerca del servicio de segmentación de Adobe Experience Platform y la función que desempeña en el ecosistema de Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 4ef3f6dc07cb5d17146d48c7a41e3745fd9a3a58
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 12%

---

# Información general de [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API RESTful que le permiten crear audiencias a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y la función que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Debe comprender los siguientes términos clave utilizados en este documento:

- **Audiencia**: Una colección de personas que comparten comportamientos o características similares. Adobe Experience Platform puede generar esta colección de personas mediante definiciones de segmento (audiencia generada por Platform) o a partir de fuentes externas (audiencia generada externamente).
- **Definición de segmento**: El conjunto de reglas que utiliza Adobe Experience Platform para describir las características clave o el comportamiento de una audiencia de destino.
- **Segmento**: Acto de separar Perfiles en audiencias.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Se olvidó de comprar sus zapatillas de deporte?&quot;, es posible que desee una audiencia de todos los usuarios que buscaron zapatillas de running en los últimos 30 días, pero que no completaron una compra.

Una vez definida conceptualmente una audiencia, se genera en [!DNL Experience Platform]. Normalmente, las audiencias las crea el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que las cree su departamento de marketing en colaboración con los analistas de datos. Al revisar los datos que se envían a [!DNL Platform], el analista de datos puede crear la audiencia de dos formas: creando una definición de segmento seleccionando qué campos y valores se utilizarán para crear las reglas o condiciones de la audiencia, o componiendo una audiencia con la Composición de audiencia.

## Creación de públicos

Las audiencias se pueden crear de dos formas diferentes en Adobe Experience Platform: directamente compuestas como audiencias o a través de definiciones de segmentos derivadas de Platform.

### Composición del público

Al componer directamente una audiencia en Platform, puede utilizar Composición de audiencia. Para aprender a usar la Composición de audiencia con el fin de crear una audiencia, lea la [guía de Composición de audiencia](./ui/audience-composition.md) para obtener más información.

### Definiciones de segmentos

Ya se creen usando la API o usando [!DNL Segment Builder], las definiciones de segmentos se definen finalmente usando [!DNL Profile Query Language] (PQL). Aquí es donde se describe la definición del segmento conceptual en el lenguaje creado para recuperar perfiles que cumplan los criterios. Para obtener más información, consulte la [descripción general de PQL](./pql/overview.md).

Para obtener información sobre cómo crear y usar segmentos en [!DNL Segment Builder] (la implementación de la interfaz de usuario de [!DNL Segmentation Service]), consulte la [guía del Generador de segmentos](./ui/segment-builder.md).

Para obtener información sobre cómo generar definiciones de segmentos mediante la API, consulte el tutorial de [creación de definiciones de segmentos mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En caso de que se amplíe un esquema, todas las cargas futuras deben actualizar los campos recién añadidos en consecuencia. Para obtener más información sobre cómo personalizar [!DNL Experience Data Model] (XDM), visite el [tutorial del editor de esquemas](../xdm/tutorials/create-schema-ui.md).
>
>Además, si un valor de caducidad de Evento de experiencia está habilitado en el conjunto de datos, esto podría afectar al abono de la definición de segmento creada. Lea la guía sobre [Caducidad de eventos de experiencia](../profile/event-expirations.md) para obtener más información sobre cómo esta característica puede afectar la segmentación.

### Composición de público federado {#fac}

Además de las composiciones de audiencias y las definiciones de segmentos, puede utilizar Composición de audiencia federada de Adobe para crear nuevas audiencias a partir de conjuntos de datos empresariales sin copiar los datos subyacentes y almacenarlas en Adobe Experience Platform Audience Portal. También puede enriquecer las audiencias existentes en Adobe Experience Platform utilizando datos de audiencia compuestos que se han federado desde Enterprise Data Warehouse. Lea la guía de [Composición federada de audiencias](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/home).

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

La segmentación de streaming es un proceso continuo de selección de datos que actualiza los públicos en respuesta a la actividad de los usuarios. Una vez creada y guardada una audiencia, la definición del segmento se aplica a los datos entrantes de [!DNL Real-Time Customer Profile]. Las adiciones y eliminaciones a la audiencia se procesan regularmente, lo que garantiza que la audiencia de destino siga siendo relevante.

Para obtener más información acerca de la segmentación por transmisión, lea la [documentación de segmentación por transmisión](./api/streaming-segmentation.md).

### Segmentación por lotes {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Evaluación por lotes"
>abstract="Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, el público se guarda y se almacena para que pueda exportarlo para utilizarlo."

Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creada, la audiencia resultante se guarda y almacena para que pueda exportarla y utilizarla.

Las audiencias por lotes se evalúan automáticamente cada 24 horas. Si desea evaluar una audiencia por lotes bajo demanda, puede utilizar un trabajo de segmentación. Para obtener más información acerca de los trabajos de segmentos, lea la [documentación de trabajos de segmentos](./api/segment-jobs.md).

### Segmentación de Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Evaluación de Edge"
>abstract="La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en la red de Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente página."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=es" text="Guía de la interfaz de usuario de segmentación de Edge"

La segmentación de Edge es la capacidad para evaluar segmentos en Platform de forma instantánea [en el Edge Network](../web-sdk/home.md), lo que permite casos de uso de personalización de la misma página y de la siguiente.

Para obtener más información acerca de la segmentación de Edge, lea la [documentación de la API](./api/edge-segmentation.md) o la [documentación de la interfaz de usuario](./ui/edge-segmentation.md).

## Acceso a resultados de segmentación

Para obtener información sobre cómo tener acceso a una audiencia exportada, consulte el [tutorial de evaluación de definición de segmento](./tutorials/evaluate-a-segment.md).

## Metadatos de definición de segmento

Los metadatos de definición de segmentos facilitan la indexación en el caso de que alguna de sus audiencias se vaya a reutilizar o combinar.

La composición de una definición de segmento (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre y una política de combinación.

### Nombres de definición de segmento

Al crear una nueva definición de segmento, es necesario proporcionar un nombre. El nombre de la definición del segmento se usa para identificar una definición de segmento determinada entre la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de las definiciones de segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar una definición de segmento, recuerde que se puede hacer referencia a las definiciones de segmento desde cualquier otra definición de segmento y combinarlas con ella. Al seleccionar un nombre, considere la posibilidad de que la definición del segmento contenga partes reutilizables.

### Combinar políticas

Las políticas de combinación son reglas utilizadas por [!DNL Profile] para determinar cómo se priorizarán y combinarán los datos en una vista unificada en ciertas condiciones.

Si no se define una política de combinación, se utilizará la política de combinación predeterminada [!DNL Platform]. Si prefiere utilizar una política de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación del tamaño de la audiencia se basa en la política de combinación de perfiles predeterminada de la organización.

### Otros metadatos de definición de segmento

Además de las políticas de nomenclatura y combinación, [!DNL Segment Builder] le ofrece un campo de metadatos de descripción adicional en el que puede resumir el propósito de la definición del segmento.

## Funciones de segmentación avanzada

Las definiciones de segmentos se pueden configurar para generar una audiencia de forma continua combinando [la transmisión de datos](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes características de segmentación avanzada:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación de varias entidades](#multi-entity)

Estas funciones avanzadas se analizan con más detalle en las siguientes secciones.

### Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es de naturaleza secuencial. Adobe Experience Platform le permite definir una serie ordenada de audiencias para reflejar este recorrido y, por lo tanto, capturar secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden que desee mediante la escala de tiempo del evento visual en [!DNL Segment Builder].

Un ejemplo de recorrido de cliente que requeriría segmentación secuencial sería vista de producto > adición de producto > cierre de compra > Sin compra.

### Segmentación dinámica {#dynamic}

La segmentación dinámica resuelve los problemas de escalabilidad a los que se enfrentan los especialistas en marketing tradicionalmente al crear audiencias para campañas de marketing.

A diferencia de la segmentación estática, que requiere que capture de forma explícita y repetida todos los casos de uso posibles, la segmentación dinámica utiliza variables para crear la lógica de regla y expresar relaciones de forma dinámica.

Para ilustrar el valor de esta función de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un experto en marketing para identificar a los clientes que realizaron compras fuera de su estado natal.

La segmentación estática requiere que defina segmentos individuales con un atributo de estado de inicio único antes de filtrar por eventos de compra que no sean iguales al estado de inicio. Una definición explícita de segmento de este tipo diría &quot;Busco personas de Utah donde el estado de su compra no sea Utah&quot;. La creación de una audiencia con este método requiere que defina una definición de segmento para cada estado de EE. UU., para un total de 50 segmentos.

Como resultado de las diferentes combinaciones de definiciones de segmentos que surgen inevitablemente a medida que se escala, el proceso manual necesario para la segmentación estática requiere más tiempo, lo que reduce su eficiencia general.

Al asignar una variable al atributo de estado de compra, la definición del segmento dinámico se simplifica a &quot;buscarme una compra en la que el estado de esa compra no sea igual al estado de inicio del cliente&quot;. Al hacerlo, puede consolidar 50 segmentos estáticos en una sola definición de segmento dinámico.

### Segmentación de varias entidades {#multi-entity}

Con la característica de segmentación avanzada de varias entidades, puede ampliar los datos de [!DNL Real-Time Customer Profile] con datos adicionales basados en productos, tiendas u otras entidades que no sean personas, también conocidas como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento como si fueran nativos del almacén de datos [!DNL Profile]. La segmentación de varias entidades proporciona flexibilidad a la hora de identificar audiencias en función de datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos casos de uso y flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite diversos tipos de datos primitivos y complejos. Encontrará información detallada, incluida una lista de tipos de datos admitidos, en la [guía de tipos de datos admitidos](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado para generar audiencias a partir de los datos de [!DNL Real-Time Customer Profile].

Para obtener más información sobre el uso de la interfaz de usuario del servicio de segmentación, lea la [descripción general de la interfaz de usuario del servicio de segmentación](./ui/overview.md).

Para aprender a componer audiencias en la interfaz de usuario, lea la [guía de composición de audiencias](./ui/audience-composition.md). Para obtener información sobre cómo definir definiciones de segmentos en la interfaz de usuario, consulte la [guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre cómo generar definiciones de segmentos mediante la API, consulte el tutorial de [creación de definiciones de segmentos mediante la API](./tutorials/create-a-segment.md).
