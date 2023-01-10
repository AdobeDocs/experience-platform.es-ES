---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;enumeración;identidad principal;identidad principal;perfil individual XDM;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;evento de experiencia;evento de experiencias;evento de experiencias XDM;evento de experiencias XDM;diseño de esquema;prácticas recomendadas
solution: Experience Platform
title: Prácticas Recomendadas Para El Modelado De Datos
description: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se van a utilizar en Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2699'
ht-degree: 2%

---

# Prácticas recomendadas para el modelado de datos

[!DNL Experience Data Model] (XDM) es el marco principal que estandariza los datos de experiencia del cliente proporcionando estructuras y definiciones comunes para su uso en los servicios de Adobe Experience Platform descendentes. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente pueden incorporarse a una representación común que le permite obtener perspectivas valiosas de las acciones del cliente, definir audiencias del cliente mediante segmentos y expresar atributos del cliente con fines de personalización.

Dado que XDM es extremadamente versátil y personalizable por diseño, es importante seguir las prácticas recomendadas para el modelado de datos al diseñar sus esquemas. Este documento cubre las decisiones y consideraciones clave que debe tomar al asignar los datos de experiencia del cliente a XDM.

## Primeros pasos

Antes de leer esta guía, revise la [Información general del sistema XDM](../home.md) para una introducción de alto nivel a XDM y su función en Experience Platform.

Además, esta guía se centra exclusivamente en consideraciones clave relacionadas con el diseño de esquemas. Por lo tanto, es muy recomendable consultar la [conceptos básicos de la composición del esquema](./composition.md) para obtener explicaciones detalladas de los elementos de esquema individuales mencionados en esta guía.

## Resumen de prácticas recomendadas

El método recomendado para diseñar el modelo de datos para su uso en Experience Platform puede resumirse de la siguiente manera:

1. Comprender los casos de uso empresarial de sus datos.
1. Identificar las fuentes de datos principales en las que se debe importar [!DNL Platform] para tratar estos casos de uso.
1. Identifique las fuentes de datos secundarias que también puedan ser de interés. Por ejemplo, si actualmente solo una unidad de negocio de su organización está interesada en transferir sus datos a [!DNL Platform], una unidad de negocio similar también podría estar interesada en portar datos similares en el futuro. Si tiene en cuenta estas fuentes secundarias, podrá estandarizar el modelo de datos en toda la organización.
1. Cree un diagrama de relación de entidad (ERD) de alto nivel para las fuentes de datos que se han identificado.
1. Conversión del ERD de alto nivel en un [!DNL Platform]ERD centrado en : (incluidos perfiles, eventos de experiencia y entidades de búsqueda).

Los pasos relacionados con la identificación de las fuentes de datos aplicables que se requieren para llevar a cabo los casos de uso comercial variarán de una organización a otra. Mientras que el resto de las secciones de este documento se centran en los últimos pasos de organización y construcción de un ERD después de que se hayan identificado las fuentes de datos, las explicaciones de los diversos componentes del diagrama pueden servir de base para sus decisiones sobre cuál de sus fuentes de datos debe migrarse a [!DNL Platform].

## Crear un ERD de alto nivel

Una vez que haya determinado las fuentes de datos en las que desea importar [!DNL Platform], cree un ERD de alto nivel para ayudar a guiar el proceso de asignación de datos a esquemas XDM.

El ejemplo siguiente representa un ERD simplificado para una empresa que desea introducir datos en [!DNL Platform]. El diagrama destaca las entidades esenciales que deben clasificarse en clases XDM, incluidas cuentas de cliente, hoteles, direcciones y varios eventos de comercio electrónico comunes.

![](../images/best-practices/erd.png)

## Ordenar entidades en categorías de perfil, búsqueda y evento

Una vez que haya creado un ERD para identificar las entidades esenciales que desea incorporar [!DNL Platform], estas entidades deben ordenarse en categorías de perfil, búsqueda y evento:

