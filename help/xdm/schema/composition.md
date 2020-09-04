---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;primary identity;primary idenity;XDM individual profile;XDM fields;enum datatype;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design;class;Class;classes;Classes;datatype;Datatype;data type;Data type;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Conceptos básicos de la composición de esquemas
topic: overview
description: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4251dc292ead3ce4dc8aef68ff04bb774047160d
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 0%

---


# Conceptos básicos de la composición de esquemas

Este documento proporciona una introducción a [!DNL Experience Data Model] (XDM) esquemas y los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en Adobe Experience Platform. Para obtener información general sobre XDM y cómo se utiliza en [!DNL Platform], consulte la información general [del sistema](../home.md)XDM.

## Explicación de los esquemas

Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. En un nivel superior, los esquemas proporcionan una definición abstracta de un objeto real (como una persona) y describen los datos que deben incluirse en cada instancia de dicho objeto (como el nombre, el apellido, el cumpleaños, etc.).

Además de describir la estructura de los datos, los esquemas aplican restricciones y expectativas a los datos para que se puedan validar a medida que se desplaza de un sistema a otro. Estas definiciones estándar permiten interpretar los datos de manera coherente, independientemente del origen, y eliminan la necesidad de traducirlos entre las aplicaciones.

[!DNL Experience Platform] mantiene esta normalización semántica mediante el uso de esquemas. Los esquemas son la manera estándar de describir los datos en [!DNL Experience Platform], permitiendo que todos los datos que se ajustan a los esquemas se puedan reutilizar sin conflictos en una organización e incluso compartir entre varias organizaciones.

### Tablas relacionales frente a objetos incrustados

Cuando se trabaja con bases de datos relacionales, las prácticas recomendadas implican normalizar datos o tomar una entidad y dividirla en partes discretas que luego se muestran en varias tablas. Para poder leer los datos en su conjunto o actualizar la entidad, las operaciones de lectura y escritura deben realizarse en muchas tablas individuales utilizando JOIN.

Mediante el uso de objetos incrustados, los esquemas XDM pueden representar directamente datos complejos y almacenarlos en documentos independientes con estructura jerárquica. Uno de los principales beneficios de esta estructura es que le permite consulta de los datos sin tener que reconstruir la entidad mediante costosas combinaciones a múltiples tablas desnormalizadas.

### Esquemas y grandes datos

Los sistemas digitales modernos generan grandes cantidades de señales conductuales (datos de transacciones, registros web, Internet de cosas, visualización, etc.). Estos datos de gran tamaño oferta oportunidades extraordinarias para optimizar experiencias, pero su uso es difícil debido a la escala y variedad de los datos. Para obtener valor de los datos, su estructura, formato y definiciones deben estar estandarizados para que se puedan procesar de manera coherente y eficiente.

Los esquemas solucionan este problema permitiendo que los datos se integren desde múltiples fuentes, que se estandaricen a través de estructuras y definiciones comunes y que se compartan entre las soluciones. Esto permite que los procesos y servicios subsiguientes respondan a cualquier tipo de pregunta que se formule sobre los datos, alejándose del enfoque tradicional de la modelización de datos, en el que todas las preguntas que se formularán sobre los datos se conocen con antelación y los datos se modelan para ajustarse a esas expectativas.

### Flujos de trabajo basados en esquemas en [!DNL Experience Platform]

La estandarización es un concepto clave detrás [!DNL Experience Platform]. XDM, impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas estándar para la administración de la experiencia del cliente.

La infraestructura en la que [!DNL Experience Platform] se construye, conocida como [!DNL XDM System], facilita los flujos de trabajo basados en esquemas e incluye los patrones de consumo [!DNL Schema Registry], [!DNL Schema Editor], metadatos de esquema y servicios. See the [XDM System overview](../home.md) for more information.

## Planificación del esquema

El primer paso para crear un esquema es determinar el concepto, o objeto real, que se intenta capturar dentro del esquema. Una vez que identifique el concepto que está tratando de describir, puede empezar a planificar su esquema pensando en cosas como el tipo de datos, los campos de identidad potenciales y cómo el esquema puede evolucionar en el futuro.

### Comportamientos de datos en [!DNL Experience Platform]

