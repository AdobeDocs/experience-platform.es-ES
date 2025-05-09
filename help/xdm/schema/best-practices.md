---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;enumeración;identidad principal;identidad principal;perfil individual de XDM;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;evento de experiencia;evento de experiencia;evento de experiencia XDM;diseño de esquema;prácticas recomendadas
solution: Experience Platform
title: Prácticas Recomendadas Para El Modelado De Datos
description: Este documento proporciona una introducción a los esquemas XDM (Experience Data Model) y a los componentes básicos, los principios y las prácticas recomendadas para componer esquemas que se utilizarán en Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 7521273c0ea4383b7141e9d7a82953257ff18c34
workflow-type: tm+mt
source-wordcount: '3236'
ht-degree: 1%

---

# Prácticas recomendadas para el modelado de datos

[!DNL Experience Data Model] (XDM) es el marco de trabajo principal que estandariza los datos de experiencia del cliente al proporcionar estructuras y definiciones comunes para su uso en servicios de Adobe Experience Platform descendentes. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común y utilizar para obtener información valiosa de las acciones del cliente, definir audiencias del cliente y expresar atributos del cliente con fines de personalización.

Dado que XDM es extremadamente versátil y personalizable por diseño, es importante seguir las prácticas recomendadas para el modelado de datos al diseñar los esquemas. Este documento cubre las decisiones y consideraciones clave que debe tomar al asignar los datos de experiencia del cliente a XDM.

## Introducción

Antes de leer esta guía, revise la [descripción general del sistema XDM](../home.md) para obtener una introducción de alto nivel a XDM y su función dentro de Experience Platform.

Como esta guía se centra exclusivamente en consideraciones clave relacionadas con el diseño de esquemas, se recomienda que lea los [conceptos básicos de la composición de esquemas](./composition.md) para obtener explicaciones detalladas de los elementos de esquema individuales mencionados en esta guía.

## Resumen de prácticas recomendadas {#summary}

El método recomendado para diseñar el modelo de datos para utilizarlo en Experience Platform se puede resumir de la siguiente manera:

1. Comprenda los casos de uso empresariales de sus datos.
1. Identifique las fuentes de datos principales que deben introducirse en Experience Platform para solucionar estos casos de uso.
1. Identifique cualquier fuente de datos secundaria que también pueda ser de interés. Por ejemplo, si actualmente solo una unidad comercial de su organización está interesada en transferir sus datos a Experience Platform, una unidad comercial similar también podría estar interesada en transferir datos similares en el futuro. Tener en cuenta estas fuentes secundarias ayuda a estandarizar el modelo de datos en toda la organización.
1. Cree un diagrama de relación de entidades de alto nivel (ERD) para las fuentes de datos que se han identificado.
1. Convertir el ERD de alto nivel en un ERD centrado en Experience Platform (incluidos perfiles, eventos de experiencia y entidades de búsqueda).

Los pasos relacionados con la identificación de las fuentes de datos aplicables necesarias para llevar a cabo los casos de uso empresarial varían de una organización a otra. Mientras que el resto de las secciones de este documento se centran en los últimos pasos de la organización y construcción de un ERD después de que se hayan identificado las fuentes de datos, las explicaciones de los distintos componentes del diagrama pueden informar sus decisiones sobre cuál de sus fuentes de datos debe migrarse a Experience Platform.

## Crear un ERD de alto nivel {#create-an-erd}

Una vez que haya determinado las fuentes de datos que desea introducir en Experience Platform, cree un ERD de alto nivel para guiar el proceso de asignación de los datos a esquemas XDM.

El ejemplo siguiente representa un ERD simplificado para una empresa que desea introducir datos en Experience Platform. El diagrama destaca las entidades esenciales que deben ordenarse en clases XDM, incluidas las cuentas de clientes, los hoteles y varios eventos de comercio electrónico comunes.

![Diagrama relacional de entidades que resalta las entidades esenciales que deben ordenarse en clases XDM para la ingesta de datos.](../images/best-practices/erd.png)

## Ordenar entidades en categorías de perfil, búsqueda y evento {#sort-entities}

