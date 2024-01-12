---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;enum;mixin;grupo de campos;grupos de campos;mezclas;tipo de datos;tipos de datos;Tipo de datos;identidad principal;identidad principal;perfil individual XDM;campos XDM;tipo de datos enum;evento de experiencia;Evento de experiencia XDM;Evento de experiencia XDM;ExperienceEvent XDM;ExperienceEvent;experienceEvent;experienceevent;XDM ExperienceEvent;diseño de esquema;clase;clases;clases;tipo de datos;tipo de datos;tipo de datos;esquemas;identityMap;mapa de identidad;mapa de identidad;unión
solution: Experience Platform
title: Conceptos básicos de composición de esquemas
description: Obtenga información acerca de los esquemas XDM (Experience Data Model) y los componentes básicos, los principios y las prácticas recomendadas para componer esquemas en Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '4229'
ht-degree: 6%

---

# Conceptos básicos de composición de esquemas

Obtenga información acerca de los esquemas XDM (Experience Data Model) y los componentes básicos, los principios y las prácticas recomendadas para componer esquemas en Adobe Experience Platform. Para obtener información general sobre XDM y cómo se utiliza en [!DNL Platform], consulte la [Información general del sistema XDM](../home.md).

## Explicación de los esquemas {#understanding-schemas}

Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. En un nivel superior, los esquemas proporcionan una definición abstracta de un objeto del mundo real (como una persona) y describen qué datos deben incluirse en cada instancia de ese objeto (como nombre, apellido, cumpleaños, etc.).  

Además de describir la estructura de los datos, los esquemas aplican restricciones y expectativas a los datos para que se puedan validar a medida que se mueven entre sistemas. Estas definiciones estándar permiten que los datos se interpreten de forma coherente, independientemente del origen, y eliminan la necesidad de traducción entre aplicaciones.

El Experience Platform mantiene esta normalización semántica utilizando esquemas. Los esquemas son la forma estándar de describir los datos en Experience Platform, lo que permite reutilizar en una organización todos los datos que se ajustan a esquemas, o incluso compartirlos entre varias organizaciones.

Los esquemas XDM son ideales para almacenar grandes cantidades de datos complejos en un formato independiente. Consulte las secciones sobre [objetos incrustados](#embedded) y [big data](#big-data) en el apéndice de este documento para obtener más información sobre cómo XDM lo consigue.

### Flujos de trabajo basados en esquemas en Experience Platform {#schema-based-workflows}

La estandarización es un concepto clave detrás de Experience Platform. XDM, impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas estándar para la administración de experiencias del cliente.

La infraestructura en la que se crea Experience Platform, conocida como [!DNL XDM System], facilita los flujos de trabajo basados en esquemas e incluye [!DNL Schema Registry], [!DNL Schema Editor], metadatos de esquema y patrones de consumo de servicio. Consulte la [Información general del sistema XDM](../home.md) para obtener más información.

El uso de esquemas en Experience Platform ofrece varias ventajas clave. En primer lugar, los esquemas permiten una mejor gobernanza y minimización de los datos, lo que es especialmente importante con las normas de privacidad. En segundo lugar, la creación de esquemas con los componentes estándar de Adobe permite obtener perspectivas y utilizar servicios AI/ML de forma predeterminada con personalizaciones mínimas. Por último, los esquemas proporcionan una infraestructura para compartir perspectivas de datos y una orquestación eficiente.

## Planificación del esquema {#planning}

El primer paso para crear un esquema es determinar el concepto, u objeto del mundo real, que está intentando capturar dentro del esquema. Una vez que identifique el concepto que intenta describir, empiece a planificar el esquema pensando en cosas como el tipo de datos, los campos de identidad potenciales y cómo puede evolucionar el esquema en el futuro.

### Comportamientos de datos en Experience Platform {#data-behaviors}

Los datos que se van a utilizar en Experience Platform se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo.
* **Datos de series temporales**: Proporciona una instantánea del sistema en el momento en que un sujeto del registro realizó una acción, ya sea directa o indirectamente.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM se describen de forma más detallada más adelante en este documento.

Los esquemas de registros y series temporales contienen un mapa de identidades (`xdm:identityMap`). Este campo contiene la representación de identidad de un asunto, extraída de los campos marcados como &quot;Identidad&quot; tal como se describe en la siguiente sección.

### [!UICONTROL Identidad] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identidades en esquemas"
>abstract="Las identidades son campos clave dentro de un esquema que pueden utilizarse para identificar un asunto, como una dirección de correo electrónico o un ID de marketing. Estos campos se utilizan para construir el gráfico de identidad para cada particular y crear perfiles de cliente. Consulte la documentación para obtener más información sobre las identidades en los esquemas."

Los esquemas se utilizan para la ingesta de datos en Experience Platform. Estos datos se pueden utilizar en varios servicios para crear una única vista unificada de una entidad individual. Por lo tanto, al diseñar esquemas para identidades de clientes, es importante tener en cuenta qué campos se pueden utilizar para identificar a un sujeto, independientemente de dónde provengan los datos.

Para ayudar con este proceso, los campos clave dentro de los esquemas se pueden marcar como identidades. Tras la ingesta de datos, los datos de esos campos se insertan en la &quot;[!UICONTROL Gráfico de identidad]&quot; para ese individuo. Se puede acceder a los datos del gráfico a través de [[!DNL Real-Time Customer Profile]](../../profile/home.md) y otros servicios de Experience Platform para proporcionar una vista unida de cada cliente individual.

Campos que normalmente se marcan como &quot;[!UICONTROL Identidad]&quot; incluir: dirección de correo electrónico, número de teléfono, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es), ID de CRM u otros campos de ID únicos. Tenga en cuenta cualquier identificador único específico de su organización, ya que puede ser bueno&quot;.[!UICONTROL Identidad]&quot; campos también.