Los datos destinados a utilizarse en [!DNL Experience Platform] se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema lo define la **clase** del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM se describen en detalle más adelante en este documento.

Tanto los esquemas de registro como de serie temporal contienen un mapa de identidades (`xdm:identityMap`). Este campo contiene la representación de identidad de un sujeto, extraída de campos marcados como &quot;Identidad&quot; como se describe en la siguiente sección.

### [!UICONTROL Identidad]

Los esquemas se utilizan para la ingesta de datos en [!DNL Experience Platform]. Estos datos se pueden utilizar en varios servicios para crear una sola vista unificada de una entidad individual. Por lo tanto, es importante que, cuando se piensa en los esquemas, se reflexione sobre las identidades de los clientes y los campos que se pueden utilizar para identificar un asunto, independientemente de la procedencia de los datos.

Para ayudarle con este proceso, los campos clave dentro de sus esquemas pueden marcarse como identidades. Tras la ingestión de datos, los datos de esos campos se insertan en el &quot;[!UICONTROL Gráfico]de identidad&quot; de esa persona. A continuación, se puede acceder a los datos del gráfico mediante [[!DNL Real-time Customer Perfil]](../../profile/home.md) y otros [!DNL Experience Platform] servicios para proporcionar una vista unida de cada cliente individual.

