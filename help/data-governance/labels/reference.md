---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas;etiquetas de uso de datos compatibles;etiquetas de contrato;etiquetas de identidad;etiquetas confidenciales
solution: Experience Platform
title: Glosario de etiquetas de uso de datos
topic-legacy: labels
description: Este documento describe todas las etiquetas de uso de datos que admite Adobe Experience Platform actualmente.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: c29b6c7dc061ea910ebedcae1fa4beaa6def10b1
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 1%

---

# Glosario de etiquetas de uso de datos {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipos de etiquetas"
>abstract="Existen varias categorías de etiquetas de uso de datos. Las etiquetas definidas por el Adobe incluyen etiquetas de contrato, de identidad y confidenciales. Las etiquetas definidas por su organización se clasifican como etiquetas personalizadas."
>text="See the data usage labels glossary for more information on these label types."

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. La Administración de datos de Adobe Experience Platform proporciona varias etiquetas de uso de datos principales listas para usar que puede usar para empezar a categorizar los datos.

Este documento describe las etiquetas de uso de datos principales que proporciona actualmente [!DNL Experience Platform]. Puede encontrar más información sobre la administración de datos en la sección [Información general sobre la administración de datos](../home.md).

## Etiquetas de contrato

Las etiquetas del contrato &quot;C&quot; se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de control de datos de su organización.

