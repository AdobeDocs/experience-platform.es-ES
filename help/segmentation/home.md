---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servicio de segmentación de la plataforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Descripción general del servicio de segmentación

El servicio de segmentación de la plataforma de experiencia de Adobe proporciona una interfaz de usuario y una API RESTful que le permite crear segmentos y generar audiencias a partir de los datos de Perfil de clientes en tiempo real. Estos segmentos están configurados y mantenidos de forma centralizada en Platform y son fácilmente accesibles para cualquier solución de Adobe.

Este documento proporciona información general sobre el servicio de segmentación y la función que desempeña en Adobe Experience Platform.

## Introducción al servicio de segmentación

Es importante comprender los siguientes términos clave utilizados en este documento:

- **Segmentación**: Dividir un gran grupo de individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.
- **Definición** del segmento: Conjunto de reglas utilizado para describir las características clave o el comportamiento de una audiencia de destinatario. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia que cumplen los requisitos para un segmento.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Funcionamiento de la segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles de su almacén de perfiles para distinguir un grupo de personas comercializables de su base de clientes. Por ejemplo: en una campaña por correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que desee una audiencia de todos los usuarios que buscaron zapatos deportivos en los últimos 30 días, pero que no completaron una compra.

Una vez definido conceptualmente un segmento, se crea en la plataforma de experiencia. Normalmente, los segmentos son creados por el especialista en marketing o audiencia, aunque algunas organizaciones prefieren que los cree su departamento de marketing, en colaboración con sus analistas de datos. Al revisar los datos que se envían a la plataforma, el analista de datos compone la definición del segmento seleccionando los campos y valores que se utilizarán para generar las reglas o condiciones del segmento. Esto se realiza mediante la interfaz de usuario o la API.

## Crear segmentos

Ya sea que se creen con la API o con el Generador de segmentos, los segmentos se definen finalmente con el Lenguaje de Consulta de Perfil (PQL). Aquí es donde se describe la definición del segmento conceptual en el lenguaje creado para recuperar perfiles que cumplan los criterios. Para obtener más información, consulte la descripción general [de](./pql/overview.md)PQL.

Para obtener información sobre cómo crear y utilizar segmentos en el Generador de segmentos (la implementación de la interfaz de usuario del servicio de segmentación), consulte la guía [Generador de](./ui/overview.md)segmentos.

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre la [creación de segmentos de audiencia mediante la API](./tutorials/create-a-segment.md).

>[!NOTE] En el evento que se amplía un esquema, todas las cargas futuras deben actualizar los campos recién agregados en consecuencia. Para obtener más información sobre la personalización del Modelo de datos de experiencia (XDM), visite el tutorial [del Editor de](../xdm/tutorials/create-schema-ui.md)Esquemas.

## Evaluar segmentos

### Segmentación por flujo continuo

>[!NOTE] La segmentación por flujo continuo es una función beta y estará disponible bajo petición.

La segmentación por flujo continuo es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario. Una vez creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes en el Perfil del cliente en tiempo real. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destinatarios siga siendo relevante.

Para obtener más información sobre la segmentación de flujo continuo, lea la documentación [de segmentación de](./ui/streaming-segmentation.md)flujo continuo.

### Segmentación por lotes

Como alternativa a un proceso de selección de datos en curso, la segmentación por lotes mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y almacena para que pueda exportarlo para su uso.

Para obtener información sobre cómo evaluar segmentos, consulte el tutorial [de evaluación de](./tutorials/evaluate-a-segment.md)segmentos.

## Acceso a los resultados de segmentación

Para obtener información sobre cómo acceder a un segmento exportado, consulte el tutorial [de evaluación de](./tutorials/evaluate-a-segment.md)segmentos.

## Metadatos del segmento

Los metadatos del segmento facilitan la indexación en el evento de que cualquiera de los segmentos se va a reutilizar o combinar.

La composición de los segmentos (a través de la API o del Generador de segmentos) requiere que defina un nombre de segmento y una política de combinación.

