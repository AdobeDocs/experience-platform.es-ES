---
keywords: Experience Platform;inicio;temas populares;administración de datos;etiqueta de uso de datos api;API de servicio de políticas;etiquetas de uso de datos admitidas;etiquetas de contrato;etiquetas de identidad;etiquetas confidenciales
solution: Experience Platform
title: Etiquetas de uso de datos principales
topic: labels
description: Este documento describe todas las etiquetas de uso de datos admitidas actualmente por Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 2%

---


# Etiquetas de uso de datos principales

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. La Administración de datos de Adobe Experience Platform proporciona varias etiquetas de uso de datos principales listas para usar que puede utilizar para clasificar los datos en inicios.

Este documento describe las etiquetas de uso de datos principales que proporciona [!DNL Experience Platform]. Encontrará más información acerca de [!DNL Data Governance] en la [información general sobre la administración de datos](../home.md).

## Etiquetas de contrato

Las etiquetas &quot;C&quot; del contrato se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de administración de datos de su organización.

| Etiqueta | Definición |
|---|---|
| **C1** | Los datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. [Más información...](#c1) |
| **C2** | Los datos no se pueden exportar a terceros. [Más información...](#c2) |
| **C3** | Los datos no pueden combinarse ni utilizarse de otro modo con información directamente identificable. [Más información...](#c3) |
| **C4** | No se pueden usar datos para dirigir anuncios o contenido, ya sea en el sitio o entre sitios. [Más información...](#c4) |
| **C5** | Los datos no se pueden usar para dirigir contenido o anuncios en varios sitios basados en intereses. [Más información...](#c5) |
| **C6** | No se pueden usar datos para la segmentación de anuncios en el sitio. [Más información...](#c6) |
| **C7** | Los datos no se pueden usar para dirigir el contenido en el sitio. [Más información...](#c7) |
| **C8** | Los datos no se pueden usar para medir los sitios web o las aplicaciones de la organización. [Más información...](#c8) |
| **C9** | Los datos no se pueden usar en flujos de trabajo de ciencia de datos. [Más información...](#c9) |
| **C10** | No se pueden usar datos para la activación de identidad vinculada. [Más información...](#c10) |

## Etiquetas de identidad

Las etiquetas &quot;I&quot; de identidad se utilizan para categorizar los datos que pueden identificar o comunicarse con una persona específica.

| Etiqueta | Definición |
|---|---|
| **I1** | Datos directamente identificables que pueden identificar o contactar a una persona específica, en lugar de un dispositivo. |
| **I2** | Datos de identificación indirecta que pueden utilizarse en combinación con cualquier otro dato para identificar o contactar a una persona específica. |

## Etiquetas sensibles

Las etiquetas &quot;S&quot; confidenciales se utilizan para categorizar los datos que usted y su organización consideran confidenciales.

Un tipo de datos que considere delicados puede ser de distintos tipos de datos geográficos; sin embargo, esta categoría no se limita a los datos geográficos.

| Etiqueta | Definición |
|---|---|
| **S1** | Datos que especifican la latitud y la longitud que pueden utilizarse para determinar la ubicación exacta de un dispositivo. |
| **S2** | Datos que pueden utilizarse para determinar un área de geofence definida de forma amplia. |

## Apéndice

Las secciones a continuación proporcionan información adicional sobre las etiquetas de uso de datos disponibles.

### Detalles de la etiqueta del contrato

En las secciones siguientes se proporciona información detallada sobre la aplicación de etiquetas específicas del contrato &quot;C&quot;.

#### C1 {#c1}

Algunos datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. Por ejemplo, los datos que se originaron en las redes sociales.

#### C2 {#c2}

Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales suelen restringir la transferencia de datos que recibe de ellos. La etiqueta C2 es más restrictiva que [C1](#c1), que sólo requiere agregación y datos anónimos.

#### C3 {#c3}

Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la combinación o utilización de esos datos con información directamente identificable. Por ejemplo, los contratos para datos provenientes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros a menudo incluyen prohibiciones contractuales específicas sobre el uso de esos datos con datos directamente identificables.

#### C4 {#c4}

C4 es la etiqueta más restrictiva: incluye etiquetas [C5](#c5), [C6](#c6) y [C7](#c7).

#### C5 {#c5}

La segmentación o personalización basada en intereses se produce si se cumplen las tres condiciones siguientes: Los datos recopilados en el sitio se utilizan (1) para hacer inferencias sobre los intereses de un usuario, (2) se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio) Y (3) se utilizan para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias.

La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Diferentes sitios representan diferentes contextos, de modo que el uso de datos entre sitios en cualquier contexto es diferente al original. Los datos entre sitios generalmente se recopilan y procesan para hacer inferencias sobre los intereses de los usuarios. Como resultado, el uso de datos entre sitios para dirigir publicidades o contenido suele calificarse como objetivo basado en intereses, independientemente de si el anuncio o el contenido aparece en el sitio o fuera de él. Por ejemplo: si los datos en el sitio se utilizaran en combinación con los datos fuera del sitio para seleccionar qué publicidad mostrar a un usuario en el propio sitio de una organización, ese uso se calificaría como objetivo basado en intereses. Otro ejemplo es que volver a dirigir las publicidades a usuarios externos también podría calificarse como objetivo basado en intereses.

Es probable que el uso de datos externos solo para objetivos también se considere objetivo basado en intereses, ya que los datos externos se recopilan y procesan normalmente para hacer inferencias sobre los intereses de los usuarios.

Sin embargo, dirigir contenido o publicidades que usen solamente datos en el sitio no suele considerarse objetivo basado en intereses. La segmentación en el sitio que de otra manera no se califica como segmentación basada en intereses se trata como dos etiquetas distintas. Específicamente, la etiqueta C6 aborda el objetivo y sistema de informes de publicidad en el sitio y habla específicamente de selección de publicidad, envío y sistema de informes, y la etiqueta C7 aborda la selección de contenido, el envío y el sistema de informes en el sitio (objetivo de contenido en el sitio).

Finalmente, usted puede interpretar la etiqueta y saber cómo se aplican los datos con esa etiqueta. Como referencia, a continuación se proporcionan los marcos de la Junta de Auditores Internos y el DAA:

IAB: Personalización. Recopilación y procesamiento de información sobre el uso que hace de este servicio para personalizar posteriormente la publicidad o el contenido para usted en otros contextos, como en otros sitios web o aplicaciones, con el paso del tiempo. Normalmente, el contenido del sitio o la aplicación se utiliza para hacer inferencias sobre sus intereses que informan la selección futura de publicidad o contenido.

DAA: Publicidad conductual en línea. Recopilación de datos de un equipo o dispositivo concreto con respecto a los comportamientos de visualización web a lo largo del tiempo y entre sitios web no afiliados con el fin de utilizar dichos datos para predecir las preferencias o intereses del usuario de enviar publicidad a ese equipo o dispositivo en función de las preferencias o intereses derivados de dichos comportamientos de visualización web.

#### C6 {#c6}

Los anuncios son mensajes o notificaciones, incluidos texto e imágenes, que aparecen en un sitio web o aplicación y que están destinados principalmente a promover la venta de bienes o servicios. Depende de usted determinar el propósito de dichos mensajes o notificaciones. Las publicidades son independientes del contenido en el sitio, y están cubiertas por la etiqueta [C7](#c7). Los datos con una etiqueta C6 no se pueden utilizar para dirigir anuncios en el sitio, incluida la selección y el envío de anuncios en los sitios web o las aplicaciones de su organización, ni para medir el envío y la eficacia de dichos anuncios. Esto incluye el uso de datos recopilados anteriormente en el sitio sobre los intereses de los usuarios para seleccionar publicidades, procesar datos sobre qué publicidades se mostraron, cuándo y dónde se mostraron y si los usuarios realizaron alguna acción relacionada con la publicidad, como seleccionar una publicidad o realizar una compra. Normalmente, hacer inferencias sobre las preferencias de un usuario en función de las actividades en el sitio de ese usuario y luego usar esas preferencias en la segmentación de anuncios en el sitio no se calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Consulte la etiqueta C5 para conocer estos requisitos.](#c5)*

Finalmente, usted puede interpretar la etiqueta y saber cómo se aplican los datos con esa etiqueta. Como referencia, a continuación se proporcionan los marcos de la Junta de Auditores Internos y el DAA:

IAB: 3. Selección de anuncios, envío, sistema de informes: La recopilación de información, y junto con la información recopilada anteriormente, para seleccionar y enviar anuncios para usted, y para medir el envío y la efectividad de dichos anuncios. Esto incluye el uso de información recopilada anteriormente sobre sus intereses para seleccionar publicidades, el procesamiento de datos sobre qué publicidades se mostraron, la frecuencia con que se mostraron, cuándo y dónde se mostraron, y si realizó alguna acción relacionada con el anuncio, incluso, por ejemplo, seleccionar una publicidad o realizar una compra. Esto no incluye la personalización, que es la recopilación y el procesamiento de información sobre el uso que hace de este servicio para personalizar posteriormente la publicidad o el contenido para usted en otros contextos, como sitios web o aplicaciones, con el paso del tiempo.

DAA: La Publicidad en línea de comportamiento no incluye las actividades de los usuarios individuales, el Envío de publicidad o el Sistema de informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que se visita, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C7 {#c7}

El contenido en el sitio es texto e imágenes que están diseñados para informar, educar o entretener, y que no se crean para promover la venta de bienes o servicios. Depende de usted determinar el propósito del contenido, incluyendo si el contenido se calificaría como publicidad nativa. La etiqueta C7 no está pensada para cubrir anuncios en el sitio, que están cubiertos por la etiqueta [C6](#c6). Los datos con una etiqueta C7 no se pueden utilizar para la segmentación de contenido en el sitio, incluida la selección y el envío de contenido en los sitios web o las aplicaciones de la organización, ni para medir el envío y la eficacia de dicho contenido. Esto incluye la información recopilada anteriormente sobre los intereses de los usuarios en el contenido seleccionado, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró, y si los usuarios realizaron alguna acción relacionada con el contenido, incluida, por ejemplo, la selección de contenido. Normalmente, hacer inferencias sobre las preferencias de los usuarios en función de las actividades en el sitio de los usuarios y luego usar esas preferencias en la segmentación de contenido en el sitio no se calificaría como segmentación basada en intereses (también denominada personalización), ya que no cumpliría los tres requisitos necesarios para la segmentación basada en intereses. *[Consulte la etiqueta C5 para conocer estos requisitos.](#c5)*

Finalmente, usted puede interpretar la etiqueta y saber cómo se aplican los datos con esa etiqueta. Como referencia, a continuación se proporcionan los marcos de la Junta de Auditores Internos y el DAA:

IAB: 4. Selección de contenido, envío, sistema de informes: La recopilación de información, y la combinación con información recopilada anteriormente, para seleccionar y entregar contenido para usted, y para medir el envío y la efectividad de dicho contenido. Esto incluye el uso de la información recopilada anteriormente sobre sus intereses para seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró y si el usuario realizó alguna acción relacionada con el contenido, incluido por ejemplo seleccionar contenido. Esto no incluye la personalización, que es la recopilación y el procesamiento de información sobre el uso que hace de este servicio para personalizar posteriormente el contenido o la publicidad para usted en otros contextos, como sitios web o aplicaciones, con el paso del tiempo.

DAA: La Publicidad de comportamiento en línea no incluye las actividades de los usuarios individuales, el Envío de publicidad o el Sistema de informes de publicidad, ni la publicidad contextual (es decir, la publicidad basada en el contenido de la página web que visita, la visita actual de un consumidor a una página web o una consulta de búsqueda).

#### C8 {#c8}

Los datos no se pueden usar para medir, comprender y generar informes sobre el uso que hacen los usuarios de los sitios o aplicaciones de su organización. Esto no incluye la segmentación basada en intereses (segmentación entre sitios), que es la recopilación de información sobre el uso que hace de este servicio para personalizar posteriormente el contenido o la publicidad para usted en otros contextos, es decir, en otros servicios, como sitios web o aplicaciones, con el paso del tiempo.

#### C9 {#c9}

Algunos contratos incluyen prohibiciones explícitas del uso de datos para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

#### C10 {#c10}

Algunas directivas de uso de datos restringen el uso de datos de identidad enlazados para la personalización. La etiqueta C10 se aplica automáticamente a los segmentos si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.