| Categoría | Descripción |
| --- | --- |
| Entidades de perfil | Las entidades de perfil representan atributos relacionados con una persona individual, normalmente un cliente. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable **[!DNL XDM Individual Profile]class**. |
| Entidades de búsqueda | Las entidades de búsqueda representan conceptos que pueden relacionarse con una persona individual, pero que no se pueden utilizar directamente para identificar a dicha persona. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en **clases personalizadas**. |
| Entidades de eventos | Las entidades de eventos representan conceptos relacionados con acciones que un cliente puede realizar, eventos del sistema o cualquier otro concepto en el que desee rastrear cambios a lo largo del tiempo. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable **[!DNL XDM ExperienceEvent]class**. |

{style=&quot;table-layout:auto&quot;}

### Consideraciones para la ordenación de entidades

Las secciones a continuación proporcionan una guía adicional sobre cómo clasificar las entidades en las categorías anteriores.

#### Datos mutables e inmutables

Una manera principal de clasificar entre categorías de entidades es si los datos que se capturan son mutables o no.

Los atributos que pertenecen a perfiles o entidades de búsqueda suelen ser mutables. Por ejemplo, las preferencias de un cliente pueden cambiar con el tiempo y los parámetros de un plan de suscripción pueden actualizarse en función de las tendencias del mercado.

Por el contrario, los datos de evento suelen ser inmutables. Dado que los eventos se adjuntan a una marca de tiempo específica, la &quot;instantánea del sistema&quot; que proporciona un evento no cambia. Por ejemplo, un evento puede capturar las preferencias de un cliente cuando cierra la compra y no cambia aunque las preferencias del cliente terminen cambiando más adelante. Los datos de evento no se pueden cambiar una vez registrados.

En resumen, los perfiles y las entidades de búsqueda contienen atributos mutables y representan la información más actual sobre los temas que capturan, mientras que los eventos son registros inmutables del sistema en un momento específico.

#### Atributos del cliente

Si una entidad contiene atributos relacionados con un cliente individual, lo más probable es que sea una entidad de perfil. Algunos ejemplos de atributos del cliente son:

* Detalles personales como nombre, fecha de nacimiento, sexo e ID de cuenta.
* Información de ubicación como direcciones e información de GPS.
* Información de contacto como números de teléfono y direcciones de correo electrónico.

#### Seguimiento de datos a lo largo del tiempo

Si desea analizar cómo cambian con el tiempo ciertos atributos dentro de una entidad, lo más probable es que se trate de una entidad de evento. Por ejemplo, agregar elementos de producto a un carro de compras se puede rastrear como eventos de complementos en el carro de compras en [!DNL Platform]:

| Customer ID | Tipo | ID del producto | Cantidad | Marca de tiempo |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1 de octubre, 10:32 AM |
| 1234567 | Eliminar | 275098 | 1 | 1 de octubre, 10:33 AM |
| 1234567 | Add | 486502 | 1 | 1 de octubre, 10:41 AM |
| 1234567 | Add | 910482 | 5 | 3 de octubre, 2:15 PM |

{style=&quot;table-layout:auto&quot;}

#### Casos de uso de segmentación

Al categorizar las entidades, es importante tener en cuenta los segmentos de audiencia que puede que desee generar para abordar sus casos de uso comerciales específicos.

Por ejemplo, una empresa quiere conocer todos los miembros de &quot;Gold&quot; o &quot;Platinum&quot; de su programa de fidelidad que han realizado más de cinco compras en el último año. Basándose en esta lógica de segmento, se pueden sacar las siguientes conclusiones sobre cómo se deben representar las entidades relevantes:

* &quot;Gold&quot; y &quot;Platinum&quot; representan estados de lealtad aplicables a un cliente individual. Dado que la lógica del segmento solo está relacionada con el estado de lealtad actual de los clientes, estos datos se pueden modelar como parte de un esquema de perfil. Si desea rastrear los cambios en el estado de lealtad con el paso del tiempo, también puede crear un esquema de evento adicional para los cambios de estado de lealtad.
* Las compras son eventos que se producen en un momento concreto y la lógica del segmento está relacionada con los eventos de compra dentro de un período de tiempo especificado. Por lo tanto, estos datos deben modelarse como un esquema de evento.

