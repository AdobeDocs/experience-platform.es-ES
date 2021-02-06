---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;enumeración;mezcla;Mezcla;Mezclas;mezclas;tipo de datos;tipos de datos;tipos de datos;tipo de datos;identidad primaria;identidad primaria;perfil individual XDM;campos XDM;tipo de datos enum;evento de experiencias;Evento de experiencias XDM;evento de experiencia XDM;evento de experiencia;diseño de esquema clase;Clase;clases;Clases;tipo de datos;Tipo de datos;tipo de datos;Tipo de datos;esquemas;Esquema;mapa de identidad;mapa de identidad;mapa de identidad;Esquema diseño de ;mapa;mapa;esquema de unión;unión
solution: Experience Platform
tiTle: Basics of Schema Composition
topic: overview
description: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '3161'
ht-degree: 0%

---


# Conceptos básicos de la composición de esquemas

Este documento proporciona una introducción a los [!DNL Experience Data Model] esquemas (XDM) y a los componentes, principios y optimizaciones para la composición de esquemas que se utilizarán en Adobe Experience Platform. Para obtener información general sobre XDM y cómo se utiliza en [!DNL Platform], consulte la [información general del sistema XDM](../home.md).

## Explicación de los esquemas

Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. En un nivel superior, los esquemas proporcionan una definición abstracta de un objeto real (como una persona) y describen los datos que deben incluirse en cada instancia de dicho objeto (como el nombre, el apellido, el cumpleaños, etc.).

Además de describir la estructura de los datos, los esquemas aplican restricciones y expectativas a los datos para que se puedan validar a medida que se desplaza de un sistema a otro. Estas definiciones estándar permiten interpretar los datos de manera coherente, independientemente del origen, y eliminan la necesidad de traducirlos entre las aplicaciones.

[!DNL Experience Platform] mantiene esta normalización semántica mediante el uso de esquemas. Los esquemas son la manera estándar de describir los datos en [!DNL Experience Platform], permitiendo que todos los datos que se ajustan a los esquemas se puedan reutilizar sin conflictos en una organización e incluso compartir entre varias organizaciones.

### Tablas relacionales frente a objetos incrustados

Cuando se trabaja con bases de datos relacionales, las prácticas recomendadas implican normalizar datos o tomar una entidad y dividirla en partes discretas que luego se muestran en varias tablas. Para poder leer los datos en su conjunto o actualizar la entidad, las operaciones de lectura y escritura deben realizarse en muchas tablas individuales utilizando JOIN.

Mediante el uso de objetos incrustados, los esquemas XDM pueden representar directamente datos complejos y almacenarlos en documentos independientes con una estructura jerárquica. Uno de los principales beneficios de esta estructura es que le permite consulta de los datos sin tener que reconstruir la entidad mediante costosas combinaciones a múltiples tablas desnormalizadas. No hay restricciones estrictas para cuántos niveles puede ser la jerarquía de esquemas.

### Esquemas y grandes datos

Los sistemas digitales modernos generan grandes cantidades de señales conductuales (datos de transacciones, registros web, Internet de cosas, visualización, etc.). Estos datos de gran tamaño oferta oportunidades extraordinarias para optimizar experiencias, pero su uso es difícil debido a la escala y variedad de los datos. Para obtener valor de los datos, su estructura, formato y definiciones deben estar estandarizados para que se puedan procesar de manera coherente y eficiente.

Los esquemas solucionan este problema permitiendo que los datos se integren desde múltiples fuentes, que se estandaricen a través de estructuras y definiciones comunes y que se compartan entre las soluciones. Esto permite que los procesos y servicios subsiguientes respondan a cualquier tipo de pregunta que se formule sobre los datos, alejándose del enfoque tradicional de la modelización de datos, en el que todas las preguntas que se formularán sobre los datos se conocen con antelación y los datos se modelan para ajustarse a esas expectativas.

### Flujos de trabajo basados en esquemas en [!DNL Experience Platform]

La estandarización es un concepto clave detrás de [!DNL Experience Platform]. XDM, impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas estándar para la administración de la experiencia del cliente.

La infraestructura en la que [!DNL Experience Platform] se genera, conocida como [!DNL XDM System], facilita los flujos de trabajo basados en esquemas e incluye los [!DNL Schema Registry], [!DNL Schema Editor], los metadatos de esquema y los patrones de consumo de servicios. Consulte la [información general del sistema XDM](../home.md) para obtener más información.

