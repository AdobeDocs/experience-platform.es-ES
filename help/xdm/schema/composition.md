---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conceptos básicos de la composición de esquemas
topic: overview
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Conceptos básicos de la composición de esquemas

Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en la plataforma de Adobe Experience. Para obtener información general sobre XDM y cómo se utiliza dentro de la plataforma, consulte la descripción general [del sistema](../home.md)XDM.

## Explicación de los esquemas

Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. En un nivel superior, los esquemas proporcionan una definición abstracta de un objeto real (como una persona) y describen los datos que deben incluirse en cada instancia de dicho objeto (como el nombre, el apellido, el cumpleaños, etc.).

Además de describir la estructura de los datos, los esquemas aplican restricciones y expectativas a los datos para que se puedan validar a medida que se desplaza de un sistema a otro. Estas definiciones estándar permiten interpretar los datos de manera coherente, independientemente del origen, y eliminan la necesidad de traducirlos entre las aplicaciones.

Experience Platform mantiene esta normalización semántica mediante el uso de esquemas. Los Esquemas son la forma estándar de describir los datos en la plataforma de experiencia, lo que permite reutilizar todos los datos que se ajustan a los esquemas sin conflictos en una organización e incluso compartir entre varias organizaciones.

### Tablas relacionales frente a objetos incrustados

Cuando se trabaja con bases de datos relacionales, las prácticas recomendadas implican normalizar datos o tomar una entidad y dividirla en partes discretas que luego se muestran en varias tablas. Para poder leer los datos en su conjunto o actualizar la entidad, las operaciones de lectura y escritura deben realizarse en muchas tablas individuales utilizando JOIN.

Mediante el uso de objetos incrustados, los esquemas XDM pueden representar directamente datos complejos y almacenarlos en documentos independientes con estructura jerárquica. Uno de los principales beneficios de esta estructura es que le permite consulta de los datos sin tener que reconstruir la entidad mediante costosas combinaciones a múltiples tablas desnormalizadas.

### Esquemas y grandes datos

Los sistemas digitales modernos generan grandes cantidades de señales conductuales (datos de transacciones, registros web, Internet de cosas, visualización, etc.). Estos datos de gran tamaño oferta oportunidades extraordinarias para optimizar experiencias, pero su uso es difícil debido a la escala y variedad de los datos. Para obtener valor de los datos, su estructura, formato y definiciones deben estar estandarizados para que se puedan procesar de manera coherente y eficiente.

Los Esquemas solucionan este problema permitiendo que los datos se integren desde múltiples fuentes, que se estandaricen a través de estructuras y definiciones comunes y que se compartan entre las soluciones. Esto permite que los procesos y servicios subsiguientes respondan a cualquier tipo de pregunta que se formule sobre los datos, alejándose del enfoque tradicional de la modelización de datos, en el que todas las preguntas que se formularán sobre los datos se conocen con antelación y los datos se modelan para ajustarse a esas expectativas.

### flujos de trabajo basados en Esquemas en la plataforma de experiencia

La estandarización es un concepto clave de la plataforma de experiencias. XDM, dirigido por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas estándar para la administración de la experiencia del cliente.

La infraestructura en la que se crea la plataforma de experiencias, conocida como sistema XDM, facilita los flujos de trabajo basados en esquemas e incluye el Registro de Esquemas, el Editor de Esquemas, los metadatos de esquema y los patrones de consumo de servicios. See the [XDM System overview](../home.md) for more information.

## Planificación del esquema

El primer paso para crear un esquema es determinar el concepto, o objeto real, que se intenta capturar dentro del esquema. Una vez que identifique el concepto que está tratando de describir, puede empezar a planificar su esquema pensando en cosas como el tipo de datos, los campos de identidad potenciales y cómo el esquema puede evolucionar en el futuro.

### Comportamientos de datos en la plataforma de experiencias

Los datos destinados a utilizarse en la plataforma de experiencia se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema lo define la **clase** del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM se describen en detalle más adelante en este documento.

Tanto los esquemas de registro como de serie temporal contienen un mapa de identidades (`xdm:identityMap`). Este campo contiene la representación de identidad de un sujeto, extraída de campos marcados como &quot;Identidad&quot; como se describe en la siguiente sección.

### Identidad

Los Esquemas se utilizan para la ingesta de datos en la plataforma de experiencia. Estos datos se pueden utilizar en varios servicios para crear una sola vista unificada de una entidad individual. Por lo tanto, es importante que, cuando se piensa en los esquemas, se reflexione sobre la &quot;identidad&quot; y los campos que pueden utilizarse para identificar un tema, independientemente de la procedencia de los datos.