Es importante tener en cuenta las identidades de los clientes durante la fase de planificación del esquema para garantizar que los datos se reúnan y se cree el perfil más sólido posible. Para obtener más información sobre cómo la información de identidad puede ayudarle a ofrecer experiencias digitales a sus clientes, consulte la [Introducción al servicio de identidad](../../identity-service/home.md). Consulte el documento Prácticas recomendadas de modelado de datos para [sugerencias sobre el uso de identidades al crear un esquema](./best-practices.md#data-validation-fields).

Existen dos formas de enviar datos de identidad a Platform:

1. Agregar descriptores de identidad a campos individuales, ya sea mediante la variable [IU del Editor de esquemas](../ui/fields/identity.md) o utilizando el [API de Registro de esquemas](../api/descriptors.md#create)
1. Uso de un [`identityMap` campo](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` es un campo de tipo mapa que describe los distintos valores de identidad de un individuo, junto con sus áreas de nombres asociadas. Este campo se puede utilizar para proporcionar información de identidad para los esquemas, en lugar de definir valores de identidad dentro de la estructura del propio esquema.

El principal inconveniente de utilizar `identityMap` es que las identidades se incrustan en los datos y, como resultado, se vuelven menos visibles. Si está introduciendo datos sin procesar, debe definir campos de identidad individuales dentro de la estructura de esquema real.

>[!NOTE]
>
>Un esquema que utiliza `identityMap` se puede utilizar como esquema de origen en una relación, pero no se puede utilizar como esquema de referencia. Esto se debe a que todos los esquemas de referencia deben tener una identidad visible que se pueda asignar en un campo de referencia dentro del esquema de origen. Consulte la guía de IU sobre [relaciones](../tutorials/relationship-ui.md) para obtener más información sobre los requisitos de los esquemas de origen y referencia.

Sin embargo, los mapas de identidad pueden resultar útiles si hay un número variable de identidades para un esquema o si está reuniendo datos de fuentes que almacenan identidades (por ejemplo, [!DNL Airship] o Adobe Audience Manager). Además, los mapas de identidad son obligatorios si utiliza [SDK de Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/home/).

Un ejemplo de mapa de identidad simple tendría el siguiente aspecto:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Como se muestra en el ejemplo anterior, cada clave de la variable `identityMap` representa un área de nombres de identidad. El valor de cada clave es una matriz de objetos, que representan los valores de identidad (`id`) para el área de nombres correspondiente. Consulte la [!DNL Identity Service] documentación de un [lista de áreas de nombres de identidad estándar](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconocido por las aplicaciones de Adobe.

>[!NOTE]
>
>Un valor booleano para saber si el valor es una identidad principal (`primary`) también se puede proporcionar para cada valor de identidad. Solo es necesario establecer identidades principales para los esquemas que se van a utilizar en [!DNL Real-Time Customer Profile]. Consulte la sección sobre [esquemas de unión](#union) para obtener más información.

### Principios de evolución del esquema {#evolution}

A medida que la naturaleza de las experiencias digitales sigue evolucionando, también lo deben hacer los esquemas utilizados para representarlas. Por lo tanto, un esquema bien diseñado es capaz de adaptarse y evolucionar según sea necesario, sin provocar cambios destructivos en versiones anteriores del esquema.

Dado que el mantenimiento de la compatibilidad con versiones anteriores es crucial para la evolución del esquema, Experience Platform aplica un principio de versiones puramente aditivo. Este principio garantiza que todas las revisiones del esquema solo resulten en actualizaciones y cambios no destructivos. En otras palabras, **no se admiten cambios importantes.**

>[!NOTE]
>
>Solo puede introducir un cambio radical en un esquema si aún no se ha utilizado para introducir datos en Experience Platform y no se ha habilitado para su uso en el Perfil del cliente en tiempo real. Sin embargo, una vez que el esquema se ha utilizado en [!DNL Platform], debe adherirse a la política de versiones aditiva.

La siguiente tabla desglosa qué cambios se admiten al editar esquemas, grupos de campos y tipos de datos:

| Cambios admitidos | Cambios importantes (no admitido) |
| --- | --- |
| <ul><li>Adición de nuevos campos al recurso</li><li>Conversión de un campo obligatorio en opcional</li><li>Introducción de nuevos campos obligatorios*</li><li>Modificación del nombre para mostrar y la descripción del recurso</li><li>Habilitar el esquema para que participe en el perfil</li></ul> | <ul><li>Eliminación de campos definidos anteriormente</li><li>Cambiar el nombre o redefinir campos existentes</li><li>Eliminación o restricción de los valores de campo admitidos anteriormente</li><li>Mover los campos existentes a una ubicación diferente en el árbol</li><li>Eliminación del esquema</li><li>Desactivación de la participación del esquema en el perfil</li></ul> |

\**Consulte la sección siguiente para conocer las consideraciones importantes sobre [definición de nuevos campos obligatorios](#post-ingestion-required-fields).*

### Campos requeridos

Los campos de esquema individuales pueden ser [marcado como obligatorio](../ui/fields/required.md), lo que significa que los registros ingeridos deben contener datos en esos campos para pasar la validación. Por ejemplo, configurar el campo de identidad principal de un esquema como obligatorio puede ayudar a garantizar que todos los registros introducidos participen en el Perfil del cliente en tiempo real. Del mismo modo, configurar un campo de marca de tiempo como obligatorio garantiza que todos los eventos de series de tiempo se conserven cronológicamente.

>[!IMPORTANT]
>
>Independientemente de si un campo de esquema es obligatorio o no, Platform no acepta `null` o valores vacíos para cualquier campo ingerido. Si no hay ningún valor para un campo en particular en un registro o evento, la clave de ese campo debe excluirse de la carga útil de ingesta.

#### Configuración de campos según sea necesario después de la ingesta {#post-ingestion-required-fields}

Si un campo se ha utilizado para introducir datos y no se estableció originalmente como obligatorio, ese campo puede tener un valor nulo para algunos registros. Si establece este campo como necesario después de la ingesta, todos los registros futuros deben contener un valor para este campo aunque los registros históricos puedan ser nulos.

Cuando configure un campo opcional anterior como obligatorio, tenga en cuenta lo siguiente:

1. Si consulta datos históricos y escribe los resultados en un nuevo conjunto de datos, algunas filas producirán un error porque contienen valores nulos para el campo requerido.
1. Si el campo participa en [Perfil del cliente en tiempo real](../../profile/home.md) y si exporta datos antes de establecerlos como es necesario, puede que sea nulo para algunos perfiles.
1. Puede utilizar la API de Registro de esquemas para ver un registro de cambios con marca de tiempo para todos los recursos XDM en Platform, incluidos los nuevos campos obligatorios. Consulte la guía en la [extremo del registro de auditoría](../api/audit-log.md) para obtener más información.

### Esquemas e ingesta de datos

Para introducir datos en Experience Platform, primero se debe crear un conjunto de datos. Los conjuntos de datos son los componentes básicos para la transformación y el seguimiento de datos para [[!DNL Catalog Service]](../../catalog/home.md)y generalmente representan tablas o archivos que contienen datos ingeridos. Todos los conjuntos de datos se basan en esquemas XDM existentes, que proporcionan restricciones sobre qué deben contener los datos ingeridos y cómo deben estructurarse. Consulte la información general sobre [Ingesta de datos de Adobe Experience Platform](../../ingestion/home.md) para obtener más información.

## Bloques de creación de un esquema {#schema-building-blocks}

Experience Platform utiliza un método de maquetación en el que los bloques de creación estándar se combinan para crear esquemas. Este enfoque promueve la reutilización de los componentes existentes e impulsa la estandarización en todo el sector para admitir esquemas y componentes de proveedores en [!DNL Platform].

Los esquemas se componen mediante la fórmula siguiente:

**Clase + Grupo de campos de esquema&amp;ast; = Esquema XDM**

&amp;ast;Un esquema está compuesto por una clase y cero o más grupos de campos de esquema. Esto significa que puede componer un esquema de conjunto de datos sin utilizar grupos de campos.

### Clase {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Clase"
>abstract="Cada esquema se basa en una sola clase. La clase define el comportamiento del esquema y las propiedades comunes que deben contener todos los esquemas basados en esa clase. Consulte la documentación para obtener más información sobre cómo participan las clases en la composición de esquemas."

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Además, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían incluir y proporcionan una forma de combinar varios conjuntos de datos compatibles.

La clase de un esquema determina qué grupos de campos pueden utilizarse en ese esquema. Esto se analiza con más detalle en la [sección siguiente](#field-group).

Adobe proporciona varias clases XDM estándar (&quot;principales&quot;). Dos de estas clases, [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent], son necesarios para casi todos los procesos de Platform secundarios. Además de estas clases principales, también puede crear sus propias clases personalizadas para describir casos de uso más específicos para su organización. Una organización define las clases personalizadas cuando no hay clases principales definidas por el Adobe disponibles para describir un caso de uso único.

La siguiente captura de pantalla muestra cómo se representan las clases en la interfaz de usuario de Platform. Dado que el esquema de ejemplo mostrado no contiene ningún grupo de campos, la clase del esquema ( ) proporciona todos los campos mostrados[!UICONTROL Perfil individual de XDM]).

![El [!UICONTROL Perfil individual de XDM] en el Editor de esquemas.](../images/schema-composition/class.png)

Para obtener la lista más actualizada de clases XDM estándar disponibles, consulte la [repositorio XDM oficial](https://github.com/adobe/xdm/tree/master/components/classes). También puede consultar la guía de [exploración de componentes XDM](../ui/explore.md) si prefiere ver los recursos en la interfaz de usuario.

### Grupo de campo {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Grupo de campo"
>abstract="Los grupos de campos son componentes reutilizables que permiten ampliar esquemas con atributos adicionales. La mayoría de los grupos de campos solo son compatibles con ciertas clases. Puede utilizar grupos de campos estándar definidos por Adobe o puede definir manualmente sus propios grupos de campos personalizados. Consulte la documentación para obtener más información sobre cómo participan los grupos de campos en la composición de esquemas."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Grupo de campos obligatorio"
>abstract="La fuente que utiliza requiere este grupo de campos. Por este motivo, no puede eliminarlo del esquema."

Un grupo de campos es un componente reutilizable que define uno o varios campos que implementan determinadas funciones, como detalles personales, preferencias de hotel o dirección. Los grupos de campos están pensados para incluirse como parte de un esquema que implementa una clase compatible.

Los grupos de campos definen con qué clase o clases son compatibles, según el comportamiento de los datos que representan (registro o serie temporal). Esto significa que no todos los grupos de campos están disponibles para su uso con todas las clases.

Experience Platform incluye muchos grupos de campos de Adobe estándar, pero también permite a los proveedores definir grupos de campos para sus usuarios y a los usuarios individuales definir grupos de campos para sus propios conceptos específicos.

Por ejemplo, para capturar detalles como &quot;[!UICONTROL Nombre]&quot; y &quot;[!UICONTROL Dirección particular]&quot; para su &quot;[!UICONTROL Miembros socio]&quot;, podría utilizar grupos de campos estándar que definan esos conceptos comunes. Sin embargo, los conceptos más específicos de su organización (como los detalles del programa de fidelidad personalizado o los atributos de producto) que pueden no estar cubiertos por los grupos de campos estándar. En este caso, debe definir su propio grupo de campos para capturar esta información.

>[!NOTE]
>
>Se recomienda encarecidamente utilizar grupos de campos estándar siempre que sea posible en los esquemas, ya que estos campos los entienden implícitamente los servicios de Experience Platform y proporcionan una mayor coherencia cuando se utilizan en [!DNL Platform] componentes.
>
>Los campos proporcionados por componentes estándar (como &quot;Nombre&quot; y &quot;Dirección de correo electrónico&quot;) contienen connotaciones agregadas más allá de los tipos de campo escalares básicos. Ellos dicen [!DNL Platform] Tenga en cuenta que cualquier campo que comparta el mismo tipo de datos se comportará de la misma manera. Se puede confiar en que este comportamiento sea coherente independientemente de la procedencia de los datos o en que [!DNL Platform] servicio los datos se están utilizando.

Recuerde que los esquemas están compuestos por grupos de campos &quot;cero o más&quot;, lo que significa que puede crear un esquema válido sin utilizar ningún grupo de campos.

La siguiente captura de pantalla muestra cómo se representan los grupos de campos en la IU de Platform. Un solo grupo de campos ([!UICONTROL Datos demográficos]) se agrega a un esquema en este ejemplo, que proporciona una agrupación de campos a la estructura del esquema.

![El Editor de esquemas con [!UICONTROL Datos demográficos] grupo de campos resaltado en un esquema de ejemplo.](../images/schema-composition/field-group.png)

Para obtener la lista más actualizada de grupos de campos XDM estándar disponibles, consulte la [repositorio XDM oficial](https://github.com/adobe/xdm/tree/master/components/fieldgroups). También puede consultar la guía de [exploración de componentes XDM](../ui/explore.md) si prefiere ver los recursos en la interfaz de usuario.

### Tipo de datos {#data-type}

Los tipos de datos se utilizan como tipos de campo de referencia en clases o esquemas de la misma manera que los campos literales básicos. La diferencia clave es que los tipos de datos pueden definir varios subcampos de la misma manera que los grupos de campos. La diferencia clave entre ellos es que los tipos de datos se pueden incluir en cualquier lugar de un esquema agregándolo como el &quot;tipo de datos&quot; de un campo. Aunque los grupos de campos solo son compatibles con determinadas clases, los tipos de datos se pueden incluir en cualquier clase principal o grupo de campos.

>[!NOTE]
>
>Si un campo está definido como un tipo de datos específico, no se puede crear el mismo campo con un tipo de datos diferente en otro esquema. Esta restricción se aplica a todo el inquilino de la organización.

Experience Platform proporciona una serie de tipos de datos comunes como parte de [!DNL Schema Registry] para admitir el uso de patrones estándar para describir estructuras de datos comunes. Esto se explica con más detalle en la [Tutoriales del Registro de esquemas](../tutorials/create-schema-api.md) y serán más claros a medida que avance en los pasos para definir los tipos de datos.

La siguiente captura de pantalla muestra cómo se representan los tipos de datos en la interfaz de usuario de Platform. Uno de los campos proporcionados por el [!UICONTROL Datos demográficos] El grupo de campos utiliza el &quot;[!UICONTROL Objeto]&quot;, tal como indica el texto que sigue al carácter de barra vertical (`|`) junto al nombre del campo. Este tipo de datos en particular proporciona varios subcampos relacionados con el nombre de una persona individual, una construcción que se puede reutilizar para otros campos en los que sea necesario capturar el nombre de una persona.

![Diagrama del Editor de esquemas para una persona individual con el objeto Nombre completo y los atributos resaltados.](../images/schema-composition/data-type.png)

Para obtener la lista más actualizada de tipos de datos XDM estándar disponibles, consulte la [repositorio XDM oficial](https://github.com/adobe/xdm/tree/master/components/datatypes). También puede consultar la guía de [exploración de componentes XDM](../ui/explore.md) si prefiere ver los recursos en la interfaz de usuario.

### Campo {#field}

Un campo es el bloque de creación más básico de un esquema. Los campos proporcionan restricciones con respecto al tipo de datos que pueden contener al definir un tipo de datos específico. Estos tipos de datos básicos definen un único campo, mientras que la variable [tipos de datos](#data-type) los campos mencionados anteriormente permiten definir varios subcampos y reutilizar la misma estructura de varios campos en varios esquemas. Por tanto, además de definir el &quot;tipo de datos&quot; de un campo como uno de los tipos de datos definidos en el Registro, Experience Platform admite tipos escalares básicos como:

* Cadena
* Número entero
* Doble
* Booleano
* Matriz
* Objeto

>[!TIP]
>
>Consulte la [apéndice](#objects-v-freeform) para obtener información sobre las ventajas y desventajas de utilizar campos de forma libre sobre campos de tipo objeto.

Los intervalos válidos de estos tipos escalares se pueden restringir aún más a ciertos patrones, formatos, mínimos/máximos o valores predefinidos. Con estas restricciones, se puede representar una amplia gama de tipos de campo más específicos, incluidos los siguientes:

* Enumeración
* Largo
* corto
* Byte
* Fecha
* Fecha-hora
* Mapa

>[!NOTE]
>
>El tipo de campo &quot;asignación&quot; permite datos de par clave-valor, incluidos varios valores para una sola clave. Las asignaciones se pueden encontrar en clases XDM estándar y grupos de campos, pero también puede definir asignaciones personalizadas mediante la API de Registro de esquemas. Consulte el tutorial sobre [definición de campos personalizados](../tutorials/custom-fields-api.md#custom-maps) para obtener más información.

## Ejemplo de composición {#composition-example}

Los esquemas se crean utilizando un modelo de composición y representan el formato y la estructura de los datos que se van a introducir en [!DNL Platform]. Como se ha mencionado anteriormente, estos esquemas están compuestos por una clase y cero o más grupos de campos compatibles con esa clase.

Por ejemplo, un esquema que describa las compras realizadas en una tienda minorista podría llamarse &quot;[!UICONTROL Transacciones de tienda]&quot;. El esquema implementa las [!DNL XDM ExperienceEvent] clase combinada con el estándar [!UICONTROL Comercio] y un grupo de campos definido por el usuario [!UICONTROL Información del producto] grupo de campos.

Se puede llamar a otro esquema que rastrea el tráfico del sitio web &quot;[!UICONTROL Visitas web]&quot;. También implementa la [!DNL XDM ExperienceEvent] clase, pero esta vez combina el estándar [!UICONTROL Web] grupo de campos.

El diagrama siguiente muestra estos esquemas y los campos aportados por cada grupo de campos. También contiene dos esquemas basados en la variable [!DNL XDM Individual Profile] clase, incluido el &quot;[!UICONTROL Miembros socio]Esquema &quot; mencionado anteriormente en esta guía.

![Diagrama de flujo de cuatro esquemas y grupos de campos que contribuyen a ellos.](../images/schema-composition/composition.png)

### Unión {#union}

Aunque Experience Platform le permite componer esquemas para casos de uso específicos, también le permite ver una &quot;unión&quot; de esquemas para un tipo de clase específico. El diagrama anterior muestra dos esquemas basados en la clase XDM ExperienceEvent y dos esquemas basados en [!DNL XDM Individual Profile] clase. La unión, que se muestra a continuación, agrega los campos de todos los esquemas que comparten la misma clase ([!DNL XDM ExperienceEvent] y [!DNL XDM Individual Profile], respectivamente).

![Diagrama de flujo de esquema de unión que representa los campos que los componen.](../images/schema-composition/union.png)

Al habilitar un esquema para su uso con [!DNL Real-Time Customer Profile], se incluye en la unión para ese tipo de clase. [!DNL Profile] ofrece perfiles sólidos y centralizados de los atributos del cliente y una cuenta con marca de tiempo de cada evento que el cliente ha tenido en cualquier sistema integrado con [!DNL Platform]. [!DNL Profile] utiliza la vista unión para representar estos datos y proporcionar una vista integral de cada cliente individual.

Para obtener más información sobre cómo trabajar con [!DNL Profile], consulte la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Asignación de archivos de datos a esquemas XDM {#mapping-datafiles}

Todos los archivos de datos que se incorporan al Experience Platform deben ajustarse a la estructura de un esquema XDM. Para obtener más información sobre cómo dar formato a los archivos de datos para que cumplan con las jerarquías XDM (incluidos los archivos de ejemplo), consulte el documento sobre [transformaciones de ETL de muestra](../../etl/transformations.md). Para obtener información general sobre la ingesta de archivos de datos en Experience Platform, consulte la [introducción a la ingesta por lotes](../../ingestion/batch-ingestion/overview.md).

## Esquemas para audiencias externas

Si va a llevar audiencias de sistemas externos a Platform, debe utilizar los siguientes componentes para capturarlas en los esquemas:

* [[!UICONTROL Definición del segmento] clase](../classes/segment-definition.md): Utilice esta clase estándar para capturar atributos clave de una definición de segmento externa.
* [[!UICONTROL Detalles de abono de segmento] grupo de campos](../field-groups/profile/segmentation.md): Añada este grupo de campos a su [!UICONTROL Perfil individual de XDM] para asociar perfiles de clientes con audiencias específicas.

## Pasos siguientes

Ahora que comprende los conceptos básicos de la composición de esquemas, está listo para empezar a explorar y crear esquemas utilizando [!DNL Schema Registry].

Para revisar la estructura de las dos clases XDM principales y sus grupos de campos compatibles comúnmente utilizados, consulte la siguiente documentación de referencia:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

El [!DNL Schema Registry] se utiliza para acceder a [!DNL Schema Library] en Adobe Experience Platform y proporciona una interfaz de usuario y una API RESTful desde las cuales se puede acceder a todos los recursos de biblioteca disponibles. El [!DNL Schema Library] contiene recursos del sector definidos por el Adobe, recursos del proveedor definidos por socios de Experience Platform y clases, grupos de campos, tipos de datos y esquemas compuestos por miembros de su organización.

Para empezar a maquetar esquemas con la interfaz de usuario, siga los [Tutorial del Editor de esquemas](../tutorials/create-schema-ui.md) para generar el esquema &quot;Miembros fieles&quot; mencionado a lo largo de este documento.

Para empezar a utilizar [!DNL Schema Registry] API, comience por leer el [Guía para desarrolladores de API de Registro de esquemas](../api/getting-started.md). Después de leer la guía para desarrolladores, siga los pasos descritos en el tutorial sobre [creación de un esquema mediante la API de Registro de esquemas](../tutorials/create-schema-api.md).

## Apéndice

Las secciones siguientes contienen información adicional sobre los principios de la composición de esquemas.

### Tablas relacionales y objetos incrustados {#embedded}

Al trabajar con bases de datos relacionales, las prácticas recomendadas implican normalizar los datos o tomar una entidad y dividirla en partes discretas que luego se muestran en varias tablas. Para leer los datos en conjunto o actualizar la entidad, se deben realizar operaciones de lectura y escritura en muchas tablas individuales utilizando JOIN.

Mediante el uso de objetos incrustados, los esquemas XDM pueden representar directamente datos complejos y almacenarlos en documentos independientes con una estructura jerárquica. Una de las principales ventajas de esta estructura es que le permite consultar los datos sin tener que reconstruir la entidad mediante costosas uniones a varias tablas desnormalizadas. No hay restricciones estrictas en cuanto a la cantidad de niveles que puede tener la jerarquía de esquema.

### Esquemas y big data {#big-data}

Los sistemas digitales modernos generan grandes cantidades de señales de comportamiento (datos de transacción, registros web, Internet de las cosas, visualización, etc.). Estos big data ofrecen oportunidades extraordinarias para optimizar experiencias, pero su uso es complicado debido a la escala y variedad de los datos. Para obtener valor de los datos, su estructura, formato y definiciones deben estar estandarizados para que puedan procesarse de forma coherente y eficaz.

Los esquemas resuelven este problema al permitir que los datos se integren desde varias fuentes, se estandaricen a través de estructuras y definiciones comunes y se compartan entre soluciones. Esto permite que los procesos y servicios subsiguientes respondan a cualquier tipo de pregunta que se haga sobre los datos. Se aleja del enfoque tradicional del modelado de datos, donde todas las preguntas que se le hacen a los datos se conocen de antemano y los datos se modelan para ajustarse a esas expectativas.

### Objetos en comparación con campos de forma libre {#objects-v-freeform}

Hay algunos factores clave a tener en cuenta al elegir objetos en lugar de campos de forma libre al diseñar los esquemas:

| Objetos | Campos de forma libre |
| --- | --- |
| Aumenta el anidamiento | Menos o ningún anidamiento |
| Crea agrupaciones de campos lógicos | Los campos se colocan en ubicaciones ad hoc |

{style="table-layout:auto"}

#### Objetos

A continuación se enumeran los pros y los contras de utilizar objetos sobre campos de forma libre.

**Pros**:

* Los objetos se utilizan mejor cuando desea crear una agrupación lógica de ciertos campos.
* Los objetos organizan el esquema de forma más estructurada.
* Los objetos ayudan indirectamente a crear una buena estructura de menú en la interfaz de usuario del Generador de segmentos. Los campos agrupados dentro del esquema se reflejan directamente en la estructura de carpetas proporcionada en la interfaz de usuario del Generador de segmentos.

**Contras**:

* Los campos se anidan más.
* Al utilizar [Adobe Experience Platform Query Service](../../query-service/home.md), se deben proporcionar cadenas de referencia más largas a los campos de consulta anidados en objetos.

#### Campos de forma libre

A continuación se enumeran los pros y los contras de utilizar campos de forma libre sobre objetos.

**Pros**:

* Los campos de forma libre se crean directamente bajo el objeto raíz del esquema (`_tenantId`), aumentando la visibilidad.
* Las cadenas de referencia para campos de forma libre tienden a ser más cortas al utilizar el servicio de consulta.

**Contras**:

* La ubicación de los campos de forma libre dentro del esquema es ad hoc, lo que significa que aparecen en orden alfabético dentro del Editor de esquemas. Esto puede hacer que los esquemas estén menos estructurados y campos de forma libre similares pueden terminar estando muy separados según sus nombres.