Una vez creado un ERD para identificar las entidades esenciales que desea introducir en Experience Platform, estas entidades deben ordenarse en categorías de perfil, búsqueda y evento:

| Categoría | Descripción |
| --- | --- |
| Entidades de perfil | Las entidades de perfil representan atributos relacionados con una persona individual, normalmente un cliente. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la clase **[!DNL XDM Individual Profile]**. |
| Entidades de búsqueda | Las entidades de búsqueda representan conceptos que pueden relacionarse con una persona individual, pero no se pueden utilizar directamente para identificarla. Las entidades incluidas en esta categoría deben representarse mediante esquemas basados en **clases personalizadas** y estar vinculadas a perfiles y eventos a través de [relaciones de esquema](../tutorials/relationship-ui.md). |
| Entidades de evento | Las entidades de eventos representan conceptos relacionados con las acciones que un cliente puede realizar, eventos del sistema o cualquier otro concepto en el que desee realizar un seguimiento de los cambios a lo largo del tiempo. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la clase **[!DNL XDM ExperienceEvent]**. |

{style="table-layout:auto"}

### Consideraciones para la ordenación de entidades {#considerations}

Las secciones siguientes proporcionan más instrucciones para ordenar las entidades en las categorías anteriores.

#### Datos mutables e inmutables {#mutable-and-immutable-data}

Una forma principal de ordenar entre categorías de entidades es si los datos capturados son mutables o no.

Los atributos pertenecientes a perfiles o entidades de búsqueda suelen ser mutables. Por ejemplo, las preferencias de un cliente pueden cambiar con el tiempo y los parámetros de un plan de suscripción se pueden actualizar según las tendencias del mercado.

Por el contrario, los datos de evento suelen ser inmutables. Dado que los eventos se adjuntan a una marca de tiempo específica, la &quot;captura del sistema&quot; que proporciona un evento no cambia. Por ejemplo, un evento puede capturar las preferencias de un cliente cuando cierra la compra de un carro de compras y no cambia aunque las preferencias del cliente terminen cambiando más adelante. Los datos de evento no se pueden cambiar una vez registrados.

En resumen, los perfiles y las entidades de búsqueda contienen atributos mutables y representan la información más actual sobre los temas que capturan, mientras que los eventos son registros inmutables del sistema en un momento específico.

#### Atributos del cliente {#customer-attributes}

Si una entidad contiene atributos relacionados con un cliente individual, lo más probable es que sea una entidad de perfil. Algunos ejemplos de atributos del cliente son:

* Datos personales como nombre, fecha de nacimiento, sexo e ID de cuenta.
* Información de ubicación, como direcciones e información de GPS.
* Información de contacto, como números de teléfono y direcciones de correo electrónico.

#### Seguimiento de datos con el tiempo {#track-data}

Si desea analizar cómo cambian ciertos atributos dentro de una entidad con el paso del tiempo, lo más probable es que sea una entidad de evento. Por ejemplo, añadir elementos de producto a un carro de compras se puede rastrear como eventos de complemento al carro de compras en Experience Platform:

| ID de cliente | Tipo | ID del producto | Cantidad | Marca de tiempo |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1 de octubre, 10:32 |
| 1234567 | Quitar | 275098 | 1 | 1 de octubre, 10:33 |
| 1234567 | Add | 486502 | 1 | 1 de octubre, 10:41 |
| 1234567 | Add | 910482 | 5 | 3 de octubre, 14:15 |

{style="table-layout:auto"}

#### Casos de uso de segmentación {#segmentation-use-cases}

Al categorizar las entidades, es importante tener en cuenta las audiencias que puede interesarle crear para abordar los casos de uso empresariales específicos.

Por ejemplo, una empresa quiere conocer todos los miembros &quot;Gold&quot; o &quot;Platinum&quot; de su programa de fidelidad que han realizado más de cinco compras en el último año. En función de esta lógica de segmentación, se pueden extraer las siguientes conclusiones sobre cómo deben representarse las entidades relevantes:

