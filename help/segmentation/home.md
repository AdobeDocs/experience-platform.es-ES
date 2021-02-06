---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;servicio de segmentos;segmento;Segmento;Segmentos;Segmentos;segmentos
solution: Experience Platform
title: Información general del servicio de segmentación
topic: overview
description: Obtenga información sobre el servicio de segmentación de Adobe Experience Platform y el papel que desempeña en el ecosistema de la plataforma.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---


# Información general del [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API RESTful que le permite generar segmentos y audiencias a partir de sus datos [!DNL Real-time Customer Profile]. Estos segmentos están configurados y mantenidos centralmente en [!DNL Platform] y son fácilmente accesibles para cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y la función que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Es importante comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: Dividir un gran grupo de individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.
- **Definición** del segmento: Conjunto de reglas utilizado para describir las características clave o el comportamiento de una audiencia de destinatario. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia que cumplen los requisitos para un segmento.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles de su almacén de perfiles para distinguir un grupo de personas comercializables de su base de clientes. Por ejemplo: en una campaña por correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que desee una audiencia de todos los usuarios que buscaron zapatos deportivos en los últimos 30 días, pero que no completaron una compra.

Una vez definido conceptualmente un segmento, se genera en [!DNL Experience Platform]. Normalmente, los segmentos son creados por el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que los cree su departamento de marketing, en colaboración con sus analistas de datos. Al revisar los datos que se envían a [!DNL Platform], el analista de datos compone la definición del segmento seleccionando los campos y valores que se utilizarán para generar las reglas o condiciones del segmento. Esto se realiza mediante la interfaz de usuario o la API.

## Crear segmentos

Ya sea que se creen con la API o con el [!DNL Segment Builder], los segmentos se definen finalmente con [!DNL Profile Query Language] (PQL). Aquí es donde se describe la definición del segmento conceptual en el lenguaje creado para recuperar perfiles que cumplan los criterios. Para obtener más información, consulte la [información general de PQL](./pql/overview.md).

