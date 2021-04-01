---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentos;segmento;segmento;segmentos;segmentos
solution: Experience Platform
title: Información general del servicio de segmentación
topic: sobre validación
description: Obtenga información sobre el servicio de segmentación de Adobe Experience Platform y la función que desempeña en el ecosistema de Platform.
translation-type: tm+mt
source-git-commit: eff833f20eba4e51579a43fbb98c1e2333e326ef
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# Información general del [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite crear segmentos y generar audiencias a partir de sus datos [!DNL Real-time Customer Profile]. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform] y son fácilmente accesibles para cualquier solución de Adobe.

Este documento proporciona información general sobre [!DNL Segmentation Service] y la función que desempeña en Adobe Experience Platform.

## Introducción a [!DNL Segmentation Service]

Es importante comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: Dividir un grupo grande de personas (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que compartan características similares y que respondan de manera similar a las estrategias de marketing.
- **Definición** de segmento: Conjunto de reglas utilizado para describir características clave o el comportamiento de una audiencia de destino. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia cualificados para un segmento.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que quiera una audiencia de todos los usuarios que buscaron zapatillas en los últimos 30 días, pero que no completaron una compra.

Una vez definido conceptualmente un segmento, se crea en [!DNL Experience Platform]. Normalmente, los segmentos los crea el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que los cree su departamento de marketing, en colaboración con sus analistas de datos. Tras revisar los datos que se envían a [!DNL Platform], el analista de datos compone la definición del segmento seleccionando los campos y valores que se utilizarán para crear las reglas o condiciones del segmento. Esto se realiza mediante la interfaz de usuario o la API.

## Crear segmentos

Tanto si se crean mediante la API como si utilizan [!DNL Segment Builder], los segmentos se definen finalmente mediante [!DNL Profile Query Language] (PQL). Aquí es donde la definición del segmento conceptual se describe en el idioma creado para recuperar perfiles que cumplen los criterios. Para obtener más información, consulte la [información general de PQL](./pql/overview.md).

Para obtener información sobre cómo crear y utilizar segmentos en [!DNL Segment Builder] (la implementación de [!DNL Segmentation Service] en la interfaz de usuario), consulte la [guía del Generador de segmentos](./ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre la [creación de segmentos de audiencia mediante la API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>En caso de que se amplíe un esquema, todas las cargas futuras deben actualizar los campos recién añadidos en consecuencia. Para obtener más información sobre la personalización de [!DNL Experience Data Model] (XDM), visite el [tutorial del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

## Evaluar segmentos

Actualmente, Platform admite tres métodos de evaluación de segmentos: segmentación de flujo continuo, segmentación por lotes y segmentación perimetral.

### Segmentación por transmisión

La segmentación por transmisión es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario. Una vez creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes en [!DNL Real-time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destino siga siendo relevante.

Para obtener más información sobre la segmentación de flujo continuo, lea la [documentación de segmentación de flujo continuo](./api/streaming-segmentation.md).

### Segmentación por lotes

Como alternativa a un proceso continuo de selección de datos, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y se almacena para que pueda exportarlo para utilizarlo.

**Segmentación incremental (beta)**

Los segmentos por lotes se evalúan cada 24 horas. Sin embargo, para los segmentos existentes, la segmentación incremental mantiene los segmentos actualizados durante hasta una hora.

La segmentación incremental se ejecuta con nuevos datos que llegan al almacén de perfiles. Sin embargo, se aplican las siguientes advertencias para la segmentación incremental:

- Para cualquier segmento nuevo o modificado recientemente, los perfiles con datos nuevos empezarán a clasificarse en la siguiente ejecución incremental. Sin embargo, los perfiles sin cambios se pondrán al día en el siguiente trabajo de segmentación por lotes completo.
- Los segmentos de varias entidades se actualizarán en la segmentación incremental. Si hay actualizaciones de entidad, cualquier perfil con nuevos datos empezará a utilizarlos en la siguiente ejecución incremental. Sin embargo, los perfiles sin cambios se pondrán al día en el siguiente trabajo de segmentación por lotes completo.
- Los eventos que se pierdan en el periodo de tiempo de un segmento se reconciliarán en el siguiente trabajo de segmentación por lotes completo.

Para obtener información sobre cómo evaluar segmentos, consulte el [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

### Segmentación de Edge

La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.

Para obtener más información sobre la segmentación de Edge, lea la [documentación de API](./api/edge-segmentation.md) o la [documentación de la interfaz de usuario](./ui/edge-segmentation.md).

## Acceso a los resultados de segmentación

Para obtener información sobre cómo acceder a un segmento exportado, consulte el [tutorial de evaluación de segmentos](./tutorials/evaluate-a-segment.md).

## Metadatos del segmento

Los metadatos de segmento facilitan la indexación en caso de que se reutilice o combine cualquiera de los segmentos.

La composición de los segmentos (a través de la API o [!DNL Segment Builder]) requiere que defina un nombre de segmento y una política de combinación.

### Nombres de segmentos

Al crear un segmento nuevo, debe proporcionar un nombre de segmento. El nombre del segmento se utiliza para identificar un segmento concreto de la colección creada por [!DNL Segmentation Service]. Por lo tanto, los nombres de los segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE]
>
>Al planificar un segmento, recuerde que se puede hacer referencia a los segmentos desde cualquier otro segmento y combinarlos con él. Al seleccionar un nombre, tenga en cuenta la posibilidad de que el segmento contenga partes reutilizables.

### Combinar directivas

Las políticas de combinación son reglas que utiliza [!DNL Profile] para determinar cómo se priorizarán los datos y cómo se combinarán en una vista unificada bajo ciertas condiciones.
Si no se define una directiva de combinación, se utiliza la directiva de combinación predeterminada [!DNL Platform]. Si prefiere usar una directiva de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

Puede encontrar más información sobre las políticas de combinación en la [guía de políticas de combinación](../profile/api/merge-policies.md).

>[!NOTE]
>
>La estimación de los tamaños de audiencia se basa en la política de combinación de perfiles predeterminada de la organización.

### Otros metadatos de segmentos

Además del nombre del segmento y la política de combinación, [!DNL Segment Builder] le ofrece un campo de metadatos de &quot;descripción del segmento&quot; adicional en el que puede resumir el propósito de su definición del segmento.

## Funciones de segmentación avanzada

Los segmentos se pueden configurar para generar una audiencia de forma continua combinando [ingesta de datos de flujo continuo](../ingestion/streaming-ingestion/overview.md) con cualquiera de las siguientes funciones avanzadas de segmentación:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación de varias entidades](#multi-entity)

Estas funciones avanzadas se describen con más detalle en las secciones siguientes.

## Segmentación secuencial {#sequential}

Un recorrido de usuario estándar es secuencial. Adobe Experience Platform le permite definir una serie ordenada de segmentos para que reflejen este recorrido y, por lo tanto, capturar secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado utilizando la cronología del evento visual en [!DNL Segment Builder].

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

Con la característica avanzada de segmentación multientidad, puede ampliar los datos [!DNL Real-time Customer Profile] con datos adicionales basados en productos, tiendas u otras personas no físicas, también conocidas como entidades de &quot;dimensión&quot;. Como resultado, [!DNL Segmentation Service] puede acceder a campos adicionales durante la definición del segmento como si fueran nativos del almacén de datos [!DNL Profile]. La segmentación multientidad proporciona flexibilidad a la hora de identificar audiencias basándose en datos relevantes para sus necesidades comerciales únicas. Para obtener más información, incluidos los casos de uso y los flujos de trabajo, consulte la [guía de segmentación de varias entidades](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipos de datos

[!DNL Segmentation Service] admite una variedad de tipos de datos simples y complejos. Puede encontrar información detallada, incluida una lista de tipos de datos compatibles, en la [guía de tipos de datos admitidos](./data-types.md).

## Pasos siguientes

[!DNL Segmentation Service] proporciona un flujo de trabajo consolidado para crear segmentos a partir de  [!DNL Real-time Customer Profile] datos. En resumen:

- [!DNL Segmentation] es el proceso de definición de un subconjunto de perfiles del almacén de perfiles, que le permite caracterizar el comportamiento o los atributos de un grupo comercializable deseado. [!DNL Segmentation Service] hace posible este proceso.
- Al planificar un segmento, tenga en cuenta que se puede hacer referencia a un segmento desde cualquier otro segmento y combinarlo con él.
- Un segmento se puede crear a partir de reglas basadas en datos de perfil, datos de series temporales relacionadas o ambos.
- Los segmentos se pueden evaluar bajo demanda o de forma continua. Cuando se evalúan bajo demanda, todos los datos de perfil se pasan a través de las definiciones de segmento a la vez. Cuando se evalúan continuamente, los datos se transmiten a través de definiciones de segmento a medida que se introduce [!DNL Platform].

Para aprender a definir segmentos en la interfaz de usuario, consulte la [guía del Generador de segmentos](./ui/overview.md). Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre la [creación de segmentos mediante la API](./tutorials/create-a-segment.md).