Para ayudar con este proceso, los campos clave pueden marcarse como &quot;Identidad&quot;. Tras la ingestión de datos, los datos de esos campos se insertarán en el &quot;Gráfico de identidad&quot; de esa persona. A continuación, el Perfil [del cliente en tiempo](../../profile/home.md) real y otros servicios de la plataforma de experiencias pueden acceder a los datos del gráfico para proporcionar una vista conjunta de cada cliente individual.

Los campos que se marcan comúnmente como &quot;Identidad&quot; incluyen: dirección de correo electrónico, número de teléfono, ID de [Experience Cloud (ECID)](https://marketing.adobe.com/resources/help/en_US/mcvid/), ID de CRM u otros campos de ID únicos. También debe tener en cuenta cualquier identificador único específico de su organización, ya que también pueden ser buenos campos de &quot;Identidad&quot;.

Es importante pensar en las identidades de los clientes durante la fase de planificación de esquemas para ayudar a garantizar que los datos se reúnan a fin de generar el perfil más sólido posible. Consulte la descripción general [del servicio de](../../identity-service/home.md) identidad para obtener más información sobre cómo la información de identidad puede ayudarle a ofrecer experiencias digitales a sus clientes.

### Principios de evolución del Esquema {#evolution}

A medida que la naturaleza de las experiencias digitales sigue evolucionando, también deben evolucionar los esquemas utilizados para representarlas. Por lo tanto, un esquema bien diseñado puede adaptarse y evolucionar según sea necesario, sin causar cambios destructivos en versiones anteriores del esquema.

Dado que el mantenimiento de la compatibilidad con versiones anteriores es crucial para la evolución del esquema, la plataforma de experiencias aplica un principio de versiones puramente aditivo para garantizar que cualquier revisión del esquema solo dé lugar a actualizaciones y cambios no destructivos. En otras palabras, no se admiten los cambios de **salto.**

| Cambios admitidos | Romper cambios (no compatible) |
|------------------------------------|---------------------------------|
| <ul><li>Añadir nuevos campos a un esquema existente</li><li>Hacer opcional un campo obligatorio</li></ul> | <ul><li>Eliminación de campos definidos previamente</li><li>Introducción de nuevos campos obligatorios</li><li>Cambio de nombre o redefinición de campos existentes</li><li>Eliminación o restricción de valores de campo admitidos anteriormente</li><li>Desplazamiento de atributos a una ubicación diferente en el árbol</li></ul> |

>[!NOTE] Si todavía no se ha utilizado un esquema para ingerir datos en la plataforma de experiencias, puede introducir un cambio de ruptura en ese esquema. Sin embargo, una vez que el esquema se ha utilizado en la Plataforma, debe cumplir la política de control de versiones acumulativas.

### Esquemas e ingestión de datos

Para poder ingerir datos en la plataforma de experiencia, primero debe crearse un conjunto de datos. Los conjuntos de datos son los componentes básicos de la transformación y el seguimiento de datos para el servicio [de](../../catalog/home.md)catálogos y generalmente representan tablas o archivos que contienen datos ingestados. Todos los conjuntos de datos se basan en esquemas XDM existentes, que establecen restricciones para lo que deben contener los datos ingestados y cómo deben estructurarse. Para obtener más información, consulte la información general sobre la introducción [de datos de la plataforma de](../../ingestion/home.md) Adobe Experience Platform.

## Componentes de un esquema

La plataforma de experiencias utiliza un enfoque de composición en el que los componentes básicos estándar se combinan para crear esquemas. Este enfoque fomenta la reutilización de los componentes existentes e impulsa la estandarización en todo el sector para admitir esquemas y componentes de proveedores en la plataforma.

Los Esquemas se componen con la fórmula siguiente:

**Clase + Mixin&amp;ast; = Esquema XDM**

&amp;ast;Un esquema está compuesto por una clase y _cero o más_ mezclas. Esto significa que puede componer un esquema de conjunto de datos sin usar mezclas.

### Clase

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Además de esto, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían incluir y proporcionar una manera de combinar varios conjuntos de datos compatibles.

Una clase también determina qué mezclas serán elegibles para su uso en el esquema. Esto se analiza más detalladamente en la sección de [mezclas](#mixin) que sigue.

Existen clases estándar que se proporcionan con cada integración de la plataforma de experiencia, conocidas como clases &quot;del sector&quot;. Las clases industriales son normas generalmente aceptadas que se aplican a un amplio conjunto de casos de uso. Algunos ejemplos de clases del sector incluyen las clases XDM Individual Perfil y XDM ExperienceEvent proporcionadas por Adobe.

La plataforma de experiencia también permite clases de &quot;proveedores&quot;, que son clases definidas por los socios de la plataforma de experiencia y que están disponibles para todos los clientes que utilizan ese servicio o aplicación de proveedor dentro de la plataforma.

También existen clases que se utilizan para describir casos de uso más específicos para organizaciones individuales dentro de la plataforma, las cuales se denominan clases de &quot;cliente&quot;. Las clases de cliente son definidas por una organización cuando no hay clases del sector o del proveedor disponibles para describir un caso de uso único.

Por ejemplo, un esquema que representa a los miembros de un programa de Lealtad describe los datos de registro de un individuo y, por lo tanto, pueden basarse en la clase de Perfil individual XDM, una clase industrial estándar definida por Adobe.

### Mixin {#mixin}

Una mezcla es un componente reutilizable que define uno o varios campos que implementan determinadas funciones, como detalles personales, preferencias del hotel o dirección. Las mezclas están pensadas para incluirse como parte de un esquema que implementa una clase compatible.

Las mezclas definen con qué clase o clases son compatibles en función del comportamiento de los datos que representan (registro o serie temporal). Esto significa que no todas las mezclas están disponibles para su uso con todas las clases.

Las mezclas tienen el mismo ámbito y definición que las clases: hay mezclas del sector, mezclas de proveedores y mezclas de clientes que las organizaciones individuales definen mediante Plataforma. La plataforma de experiencia incluye muchas mezclas estándar del sector, al tiempo que permite a los proveedores definir mezclas para sus usuarios, y a los usuarios individuales definir mezclas para sus propios conceptos específicos.

Por ejemplo, para capturar detalles como &quot;Nombre&quot; y &quot;Dirección de inicio&quot; para el esquema &quot;Miembros de lealtad&quot;, podría utilizar mezclas estándar que definan esos conceptos comunes. Sin embargo, los conceptos específicos de casos de uso menos comunes (como &quot;Nivel de Programa de lealtad&quot;) no suelen tener una mezcla predefinida. En este caso, debe definir su propia mezcla para capturar esta información.

Recuerde que los esquemas están compuestos de mezclas &quot;cero o más&quot;, lo que significa que puede componer un esquema válido sin usar ninguna mezcla.

### Tipo de datos {#data-type}

Los tipos de datos se utilizan como tipos de campos de referencia en clases o esquemas del mismo modo que los campos literales básicos. La diferencia clave es que los tipos de datos pueden definir varios subcampos. Al igual que una mezcla, un tipo de datos permite el uso coherente de una estructura de varios campos, pero tiene más flexibilidad que una mezcla, ya que se puede incluir un tipo de datos en cualquier parte de un esquema agregándolo como el &quot;tipo de datos&quot; de un campo.

La plataforma de experiencias proporciona varios tipos de datos comunes como parte del Registro de Esquemas para admitir el uso de patrones estándar para describir estructuras de datos comunes. Esto se explica con más detalle en los tutoriales del Registro de Esquemas, donde se aclarará a medida que avance por los pasos para definir los tipos de datos.

### Campo

Un campo es el componente básico más básico de un esquema. Los campos proporcionan restricciones con respecto al tipo de datos que pueden contener al definir un tipo de datos específico. Estos tipos de datos básicos definen un solo campo, mientras que los tipos [de](#data-type) datos mencionados anteriormente le permiten definir varios subcampos y reutilizar la misma estructura de varios campos en varios esquemas. Por lo tanto, además de definir el &quot;tipo de datos&quot; de un campo como uno de los tipos de datos definidos en el Registro, la plataforma de experiencias admite tipos escalares básicos como:

* Cadena
* Número entero
* Número
* Booleano
* Matriz
* Objeto

Los rangos válidos de estos tipos escalares se pueden restringir aún más a ciertos patrones, formatos, mínimos/máximos o valores predefinidos. Con estas restricciones, se puede representar una amplia gama de tipos de campo más específicos, incluidos:

* Enum
* Largo
* Corto
* Byte
* Fecha
* Fecha y hora
* Mapa

>[!NOTE] El tipo de campo &quot;map&quot; permite datos de pares de clave-valor, incluidos varios valores para una sola clave. Los mapas solo se pueden definir en el nivel del sistema, lo que significa que puede encontrar un mapa en un esquema definido por el sector o el proveedor, pero no está disponible para utilizarse en los campos definidos. La guía [para desarrolladores de la API de registro de](../api/getting-started.md) Esquema contiene más información sobre la definición de tipos de campo.

Algunas operaciones de datos utilizadas por los servicios y las aplicaciones posteriores imponen restricciones a tipos de campo específicos. Los servicios afectados incluyen, entre otros:

* [Perfil del cliente en tiempo real](../../profile/home.md)
* [Servicio de identidad](../../identity-service/home.md)
* [Segmentación](../../segmentation/home.md)
* [Servicio de Consulta](../../query-service/home.md)
* [Área de trabajo de ciencia de datos](../../data-science-workspace/home.md)

Antes de crear un esquema para su uso en los servicios intermedios, revise la documentación apropiada para esos servicios a fin de comprender mejor los requisitos y las limitaciones sobre el terreno para las operaciones de datos a las que está destinado el esquema.

### Campos XDM

Además de los campos básicos y la capacidad de definir sus propios tipos de datos, XDM proporciona un conjunto estándar de campos y tipos de datos que los servicios de la plataforma de experiencia entienden implícitamente y proporcionan buena coherencia cuando se utiliza en los componentes de la plataforma.

Estos campos, como &quot;Nombre&quot; y &quot;Dirección de correo electrónico&quot;, contienen connotaciones agregadas que van más allá de los tipos de campos escalares básicos, lo que indica a Platform que cualquier campo que comparta el mismo tipo de datos XDM se comportará de la misma manera. Se puede confiar en este comportamiento para que sea coherente independientemente de la procedencia de los datos o del servicio de plataforma en el que se utilicen los datos.

Consulte el diccionario [de campos](field-dictionary.md) XDM para obtener una lista completa de los campos XDM disponibles. Se recomienda utilizar campos XDM y tipos de datos siempre que sea posible para admitir la coherencia y la estandarización en toda la plataforma de experiencia.

## Ejemplo de composición

Los Esquemas representan el formato y la estructura de los datos que se van a ingerir en la plataforma y se crean utilizando un modelo de composición. Como se mencionó anteriormente, estos esquemas están compuestos de una clase y cero o más mezclas compatibles con esa clase.

Por ejemplo, un esquema que describe las compras realizadas en una tienda minorista puede denominarse &quot;Transacciones de almacenamiento&quot;. El esquema implementa la clase XDM ExperienceEvent combinada con la combinación de comercio estándar y una combinación de información del producto definida por el usuario.

Otro esquema que rastrea el tráfico del sitio web puede llamarse &quot;Visitas web&quot;. También implementa la clase XDM ExperienceEvent, pero esta vez combina la mezcla web estándar.

El diagrama siguiente muestra estos esquemas y los campos que aporta cada mezcla. También contiene dos esquemas basados en la clase de Perfil individual XDM, incluido el esquema &quot;Miembros de la lealtad&quot; mencionado anteriormente en esta guía.

![](../images/schema-composition/composition.png)

### Unión {#union}

Aunque la plataforma de experiencia le permite componer esquemas para casos de uso específicos, también le permite ver una &quot;unión&quot; de esquemas para un tipo de clase específico. El diagrama anterior muestra dos esquemas basados en la clase XDM ExperienceEvent y dos esquemas basados en la clase de Perfil individual XDM. La unión, que se muestra a continuación, agrega los campos de todos los esquemas que comparten la misma clase (XDM ExperienceEvent y XDM Individual Perfil, respectivamente).

![](../images/schema-composition/union.png)

Al habilitar un esquema para su uso con el Perfil del cliente en tiempo real, se incluirá en la unión para ese tipo de clase. Perfil ofrece perfiles robustos y centralizados de atributos del cliente, así como una cuenta con marca de hora de cada evento que el cliente ha tenido en cualquier sistema integrado con Platform. Perfil utiliza la vista de unión para representar estos datos y proporcionar una vista holística de cada cliente individual.

Para obtener más información sobre cómo trabajar con Perfil, consulte la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Asignación de archivos de datos a esquemas XDM

Todos los archivos de datos que se ingieren en la plataforma de experiencia deben cumplir la estructura de un esquema XDM. Para obtener más información sobre cómo dar formato a los archivos de datos para cumplir con las jerarquías XDM (incluidos los archivos de ejemplo), consulte el documento sobre las transformaciones [ETL de](../../etl/transformations.md)ejemplo. Para obtener información general sobre la ingesta de archivos de datos en la plataforma de experiencias, consulte la descripción general [de la ingestión de](../../ingestion/batch-ingestion/overview.md)lotes.

## Pasos siguientes

Ahora que comprende los aspectos básicos de la composición de esquemas, está listo para empezar a crear esquemas mediante el Registro de Esquemas.

El Registro de Esquema se utiliza para acceder a la biblioteca de Esquemas en Adobe Experience Platform y proporciona una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles. La biblioteca de Esquemas contiene los recursos del sector definidos por Adobe, los recursos del proveedor definidos por los socios de la plataforma de experiencia y las clases, mezclas, tipos de datos y esquemas compuestos por miembros de la organización.

Para empezar a componer esquemas mediante la interfaz de usuario, siga el tutorial [del Editor de](../tutorials/create-schema-ui.md) Esquemas para crear el esquema &quot;Miembros de lealtad&quot; mencionado a lo largo de este documento.

Para empezar a utilizar la API del Registro de Esquema, lea la guía [para desarrolladores de la API del Registro de](../api/getting-started.md)Esquema. Después de leer la guía para desarrolladores, siga los pasos descritos en el tutorial sobre la [creación de un esquema con la API](../tutorials/create-schema-api.md)del Registro de Esquemas.