Para obtener información sobre cómo crear y utilizar segmentos en [!DNL Segment Builder] (la implementación de IU de [!DNL Segmentation Service]), consulte la [Guía del Generador de segmentos](./ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos de audiencia mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En el evento que se amplía un esquema, todas las cargas futuras deben actualizar los campos recién agregados en consecuencia. Para obtener más información sobre la personalización de [!DNL Experience Data Model] (XDM), visite el [tutorial del Editor de Esquema](../xdm/tutorials/create-schema-ui.md).

## Evaluar segmentos

### Segmentación por flujo continuo

La segmentación por flujo continuo es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario. Una vez creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destinatarios siga siendo relevante.

Para obtener más información acerca de la segmentación de flujo continuo, lea la [documentación de segmentación de flujo](./api/streaming-segmentation.md).

### Segmentación por lotes

Como alternativa a un proceso de selección de datos en curso, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y almacena para que pueda exportarlo para su uso.

Para obtener más información sobre cómo evaluar segmentos, consulte el [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

## Acceso a los resultados de segmentación

Para obtener información sobre cómo acceder a un segmento exportado, consulte el [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

## Metadatos del segmento

Los metadatos del segmento facilitan la indexación en el evento de que cualquiera de los segmentos se va a reutilizar o combinar.

La composición de los segmentos (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre de segmento y una política de combinación.

### Nombres de segmentos

Al crear un nuevo segmento, debe proporcionar un nombre de segmento. El nombre del segmento se utiliza para identificar un segmento particular entre la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de los segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar un segmento, recuerde que se puede hacer referencia a los segmentos desde cualquier otro segmento y combinarlos con él. Al seleccionar un nombre, considere la posibilidad de que el segmento contenga partes reutilizables.

### Combinar directivas

Las políticas de combinación son reglas que [!DNL Profile] utiliza para determinar cómo se priorizarán los datos y cómo se combinarán en una vista unificada bajo ciertas condiciones.
Si no se define una directiva de combinación, se utiliza la directiva de combinación predeterminada [!DNL Platform]. Si prefiere utilizar una directiva de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Encontrará más información sobre las políticas de combinación en la [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación de los tamaños de audiencia se basa en la directiva de combinación de perfiles predeterminada de la organización.

### Otros metadatos de segmentos

Además del nombre del segmento y la directiva de combinación, [!DNL Segment Builder] oferta un campo de metadatos de &quot;descripción del segmento&quot; adicional donde puede resumir el propósito de la definición del segmento.

## Funciones de segmentación avanzada

Los segmentos se pueden configurar para generar continuamente una audiencia combinando [ingestión de datos de flujo](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes características avanzadas de segmentación:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación multientidad](#multi-entity)

Estas funciones avanzadas se analizan con más detalle en las siguientes secciones.

## Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es secuencial. Adobe Experience Platform le permite definir una serie ordenada de segmentos para reflejar este recorrido, capturando así secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado mediante la línea de tiempo del evento visual en [!DNL Segment Builder].

Un ejemplo de un recorrido de cliente que requeriría una segmentación secuencial sería la vista del producto > adición del producto > cierre de compra > Sin compra.

## Segmentación dinámica {#dynamic}

La segmentación dinámica resuelve los problemas de escalabilidad que tradicionalmente enfrentan los especialistas en mercadotecnia al crear segmentos para campañas de mercadotecnia.

A diferencia de la segmentación estática, que requiere capturar explícita y repetidamente cada caso de uso posible, la segmentación dinámica utiliza variables para generar la lógica de regla y expresar relaciones de forma dinámica.

### Caso de uso: Buscando clientes que realizan compras fuera de su estado de origen

Para ilustrar el valor de esta función de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un especialista en mercadotecnia para identificar a los clientes que realizaron compras fuera de su estado de origen.

**El problema**

La segmentación estática requiere que defina segmentos individuales con un atributo de estado principal único, antes de filtrar por eventos de compra que no sean iguales al estado principal. Un segmento explícito de este tipo diría &quot;Estoy buscando personas de Utah donde el estado de su compra no es Utah&quot;. La creación de una audiencia con este método requiere que defina un segmento para cada estado de EE.UU., para un total de 50 segmentos.

Como resultado de las diferentes combinaciones de segmentos que inevitablemente surgen a medida que se escala, el proceso manual requerido para la segmentación estática consume más tiempo, lo que reduce su eficacia general.

**La solución**

Al asignar una variable al atributo de estado de compra, el segmento dinámico se simplifica para que &quot;encuentre una compra en la que el estado de dicha compra no sea igual al estado de origen del cliente&quot;. Esto le permite consolidar 50 segmentos estáticos en un solo segmento dinámico.

## Segmentación de varias entidades {#multi-entity}

Con la característica de segmentación avanzada de varias entidades, puede ampliar [!DNL Real-time Customer Profile] datos con datos adicionales basados en productos, almacenes u otras entidades no personales, también conocidas como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento como si fueran nativos del almacén de datos [!DNL Profile]. La segmentación multientidad proporciona flexibilidad a la hora de identificar audiencias basadas en datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos casos de uso y flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite una variedad de tipos de datos simples y complejos. Encontrará información detallada, incluida una lista de los tipos de datos admitidos, en la [guía de tipos de datos admitidos](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado para crear segmentos a partir de  [!DNL Real-time Customer Profile] datos. En resumen:

- [!DNL Segmentation] es el proceso de definir un subconjunto de perfiles de su almacén de perfiles, lo que permite caracterizar el comportamiento o los atributos de un grupo comercializable deseado. [!DNL Segmentation Service] hace posible este proceso.
- Al planificar un segmento, tenga en cuenta que se puede hacer referencia a un segmento desde cualquier otro segmento y combinarlo con él.
- Un segmento se puede crear a partir de reglas basadas en datos de perfil, datos de series temporales relacionados o ambos.
- Los segmentos se pueden evaluar según sea necesario o de forma continua. Cuando se evalúa según demanda, todos los datos de perfil se pasan a través de las definiciones de segmentos a la vez. Cuando se evalúa continuamente, los datos se transmiten a través de definiciones de segmentos a medida que ingresan [!DNL Platform].

Para obtener información sobre cómo definir segmentos en la interfaz de usuario, consulte la [guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos mediante la API](./tutorials/create-a-segment.md).