#### Casos de uso de activación

Además de las consideraciones relativas a los casos de uso de segmentación, también debe revisar los casos de uso de activación de dichos segmentos para identificar atributos relevantes adicionales.

Por ejemplo, una empresa ha creado un segmento de audiencia basado en la regla que `country = US`. A continuación, al activar ese segmento en determinados destinos de flujo descendente, la empresa desea filtrar todos los perfiles exportados en función del estado de origen. Por lo tanto, `state` también debe capturarse en la entidad de perfil aplicable.

#### Valores agregados

En función del caso de uso y la granularidad de los datos, debe decidir si ciertos valores deben agregarse previamente antes de incluirse en un perfil o entidad de evento.

Por ejemplo: una empresa desea generar un segmento basado en el número de compras del carro de compras. Puede elegir incorporar estos datos a la granularidad más baja incluyendo cada evento de compra con marca de tiempo como su propia entidad. Sin embargo, esto a veces puede aumentar el número de eventos registrados de forma exponencial. Para reducir el número de eventos introducidos, puede elegir crear un valor agregado `numberOfPurchases` durante un período de una semana o de un mes. Otras funciones agregadas como MIN y MAX también se pueden aplicar a estas situaciones.

>[!CAUTION]
>
>Actualmente, el Experience Platform no realiza la agregación automática de valores, aunque esto está planificado para futuras versiones. Si decide utilizar valores agregados, debe realizar los cálculos de forma externa antes de enviar los datos a [!DNL Platform].

#### Cardinalidad

Las cardinalidades establecidas en su ERD también pueden proporcionar algunas pistas sobre cómo categorizar sus entidades. Si hay una relación &quot;uno a varios&quot; entre dos entidades, la entidad que representa &quot;muchos&quot; probablemente sea una entidad de evento. Sin embargo, también hay casos en los que &quot;muchos&quot; es un conjunto de entidades de búsqueda que se proporcionan como una matriz dentro de una entidad de perfil.