Existen varios beneficios clave para construir y utilizar esquemas en [!DNL Experience Platform]. En primer lugar, los esquemas permiten una mejor gobernanza de los datos y la minimización de los mismos, lo cual es especialmente importante con las regulaciones de privacidad. En segundo lugar, la creación de esquemas con los componentes estándar de Adobe permite obtener perspectivas integradas y utilizar servicios de AI/ML con personalizaciones mínimas. Por último, los esquemas proporcionan infraestructura para el uso compartido de datos y la orquestación eficiente.

## Planificación del esquema

El primer paso para crear un esquema es determinar el concepto, o objeto real, que se intenta capturar dentro del esquema. Una vez que identifique el concepto que está tratando de describir, puede empezar a planificar su esquema pensando en cosas como el tipo de datos, los campos de identidad potenciales y cómo el esquema puede evolucionar en el futuro.

### Comportamientos de datos en [!DNL Experience Platform]

Los datos destinados a utilizarse en [!DNL Experience Platform] se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema lo define la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM se describen en detalle más adelante en este documento.

Tanto los esquemas de registro como de serie temporal contienen un mapa de identidades (`xdm:identityMap`). Este campo contiene la representación de identidad de un sujeto, extraída de campos marcados como &quot;Identidad&quot; como se describe en la siguiente sección.

### [!UICONTROL Identidad] {#identity}

Los esquemas se utilizan para ingerir datos en [!DNL Experience Platform]. Estos datos se pueden utilizar en varios servicios para crear una sola vista unificada de una entidad individual. Por lo tanto, es importante que, cuando se piensa en los esquemas, se reflexione sobre las identidades de los clientes y los campos que se pueden utilizar para identificar un asunto, independientemente de la procedencia de los datos.

Para ayudarle con este proceso, los campos clave dentro de sus esquemas pueden marcarse como identidades. Tras la ingestión de datos, los datos de esos campos se insertan en el &quot;[!UICONTROL Gráfico de identidad]&quot; de ese individuo. A los datos del gráfico se puede acceder mediante [[!DNL Real-time Customer Profile]](../../profile/home.md) y otros [!DNL Experience Platform] servicios para proporcionar una vista conjunta de cada cliente individual.

Los campos que se marcan comúnmente como &quot;[!UICONTROL Identidad]&quot; incluyen: dirección de correo electrónico, número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID de CRM u otros campos de ID únicos. También debe tener en cuenta cualquier identificador único específico de su organización, ya que puede que también sean buenos campos de &quot;[!UICONTROL Identidad]&quot;.

Es importante pensar en las identidades de los clientes durante la fase de planificación de esquemas para ayudar a garantizar que los datos se reúnan a fin de generar el perfil más sólido posible. Consulte la información general en [Adobe Experience Platform Identity Service](../../identity-service/home.md) para obtener más información sobre cómo la información de identidad puede ayudarle a ofrecer experiencias digitales a sus clientes.

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

