---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;políticas de combinación;IU;interfaz de usuario;marca de tiempo ordenada;prioridad de conjuntos de datos
title: Resumen de políticas de combinación
type: Documentation
description: Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada cliente. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear la vista unificada.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 1%

---

# Información general de las políticas de combinación

Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear una vista unificada.

Mediante las API de RESTful o la interfaz de usuario de, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización. Este documento proporciona información general sobre las políticas de combinación y la función que desempeñan en Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de varias características importantes de [!DNL Experience Platform]. Antes de seguir esta guía y trabajar con las políticas de combinación, revise la documentación de los siguientes servicios:

* [Perfil del cliente en tiempo real](../home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): habilita el perfil del cliente en tiempo real al unir identidades de diferentes fuentes de datos que se están ingiriendo en [!DNL Platform].
* [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

## Explicación de las políticas de combinación

Adobe Experience Platform permite reunir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa y unificada de cada uno de los clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que utiliza Platform para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Platform, se combinan para crear un único perfil para ese cliente.

Cuando los datos de varias fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;único&quot;, mientras que el otro indica al cliente como &quot;casado&quot;), la política de combinación determina qué información se incluye en el perfil de la persona.

Las políticas de combinación son privadas para su organización, lo que le permite crear diferentes políticas para combinar esquemas de las formas específicas que necesite. También puede especificar una política de combinación predeterminada que se utilizará si no se proporciona una de forma explícita. Consulte la sección sobre [políticas de combinación predeterminadas](#default-merge-policy) más adelante en este documento para obtener más información. Tenga en cuenta que se permite un máximo de cinco políticas de combinación por organización.

## Métodos de combinación {#merge-methods}

Cada fragmento de perfil contiene información para una sola identidad de la cantidad total de identidades que podrían existir para un individuo. Al combinar esos datos para formar un perfil de cliente, existe la posibilidad de que esa información entre en conflicto y se deba especificar la prioridad.

La selección de un método de combinación le permite especificar qué atributos del conjunto de datos priorizar si se produce un conflicto de combinación entre conjuntos de datos.

Existen dos métodos de combinación posibles para las políticas de combinación. Cada uno de estos métodos se resume a continuación con detalles adicionales proporcionados en las secciones siguientes:

* **[!UICONTROL Prioridad de conjuntos de datos]:** En caso de conflicto, dé prioridad a los fragmentos de perfil en función del conjunto de datos del que procedan. Al seleccionar esta opción, debe elegir los conjuntos de datos relacionados y su orden de prioridad. Más información sobre el método de combinación [prioridad de conjuntos de datos](#dataset-precedence).
* **[!UICONTROL Marca de tiempo solicitada]:** En caso de conflicto, se da prioridad al fragmento de perfil que se actualizó más recientemente. Más información sobre el método de combinación [timestamp ordered](#timestamp-ordered).

### Prioridad de conjuntos de datos {#dataset-precedence}

Cuando se selecciona **[!UICONTROL Prioridad de conjuntos de datos]** como método de combinación para una política de combinación, puede dar prioridad a los fragmentos de perfil en función del conjunto de datos del que proceden. Un ejemplo de uso sería si su organización tuviera información presente en un conjunto de datos que es preferible o de confianza sobre los datos de otro conjunto de datos.

Para crear una política de combinación con **[!UICONTROL Prioridad de conjuntos de datos]**, debe seleccionar los conjuntos de datos de perfil y ExperienceEvent que se incluyen y, a continuación, puede ordenar manualmente la prioridad de los conjuntos de datos de perfil. Una vez seleccionados y ordenados los conjuntos de datos, el conjunto de datos superior tendrá la prioridad más alta, el segundo conjunto de datos será el segundo más alto, y así sucesivamente.

### Marca de tiempo solicitada {#timestamp-ordered}

A medida que los registros de perfil se incorporan a Experience Platform, se obtiene una marca de tiempo del sistema en el momento de la ingesta y se añade al registro. Cuando se selecciona **[!UICONTROL Marca de tiempo solicitada]** como método de combinación para una política de combinación, los perfiles se combinan según la marca de tiempo del sistema. En otras palabras, la combinación se realiza en función de la marca de tiempo del momento en el que se incorporó el registro en Platform.

## Vinculación de identidad {#id-stitching}

La vinculación de identidad ([!UICONTROL vinculación de ID]) es el proceso de identificar fragmentos de datos y combinarlos para formar un registro de perfil completo. Para ilustrar los diferentes comportamientos de vinculación, considere la posibilidad de un solo cliente que interactúe con una marca mediante dos direcciones de correo electrónico diferentes.

* **[!UICONTROL Ninguno]:** Cuando se selecciona esta opción, los identificadores no se vincularán. Cuando se produce la segmentación, las identidades que puedan pertenecer a la misma persona no se vinculan, y la segmentación solo tendrá en cuenta los atributos adjuntos a cada ID individual al determinar si un cliente cumple los requisitos para pertenecer a la audiencia. Esto podría hacer que un solo cliente tenga varios perfiles y que cada perfil cumpla los requisitos de audiencias diferentes, lo que provocaría que se enviaran varios mensajes de marketing al mismo cliente.
* **[!UICONTROL Gráfico privado]:** Cuando se selecciona el gráfico privado, se vinculan varias identidades relacionadas con el mismo individuo. Esto hace que el cliente tenga un único perfil y permite que la segmentación tenga en cuenta varios atributos de varias identidades relacionadas al determinar la calificación del segmento. En esta situación, es probable que el cliente tenga un solo perfil, cumpla los requisitos de una audiencia en función de la combinación de atributos entre identidades y reciba solo un mensaje de marketing.

Para obtener más información acerca de las identidades y su función en la generación de perfiles y audiencias, comience por leer la [descripción general del servicio de identidad](../../identity-service/home.md).

## Política de combinación predeterminada {#default-merge-policy}

Una organización puede crear una política de combinación predeterminada para que la organización la utilice al combinar fragmentos de perfil. Esto permite a los usuarios seleccionar fácilmente la directiva predeterminada al realizar acciones en Experience Platform, como ver perfiles de clientes o crear audiencias. En la mayoría de los casos, a menos que se especifique otra política de combinación, se utilizará la política de combinación predeterminada.

Cada organización puede crear varias políticas de combinación relacionadas con una sola clase de esquema XDM, pero solo puede tener una política de combinación predeterminada declarada para cada clase. Por ejemplo, su organización podría tener una política de combinación predeterminada relacionada con la clase [!DNL XDM Individual Profile] y una política de combinación predeterminada diferente para una clase de inventario de productos personalizada.

Si crea una nueva política de combinación y la establece como predeterminada, el sistema actualizará automáticamente la política de combinación predeterminada anterior para que ya no sea la predeterminada.

>[!WARNING]
>
>Los recuentos de perfiles y las audiencias con una política de combinación predeterminada asociada existente pueden verse afectados. Cualquier audiencia que tenga aplicada una política de combinación predeterminada se actualizará a la nueva política de combinación predeterminada.

## Pasos siguientes

Después de leer esta guía, ahora sabe qué son las políticas de combinación y la función que desempeñan dentro del Experience Platform. Para empezar a trabajar con políticas de combinación en la interfaz de usuario del Experience Platform, consulte la [guía de la interfaz de usuario de las políticas de combinación](ui-guide.md). Para trabajar con políticas de combinación mediante la API, visite la [guía de extremo de API de políticas de combinación](../api/merge-policies.md).