### Nombres de segmentos

Al crear un nuevo segmento, debe proporcionar un nombre de segmento. El nombre del segmento se utiliza para identificar un segmento particular entre la colección creada por el servicio de segmentación. Por lo tanto, los nombres de los segmentos deben ser descriptivos, concisos y únicos.

>[!NOTE] Al planificar un segmento, recuerde que se puede hacer referencia a los segmentos desde cualquier otro segmento y combinarlos con él. Al seleccionar un nombre, considere la posibilidad de que el segmento contenga partes reutilizables.

### Combinar directivas

Las políticas de combinación son reglas utilizadas por Perfil para determinar cómo se priorizarán los datos y cómo se combinarán en una vista unificada bajo ciertas condiciones.
Si no se define una directiva de combinación, se utiliza la directiva de combinación de plataforma predeterminada. Si prefiere utilizar una directiva de combinación específica de su organización, puede crear la suya propia y marcarla como la predeterminada de su organización.

>[!NOTE] La estimación de los tamaños de audiencia se basa en la directiva de combinación de perfiles predeterminada de la organización.

### Otros metadatos de segmentos

Además del nombre del segmento y la política de combinación, el Generador de segmentos le oferta un campo de metadatos de &quot;descripción del segmento&quot; adicional en el que puede resumir el propósito de la definición del segmento.

## Funciones de segmentación avanzada