Los campos que se marcan comúnmente como &quot;[!UICONTROL Identidad]&quot; incluyen: dirección de correo electrónico, número de teléfono, [[!DNL ID de Experience Cloud (ECID)]](https://docs.adobe.com/content/help/es-ES/id-service/using/home.html), ID de CRM u otros campos de ID únicos. También debe tener en cuenta cualquier identificador único específico de su organización, ya que también pueden ser buenos campos de &quot;[!UICONTROL identidad]&quot;.

Es importante pensar en las identidades de los clientes durante la fase de planificación de esquemas para ayudar a garantizar que los datos se reúnan a fin de generar el perfil más sólido posible. Consulte la descripción general de [Adobe Experience Platform Identity Service](../../identity-service/home.md) para obtener más información sobre cómo la información de identidad puede ayudarle a ofrecer experiencias digitales a sus clientes.

#### xdm:identityMap {#identityMap}

`xdm:identityMap` es un campo de tipo mapa que describe los distintos valores de identidad de un individuo, junto con sus Áreas de nombres asociadas. Este campo se puede utilizar para proporcionar información de identidad para los esquemas, en lugar de definir valores de identidad dentro de la estructura del propio esquema.

Un ejemplo de mapa de identidad simple sería el siguiente:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Como se muestra en el ejemplo anterior, cada clave del `identityMap` objeto representa una Área de nombres de identidad. El valor de cada clave es una matriz de objetos que representa los valores de identidad (`id`) de la Área de nombres correspondiente. Consulte la [!DNL Identity Service] documentación para obtener una [lista de Áreas de nombres](../../identity-service/troubleshooting-guide.md#standard-namespaces) de identidad estándar reconocidas por las aplicaciones de Adobe.

>[!NOTE]
>
>También se puede proporcionar un valor booleano para determinar si el valor es o no una identidad principal (`primary`) para cada valor de identidad. Las identidades primarias solo deben establecerse para esquemas destinados a utilizarse en [!DNL Real-time Customer Profile]. Consulte la sección sobre esquemas [de](#union) unión para obtener más información.

### Principios de evolución del esquema {#evolution}

A medida que la naturaleza de las experiencias digitales sigue evolucionando, también deben evolucionar los esquemas utilizados para representarlas. Por lo tanto, un esquema bien diseñado puede adaptarse y evolucionar según sea necesario, sin causar cambios destructivos en versiones anteriores del esquema.

Dado que el mantenimiento de la compatibilidad con versiones anteriores es crucial para la evolución del esquema, [!DNL Experience Platform] aplica un principio de control de versiones puramente aditivo para garantizar que cualquier revisión del esquema sólo dé lugar a actualizaciones y cambios no destructivos. En otras palabras, no se admiten los cambios de **salto.**

| Cambios admitidos | Romper cambios (no compatible) |
|------------------------------------|---------------------------------|
| <ul><li>Añadir nuevos campos a un esquema existente</li><li>Hacer opcional un campo obligatorio</li></ul> | <ul><li>Eliminación de campos definidos previamente</li><li>Introducción de nuevos campos obligatorios</li><li>Cambio de nombre o redefinición de campos existentes</li><li>Eliminación o restricción de valores de campo admitidos anteriormente</li><li>Desplazamiento de atributos a una ubicación diferente en el árbol</li></ul> |

>[!NOTE]
>
>Si todavía no se ha utilizado un esquema para ingerir datos en [!DNL Experience Platform], puede introducir un cambio de ruptura en ese esquema. Sin embargo, una vez que el esquema se haya utilizado en [!DNL Platform]el, debe adherirse a la política de control de versiones de aditivos.

### Esquemas e ingestión de datos

Para poder ingerir datos en [!DNL Experience Platform], primero se debe crear un conjunto de datos. Los conjuntos de datos son los componentes básicos de la transformación y el seguimiento de datos para [[!DNL Catalog Service]](../../catalog/home.md)y generalmente representan tablas o archivos que contienen datos ingestados. Todos los conjuntos de datos se basan en esquemas XDM existentes, que establecen restricciones para lo que deben contener los datos ingestados y cómo deben estructurarse. Consulte la información general sobre la ingestión [de datos de](../../ingestion/home.md) Adobe Experience Platform para obtener más información.

## Componentes de un esquema

[!DNL Experience Platform] utiliza un enfoque de composición en el que los componentes básicos estándar se combinan para crear esquemas. Este enfoque fomenta la reutilización de los componentes existentes e impulsa la estandarización en toda la industria para admitir esquemas y componentes de proveedores en [!DNL Platform].

Los esquemas se componen con la fórmula siguiente:

**Clase + Mixin&amp;ast; = Esquema XDM**

&amp;ast;Un esquema está compuesto por una clase y _cero o más_ mezclas. Esto significa que puede componer un esquema de conjunto de datos sin usar mezclas.

### Clase

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Además de esto, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían incluir y proporcionar una manera de combinar varios conjuntos de datos compatibles.

Una clase también determina qué mezclas serán elegibles para su uso en el esquema. Esto se analiza más detalladamente en la sección de [mezclas](#mixin) que sigue.

Existen clases estándar que se proporcionan con cada integración de [!DNL Experience Platform], conocidas como clases &quot;Industria&quot;. Las clases industriales son normas generalmente aceptadas que se aplican a un amplio conjunto de casos de uso. Algunos ejemplos de clases del sector incluyen las [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent] clases proporcionadas por Adobe.

[!DNL Experience Platform] también permite clases de &quot;proveedor&quot;, que son clases definidas por [!DNL Experience Platform] socios y que se ponen a disposición de todos los clientes que utilizan ese servicio o aplicación de proveedor dentro de [!DNL Platform].

También hay clases que se utilizan para describir casos de uso más específicos para organizaciones individuales dentro de [!DNL Platform], llamadas clases de &quot;cliente&quot;. Las clases de cliente son definidas por una organización cuando no hay clases del sector o del proveedor disponibles para describir un caso de uso único.

Por ejemplo, un esquema que representa a los miembros de un programa de Lealtad describe los datos de registro de un individuo y, por lo tanto, se pueden basar en la [!DNL XDM Individual Profile] clase, una clase de sector estándar definida por el Adobe.

### Mixin {#mixin}

Una mezcla es un componente reutilizable que define uno o varios campos que implementan determinadas funciones, como detalles personales, preferencias del hotel o dirección. Las mezclas están pensadas para incluirse como parte de un esquema que implementa una clase compatible.

Las mezclas definen con qué clase o clases son compatibles en función del comportamiento de los datos que representan (registro o serie temporal). Esto significa que no todas las mezclas están disponibles para su uso con todas las clases.

Las mezclas tienen el mismo ámbito y definición que las clases: hay mezclas del sector, mezclas de proveedores y mezclas de clientes que las organizaciones individuales definen mediante [!DNL Platform]. [!DNL Experience Platform] incluye muchas mezclas estándar del sector, al tiempo que permite a los proveedores definir mezclas para sus usuarios, y a los usuarios individuales definir mezclas para sus propios conceptos específicos.

Por ejemplo, para capturar detalles como &quot;[!UICONTROL Nombre]&quot; y &quot;Direcciónprincipal&quot; para el esquema &quot;Miembros[!UICONTROL de la]lealtad&quot;, podría utilizar mezclas estándar que definen esos conceptos comunes. Sin embargo, los conceptos específicos de casos de uso menos comunes (como &quot;Nivel[!UICONTROL de Programa de]lealtad&quot;) no suelen tener una mezcla predefinida. En este caso, debe definir su propia mezcla para capturar esta información.

Recuerde que los esquemas están compuestos de mezclas &quot;cero o más&quot;, lo que significa que puede componer un esquema válido sin usar ninguna mezcla.

### Data type {#data-type}

Los tipos de datos se utilizan como tipos de campos de referencia en clases o esquemas del mismo modo que los campos literales básicos. La diferencia clave es que los tipos de datos pueden definir varios subcampos. Al igual que una mezcla, un tipo de datos permite el uso coherente de una estructura de varios campos, pero tiene más flexibilidad que una mezcla, ya que se puede incluir un tipo de datos en cualquier parte de un esquema agregándolo como el &quot;tipo de datos&quot; de un campo.

[!DNL Experience Platform] proporciona una serie de tipos de datos comunes como parte del [!DNL Schema Registry] informe para admitir el uso de patrones estándar para describir estructuras de datos comunes. Esto se explica con más detalle en los [!DNL Schema Registry] tutoriales, donde se aclarará a medida que avance por los pasos para definir los tipos de datos.

### Campo

Un campo es el componente básico más básico de un esquema. Los campos proporcionan restricciones con respecto al tipo de datos que pueden contener al definir un tipo de datos específico. Estos tipos de datos básicos definen un solo campo, mientras que los tipos [de](#data-type) datos mencionados anteriormente le permiten definir varios subcampos y reutilizar la misma estructura de varios campos en varios esquemas. Por lo tanto, además de definir el &quot;tipo de datos&quot; de un campo como uno de los tipos de datos definidos en el Registro, [!DNL Experience Platform] admite tipos escalares básicos como:

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

>[!NOTE]
>
>El tipo de campo &quot;map&quot; permite datos de pares de clave-valor, incluidos varios valores para una sola clave. Los mapas solo se pueden definir en el nivel del sistema, lo que significa que puede encontrar un mapa en un esquema definido por el sector o el proveedor, pero no está disponible para utilizarse en los campos definidos. La guía [para desarrolladores de la API de registro de](../api/getting-started.md) Esquema contiene más información sobre la definición de tipos de campo.

Algunas operaciones de datos utilizadas por los servicios y las aplicaciones posteriores imponen restricciones a tipos de campo específicos. Los servicios afectados incluyen, entre otros:

* [[!DNL Perfil del cliente en tiempo real]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!Segmentación DNL]](../../segmentation/home.md)
* [[!Servicio de Consulta DNL]](../../query-service/home.md)
* [[!Espacio de trabajo de ciencias de datos DNL]](../../data-science-workspace/home.md)

Antes de crear un esquema para su uso en los servicios intermedios, revise la documentación apropiada para esos servicios a fin de comprender mejor los requisitos y las limitaciones sobre el terreno para las operaciones de datos a las que está destinado el esquema.

### Campos XDM

Además de los campos básicos y la capacidad de definir sus propios tipos de datos, XDM proporciona un conjunto estándar de campos y tipos de datos que los servicios entienden implícitamente y proporcionan una buena coherencia cuando se utilizan en [!DNL Experience Platform] [!DNL Platform] los componentes.

Estos campos, como &quot;Nombre&quot; y &quot;Dirección de correo electrónico&quot;, contienen connotaciones agregadas más allá de los tipos de campo escalar básicos, lo [!DNL Platform] que indica que cualquier campo que comparta el mismo tipo de datos XDM se comportará de la misma manera. Se puede confiar en este comportamiento para que sea coherente independientemente de dónde procedan los datos o en qué servicio se utilicen los datos [!DNL Platform] .

Consulte el diccionario [de campos](field-dictionary.md) XDM para obtener una lista completa de los campos XDM disponibles. Se recomienda utilizar campos XDM y tipos de datos siempre que sea posible para mantener la coherencia y la estandarización en todo [!DNL Experience Platform].

## Ejemplo de composición

Los esquemas representan el formato y la estructura de los datos que se van a ingerir [!DNL Platform]y se crean utilizando un modelo de composición. Como se mencionó anteriormente, estos esquemas están compuestos de una clase y cero o más mezclas compatibles con esa clase.

Por ejemplo, un esquema que describa las compras realizadas en una tienda minorista podría denominarse &quot;Transacciones[!UICONTROL de]almacenamiento&quot;. El esquema implementa la [!DNL XDM ExperienceEvent] clase combinada con la mezcla de [!UICONTROL comercio] estándar y una mezcla de información [!UICONTROL del] producto definida por el usuario.

Otro esquema que rastrea el tráfico del sitio web puede llamarse &quot;Visitas[!UICONTROL web]&quot;. También implementa la [!DNL XDM ExperienceEvent] clase, pero esta vez combina la mezcla estándar de [!UICONTROL Web] .

El diagrama siguiente muestra estos esquemas y los campos que aporta cada mezcla. También contiene dos esquemas basados en la [!DNL XDM Individual Profile] clase, incluido el esquema &quot;Miembros[!UICONTROL de la]Lealtad&quot; mencionado anteriormente en esta guía.

![](../images/schema-composition/composition.png)

### Union {#union}

Aunque [!DNL Experience Platform] le permite componer esquemas para casos de uso específicos, también le permite ver una &quot;unión&quot; de esquemas para un tipo de clase específico. El diagrama anterior muestra dos esquemas basados en la clase ExperienceEvent de XDM y dos esquemas basados en [!DNL XDM Individual Profile] la clase. La unión, que se muestra a continuación, agrega los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] y [!DNL XDM Individual Profile], respectivamente).

![](../images/schema-composition/union.png)

Al habilitar un esquema para utilizarlo con [!DNL Real-time Customer Profile], se incluirá en la unión para ese tipo de clase. [!DNL Profile] ofrece perfiles robustos y centralizados de atributos del cliente, así como una cuenta con marca de hora de cada evento que el cliente ha tenido en cualquier sistema integrado con [!DNL Platform]. [!DNL Profile] utiliza la vista de unión para representar estos datos y proporcionar una vista holística de cada cliente individual.

Para obtener más información sobre cómo trabajar con [!DNL Profile], consulte la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Asignación de archivos de datos a esquemas XDM

Todos los archivos de datos que se ingieran [!DNL Experience Platform] deben cumplir la estructura de un esquema XDM. Para obtener más información sobre cómo dar formato a los archivos de datos para cumplir con las jerarquías XDM (incluidos los archivos de ejemplo), consulte el documento sobre las transformaciones [ETL de](../../etl/transformations.md)ejemplo. Para obtener información general sobre la ingesta de archivos de datos en [!DNL Experience Platform], consulte la información general [sobre la ingestión de](../../ingestion/batch-ingestion/overview.md)lotes.

## Pasos siguientes

Ahora que comprendes los conceptos básicos de la composición de esquemas, estás listo para empezar a crear esquemas usando el [!DNL Schema Registry].

El [!DNL Schema Registry] se utiliza para acceder a [!DNL Schema Library] dentro de Adobe Experience Platform y proporciona una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles. El [!DNL Schema Library] contiene recursos del sector definidos por Adobes, recursos del proveedor definidos por [!DNL Experience Platform] socios y clases, mezclas, tipos de datos y esquemas que han sido compuestos por miembros de su organización.

Para empezar a componer esquemas mediante la interfaz de usuario, siga el tutorial [del Editor de](../tutorials/create-schema-ui.md) Esquemas para crear el esquema &quot;Miembros de lealtad&quot; mencionado a lo largo de este documento.

Para empezar a utilizar la [!DNL Schema Registry] API, lea la guía [para desarrolladores de la API de registro de](../api/getting-started.md)Esquema para inicio. Después de leer la guía para desarrolladores, siga los pasos descritos en el tutorial sobre la [creación de un esquema con la API](../tutorials/create-schema-api.md)del Registro de Esquemas.