* &quot;Gold&quot; y &quot;Platinum&quot; representan estados de lealtad aplicables a un cliente individual. Dado que la lógica de segmentación solo afecta al estado de lealtad actual de los clientes, estos datos se pueden modelar como parte de un esquema de perfil. Si desea rastrear los cambios en el estado de lealtad a lo largo del tiempo, también puede crear un esquema de evento adicional para los cambios de estado de lealtad.
* Las compras son eventos que se producen en un momento determinado y la lógica de segmentación se refiere a los eventos de compra dentro de un intervalo de tiempo especificado. Por lo tanto, estos datos deben modelarse como un esquema de evento.

#### Casos de uso de activación {#activation-use-cases}

Además de las consideraciones relativas a los casos de uso de segmentación, también debe revisar los casos de uso de activación de dichas audiencias para identificar atributos relevantes adicionales.

Por ejemplo, una compañía ha creado una audiencia basada en la regla que `country = US`. A continuación, al activar esa audiencia en ciertos objetivos descendentes, la empresa desea filtrar todos los perfiles exportados en función del estado de inicio. Por lo tanto, también se debe capturar un atributo `state` en la entidad de perfil aplicable.

#### Valores agregados {#aggregated-values}

En función del caso de uso y la granularidad de los datos, debe decidir si es necesario acumular previamente ciertos valores antes de incluirlos en un perfil o entidad de evento.

Por ejemplo: una empresa desea crear una audiencia basada en el número de compras al carro de compras. Puede incorporar estos datos con la granularidad más baja incluyendo cada evento de compra con marca de tiempo como su propia entidad. Sin embargo, a veces esto puede aumentar exponencialmente el número de eventos registrados. Para reducir el número de eventos ingeridos, puede elegir crear un valor agregado `numberOfPurchases` durante un período de una semana o un mes. Otras funciones agregadas como MIN y MAX también se pueden aplicar a estas situaciones.

>[!CAUTION]
>
>Experience Platform no realiza actualmente la agregación automática de valores, aunque esto está planificado para futuras versiones. Si decide utilizar valores agregados, debe realizar los cálculos externamente antes de enviar los datos a Experience Platform.

#### Cardinalidad {#cardinality}

Las cardinalidades establecidas en su ERD también pueden proporcionar algunas pistas sobre cómo categorizar sus entidades. Si existe una relación &quot;uno a varios&quot; entre dos entidades, es probable que la entidad que representa a &quot;varios&quot; sea una entidad de evento. Sin embargo, también hay casos en los que &quot;varios&quot; es un conjunto de entidades de búsqueda que se proporcionan como una matriz dentro de una entidad de perfil.

