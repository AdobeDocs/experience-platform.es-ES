---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;políticas de combinación;interfaz de usuario;interfaz de usuario;marca de tiempo solicitada;prioridad del conjunto de datos
title: Información general sobre políticas de combinación
type: Documentation
description: Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de sus clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.
source-git-commit: c2cc1428e3a70cf987adab583e9f9fb5d5140c74
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---


# Información general sobre las directivas de combinación

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.

Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización. Este documento proporciona información general sobre las políticas de combinación y la función que desempeñan en el Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de varias funciones [!DNL Experience Platform] importantes. Antes de seguir esta guía y trabajar con políticas de combinación, revise la documentación de los siguientes servicios:

* [Perfil](../home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Habilita el perfil del cliente en tiempo real al unir identidades de fuentes de datos dispares que se están incorporando en  [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

## Conceptos básicos de las políticas de combinación

Adobe Experience Platform le permite unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa y unificada de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente.

Cuando los datos de múltiples fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;soltero&quot; mientras que el otro indica que el cliente está &quot;casado&quot;), la política de combinación determina qué información incluir en el perfil del individuo.

Las políticas de combinación son privadas para su organización de IMS, lo que le permite crear distintas políticas para combinar esquemas de las formas específicas que necesite. También puede especificar una directiva de combinación predeterminada que se utilizará si no se proporciona explícitamente. Consulte la sección [políticas de combinación predeterminadas](#default-merge-policy) más adelante en este documento para obtener más información.

## Métodos de combinación {#merge-methods}

Cada fragmento de perfil contiene información para una sola identidad del número total de identidades que podría existir para un individuo. Al combinar esos datos para formar un perfil de cliente, existe la posibilidad de que esa información entre en conflicto y se debe especificar la prioridad.

La selección de un método de combinación le permite especificar qué atributos del conjunto de datos priorizar si se produce un conflicto de combinación entre conjuntos de datos.

Hay dos métodos de combinación disponibles para las directivas de combinación. A continuación se resumen cada uno de estos métodos y se proporcionan detalles adicionales en las secciones siguientes:

* **[!UICONTROL Prioridad] del conjunto de datos:** en caso de conflicto, asigne prioridad a los fragmentos de perfil según el conjunto de datos del que procedan. Al seleccionar esta opción, debe elegir los conjuntos de datos relacionados y su orden de prioridad. Obtenga más información sobre el método de combinación [precedencia del conjunto de datos](#dataset-precedence).
* **[!UICONTROL Marca de tiempo solicitada]:** En caso de conflicto, se da prioridad al fragmento de perfil que se actualizó más recientemente. Obtenga más información sobre el método de combinación [timestamp ordered](#timestamp-ordered).
   * **Marcas de hora personalizadas:** el método de combinación ordenada de marcas de hora también admite marcas de hora personalizadas que tienen prioridad sobre las marcas de hora del sistema al combinar datos dentro del mismo conjunto de datos (varias identidades) o entre conjuntos de datos. Para obtener más información, consulte la sección sobre [uso de marcas de hora personalizadas](#custom-timestamps).

### Prioridad del conjunto de datos {#dataset-precedence}

Cuando se selecciona **[!UICONTROL Prioridad del conjunto de datos]** como método de combinación para una política de combinación, se puede dar prioridad a los fragmentos de perfil en función del conjunto de datos del que provienen. Un caso de uso de ejemplo sería si su organización tuviera información presente en un conjunto de datos que es preferible o de confianza sobre los datos de otro conjunto de datos.

Para crear una directiva de combinación utilizando **[!UICONTROL Dataset priority]**, debe seleccionar los conjuntos de datos de Perfil y ExperienceEvent que se incluyen y, a continuación, puede ordenar manualmente los conjuntos de datos de Perfil para que tengan prioridad. Una vez seleccionados y ordenados los conjuntos de datos, se asignará la prioridad más alta al conjunto de datos superior, el segundo será el segundo más alto, y así sucesivamente.

### Marca de tiempo solicitada {#timestamp-ordered}

A medida que los registros de perfil se incorporan al Experience Platform, se obtiene una marca de tiempo del sistema en el momento de la ingesta y se agrega al registro. Cuando se selecciona **[!UICONTROL Timestamp ordered]** como método de combinación para una directiva de combinación, los perfiles se combinan en función de la marca de tiempo del sistema. En otras palabras, la combinación se realiza en función de la marca de tiempo para cuando el registro se incorporó a Platform.

#### Uso de marcas de hora personalizadas {#custom-timestamps}

En ocasiones puede haber casos de uso en los que sea necesario proporcionar una marca de tiempo personalizada y en los que la política de combinación respete la marca de tiempo personalizada en lugar de la marca de tiempo del sistema. Algunos ejemplos de esto son rellenar los datos o garantizar el orden correcto de los eventos si los registros se introducen de forma desordenada.

Para utilizar una marca de tiempo personalizada, el grupo de campos de esquema **[!UICONTROL External Source System Audit Details]** debe agregarse al esquema de perfil. Una vez añadida, la marca de tiempo personalizada se puede rellenar con el campo `lastUpdatedDate` . Cuando se ingesta un registro con el campo `lastUpdatedDate` rellenado, el Experience Platform utilizará ese campo para combinar registros entre conjuntos de datos. Si `lastUpdatedDate` no está presente o no se rellena, Platform seguirá usando la marca de tiempo del sistema.

>[!NOTE]
>
>Debe asegurarse de que la marca de tiempo `lastUpdatedDate` se rellene al ingerir una actualización en el mismo registro.

La siguiente captura de pantalla muestra los campos del grupo de campos [!UICONTROL External Source System Audit Details]. Para obtener instrucciones paso a paso sobre cómo trabajar con esquemas mediante la interfaz de usuario de Platform, incluido cómo añadir grupos de campos a esquemas, visite el [tutorial para crear un esquema con la IU](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-field-group.png)

Para trabajar con marcas de hora personalizadas mediante la API, consulte la sección [guía de extremo de directivas de combinación sobre el uso de marcas de hora personalizadas](../api/merge-policies.md#custom-timestamps).

## Vinculación de identidad {#id-stitching}

La vinculación de identidad ([!UICONTROL identificación]) es el proceso de identificación de fragmentos de datos y de combinación para formar un registro de perfil completo. Para ayudar a ilustrar los diferentes comportamientos de vinculación, considere un cliente único que interactúa con una marca utilizando dos direcciones de correo electrónico diferentes.

* **[!UICONTROL Ninguno]:** Cuando se selecciona esta opción, los ID no se vinculan. Cuando se produce la segmentación, las identidades que pueden pertenecer a la misma persona no se vinculan y la segmentación solo tendrá en cuenta los atributos adjuntos a cada ID individual al determinar si un cliente cumple los requisitos para pertenecer a un segmento. Esto podría hacer que un único cliente tenga varios perfiles y cada perfil cumpla los requisitos para segmentos diferentes, lo que resultaría en que se envíen varios mensajes de marketing al mismo cliente.
* **[!UICONTROL Gráfico privado]:** cuando se selecciona el gráfico privado, se vinculan varias identidades relacionadas con la misma persona. Esto hace que el cliente tenga un solo perfil y permite que la segmentación tenga en cuenta múltiples atributos de varias identidades relacionadas al determinar la calificación del segmento. En este escenario, es probable que el cliente tenga un solo perfil, cumpla los requisitos de un segmento en función de la combinación de atributos entre identidades y reciba solo un mensaje de marketing.

Para obtener más información sobre las identidades y su función en la generación de perfiles y segmentos, lea por favor la [descripción general del servicio de identidad](../../identity-service/home.md).

## Directiva de combinación predeterminada {#default-merge-policy}

Una organización puede crear una directiva de combinación predeterminada para que la utilice su organización al combinar fragmentos de perfil. Esto permite a los usuarios seleccionar fácilmente la directiva predeterminada al realizar acciones en el Experience Platform, como ver perfiles de clientes o crear segmentos. En la mayoría de los casos, a menos que se especifique otra directiva de combinación, se utilizará la directiva de combinación predeterminada.

Cada organización puede crear varias políticas de combinación relacionadas con una sola clase de esquema XDM, pero solo puede declararse una política de combinación predeterminada para cada clase. Por ejemplo, su organización podría tener una directiva de combinación predeterminada relacionada con la clase [!DNL XDM Individual Profile] y una directiva de combinación predeterminada diferente para una clase de inventario de productos personalizada.

Si crea una nueva directiva de combinación y la establece como predeterminada, el sistema actualizará automáticamente la directiva de combinación predeterminada anterior para que ya no sea la predeterminada.

>[!WARNING]
>
>Los recuentos de perfiles y los segmentos con una política de combinación predeterminada asociada existente pueden verse afectados. Cualquier segmento que tenga aplicada una directiva de combinación predeterminada se actualizará a la nueva directiva de combinación predeterminada.

## Pasos siguientes

Después de leer esta guía, ahora sabe qué son las políticas de combinación y la función que desempeñan dentro de Experience Platform. Para empezar a trabajar con políticas de combinación en la interfaz de usuario del Experience Platform, consulte la [guía de la interfaz de usuario de directivas de combinación](ui-guide.md). Para trabajar con políticas de combinación usando la API, visite la [guía de extremo de la API de directivas de combinación](../api/merge-policies.md).