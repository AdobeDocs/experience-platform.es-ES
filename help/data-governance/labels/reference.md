---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas;etiquetas de uso de datos admitidas;etiquetas de contrato;etiquetas de identidad;etiquetas confidenciales
solution: Experience Platform
title: Glosario de etiquetas de uso de datos
description: Este documento describe todas las etiquetas de uso de datos que admite Adobe Experience Platform en la actualidad.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 7%

---

# Glosario de etiquetas de uso de datos {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipos de etiquetas"
>abstract="Existen varias categorías de etiquetas de uso de datos. Las etiquetas definidas por Adobe incluyen etiquetas de contrato, de identidad y confidenciales. Las etiquetas definidas por su organización se clasifican como etiquetas personalizadas."
>text="See the data usage labels glossary for more information on these label types."

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según [políticas de gobernanza](../policies/overview.md) y [políticas de control de acceso](../../access-control/abac/overview.md) que se aplican a esos datos. Adobe Experience Platform proporciona varias etiquetas de uso de datos principales listas para usarse que puede utilizar para categorizar los datos.

Este documento describe las etiquetas de uso de datos principales que proporciona actualmente Experience Platform.

## Etiquetas de contrato {#contract}

Las etiquetas del contrato &quot;C&quot; se utilizan para categorizar los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos de su organización.