>[!NOTE]
>
>Dado que no existe un enfoque universal que se ajuste a todos los casos de uso, es importante tener en cuenta los pros y los contras de cada situación al categorizar las entidades en función de la cardinalidad. Consulte la [sección siguiente](#pros-and-cons) para obtener más información.

En la tabla siguiente se describen algunas relaciones de entidad comunes y las categorías que pueden derivarse de ellas:

| Relación | Cardinalidad | Categorías de entidad |
| --- | --- | --- |
| Cierre de compra de cliente y carro | Uno a varios | Un solo cliente puede tener muchas cierres de compra del carro de compras, que son eventos que se pueden rastrear a lo largo del tiempo. Por lo tanto, el cliente sería una entidad de perfil, mientras que el cierre de compra del carro sería una entidad de evento. |
| Cuenta de cliente y fidelización | Uno a uno | Un solo cliente solo puede tener una cuenta de fidelización y una cuenta de fidelización solo puede pertenecer a un cliente. Dado que la relación es uno a uno, tanto la cuenta del cliente como la de fidelización representan entidades de perfil. |
| Cliente y suscripción | Uno a varios | Un solo cliente puede tener muchas suscripciones. Dado que a la empresa solo le interesan las suscripciones actuales de un cliente, el cliente es una entidad de perfil, mientras que la suscripción es una entidad de búsqueda. |

{style="table-layout:auto"}

### Ventajas e inconvenientes de las diferentes clases de entidad {#pros-and-cons}

Aunque en la sección anterior se proporcionaban algunas directrices generales para decidir cómo categorizar las entidades, es importante tener en cuenta que a menudo puede haber ventajas e inconvenientes a la hora de elegir una categoría de entidad antes que otra. El siguiente caso práctico pretende ilustrar cómo podría considerar sus opciones en estas situaciones.

Una compañía realiza un seguimiento de las suscripciones activas de sus clientes, donde un cliente puede tener muchas suscripciones. La empresa también quiere incluir suscripciones para casos de uso de segmentación, como encontrar todos los usuarios con suscripciones activas.

En esta situación, la compañía tiene dos opciones potenciales para representar las suscripciones de un cliente en su modelo de datos:

1. [Usar atributos de perfil](#profile-approach)
1. [Uso de entidades de evento](#event-approach)

#### Enfoque 1: Uso de atributos de perfil {#profile-approach}

El primer método sería incluir una matriz de `subscriptionID` en la entidad de perfil para el cliente.

![Esquema del cliente en el Editor de esquemas con la clase y estructura resaltadas](../images/best-practices/profile-schema.png)

**Profesionales**

* La segmentación es factible para el caso de uso previsto.
* El esquema solo conserva los registros de suscripción más recientes para un cliente.

**Inconvenientes**

* Se debe restaurar toda la matriz cada vez que se produzcan cambios en cualquier campo de la matriz.
* Si hay diferentes fuentes de datos o unidades comerciales que introducen datos en la matriz, es difícil mantener la matriz actualizada sincronizada en todos los canales.

#### Enfoque 2: Uso de entidades de evento {#event-approach}

El segundo método sería utilizar esquemas de eventos para representar un evento de suscripción. Esto incluiría el ID de suscripción junto con un ID de cliente y una marca de tiempo de cuándo se produjo el evento de suscripción.

![Diagrama del esquema de Evento de suscripción con la clase de Evento de experiencia XDM y la estructura de suscripciones resaltadas.](../images/best-practices/event-schema.png)

**Profesionales**

* Las reglas de segmentación pueden ser más flexibles (como encontrar todos los clientes o aquellos que cambiaron sus suscripciones en los últimos 30 días).
* Cuando cambia el estado de suscripción de un cliente, ya no tiene que actualizar una matriz larga y potencialmente compleja dentro de los atributos de perfil del cliente. Esto resulta especialmente útil si se producen cambios simultáneos en la lista de suscripción del cliente desde varias fuentes.

**Inconvenientes**

* La segmentación se vuelve más compleja para el caso de uso previsto original (identificando el estado de las suscripciones más recientes de los clientes). La audiencia ahora necesita una lógica adicional para marcar el último evento de suscripción para que un cliente compruebe su estado.
* Los eventos tienen un mayor riesgo de caducar automáticamente y de purgarse del almacén de perfiles. Consulte la guía sobre [Caducidad de eventos de experiencia](../../profile/event-expirations.md) para obtener más información.

## Cree esquemas basados en las entidades clasificadas {#schemas-for-categorized-entities}

Una vez que haya ordenado las entidades en categorías de perfil, búsqueda y evento, puede empezar a convertir el modelo de datos en esquemas XDM. A efectos de demostración, el modelo de datos de ejemplo mostrado anteriormente se ha ordenado en las categorías adecuadas en el diagrama siguiente:

![Diagrama de los esquemas contenidos en las entidades de perfil, búsqueda y evento](../images/best-practices/erd-sorted.png)

La categoría en la que se ha ordenado una entidad debe determinar la clase XDM en la que se basa su esquema. Para reiterar:

* Las entidades de perfil deben utilizar la clase [!DNL XDM Individual Profile].
* Las entidades de eventos deben utilizar la clase [!DNL XDM ExperienceEvent].
* Las entidades de búsqueda deben utilizar clases XDM personalizadas definidas por su organización. Las entidades de perfil y evento pueden hacer referencia a estas entidades de búsqueda mediante relaciones de esquema.

>[!NOTE]
>
>Aunque las entidades de evento casi siempre se representan mediante esquemas independientes, las entidades de las categorías de perfil o búsqueda pueden combinarse en un único esquema XDM, según su cardinalidad.
>
>Por ejemplo, dado que la entidad Cliente tiene una relación uno a uno con la entidad LoyaltyAccount, el esquema para la entidad Cliente también podría incluir un objeto `LoyaltyAccount` para contener los campos de lealtad adecuados para cada cliente. Sin embargo, si la relación es de uno a varios, la entidad que representa a &quot;varios&quot; puede representarse mediante un esquema independiente o una matriz de atributos de perfil, según su complejidad.

Las secciones a continuación proporcionan una guía general sobre la construcción de esquemas basados en su ERD.

### Adoptar un enfoque de modelado iterativo {#iterative-modeling}

Las [reglas de evolución de esquema](./composition.md#evolution) dictan que solo se pueden realizar cambios no destructivos en los esquemas una vez que se han implementado. En otras palabras, una vez que se agrega un campo a un esquema y se han introducido datos en ese campo, el campo ya no se puede eliminar. Por lo tanto, es esencial adoptar un enfoque de modelado iterativo cuando cree sus esquemas por primera vez, empezando con una implementación simplificada que aumente progresivamente la complejidad con el tiempo.

Si no está seguro de si es necesario incluir un campo en particular en un esquema, la práctica recomendada es dejarlo fuera. Si posteriormente se determina que el campo es necesario, siempre se puede añadir en la siguiente iteración del esquema.

### Campos de identidad {#identity-fields}

En Experience Platform, los campos XDM marcados como identidades se utilizan para unir información sobre clientes individuales procedentes de varias fuentes de datos. Aunque un esquema puede tener varios campos marcados como identidades, se debe definir una sola identidad principal para habilitar el esquema para su uso en [!DNL Real-Time Customer Profile]. Consulte la sección sobre [campos de identidad](./composition.md#identity) en los conceptos básicos de la composición de esquemas para obtener información más detallada sobre el caso de uso de estos campos.

Al diseñar los esquemas, cualquier clave principal de las tablas de bases de datos relacionales es probablemente candidata para identidades principales. Otros ejemplos de campos de identidad aplicables son las direcciones de correo electrónico de los clientes, los números de teléfono, los ID de cuenta y [ECID](../../identity-service/features/ecid.md).

### Grupos de campos de esquema de aplicación de Adobe {#adobe-application-schema-field-groups}

Experience Platform proporciona varios grupos de campos de esquema XDM predeterminados para capturar datos relacionados con las siguientes aplicaciones de Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Por ejemplo, puede utilizar la [[!UICONTROL plantilla de Adobe Analytics ExperienceEvent] grupo de campos](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) para asignar campos específicos de [!DNL Analytics] a sus esquemas XDM. Según las aplicaciones de Adobe con las que trabaje, debe utilizar estos grupos de campos proporcionados por Adobe en los esquemas.

![Diagrama de esquema de la [!UICONTROL plantilla de Adobe Analytics ExperienceEvent].](../images/best-practices/analytics-field-group.png)

Los grupos de campos de aplicación de Adobe asignan automáticamente una identidad principal predeterminada mediante el uso del campo `identityMap`, que es un objeto de solo lectura generado por el sistema que asigna valores de identidad estándar para un cliente individual.

Para Adobe Analytics, ECID es la identidad principal predeterminada. Si un cliente no proporciona un valor ECID, la identidad principal toma el valor predeterminado AAID.

>[!IMPORTANT]
>
>Al utilizar grupos de campos de aplicación de Adobe, no se deben marcar otros campos como la identidad principal. Si hay propiedades adicionales que deben marcarse como identidades, estos campos deben asignarse como identidades secundarias.

## Campos de validación de datos {#data-validation-fields}

Cuando se introducen datos en el lago de datos, la validación de datos solo se impone en el caso de campos restringidos. Para validar un campo determinado durante una ingesta por lotes, debe marcar el campo como restringido en el esquema XDM. Para evitar que se ingieran datos incorrectos en Experience Platform, se recomienda definir los criterios de validación de nivel de campo al crear los esquemas.

>[!IMPORTANT]
>
>La validación no se aplica a columnas anidadas. Si el formato de campo se encuentra dentro de una columna de matriz, los datos no se validan.

Para establecer restricciones en un campo determinado, seleccione el campo en el Editor de esquemas para abrir la barra lateral **[!UICONTROL Propiedades del campo]**. Consulte la documentación sobre [propiedades de campo específicas del tipo](../ui/fields/overview.md#type-specific-properties) para obtener descripciones exactas de los campos disponibles.

![Editor de esquemas con los campos de restricción resaltados en la barra lateral de [!UICONTROL Propiedades del campo].](../images/best-practices/data-validation-fields.png)

### Sugerencias para mantener la integridad de los datos {#data-integrity-tips}

A continuación se muestra una colección de sugerencias para mantener la integridad de los datos al crear un esquema.

* **Tenga en cuenta las identidades principales**: Para productos de Adobe como Web SDK, SDK móvil, Adobe Analytics y Adobe Journey Optimizer, el campo `identityMap` suele servir como identidad principal. Evite designar campos adicionales como identidades principales para ese esquema.
* **Asegúrese de que `_id` no se use como identidad**: el campo `_id` de los esquemas de Experience Event no se puede usar como identidad porque está pensado para la exclusividad de los registros.
* **Establecer restricciones de longitud**: se recomienda establecer longitudes mínimas y máximas en los campos marcados como identidades. Se muestra un déclencheur de advertencia si intenta asignar un área de nombres personalizada a un campo de identidad sin cumplir las restricciones de longitud mínima y máxima. Estas limitaciones ayudan a mantener la coherencia y la calidad de los datos.
* **Aplicar patrones para valores coherentes**: Si los valores de identidad siguen un patrón específico, debe usar la configuración **[!UICONTROL Patrón]** para aplicar esta restricción. Esta configuración puede incluir reglas como solo dígitos, mayúsculas o minúsculas, o combinaciones de caracteres específicas. Utilice expresiones regulares para hacer coincidir patrones en las cadenas.
* **Limitar eVars en esquemas de Analytics**: normalmente, un esquema de Analytics solo debe tener una eVar designada como identidad. Si tiene intención de utilizar más de una eVar como identidad, debe comprobar si la estructura de datos se puede optimizar.
* **Asegúrese de que un campo seleccionado sea único**: el campo elegido debe ser único en comparación con la identidad principal del esquema. Si no es así, no la marque como identidad. Por ejemplo, si varios clientes pueden proporcionar la misma dirección de correo electrónico, ese área de nombres no es una identidad adecuada. Este principio también se aplica a otras áreas de nombres de identidad, como los números de teléfono. Marcar un campo no único como identidad podría provocar el colapso no deseado del perfil.
* **Verificar la longitud mínima de las cadenas**: todos los campos de cadena deben tener al menos un carácter, ya que los valores de cadena nunca deben estar vacíos. Sin embargo, se aceptan valores nulos para los campos no obligatorios. Los nuevos campos de cadena tienen una longitud mínima de uno de forma predeterminada.

## Pasos siguientes

Este documento abarcaba las directrices generales y las prácticas recomendadas para diseñar el modelo de datos para Experience Platform. Para resumir:

* Utilice un enfoque descendente ordenando las tablas de datos en categorías de perfil, búsqueda y evento antes de construir los esquemas.
* A menudo hay varios enfoques y opciones a la hora de diseñar esquemas para diferentes propósitos.
* El modelo de datos debe admitir casos de uso empresarial, como la segmentación o el análisis del recorrido del cliente.
* Simplifique los esquemas lo más posible y solo añada nuevos campos cuando sea absolutamente necesario.

Una vez que esté listo, vea el tutorial de [creación de un esquema en la interfaz de usuario](../tutorials/create-schema-ui.md) para obtener instrucciones paso a paso sobre cómo crear un esquema, asignar la clase adecuada para la entidad y agregar campos a los que asignar los datos.