Como se muestra en el ejemplo anterior, cada clave del objeto `identityMap` representa una Área de nombres de identidad. El valor de cada clave es una matriz de objetos que representa los valores de identidad (`id`) de la Área de nombres correspondiente. Consulte la [!DNL Identity Service] documentación para obtener una [lista de Áreas de nombres de identidad estándar](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconocidas por las aplicaciones de Adobe.

>[!NOTE]
>
>También se puede proporcionar un valor booleano para determinar si el valor es o no una identidad principal (`primary`) para cada valor de identidad. Las identidades primarias sólo deben configurarse para esquemas destinados a utilizarse en [!DNL Real-time Customer Profile]. Consulte la sección sobre [esquemas de unión](#union) para obtener más información.

### Principios de evolución del esquema {#evolution}

A medida que la naturaleza de las experiencias digitales sigue evolucionando, también deben evolucionar los esquemas utilizados para representarlas. Por lo tanto, un esquema bien diseñado puede adaptarse y evolucionar según sea necesario, sin causar cambios destructivos en versiones anteriores del esquema.

Dado que el mantenimiento de la compatibilidad con versiones anteriores es crucial para la evolución del esquema, [!DNL Experience Platform] aplica un principio de control de versiones puramente aditivo para garantizar que cualquier revisión del esquema sólo dé como resultado actualizaciones y cambios no destructivos. En otras palabras, **no se admiten cambios de salto.**

| Cambios admitidos | Romper cambios (no compatible) |
|------------------------------------|---------------------------------|
| <ul><li>Añadir nuevos campos a un esquema existente</li><li>Hacer opcional un campo obligatorio</li></ul> | <ul><li>Eliminación de campos definidos previamente</li><li>Introducción de nuevos campos obligatorios</li><li>Cambio de nombre o redefinición de campos existentes</li><li>Eliminación o restricción de valores de campo admitidos anteriormente</li><li>Desplazamiento de atributos a una ubicación diferente en el árbol</li></ul> |

>[!NOTE]
>
>Si todavía no se ha utilizado un esquema para ingerir datos en [!DNL Experience Platform], puede introducir un cambio de ruptura en ese esquema. Sin embargo, una vez que el esquema se ha utilizado en [!DNL Platform], debe cumplir la política de versiones aditivas.

### Esquemas e ingestión de datos

Para poder ingerir datos en [!DNL Experience Platform], primero debe crearse un conjunto de datos. Los conjuntos de datos son los componentes básicos de la transformación y el seguimiento de datos para [[!DNL Catalog Service]](../../catalog/home.md) y generalmente representan tablas o archivos que contienen datos ingestados. Todos los conjuntos de datos se basan en esquemas XDM existentes, que establecen restricciones para lo que deben contener los datos ingestados y cómo deben estructurarse. Consulte la información general sobre [Adobe Experience Platform Data Ingestion](../../ingestion/home.md) para obtener más información.

## Componentes de un esquema

[!DNL Experience Platform] utiliza un enfoque de composición en el que los componentes básicos estándar se combinan para crear esquemas. Este enfoque fomenta la reutilización de los componentes existentes e impulsa la estandarización en toda la industria para admitir esquemas y componentes de proveedores en [!DNL Platform].

Los esquemas se componen con la fórmula siguiente:

**Clase + Mixin&amp;ast; = Esquema XDM**

&amp;ast;Un esquema se compone de una clase y cero o más mezclas. Esto significa que puede componer un esquema de conjunto de datos sin usar mezclas.

### Clase {#class}

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Además de esto, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían incluir y proporcionar una manera de combinar varios conjuntos de datos compatibles.

Una clase de esquema determina qué mezclas serán elegibles para su uso en ese esquema. Esto se analiza más detalladamente en la [siguiente sección](#mixin).

Adobe proporciona dos clases XDM estándar (&quot;core&quot;): [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent]. Además de estas clases principales, también puede crear sus propias clases personalizadas para describir casos de uso más específicos para su organización. Las clases personalizadas son definidas por una organización cuando no hay clases principales definidas por el Adobe disponibles para describir un caso de uso único.

### Mixin {#mixin}

Una mezcla es un componente reutilizable que define uno o varios campos que implementan determinadas funciones, como detalles personales, preferencias del hotel o dirección. Las mezclas están pensadas para incluirse como parte de un esquema que implementa una clase compatible.

Las mezclas definen con qué clase o clases son compatibles en función del comportamiento de los datos que representan (registro o serie temporal). Esto significa que no todas las mezclas están disponibles para su uso con todas las clases.

[!DNL Experience Platform] incluye muchas mezclas de Adobe estándar, a la vez que permite a los proveedores definir mezclas para sus usuarios, y a los usuarios individuales definir mezclas para sus propios conceptos específicos.

Por ejemplo, para capturar detalles como &quot;[!UICONTROL Nombre]&quot; y &quot;[!UICONTROL Dirección principal]&quot; para el esquema &quot;[!UICONTROL Miembros de lealtad]&quot;, podría utilizar mezclas estándar que definan esos conceptos comunes. Sin embargo, los conceptos específicos de casos de uso menos comunes (como &quot;[!UICONTROL Nivel de Programa de lealtad]&quot;) no suelen tener una mezcla predefinida. En este caso, debe definir su propia mezcla para capturar esta información.

Recuerde que los esquemas están compuestos de mezclas &quot;cero o más&quot;, lo que significa que puede componer un esquema válido sin usar ninguna mezcla.

Para obtener una lista de todas las mezclas estándar actuales, consulte el [repositorio XDM oficial](https://github.com/adobe/xdm/tree/master/components/mixins).

### Tipo de datos {#data-type}

Los tipos de datos se utilizan como tipos de campos de referencia en clases o esquemas del mismo modo que los campos literales básicos. La diferencia clave es que los tipos de datos pueden definir varios subcampos. Al igual que una mezcla, un tipo de datos permite el uso coherente de una estructura de varios campos, pero tiene más flexibilidad que una mezcla, ya que se puede incluir un tipo de datos en cualquier parte de un esquema agregándolo como el &quot;tipo de datos&quot; de un campo.

>[!NOTE]
>
>Consulte el [apéndice](#mixins-v-datatypes) para obtener más información sobre las diferencias entre las mezclas y los tipos de datos, y las ventajas y desventajas de utilizar una sobre la otra para casos de uso similares.

[!DNL Experience Platform] proporciona una serie de tipos de datos comunes como parte del informe  [!DNL Schema Registry] para admitir el uso de patrones estándar para describir estructuras de datos comunes. Esto se explica con más detalle en los tutoriales [!DNL Schema Registry], donde se aclarará a medida que avance en los pasos para definir los tipos de datos.

### Campo

Un campo es el componente básico más básico de un esquema. Los campos proporcionan restricciones con respecto al tipo de datos que pueden contener al definir un tipo de datos específico. Estos tipos de datos básicos definen un solo campo, mientras que los [tipos de datos](#data-type) antes mencionados le permiten definir varios subcampos y reutilizar la misma estructura de varios campos en varios esquemas. Por lo tanto, además de definir el &quot;tipo de datos&quot; de un campo como uno de los tipos de datos definidos en el Registro, [!DNL Experience Platform] admite tipos escalares básicos como:

* Cadena
* Número entero
* Duplicada
* Booleano
* Matriz
* Objeto

>[!TIP]
>
>Consulte el [apéndice](#objects-v-freeform) para obtener información sobre los pros y los contras del uso de campos de formato libre en campos de tipo de objeto.

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
>El tipo de campo &quot;map&quot; permite datos de pares de clave-valor, incluidos varios valores para una sola clave. Los mapas solo se pueden definir en el nivel del sistema, lo que significa que puede encontrar un mapa en un esquema definido por el sector o el proveedor, pero no está disponible para utilizarse en los campos definidos. La [guía para desarrolladores de la API de registro de Esquema](../api/getting-started.md) contiene más información sobre la definición de tipos de campo.

Algunas operaciones de datos utilizadas por los servicios y las aplicaciones posteriores imponen restricciones a tipos de campo específicos. Los servicios afectados incluyen, entre otros:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Antes de crear un esquema para su uso en los servicios intermedios, revise la documentación apropiada para esos servicios a fin de comprender mejor los requisitos y las limitaciones sobre el terreno para las operaciones de datos a las que está destinado el esquema.

### Campos XDM

Además de los campos básicos y la capacidad de definir sus propios tipos de datos, XDM proporciona un conjunto estándar de campos y tipos de datos que los servicios [!DNL Experience Platform] entienden implícitamente y proporcionan buena consistencia cuando se utilizan en [!DNL Platform] componentes.

Estos campos, como &quot;Nombre&quot; y &quot;Dirección de correo electrónico&quot;, contienen connotaciones agregadas que van más allá de los tipos de campo escalar básicos, lo que indica a [!DNL Platform] que cualquier campo que comparta el mismo tipo de datos XDM se comportará de la misma manera. Se puede confiar en este comportamiento para que sea coherente independientemente de dónde provengan los datos o en qué [!DNL Platform] servicio se utilizan los datos.

Consulte el [diccionario de campo XDM](field-dictionary.md) para obtener una lista completa de los campos XDM disponibles. Se recomienda utilizar campos XDM y tipos de datos siempre que sea posible para admitir la consistencia y la estandarización en [!DNL Experience Platform].

## Ejemplo de composición

Los esquemas representan el formato y la estructura de los datos que se van a ingerir en [!DNL Platform] y se crean utilizando un modelo de composición. Como se mencionó anteriormente, estos esquemas están compuestos de una clase y cero o más mezclas compatibles con esa clase.

Por ejemplo, un esquema que describe las compras realizadas en una tienda minorista puede llamarse &quot;[!UICONTROL Transacciones de almacenamiento]&quot;. El esquema implementa la clase [!DNL XDM ExperienceEvent] combinada con la mezcla estándar [!UICONTROL Commerce] y una mezcla definida por el usuario [!UICONTROL Product Info].

Otro esquema que rastrea el tráfico del sitio Web puede llamarse &quot;[!UICONTROL Visitas Web]&quot;. También implementa la clase [!DNL XDM ExperienceEvent], pero esta vez combina la mezcla estándar [!UICONTROL Web].

El diagrama siguiente muestra estos esquemas y los campos que aporta cada mezcla. También contiene dos esquemas basados en la clase [!DNL XDM Individual Profile], incluido el esquema &quot;[!UICONTROL Miembros de lealtad]&quot; mencionado anteriormente en esta guía.

![](../images/schema-composition/composition.png)

### Union {#union}

Aunque [!DNL Experience Platform] le permite componer esquemas para casos de uso específicos, también le permite ver una &quot;unión&quot; de esquemas para un tipo de clase específico. El diagrama anterior muestra dos esquemas basados en la clase XDM ExperienceEvent y dos esquemas basados en la clase [!DNL XDM Individual Profile]. La unión, que se muestra a continuación, agrega los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] y [!DNL XDM Individual Profile], respectivamente).

![](../images/schema-composition/union.png)

Al habilitar un esquema para utilizarlo con [!DNL Real-time Customer Profile], se incluirá en la unión para ese tipo de clase. [!DNL Profile] ofrece perfiles robustos y centralizados de atributos del cliente, así como una cuenta con marca de hora de cada evento que el cliente ha tenido en cualquier sistema integrado con  [!DNL Platform]. [!DNL Profile] utiliza la vista de unión para representar estos datos y proporcionar una vista holística de cada cliente individual.

Para obtener más información sobre cómo trabajar con [!DNL Profile], consulte la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

## Asignación de archivos de datos a esquemas XDM

Todos los archivos de datos que se ingieren en [!DNL Experience Platform] deben cumplir la estructura de un esquema XDM. Para obtener más información sobre cómo dar formato a los archivos de datos para cumplir con las jerarquías XDM (incluidos los archivos de ejemplo), consulte el documento sobre [transformaciones ETL de muestra](../../etl/transformations.md). Para obtener información general sobre la ingesta de archivos de datos en [!DNL Experience Platform], consulte la [información general sobre la ingestión por lotes](../../ingestion/batch-ingestion/overview.md).

## Pasos siguientes

Ahora que comprende los conceptos básicos de la composición de esquemas, está listo para empezar a explorar y generar esquemas usando el [!DNL Schema Registry].

Para revisar la estructura de las dos clases XDM principales y sus mezclas compatibles de uso común, consulte la siguiente documentación de referencia:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

El [!DNL Schema Registry] se utiliza para acceder al [!DNL Schema Library] dentro de Adobe Experience Platform y proporciona una interfaz de usuario y una API RESTful desde la que se puede acceder a todos los recursos de biblioteca disponibles. El [!DNL Schema Library] contiene los recursos del sector definidos por el Adobe, los recursos del proveedor definidos por [!DNL Experience Platform] socios y las clases, mezclas, tipos de datos y esquemas compuestos por miembros de su organización.

Para empezar a componer esquemas mediante la interfaz de usuario, siga el tutorial [Editor de Esquemas](../tutorials/create-schema-ui.md) para crear el esquema &quot;Miembros de lealtad&quot; mencionado en este documento.

Para empezar a utilizar la API [!DNL Schema Registry], lea la guía para desarrolladores de la API de registro de Esquema [inicio](../api/getting-started.md). Después de leer la guía para desarrolladores, siga los pasos descritos en el tutorial sobre [creación de un esquema con la API del Registro de Esquema](../tutorials/create-schema-api.md).

## Apéndice

La siguiente sección contiene información adicional sobre los principios de la composición del esquema.

### Objetos frente a campos de formato libre {#objects-v-freeform}

Existen algunos factores clave que deben tenerse en cuenta al elegir objetos en lugar de campos de formulario libre al diseñar sus esquemas:

| Objetos | Campos de forma libre |
| --- | --- |
| Aumenta la anidación | Menos o sin anidación |
| Crea grupos de campos lógicos | Los campos se colocan en ubicaciones ad-hoc |

#### Objetos

Los pros y los contras del uso de objetos sobre campos de formulario libre se enumeran a continuación.

**Ventajas**:

* Los objetos se utilizan mejor cuando se desea crear una agrupación lógica de determinados campos.
* Los objetos organizan el esquema de forma más estructurada.
* Los objetos ayudan indirectamente a crear una buena estructura de menús en la interfaz de usuario del Generador de segmentos. Los campos agrupados dentro del esquema se reflejan directamente en la estructura de carpetas proporcionada en la interfaz de usuario del Generador de segmentos.

**Contras**:

* Los campos se anidan más.
* Al utilizar [Servicio de Consulta de Adobe Experience Platform](../../query-service/home.md), se deben proporcionar cadenas de referencia más largas a los campos de consulta anidados en objetos.

#### Campos de forma libre

Los pros y los contras del uso de campos de formulario libre sobre objetos se enumeran a continuación.

**Ventajas**:

* Los campos de formato libre se crean directamente bajo el objeto raíz del esquema (`_tenantId`), lo que aumenta la visibilidad.
* Las cadenas de referencia de los campos de formato libre tienden a ser más cortas cuando se utiliza el servicio de Consulta.

**Contras**:

* La ubicación de los campos de forma libre dentro del esquema es ad-hoc, lo que significa que aparecen en orden alfabético en el Editor de Esquemas. Esto puede hacer que los esquemas estén menos estructurados y que los campos de forma libre similares terminen estando muy separados según sus nombres.