| Etiqueta | Definición |
| --- | --- |
| [C1](#c1) | Los datos solo se pueden exportar desde Adobe Experience Cloud de forma agregada sin incluir identificadores individuales o de dispositivo. |
| [C2](#c2) | Los datos no se pueden exportar a terceros. |
| [C3](#c3) | Los datos no se pueden combinar ni utilizar de otro modo con información directamente identificable. |
| [C4](#c4) | Los datos no pueden utilizarse para segmentar anuncios o contenido, ya sea en el sitio o entre sitios. |
| [C5](#c5) | Los datos no pueden utilizarse para la segmentación de contenido o anuncios entre sitios basada en intereses. |
| [C6](#c6) | Los datos no pueden utilizarse para la segmentación de anuncios en el sitio. |
| [C7](#c7) | Los datos no pueden utilizarse para la segmentación de contenido en el sitio. |
| [C8](#c8) | Los datos no pueden utilizarse para medir los sitios web o las aplicaciones de la organización. |
| [C9](#c9) | Los datos no se pueden usar en flujos de trabajo de ciencia de datos. |
| [C10](#c10) | Los datos no se pueden usar para la activación de identidad vinculada. |
| [C11](#c11) | Los datos no se pueden compartir con socios de coincidencia de segmentos. |
| [C12](#c12) | Los datos no se pueden exportar de ninguna manera. |

## Etiquetas de identidad {#identity}

Las etiquetas de identidad “I” se utilizan para categorizar datos que pueden identificar o usarse para contactar a una persona específica.

| Etiqueta | Definición |
| --- | --- |
| **I1** | Datos directamente identificables que permiten identificar a una persona específica o ponerse en contacto con ella, en lugar de un dispositivo. |
| **I2** | Datos indirectamente identificables que pueden utilizarse en combinación con otros datos para identificar a una persona específica o ponerse en contacto con ella. |

## Etiquetas confidenciales {#sensitive}

Las etiquetas confidenciales &quot;S&quot; se utilizan para categorizar los datos que usted y su organización consideran confidenciales.

Un tipo de datos que puede considerar confidencial puede ser un tipo diferente de datos geográficos; sin embargo, esta categoría no se limita a los datos geográficos.

| Etiqueta | Definición |
| --- | --- |
| **S1** | Datos que especifican la latitud y longitud que pueden utilizarse para determinar la ubicación exacta de un dispositivo. |
| **S2** | Datos que pueden utilizarse para determinar un área de geovalla definida en sentido amplio. |
| **PSPD** | Los datos personales confidenciales permitidos (PSPD) se refieren a datos que Adobe le permite cargar de forma contractual y que se consideran &quot;confidenciales&quot;, &quot;categoría especial de datos&quot; o un término similar utilizado por las leyes aplicables. Esto excluye específicamente la información médica protegida (PHI) y otros datos de salud regulados. |
| **RHD** | Datos que hacen referencia a información médica protegida (PHI) o información sobre un paciente que Adobe le permite cargar de forma contractual. |

## Etiquetas de Partner Ecosystem {#partner}

Las etiquetas de ecosistema de socio se utilizan para categorizar los datos obtenidos de fuentes externas a su organización.

Esta etiqueta se utiliza para regular el uso de los datos de clientes potenciales.

| Etiqueta | Definición |
| --- | --- |
| **Terceros** | Los datos de terceros son datos que le proporciona un proveedor de datos de terceros. Un proveedor de datos de terceros es una entidad que ha celebrado un acuerdo con su organización que le autoriza a acceder, utilizar, mostrar y transmitir los datos de terceros junto con Experience Platform. |
| **Enriquecimiento De Terceros** | Datos recopilados por una organización de terceros que no esté directamente relacionada con el interesado. La etiqueta debe aplicarse a datos de terceros que se utilizan para enriquecer perfiles de origen. |
| **Prospección de terceros** | Datos recopilados por una organización de terceros que no esté directamente relacionada con el interesado. La etiqueta debe aplicarse a los datos de terceros utilizados para la parte superior de la prospección del canal para los clientes nuevos netos. |

## Apéndice

Las secciones siguientes proporcionan información adicional sobre las etiquetas de uso de datos disponibles.

### Detalles de etiqueta de contrato

En las secciones siguientes se proporciona información detallada sobre la aplicación de las etiquetas específicas del contrato &quot;C&quot;.

#### C1 {#c1}

Algunos datos solo se pueden exportar desde Adobe Experience Cloud de forma acumulada sin incluir identificadores individuales o de dispositivo. Por ejemplo, los datos que se originaron en las redes sociales.

#### C2 {#c2}

Algunos proveedores de datos tienen condiciones en sus contratos que prohíben la exportación de datos desde el lugar donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales suelen restringir la transferencia de datos que se reciben de ellas. La etiqueta C2 es más restrictiva que [C1](#c1), que solo requiere agregación y datos anónimos, pero es menos restrictiva que [C12](#c12), lo que impide totalmente las exportaciones de datos independientemente del destino.

#### C3 {#c3}

Algunos proveedores de datos tienen términos en sus contratos que prohíben la combinación o el uso de esos datos con información directamente identificable. Por ejemplo, los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables.

#### C4 {#c4}

C4 incluye las etiquetas [C5](#c5), [C6](#c6) y [C7](#c7). Es una de las etiquetas más restrictivas, sólo superada por [C12](#c12).

#### C5 {#c5}

La segmentación basada en intereses, o personalización, se produce si se cumplen las tres condiciones siguientes: Los datos recopilados en el sitio se (1) utilizan para hacer deducciones sobre los intereses de un usuario, (2) se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) Y (3) se utilizan para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.

La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Los distintos sitios representan contextos diferentes, de modo que el uso de datos entre sitios en cualquier contexto es diferente al original. Los datos entre sitios generalmente se recopilan y procesan para hacer deducciones sobre los intereses de los usuarios. Como resultado, el uso de datos entre sitios para segmentar anuncios o contenido suele calificarse como segmentación basada en intereses, independientemente de si el anuncio o el contenido aparece en el sitio o fuera de él. Por ejemplo, si los datos in situ se utilizaran en combinación con datos externos para seleccionar qué anuncio mostrar a un usuario en el sitio de una organización, ese uso podría calificarse como segmentación basada en intereses. Otro ejemplo: es probable que la reorientación de anuncios a usuarios fuera del sitio también se califique como segmentación basada en intereses.

Es probable que el uso de datos externos únicamente para la segmentación también se califique como segmentación basada en intereses, ya que los datos externos generalmente se recopilan y procesan para hacer deducciones sobre los intereses de los usuarios.

Sin embargo, segmentar contenido o anuncios que solo utilicen datos en el sitio no suele considerarse una segmentación basada en intereses. La segmentación en el sitio que, de lo contrario, no cumple los requisitos para considerarse una segmentación basada en intereses se trata como dos etiquetas distintas. Específicamente, Label C6 se dirige a la segmentación y creación de informes de anuncios en el sitio y habla específicamente de la selección de anuncios, la entrega y la creación de informes, y Label C7 se dirige a la selección de contenido en el sitio, la entrega y la creación de informes (segmentación de contenido en el sitio).

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, los marcos de IAB y DAA se proporcionan a continuación:

IAB: Personalization. La recopilación y el procesamiento de información sobre su uso de este servicio para posteriormente personalizar la publicidad y / o el contenido para usted en otros contextos, como en otros sitios web o aplicaciones, a lo largo del tiempo. Normalmente, el contenido del sitio o aplicación se utiliza para hacer deducciones sobre sus intereses que informan la futura selección de publicidad o contenido.

DAA: publicidad en línea basada en el comportamiento. Recopilar datos de un equipo o dispositivo determinado sobre los comportamientos de visualización web a lo largo del tiempo y en sitios web no afiliados con el fin de utilizar dichos datos para predecir las preferencias o intereses del usuario y ofrecer publicidad a ese equipo o dispositivo en función de las preferencias o intereses deducidos de dichos comportamientos de visualización web.

#### C6 {#c6}

Los anuncios son mensajes o notificaciones, incluidos texto e imágenes, que aparecen en un sitio web o aplicación y que están destinados principalmente a promover la venta de bienes o servicios. Depende de usted determinar el propósito de dichos mensajes o notificaciones. Los anuncios son independientes del contenido del sitio y están cubiertos por la etiqueta [C7](#c7). Los datos con una etiqueta C6 no se pueden utilizar para la segmentación de anuncios en el sitio, incluida la selección y el envío de anuncios en los sitios web o las aplicaciones de la organización, ni para medir el envío y la eficacia de dichos anuncios. Esto incluye el uso de datos en el sitio recopilados anteriormente sobre los intereses de los usuarios para seleccionar anuncios, procesar datos sobre qué anuncios se mostraron, cuándo y dónde se mostraron y si los usuarios tomaron alguna acción relacionada con el anuncio, como seleccionar un anuncio o realizar una compra. Normalmente, hacer deducciones sobre las preferencias de un usuario en función de las actividades en el sitio de ese usuario y luego usar esas preferencias en la segmentación de anuncios en el sitio no calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Vea la etiqueta C5 para conocer estos requisitos.](#c5)*

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, los marcos de IAB y DAA se proporcionan a continuación:

IAB: 3. Selección de anuncios, envío, creación de informes: recopilación de información y combinación con información recopilada anteriormente, para seleccionar y enviar anuncios para usted y para medir el envío y la eficacia de dichos anuncios. Esto incluye el uso de información recopilada anteriormente sobre sus intereses para seleccionar anuncios, el procesamiento de datos sobre qué anuncios se mostraron, con qué frecuencia se mostraron, cuándo y dónde se mostraron y si realizó alguna acción relacionada con el anuncio, incluida, por ejemplo, la selección de un anuncio o la realización de una compra. Esto no incluye Personalization, que es la recopilación y el procesamiento de información sobre su uso de este servicio para posteriormente personalizar la publicidad y / o el contenido para usted en otros contextos, como sitios web o aplicaciones, a lo largo del tiempo.

DAA: La publicidad basada en el comportamiento en línea no incluye las actividades de Primeras partes, Entrega de publicidad o Creación de informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que se está visitando, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C7 {#c7}

El contenido del sitio es texto e imágenes que están diseñados para informar, educar o entretener, y no se crean para promover la venta de bienes o servicios. Depende de usted determinar el propósito del contenido, incluso si el contenido podría calificarse como publicidad nativa. La etiqueta C7 no pretende cubrir los anuncios en el sitio, que están cubiertos por la etiqueta [C6](#c6). Los datos con una etiqueta C7 no se pueden utilizar para la segmentación de contenido en el sitio, incluida la selección y entrega de contenido en los sitios web o las aplicaciones de la organización, ni para medir la entrega y la eficacia de dicho contenido. Esto incluye información recopilada anteriormente sobre los intereses de los usuarios en el contenido seleccionado, el procesamiento de datos sobre qué contenido se mostró, con qué frecuencia o durante cuánto tiempo, cuándo y dónde se mostró y si los usuarios realizaron alguna acción relacionada con el contenido, incluida la selección de contenido, por ejemplo. Normalmente, hacer deducciones sobre las preferencias de un usuario en función de las actividades en el sitio de ese usuario y luego usar esas preferencias en la segmentación de contenido en el sitio no calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Vea la etiqueta C5 para conocer estos requisitos.](#c5)*

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, los marcos de IAB y DAA se proporcionan a continuación:

IAB: 4. Selección de contenido, envío, creación de informes: Recopilación de información y, en combinación con la información recopilada anteriormente, para seleccionar y enviar contenido para usted y para medir la entrega y la eficacia de dicho contenido. Esto incluye el uso de información recopilada anteriormente sobre sus intereses para seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, con qué frecuencia o durante cuánto tiempo, cuándo y dónde se mostró y si realizó alguna acción relacionada con el contenido, incluida, por ejemplo, la selección de contenido. Esto no incluye Personalization, que es la recopilación y el procesamiento de información sobre su uso de este servicio para posteriormente personalizar el contenido y/o la publicidad para usted en otros contextos, como sitios web o aplicaciones, a lo largo del tiempo.

DAA: La publicidad basada en el comportamiento en línea no incluye las actividades de Primeras partes, Entrega de publicidad o Creación de informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que está visitando, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C8 {#c8}

Los datos no pueden utilizarse para medir, comprender e informar sobre el uso que hacen los usuarios de los sitios o las aplicaciones de su organización. Esto no incluye la segmentación basada en intereses (segmentación entre sitios), que es la recopilación de información sobre su uso de este servicio para posteriormente personalizar el contenido o la publicidad en otros contextos, es decir, en otros servicios, como sitios web o aplicaciones, a lo largo del tiempo.

#### C9 {#c9}

Algunos contratos incluyen prohibiciones explícitas sobre el uso de datos para la ciencia de datos. A veces se formulan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

#### C10 {#c10}

Algunas políticas de gobernanza de datos restringen el uso de datos de identidad vinculados para la personalización. La etiqueta C10 se aplica automáticamente a las audiencias si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.

#### C11 {#c11}

La coincidencia de segmentos de Adobe Experience Platform le permite hacer coincidir audiencias generadas por Experience Platform con preferencias de privacidad y consentimiento, lo que facilita la obtención de perfiles enriquecidos y perspectivas descendentes. La etiqueta C11 indica datos que no deben usarse en [!DNL Segment Match] procesos. Después de determinar qué conjuntos de datos o campos desea excluir de Coincidencia de segmentos y agregar la etiqueta C11 en consecuencia, el flujo de trabajo de Coincidencia de segmentos aplica automáticamente la etiqueta.

#### C12 {#c12}

Los datos con esta etiqueta no se pueden exportar desde Experience Platform de ninguna manera. Los campos etiquetados con C12 se excluyen de las descargas de CSV, el consumo de API y los flujos de trabajo de activación.