| Etiqueta | Definición |
| --- | --- |
| [C1](#c1) | Los datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. |
| [C2](#c2) | Los datos no se pueden exportar a un tercero. |
| [C3](#c3) | Los datos no se pueden combinar ni utilizar de otro modo con información directamente identificable. |
| [C4](#c4) | No se pueden usar datos para dirigir anuncios o contenido, ya sea en el sitio o entre sitios. |
| [C5](#c5) | Los datos no se pueden usar para dirigir el contenido o los anuncios en varios sitios basándose en intereses. |
| [C6](#c6) | Los datos no se pueden usar para la segmentación de anuncios en el sitio. |
| [C7](#c7) | Los datos no se pueden usar para segmentar el contenido en el sitio. |
| [C8](#c8) | Los datos no se pueden usar para medir los sitios web ni las aplicaciones de su organización. |
| [C9](#c9) | Los datos no se pueden utilizar en flujos de trabajo de ciencia de datos. |
| [C10](#c10) | Los datos no se pueden usar para la activación de identidad vinculada. |
| [C11](#c11) | Los datos no se pueden compartir con los socios de coincidencia de segmentos. |
| [C12](#c12) | Los datos no se pueden exportar de ninguna manera. |

## Etiquetas de identidad

Las etiquetas &quot;I&quot; de identidad se utilizan para categorizar los datos que pueden identificar a una persona específica o ponerse en contacto con ella.

| Etiqueta | Definición |
| --- | --- |
| **I1** | Datos directamente identificables que pueden identificar a una persona específica o ponerse en contacto con ella, en lugar de con un dispositivo. |
| **I2** | Datos de identificación indirecta que se pueden utilizar en combinación con otros datos para identificar a una persona concreta o ponerse en contacto con ella. |

## Etiquetas confidenciales {#sensitive}

Las etiquetas &quot;S&quot; confidenciales se utilizan para categorizar los datos que usted y su organización consideran confidenciales.

Un tipo de datos que puede considerar confidencial puede ser de diferentes tipos de datos geográficos; sin embargo, esta categoría no se limita a los datos geográficos.

| Etiqueta | Definición |
| --- | --- |
| **S1** | Datos que especifican la latitud y la longitud que se pueden usar para determinar la ubicación precisa de un dispositivo. |
| **S2** | Datos que se pueden utilizar para determinar un área de geovalla definida a grandes rasgos. |
| **PSPD** | Los datos personales confidenciales permitidos (PSPD) se refieren a datos que el Adobe permite contractualmente cargar que se consideran &quot;confidenciales&quot;, &quot;categoría especial de datos&quot; o un término similar utilizado por las leyes aplicables. Esto excluye específicamente la Información de Salud Protegida (PHI) y otros datos de salud regulados. |
| **RHD** | Datos que se refieren a Información de Salud Protegida (PHI) o información acerca de un paciente al que el Adobe le permite cargar de manera contractual. |

## Apéndice

Las secciones a continuación proporcionan información adicional sobre las etiquetas de uso de datos disponibles.

### Detalles de la etiqueta del contrato

En las secciones siguientes se proporciona información detallada sobre la aplicación de etiquetas específicas del contrato &quot;C&quot;.

#### C1 {#c1}

Algunos datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. Por ejemplo, datos que se originaron en redes sociales.

#### C2 {#c2}

Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales a menudo restringen la transferencia de datos que recibe de ellos. La etiqueta C2 es más restrictiva que [C1](#c1), que solo requiere agregación y datos anónimos, pero es menos restrictivo que [C12](#c12), lo que evita totalmente las exportaciones de datos independientemente del destino.

#### C3 {#c3}

Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la combinación o el uso de esos datos con información directamente identificable. Por ejemplo, los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables.

#### C4 {#c4}

C4 incluye etiquetas [C5](#c5), [C6](#c6)y [C7](#c7). Es una de las etiquetas más restrictivas, solo va seguida de [C12](#c12).

#### C5 {#c5}

La segmentación o personalización basada en intereses se produce si se cumplen las tres condiciones siguientes: Los datos recopilados en el sitio se utilizan (1) para hacer inferencias sobre los intereses de un usuario, (2) se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) Y (3) para seleccionar qué contenido o anuncios se sirven en función de esas inferencias.

La combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio, se denomina datos entre sitios. Los distintos sitios representan contextos diferentes, por lo que el uso de datos entre sitios en cualquier contexto es diferente del original. Los datos entre sitios suelen recopilarse y procesarse para hacer inferencias sobre los intereses de los usuarios. Como resultado, el uso de datos entre sitios para anuncios de objetivo o contenido suele calificarse como objetivo basado en intereses, independientemente de si el anuncio o el contenido aparece en el sitio o fuera de él. Por ejemplo, si se usaran datos en el sitio en combinación con datos fuera del sitio para seleccionar qué publicidad mostrar a un usuario en el propio sitio de una organización, ese uso se calificaría como objetivo basado en intereses. Otro ejemplo: la reorientación de anuncios para usuarios fuera del sitio también podría calificarse como objetivo basado en intereses.

Es probable que el uso de datos fuera del sitio solo para la segmentación también se califique como objetivo basado en intereses, ya que los datos fuera del sitio generalmente se recopilan y procesan para hacer inferencias sobre los intereses de los usuarios.

Sin embargo, la segmentación de contenido o anuncios que usen solamente datos en el sitio generalmente no se calificaría como segmentación basada en intereses. La segmentación en el sitio que de otra manera no cumple los requisitos para la segmentación basada en intereses se trata como dos etiquetas diferentes. Específicamente, la etiqueta C6 aborda la segmentación y el sistema de informes de los anuncios en el sitio y habla específicamente de la selección, el envío y el sistema de informes de los anuncios, y la etiqueta C7 aborda la selección, el envío y el sistema de informes del contenido en el sitio (segmentación del contenido en el sitio).

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, a continuación se proporcionan los marcos de la IAB y el DAA:

IAB: Personalización. La recopilación y el procesamiento de información sobre el uso que haga de este servicio para personalizar posteriormente la publicidad o el contenido en otros contextos, como en otros sitios web o aplicaciones, a lo largo del tiempo. Normalmente, el contenido del sitio o aplicación se utiliza para hacer inferencias sobre sus intereses que informan a la selección futura de publicidad o contenido.

DAA: Anuncio de comportamiento en línea. Recopilación de datos de un equipo o dispositivo concreto con respecto a los comportamientos de visualización de la web a lo largo del tiempo y entre sitios web no afiliados con el fin de utilizar dichos datos para predecir las preferencias o intereses del usuario en la entrega de publicidad a ese equipo o dispositivo en función de las preferencias o intereses inferidos de dichos comportamientos de visualización de la web.

#### C6 {#c6}

Los anuncios son mensajes o notificaciones, incluidos textos e imágenes, que aparecen en un sitio web o aplicación y que están destinados principalmente a promover la venta de bienes o servicios. Depende de usted determinar el propósito de dichos mensajes o notificaciones. Los anuncios son independientes del contenido en el sitio, cubierto por una etiqueta [C7](#c7). Los datos con una etiqueta C6 no se pueden usar para la segmentación de anuncios en el sitio, incluida la selección y entrega de anuncios en los sitios web o aplicaciones de su organización, ni para medir la entrega y la eficacia de dichos anuncios. Esto incluye el uso de datos en el sitio recopilados anteriormente sobre los intereses de los usuarios para seleccionar anuncios, procesar datos sobre qué anuncios se mostraron, cuándo y dónde se mostraron y si los usuarios realizaron alguna acción relacionada con el anuncio, como seleccionar un anuncio o realizar una compra. Normalmente, hacer inferencias sobre las preferencias de un usuario en función de las actividades en el sitio de ese usuario y luego usar esas preferencias en la segmentación de anuncios en el sitio no se calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Para estos requisitos, véase la etiqueta C5.](#c5)*

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, a continuación se proporcionan los marcos de la IAB y el DAA:

IAB: 3. Selección de anuncios, envío, creación de informes: La recopilación de información, y en combinación con la información recopilada anteriormente, para seleccionar y entregar anuncios para usted, y para medir la entrega y efectividad de dichos anuncios. Esto incluye el uso de información recopilada anteriormente sobre sus intereses para seleccionar anuncios, el procesamiento de datos sobre qué anuncios se mostraron, la frecuencia con que se mostraron, cuándo y dónde se mostraron y si realizó alguna acción relacionada con el anuncio, como seleccionar un anuncio o realizar una compra. Esto no incluye la personalización, que es la recopilación y el procesamiento de información sobre su uso de este servicio para posteriormente personalizar la publicidad o el contenido para usted en otros contextos, como sitios web o aplicaciones, a lo largo del tiempo.

DAA: La publicidad en línea basada en el comportamiento no incluye las actividades de las Primeras Partes, la Entrega de publicidad o los Informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que se visita, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C7 {#c7}

El contenido en el sitio es texto e imágenes que están diseñados para informar, educar o entretener, y no se crean para promover la venta de bienes o servicios. Depende de usted determinar el propósito del contenido, incluido si este se calificaría como publicidad nativa. La etiqueta C7 no cubre los anuncios en el sitio, que están cubiertos por etiquetas [C6](#c6). Los datos con una etiqueta C7 no se pueden usar para la segmentación de contenido en el sitio, incluida la selección y entrega de contenido en los sitios web o aplicaciones de su organización, ni para medir la entrega y la eficacia de dicho contenido. Esto incluye información recopilada anteriormente sobre los intereses de los usuarios en contenido seleccionado, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró y si los usuarios realizaron alguna acción relacionada con el contenido, como seleccionar contenido. Normalmente, hacer inferencias sobre las preferencias de un usuario en función de las actividades en el sitio de ese usuario y luego usar esas preferencias en la segmentación de contenido en el sitio no se calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Para estos requisitos, véase la etiqueta C5.](#c5)*

En última instancia, la interpretación de la etiqueta y cómo se aplica el uso de los datos con esa etiqueta depende de usted. Como referencia, a continuación se proporcionan los marcos de la IAB y el DAA:

IAB: 4. Selección de contenido, envío, creación de informes: La recopilación de información, y en combinación con la información recopilada anteriormente, para seleccionar y entregar contenido para usted, y para medir la entrega y efectividad de dicho contenido. Esto incluye el uso de información recopilada anteriormente sobre sus intereses para seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró y si realizó alguna acción relacionada con el contenido, como seleccionar contenido. Esto no incluye la personalización, que es la recopilación y el procesamiento de información sobre su uso de este servicio para posteriormente personalizar contenido o publicidad para usted en otros contextos, como sitios web o aplicaciones, a lo largo del tiempo.

DAA: La publicidad en línea basada en el comportamiento no incluye las actividades de las Primeras Partes, la entrega de publicidad o los informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que está visitando, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C8 {#c8}

No se pueden usar los datos para medir, comprender y crear informes sobre el uso que hacen los usuarios de los sitios o aplicaciones de su organización. Esto no incluye la segmentación basada en intereses (segmentación entre sitios), que es la recopilación de información sobre el uso de este servicio para personalizar posteriormente el contenido o la publicidad para usted en otros contextos, es decir, en otros servicios, como sitios web o aplicaciones, a lo largo del tiempo.

#### C9 {#c9}

Algunos contratos incluyen prohibiciones explícitas sobre el uso de datos para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

#### C10 {#c10}

Algunas políticas de uso de datos restringen el uso de datos de identidad vinculados para la personalización. La etiqueta C10 se aplica automáticamente a los segmentos si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.

#### C11 {#c11}

La coincidencia de segmentos de Adobe Experience Platform le permite hacer coincidir segmentos de origen con preferencias de privacidad y consentimiento, lo que facilita la generación de perfiles enriquecidos y perspectivas descendentes. La etiqueta C11 indica los datos que no deben utilizarse en [!DNL Segment Match] procesos. Después de determinar qué conjuntos de datos o campos desea excluir de la coincidencia de segmentos y de agregar la etiqueta C11 en consecuencia, el flujo de trabajo de la coincidencia de segmentos aplica automáticamente la etiqueta.

#### C12 {#c12}

Los datos con esta etiqueta no se pueden exportar desde Platform de ninguna manera. Los campos etiquetados con C12 se excluyen de las descargas de CSV, el consumo de API y los flujos de trabajo de activación.