>[!NOTE]
>
>Dado que no existe un enfoque universal que se ajuste a todos los casos de uso, es importante tener en cuenta las ventajas y desventajas de cada situación cuando se clasifican las entidades en función de la cardinalidad. Consulte la [sección siguiente](#pros-and-cons) para obtener más información.

La siguiente tabla describe algunas relaciones de entidad comunes y las categorías que se pueden derivar de ellas:

| Relación | Cardinalidad | Categorías de entidades |
| --- | --- | --- |
| Clientes y cierres de compra | Uno a muchos | Un único cliente puede tener muchas cierres de compra, que son eventos que se pueden rastrear con el tiempo. Por lo tanto, los clientes serían una entidad de perfil, mientras que las cierres de compra del carro serían una entidad de evento. |
| Clientes y cuentas de fidelidad | Uno a uno | Un único cliente solo puede tener una cuenta de fidelidad y viceversa. Dado que la relación es uno a uno, tanto los clientes como las cuentas de fidelidad representan entidades de perfil. |
| Clientes y suscripciones | Uno a muchos | Un solo cliente puede tener muchas suscripciones. Dado que la empresa solo está preocupada por las suscripciones actuales de un cliente, Customers es una entidad de perfil, mientras que Subscriptions es una entidad de búsqueda. |

{style=&quot;table-layout:auto&quot;}

### Ventajas y desventajas de diferentes clases de entidades {#pros-and-cons}

Aunque la sección anterior ofrecía algunas directrices generales para decidir cómo categorizar las entidades, es importante comprender que a menudo puede haber ventajas y desventajas para elegir una categoría de entidad en lugar de otra. El siguiente caso práctico tiene por objeto ilustrar cómo puede considerar las opciones en estas situaciones.

Una empresa rastrea las suscripciones activas para sus clientes, donde un cliente puede tener muchas suscripciones. La empresa también desea incluir suscripciones para casos de uso de segmentación, como la búsqueda de todos los usuarios con suscripciones activas.

En esta situación, la empresa tiene dos opciones posibles para representar las suscripciones de un cliente en su modelo de datos:

1. [Uso de atributos de perfil](#profile-approach)
1. [Uso de entidades de eventos](#event-approach)

#### Enfoque 1: Uso de atributos de perfil {#profile-approach}

El primer método sería incluir una matriz de suscripciones como atributos dentro de la entidad de perfil para los clientes. Los objetos de esta matriz contendrían campos para `category`, `status`, `planName`, `startDate`y `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Pros**

* La segmentación es viable para el caso de uso deseado.
* El esquema solo conserva los registros de suscripción más recientes para un cliente.

**Contras**

* La matriz completa debe reiniciarse cada vez que se produzcan cambios en cualquier campo de la matriz.
* Si diferentes fuentes de datos o unidades de negocio están incluyendo datos en el arreglo de discos, será difícil mantener sincronizado el arreglo de discos actualizado más reciente en todos los canales.

#### Enfoque 2: Uso de entidades de eventos {#event-approach}

El segundo método sería utilizar esquemas de eventos para representar suscripciones. Esto implica la ingesta de los mismos campos de suscripción que el primer método, con la adición de un ID de suscripción, un ID de cliente y una marca de tiempo del momento en el que se produjo el evento de suscripción.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Pros**

* Las reglas de segmentación pueden ser más flexibles (por ejemplo, para encontrar todos los clientes que han cambiado sus suscripciones en los últimos 30 días).
* Cuando cambia el estado de suscripción de un cliente, ya no tiene que actualizar una matriz larga y potencialmente compleja dentro de los atributos de perfil del cliente. Esto resulta especialmente útil si se producen cambios simultáneos en la lista de suscripción del cliente desde varias fuentes.

**Contras**

* La segmentación se vuelve más compleja para el caso de uso previsto original (identificación del estado de las suscripciones más recientes de los clientes). El segmento ahora necesita lógica adicional para marcar el último evento de suscripción de un cliente para comprobar su estado.
* Los eventos tienen un mayor riesgo de caducar automáticamente y de purgarse del almacén de perfiles. Consulte la guía de [Caducidad de eventos de experiencia](../../profile/event-expirations.md) para obtener más información.

## Crear esquemas basados en las entidades clasificadas

Una vez que haya clasificado las entidades en categorías de perfil, búsqueda y evento, puede empezar a convertir el modelo de datos en esquemas XDM. Para fines de demostración, el modelo de datos de ejemplo que se muestra anteriormente se ha clasificado en las categorías adecuadas en el diagrama siguiente:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

La categoría en la que se ha ordenado una entidad debe determinar la clase XDM en la que se basa su esquema. Para reiterar:

* Las entidades de perfil deben usar la variable [!DNL XDM Individual Profile] Clase .
* Las entidades de eventos deben utilizar la variable [!DNL XDM ExperienceEvent] Clase .
* Las entidades de búsqueda deben utilizar clases XDM personalizadas definidas por su organización.

>[!NOTE]
>
>Aunque las entidades de evento casi siempre se representarán mediante esquemas separados, las entidades del perfil o de las categorías de búsqueda se pueden combinar en un único esquema XDM, según su cardinalidad.
>
>Por ejemplo, como la entidad Customers tiene una relación uno a uno con la entidad LoyaltyAccounts , el esquema de la entidad Customers también puede incluir un `LoyaltyAccount` para que contenga los campos de fidelidad adecuados para cada cliente. Sin embargo, si la relación es de uno a muchos, la entidad que representa los &quot;muchos&quot; podría representarse mediante un esquema separado o una matriz de atributos de perfil, según su complejidad.

Las secciones siguientes proporcionan directrices generales sobre la construcción de esquemas basados en su ERD.

### Adoptar un enfoque de modelado iterativo

La variable [reglas de evolución de esquema](./composition.md#evolution) dicte que solo se puedan realizar cambios no destructivos en los esquemas una vez implementados. En otras palabras, una vez que se agrega un campo a un esquema y se han introducido datos para ese campo, el campo ya no se puede eliminar. Por lo tanto, es esencial adoptar un enfoque de modelado iterativo cuando se crean los esquemas por primera vez, empezando por una implementación simplificada que aumenta progresivamente la complejidad con el paso del tiempo.

Si no está seguro de si es necesario incluir un campo concreto en un esquema, la práctica recomendada es excluirlo. Si posteriormente se determina que el campo es necesario, siempre se puede añadir en la siguiente iteración del esquema.

### Campos de identidad

En Experience Platform, los campos XDM marcados como identidades se utilizan para unir información sobre clientes individuales provenientes de varias fuentes de datos. Aunque un esquema puede tener varios campos marcados como identidades, se debe definir una sola identidad principal para que el esquema esté habilitado para utilizarse en [!DNL Real-Time Customer Profile]. Consulte la sección sobre [campos de identidad](./composition.md#identity) en los conceptos básicos de la composición del esquema para obtener información más detallada sobre el caso de uso de estos campos.

Al diseñar los esquemas, cualquier clave principal en las tablas de la base de datos relacional probablemente será el candidato para identidades principales. Otros ejemplos de campos de identidad aplicables son direcciones de correo electrónico del cliente, números de teléfono, ID de cuenta y [ECID](../../identity-service/ecid.md).

### Adobe grupos de campos de esquema de aplicación

El Experience Platform proporciona varios grupos de campos de esquema XDM listos para usar para capturar datos relacionados con las siguientes aplicaciones de Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Por ejemplo, la variable [[!UICONTROL Plantilla de Adobe Analytics ExperienceEvent] grupo de campos](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) le permite asignar [!DNL Analytics]Campos específicos de los esquemas XDM. Según las aplicaciones de Adobe con las que esté trabajando, debe utilizar estos grupos de campos proporcionados por Adobe en los esquemas.

<img src="../images/best-practices/analytics-field-group.png" width="700"><br>

Los grupos de campos de la aplicación de Adobe asignan automáticamente una identidad principal predeterminada mediante el uso de la variable `identityMap` , que es un objeto de solo lectura generado por el sistema que asigna valores de identidad estándar para un cliente individual.

Para Adobe Analytics, ECID es la identidad principal predeterminada. Si un cliente no proporciona un valor ECID, la identidad principal pasará a ser AAID de forma predeterminada.

>[!IMPORTANT]
>
>Cuando se utilizan grupos de campos de aplicación de Adobe, no se debe marcar ningún otro campo como identidad principal. Si hay propiedades adicionales que deben marcarse como identidades, estos campos deben asignarse como identidades secundarias en su lugar.

## Pasos siguientes

Este documento abarcaba las directrices generales y las prácticas recomendadas para diseñar el modelo de datos para el Experience Platform. Para resumir:

* Utilice un método descendente ordenando las tablas de datos en categorías de perfil, búsqueda y evento antes de crear los esquemas.
* A menudo hay múltiples enfoques y opciones cuando se trata de diseñar esquemas para diferentes propósitos.
* El modelo de datos debe admitir casos de uso empresariales, como la segmentación o el análisis de recorrido de clientes.
* Haga los esquemas lo más simples posible y añada campos nuevos solo cuando sea absolutamente necesario.

Una vez que esté listo, consulte el tutorial en [creación de un esquema en la interfaz de usuario](../tutorials/create-schema-ui.md) para obtener instrucciones paso a paso sobre cómo crear un esquema, asigne la clase adecuada para la entidad y añada campos a los que asignar los datos.