Los segmentos se pueden configurar para generar continuamente una audiencia combinando la ingestión [de datos de](../ingestion/streaming-ingestion/overview.md) flujo continuo con cualquiera de las siguientes características avanzadas de segmentación:
- [Segmentación secuencial](#sequential)
- [Segmentación dinámica](#dynamic)
- [Segmentación multientidad](#multi-entity)

Estas funciones avanzadas se analizan con más detalle en las siguientes secciones.

## Segmentación secuencial {#sequential}

Un viaje de usuario estándar es secuencial.  Adobe Experience Platform le permite definir una serie ordenada de segmentos para reflejar este viaje y capturar así secuencias de eventos a medida que se producen. Puede organizar los eventos en el orden deseado mediante la línea de tiempo del evento visual en el Generador de segmentos.

Un ejemplo de un viaje del cliente que requeriría una segmentación secuencial sería la vista del producto > adición del producto > cierre de compra > Sin compra.

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

## Segmentación multientidad {#multi-entity}

Con la función de segmentación multientidad avanzada, puede crear segmentos utilizando varias clases XDM, agregando así extensiones a los esquemas de personas. Como resultado, el servicio de segmentación puede acceder a campos adicionales durante la definición del segmento como si fueran nativos del almacén de datos de perfil.

La segmentación multientidad proporciona la flexibilidad necesaria para identificar audiencias en base a los datos relevantes para sus necesidades comerciales. Este proceso se puede llevar a cabo de manera rápida y sencilla sin necesidad de conocimientos técnicos para consultar las bases de datos. Esto le permite agregar datos clave a los segmentos sin tener que realizar cambios costosos en los flujos de datos ni esperar a una combinación de datos back-end.

### Caso de uso: Promoción basada en precios

Para ilustrar el valor de esta función de segmentación avanzada, considere la posibilidad de que un arquitecto de datos colabore con un especialista en mercadotecnia.

En este ejemplo, el arquitecto de datos está uniendo datos de un individuo (compuesto por esquemas con XDM Individual Perfil y XDM ExperienceEvent como sus clases base) a otra clase mediante una clave. Una vez unidos, el arquitecto de datos o el especialista en mercadotecnia pueden utilizar estos nuevos campos durante la definición del segmento como si fueran nativos del esquema de clase base.

**El problema**

Tanto el arquitecto de datos como el especialista en mercadotecnia trabajan para el mismo minorista de ropa. El minorista tiene más de 1.000 tiendas en toda Norteamérica y periódicamente disminuye los precios de los productos durante todo su ciclo de vida. Como resultado, el especialista en mercadotecnia desea ejecutar una campaña especial para dar a los compradores que han comprado estos artículos la oportunidad de comprarlos a precio de descuento.

Los recursos del arquitecto de datos incluyen el acceso a los datos web de la exploración de clientes, así como datos de adición al carro de compras que contienen identificadores de SKU de producto. También tienen acceso a una clase separada de &quot;productos&quot;, donde se almacena información adicional del producto (incluido el precio del producto). Su guía es centrarse en los clientes que agregaron un producto al carro de compras en los últimos 14 días, pero que no compraron el artículo, cuyo precio ahora ha bajado.

**La solución**

>[!NOTE] En este ejemplo supondremos que el arquitecto de datos ya ha establecido una Área de nombres de ID.

Con la API, el arquitecto de datos relaciona la clave del esquema ExperienceEvent con la clase &quot;products&quot;. De este modo, el arquitecto de datos puede utilizar los campos adicionales de la clase &quot;products&quot; como si fueran nativos del esquema ExperienceEvent. A medida que el paso final de la configuración funciona, el arquitecto de datos debe incorporar los datos adecuados al Perfil del cliente en tiempo real. Esto se realiza habilitando el conjunto de datos &quot;products&quot; para su uso con Perfil. Una vez finalizado el trabajo de configuración, el arquitecto de datos o el especialista en mercadotecnia pueden generar el segmento de destinatario en el Generador de segmentos.

Consulte la descripción general [de la composición de](../xdm/schema/composition.md#union) esquema para obtener información sobre cómo definir relaciones entre clases XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Casos de uso

Para ilustrar el valor de esta función de segmentación avanzada, considere tres casos de uso estándar que ilustran los desafíos que estaban presentes en las aplicaciones de mercadotecnia antes de la mejora de la carga útil del segmento:
- Personalización de correo electrónico
- Resegmentación de correo electrónico
- Resegmentación de anuncios

**Personalización de correo electrónico**

Es posible que un especialista en mercadotecnia que crea una campaña de correo electrónico haya intentado crear un segmento para una audiencia de destinatario mediante el uso de compras recientes del almacén de clientes en los últimos tres meses. Lo ideal sería que este segmento requiriera tanto el nombre del artículo como el nombre del almacén donde se realizó la compra. Antes de la mejora, el desafío consistía en capturar el identificador del almacén del evento de compra y asignarlo al perfil de ese cliente.

**Resegmentación de correo electrónico**

A menudo es complejo crear y calificar segmentos para campañas de correo electrónico que tengan como objetivo el &quot;abandono del carro de compras&quot;. Antes de la mejora, era difícil saber qué productos incluir en un mensaje personalizado debido a la disponibilidad de los datos requeridos. Los datos sobre los que se abandonaron los productos están vinculados a eventos de experiencia que antes eran difíciles de monitorear y extraer datos.

**Resegmentación de anuncios**

Otro desafío tradicional para los especialistas en mercadotecnia ha sido la creación de publicidades para redirigirse a los clientes con artículos abandonados del carro de compras. Si bien las definiciones de los segmentos abordaban este problema, antes de la mejora no había un método formal para diferenciar entre los productos comprados y los productos abandonados. Ahora puede destinatario conjuntos de datos específicos durante la definición del segmento.

## Tipos de datos del servicio de segmentación

Todos los tipos de datos XDM son compatibles con el servicio de segmentación. Las reglas que constituyen una definición de segmento están contextualizadas por los siguientes tipos de datos.

### Datos de cadena

Las definiciones de segmentos utilizan datos de cadena para definir restricciones no numéricas para audiencias de segmentos, como &quot;nombre de país&quot; o &quot;nivel de programa de lealtad&quot;.

Los datos de cadena se incluyen en las definiciones de segmentos mediante sentencias lógicas, inclusivas/exclusivas y comparativas. Una vez que se agrega un atributo de cadena a la definición del segmento, puede utilizar afirmaciones relevantes para la cadena para evaluarlo con otros campos de cadena.

| Tipo de instrucción | Ejemplos |
| -------------- | -------- |
| Lógico | y, o bien, no |
| Incluido/exclusivo | incluir, debe existir, excluir, no debe existir |
| Comparación | es igual a, no es igual a, contiene, inicios con |


### Datos de fecha

Los datos de fecha le permiten asignar un contexto basado en la hora a las definiciones de segmentos, ya sea mediante el uso de fechas de inicio/finalización específicas o mediante declaraciones de fecha relevantes, como se muestra en la tabla siguiente. Una implementación podría estar creando una audiencia de clientes que han interactuado con su marca en cualquier momento *este año* y que también han estado activos *en los* últimos días.

| Campo de ejemplo | Declaraciones pertinentes a la fecha | Escala de tiempo |
| ------------- | ------------------------ | --------- |
| people.firstPurchase | hoy, ayer, este mes, este año | Relevante para el día en que se creó el segmento. |
| people.lastPurchase | en último lugar, durante, antes, después, en | Relevante en cualquier semana/mes. |

### Eventos de experiencias

Como esquema de Adobe Experience Platform, XDM ExperienceEvents registra las interacciones explícitas e implícitas de los clientes con aplicaciones integradas en la plataforma, incluida una instantánea del sistema en el momento en que se produjo la interacción. ExperienceEvents son registros de hechos. Por lo tanto, son una fuente de datos disponible durante la definición del segmento.

Como se muestra en la tabla siguiente, los datos de evento se representan utilizando palabras clave que ayudan a reducir el comportamiento de evento y a especificar atributos de evento.

| Palabra clave | Utilice  |
| ------- | --- |
| Incluir/excluir | Describe el comportamiento del evento mediante la inclusión u omisión de datos. |
| Cualquiera/todo | Ayuda a determinar el número de segmentos cualificados. |
| Botón de alternancia &quot;Aplicar regla de tiempo&quot; | Incorpora datos de fecha. |
| Es igual a, no es igual a, inicios con, no inicio con, termina con, no termina con, contiene, no contiene, existe, no existe | Incorpora datos de cadena. |

### Segmentos

Las definiciones de segmentos existentes también pueden utilizarse como componentes de una nueva definición de segmento, agregando sus reglas basadas en atributos y eventos al nuevo segmento.

### Audiencias

Las audiencias externas también se pueden usar como componentes de una nueva definición de segmento, agregando sus reglas de atributos al nuevo segmento.

Actualmente, solo se admite Adobe Audiencia Manager como audiencia. En el futuro se habilitarán fuentes adicionales.

### Otros tipos de datos

Además de los mencionados anteriormente, la lista de los tipos de datos admitidos también incluye:
- Cadena
- Identificador de recurso uniforme
- Enum
- Número
- Largo
- Número entero
- Corto
- Byte
- Booleano
- Fecha
- Fecha y hora
- Matriz
- Objeto
- Mapa
- Eventos

## Pasos siguientes

El servicio de segmentación proporciona un flujo de trabajo consolidado para crear segmentos a partir de datos de Perfil de clientes en tiempo real. En resumen:

- La segmentación es el proceso de definir un subconjunto de perfiles de su almacén de perfiles, lo que le permite caracterizar el comportamiento o los atributos de un grupo comercializable deseado. El servicio de segmentación hace posible este proceso.
- Al planificar un segmento, tenga en cuenta que se puede hacer referencia a un segmento desde cualquier otro segmento y combinarlo con él.
- Un segmento se puede crear a partir de reglas basadas en datos de perfil, datos de series temporales relacionados o ambos.
- Los segmentos se pueden evaluar según sea necesario o de forma continua. Cuando se evalúa según demanda, todos los datos de perfil se pasan a través de las definiciones de segmentos a la vez. Cuando se evalúa continuamente, los datos se transmiten a través de definiciones de segmentos a medida que entran en la plataforma.

Para obtener información sobre cómo definir segmentos en la interfaz de usuario, consulte la guía [Generador de](./ui/overview.md)segmentos. Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre la [creación de segmentos mediante la API](./tutorials/create-a-segment.md).