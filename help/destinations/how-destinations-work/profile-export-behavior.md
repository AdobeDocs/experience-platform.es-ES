---
title: Comportamiento de exportación del perfil
description: Descubra cómo varía el comportamiento de exportación de perfiles entre los distintos patrones de integración admitidos en los destinos de Experience Platform.
source-git-commit: 1c844d86834ef78d1206a8698dbcbfe2fae49661
workflow-type: tm+mt
source-wordcount: '2926'
ht-degree: 0%

---

# Comportamiento de exportación de perfil para diferentes tipos de destino

Hay varios tipos de destino en Experience Platform, como se muestra en el diagrama siguiente. Estos destinos presentan patrones de exportación ligeramente diferentes en cuanto a los déclencheur de una exportación de destino y a los elementos incluidos en una exportación, tal como se describe en las secciones siguientes.

>[!IMPORTANT]
>
>Esta página de documentación solo describe el comportamiento de exportación del perfil para las conexiones resaltadas en la parte inferior del diagrama.

![Tipos de diagrama de destinos](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Política de agrupamiento y agrupamiento

Antes de profundizar en información específica por tipo de destino, es importante comprender los conceptos de microagrupamiento y política de agregación para *destinos de flujo continuo*.

Los destinos de Experience Platform exportan datos a integraciones basadas en API como llamadas HTTPS. Una vez que otros servicios de flujo ascendente notifican al servicio de destinos que los perfiles se han actualizado como resultado de la ingesta por lotes, la ingesta de transmisión, la segmentación por lotes, la segmentación de flujo continuo o los cambios en el gráfico de identidad, los datos se exportan y se envían a los destinos de flujo continuo.

Se llama al proceso mediante el cual se agregan perfiles a los mensajes HTTPS antes de enviarlos a los extremos de API de destino *microagrupamiento*.

Tome el [Destino de facebook](/help/destinations/catalog/social/facebook.md) con un *[agregación configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* directiva como ejemplo: los datos se envían de forma agregada, donde el servicio de destinos toma todos los datos entrantes del servicio de perfil en sentido ascendente y los agrega en uno de los siguientes elementos, antes de enviarlos a Facebook:

* Número de registros (máximo de 10.000) o
* Intervalo de intervalo de tiempo (30 minutos)

Cualquiera de los umbrales anteriores se cumpla primero déclencheur una exportación a Facebook. Por lo tanto, en la variable [!DNL Facebook Custom Audiences] tablero, es posible que vea audiencias procedentes de Experience Platform en incrementos de registro de 10 000. Es posible que vea 10 000 registros cada 10-15 minutos porque los datos se procesan y agregan más rápido que el intervalo de exportación de 30 minutos y se envían más rápido, por lo que aproximadamente cada 10-15 minutos hasta que se procesan todos los registros. Si no hay registros suficientes para constituir un lote de 10 000, el número actual de registros se enviará tal cual cuando se alcance el umbral del período de tiempo, por lo que también puede ver lotes más pequeños enviados a Facebook.

Otro ejemplo: [Destino de la API HTTP](/help/destinations/catalog/streaming/http-destination.md), que tiene un *[agregación del mejor esfuerzo](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* directiva, con `maxUsersPerRequest: 10`. Esto significa que se agregarán un máximo de diez perfiles antes de que se active una llamada HTTP a este destino, pero el Experience Platform intenta enviar perfiles al destino en cuanto el servicio de destinos recibe información actualizada de reevaluación de un servicio ascendente.

La política de agregación se puede configurar y los desarrolladores de destino pueden decidir cómo configurar la política de agregación para satisfacer mejor las limitaciones de velocidad de los extremos de API descendentes. Más información sobre [política de agregación](/help/destinations/destination-sdk/destination-configuration.md#aggregation) en la documentación del Destination SDK.

## Destinos de exportación de perfiles de transmisión (empresa) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Los destinos empresariales solo están disponibles para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

La variable [destinos empresariales](/help/destinations/destination-types.md#streaming-profile-export) en el Experience Platform están Amazon Kinesis, Azure Event Hubs y la API HTTP.

Experience Platform optimiza el comportamiento de exportación del perfil al destino empresarial para exportar solo los datos al extremo de la API cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación del segmento u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó por un cambio en [abono de segmento](/help/xdm/field-groups/profile/segmentation.md) para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, un perfil que ya se había clasificado para uno de los segmentos asignados al destino se ha añadido una nueva identidad en el atributo de mapa de identidad.
* La actualización de perfil se determinó mediante un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde estén los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco perfiles nuevos se exportan incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación

En cuanto a los datos exportados para un perfil determinado, es importante comprender los dos conceptos diferentes de *qué determina la exportación de datos a su destino empresarial* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven como señal para una exportación de destino. Esto significa que si cualquier segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Dado que actualmente las identidades no se pueden asignar a destinos empresariales, los cambios en cualquier identidad en un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es o no el mismo valor. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>La variable `segmentMembership` incluye el segmento asignado en el flujo de datos de activación, para el cual el estado del perfil ha cambiado tras un evento de calificación o salida de segmento. Tenga en cuenta que otros segmentos sin asignar para los que el perfil cumpla los requisitos pueden formar parte de la exportación de destino, si pertenecen al mismo [combinar directiva](/help/profile/merge-policies/overview.md) como segmento asignado en el flujo de datos de activación. </li><li>Todas las identidades del `identityMap` también se incluyen (actualmente, el Experience Platform no admite la asignación de identidades en el destino de empresa).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Los destinos empresariales rellenan los datos de la secuencia al activar perfiles en un destino. Esto significa que la primera exportación de datos después de configurar un flujo de trabajo de activación en un destino incluirá perfiles que cumplen los requisitos para el segmento activado antes de que el segmento se asigne al destino.

>[!BEGINSHADEBOX]

Por ejemplo, considere este flujo de datos a un destino HTTP donde se seleccionan tres segmentos en el flujo de datos y se asignan cuatro atributos al destino.

![flujo de datos de destino empresarial](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino se puede determinar mediante un perfil que cumpla los requisitos de uno de los *tres segmentos asignados*. Sin embargo, en la exportación de datos, en la variable `segmentMembership` , podrían aparecer otros segmentos sin asignar, si ese perfil en particular es miembro de ellos y si comparten la misma política de combinación que el segmento que activó la exportación. Si un perfil cumple los requisitos para la variable **Cliente con Autos DeLorean** pero también es miembro de **Viendo la película &quot;Volver al futuro&quot;** y **Seguidores de ciencia ficción** estos otros dos segmentos también estarán presentes en la variable `segmentMembership` de la exportación de datos, aunque no estén asignados en el flujo de datos, si comparten la misma política de combinación con la variable **Cliente con Autos DeLorean** segmento.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados arriba determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

>[!ENDSHADEBOX]

>[!TIP]
>
> Puede ver ejemplos de datos exportados a varios destinos de empresa en el [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Centros de eventos de Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)y [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data) páginas de documentación de destino.

## Destinos basados en API de transmisión {#streaming-api-based-destinations}

El comportamiento de exportación del perfil para destinos de flujo continuo como Facebook, Trade Desk y otras integraciones basadas en API es idéntico al anterior.

Ejemplos de destino: publicidad, social, etc.

Experience Platform optimiza el comportamiento de exportación del perfil al destino de flujo continuo para exportar solo datos a destinos basados en API de flujo continuo cuando se hayan producido actualizaciones relevantes en un perfil tras la calificación del segmento u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó por un cambio en [abono de segmento](/help/xdm/field-groups/profile/segmentation.md) para al menos uno de los segmentos asignados al destino. Por ejemplo, el perfil se ha clasificado para uno de los segmentos asignados al destino o ha salido de uno de los segmentos asignados al destino.
* La actualización de perfil se determinó mediante un cambio en la variable [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md) para un área de nombres de identidad que esté marcada para su exportación para esta instancia de destino. Por ejemplo, un perfil que ya se había clasificado para uno de los segmentos asignados al destino se ha añadido una nueva identidad en el atributo de mapa de identidad.
* La actualización de perfil se determinó mediante un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.
* Cambios de consentimiento para un perfil cuando se configura la aplicación del consentimiento automatizada y se excluye un perfil. La aplicación del consentimiento automatizada envía un evento de salida de audiencia al destino, de modo que el perfil no se incluya en ninguna segmentación en el destino.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si un segmento asignado al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde estén los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco perfiles nuevos se exportan incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación

En cuanto a los datos que se exportan para un perfil determinado, es importante comprender los dos conceptos diferentes de qué determina una exportación de datos al destino de la API de flujo continuo y qué datos se incluyen en la exportación.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y segmentos asignados sirven como señal para una exportación de destino. Esto significa que si cualquier segmento asignado cambia de estado (de nulo a realizado o de realizado/existente a existente) o si se actualiza cualquier atributo asignado, se inicia una exportación de destino.</li><li>Un cambio en el mapa de identidad se define como una identidad que se agrega o elimina para la variable [gráfico de identidad](/help/identity-service/ui/identity-graph-viewer.md) del perfil, para áreas de nombres de identidad que se asignan para la exportación.</li><li>Un cambio para un atributo se define como cualquier actualización en el atributo, para los atributos asignados al destino.</li></ul> | <ul><li>Los segmentos asignados al destino y que han cambiado se incluirán en la variable `segmentMembership` objeto. En algunos casos, se pueden exportar mediante varias llamadas. Además, en algunos escenarios, es posible que algunos segmentos que no han cambiado también se incluyan en la llamada a . En cualquier caso, solo se exportan los segmentos asignados.</li><li>Todas las identidades de las áreas de nombres asignadas al destino en la variable `identityMap` también se incluyen .</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Los destinos de API de flujo rellenan los datos de relleno de flujo al activar perfiles en un destino. Esto significa que la primera exportación de datos después de configurar un flujo de trabajo de activación en un destino incluirá perfiles que cumplen los requisitos para el segmento activado antes de que el segmento se asigne al destino.

>[!BEGINSHADEBOX]

Por ejemplo, considere este flujo de datos a un destino de flujo continuo en el que se seleccionan tres segmentos en el flujo de datos.

![flujo de datos de destino de flujo de transmisión](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Una exportación de perfil al destino se puede determinar mediante un perfil que cumpla los requisitos de uno de los tres segmentos asignados o salga de él. Si un perfil cumple los requisitos para la variable **Cliente con Autos DeLorean** segmento, esto déclencheur una exportación. Los demás segmentos (**Ciudad de Dallas** y **Sitio básico activo**) también se puede exportar en caso de que el perfil tenga ese segmento presente con uno de los estados posibles (`realized`, `existing`, `exited`). Segmentos no asignados (como **Seguidores de ciencia ficción**) no se exporta.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los tres atributos asignados arriba determinará una exportación de destino.

>[!BEGINSHADEBOX]

## Destinos por lotes (basados en archivos) {#file-based-destinations}

Al exportar perfiles a [destinos basados en archivos](/help/destinations/destination-types.md#file-based) en Experience Platform, existen tres tipos de programas (enumerados a continuación) y dos opciones de exportación de archivos (archivos completos o incrementales) que puede utilizar. Todos estos ajustes se establecen en un nivel de segmento, incluso cuando varios segmentos están asignados a un único flujo de datos de destino.

* Exportaciones programadas: Configure un destino, añada uno o más segmentos, seleccione si desea exportar archivos completos o incrementales y seleccione una hora determinada cada día o varias veces al día cuando se deben exportar los archivos. Por ejemplo, un tiempo de exportación de 5 p. m. significa que los perfiles cualificados para el segmento se exportarán a las 5 p. m.
* Después de la evaluación de segmentos: La exportación se activa inmediatamente después de que se ejecute el trabajo diario de evaluación de segmentos. Esto significa que los números de perfil exportados en el archivo se acercan lo más posible a la población evaluada más reciente del segmento.
* Exportaciones a la carta ([exportar archivo ahora](/help/destinations/ui/export-file-now.md)): En función del trabajo de evaluación de segmentos más reciente, se exporta un archivo completo una sola vez además de las exportaciones programadas regularmente.

En cualquiera de las situaciones de exportación anteriores, los archivos exportados incluyen los perfiles que cumplen los requisitos para la exportación, junto con las columnas que ha seleccionado como atributos XDM para la exportación.

>[!TIP]
>
>Cuando un segmento de flujo continuo está asignado a un destino de lote, existe una mayor probabilidad de que el número de perfiles del archivo exportado esté más cerca del número de usuarios del segmento. Esto se debe a que existe una mayor probabilidad de que la última evaluación de segmentos se haya acercado más al tiempo de exportación.

### Exportaciones de archivos incrementales {#incremental-file-exports}

No todas las actualizaciones de un perfil cumplen los requisitos para que un perfil se incluya en las exportaciones de archivos incrementales. Por ejemplo, si se ha agregado o eliminado un atributo de un perfil, no se incluye el perfil en la exportación. Solo perfiles para los que la variable `segmentMembership` El atributo ha cambiado se incluirá en los archivos exportados. En otras palabras, solo si el perfil se convierte en parte del segmento o se elimina del segmento se incluye en las exportaciones incrementales de archivos.

Del mismo modo, si se agrega una nueva identidad (nueva dirección de correo electrónico, número de teléfono, ECID, etc.) a un perfil en la variable [gráfico de identidad](/help/identity-service/ui/identity-graph-viewer.md), que no representa un motivo para incluir el perfil en una nueva exportación incremental de archivos.

Si se agrega un nuevo segmento a una asignación de destino, esto no afecta a las cualificaciones y exportaciones de otro segmento. Las programaciones de exportación se configuran individualmente por segmento y los archivos se exportan por separado para cada segmento, incluso si los segmentos se han añadido al mismo flujo de datos de destino.

>[!BEGINSHADEBOX]

Por ejemplo, en la configuración de exportación que se muestra a continuación, donde un segmento exporta actualizaciones de archivos incrementales, tenga en cuenta las siguientes circunstancias, cuando un perfil se incluye o no en una exportación de archivos incrementales:

![Exporte la configuración con varios atributos seleccionados.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Un perfil se incluye en una exportación incremental de archivos cuando califica o descalifica para el segmento.
* Un perfil es *not* se incluye en una exportación de archivos incremental cuando se agrega un nuevo número de teléfono al gráfico de identidad.
* Un perfil es *not* incluido en una exportación de archivos incremental cuando el valor de cualquiera de los campos XDM asignados como `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` se actualiza en un perfil.
* Siempre que `segmentMembership.status` El campo XDM está asignado en el flujo de trabajo de activación de destino, los perfiles que salen del segmento también se incluyen en los archivos incrementales exportados, con un `exited` estado.

>[!ENDSHADEBOX]

### Qué determina una exportación de datos y qué se incluye en la exportación

Según la información de la sección anterior, el comportamiento de exportación de perfiles a destinos basados en archivos se puede resumir como se describe a continuación:

**Exportaciones de archivos completas**

La población completa del segmento se exporta todos los días.

| Qué determina una exportación de destino | Qué se incluye en el archivo exportado |
|---------|----------|
| <ul><li>La programación de exportación establecida en la interfaz de usuario o la API y la acción del usuario (seleccionar [Exportar archivo ahora](/help/destinations/ui/export-file-now.md) en la interfaz de usuario o utilizando el [API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) determinan el inicio de una exportación de destino.</li><li>Cualquier cambio en la pertenencia a segmentos de un perfil, tanto si califica como si no califica del segmento, califica un perfil para ser incluido en las exportaciones incrementales.</li></ul> | En las exportaciones completas de archivos, la población de perfiles completa de un segmento, según la última evaluación de segmentos, se incluye en cada exportación de archivos. Los valores más recientes de cada atributo XDM seleccionado para la exportación también se incluyen como columnas en cada archivo. |

{style=&quot;table-layout:fixed&quot;}

**Exportaciones de archivos incrementales**

En la primera exportación de archivo después de configurar el flujo de trabajo de activación, se exporta toda la población del segmento. En exportaciones posteriores, solo se exportan los perfiles modificados.

| Qué determina una exportación de destino | Qué se incluye en el archivo exportado |
|---------|----------|
| <ul><li>La programación de exportación establecida en la interfaz de usuario o la API determina el inicio de una exportación de destino.</li><li>Cualquier cambio en la pertenencia a segmentos de un perfil, tanto si califica como si no califica del segmento, califica un perfil para ser incluido en las exportaciones incrementales. Cambios en los atributos o en los mapas de identidad de un perfil *no* califica un perfil para que se incluya en exportaciones incrementales.</li></ul> | Los perfiles para los que ha cambiado la pertenencia al segmento, junto con la información más reciente de cada atributo XDM seleccionado para la exportación. |

{style=&quot;table-layout:fixed&quot;}

>[!TIP]
>
>Como recordatorio, los cambios en los valores de atributos o en los mapas de identidad de un perfil no califican para que un perfil se incluya en una exportación incremental de archivos.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe qué ver en las exportaciones de perfiles a destinos de flujo continuo, empresariales y basados en archivos.

A continuación, puede leer sobre cómo [las identidades se gestionan](/help/destinations/how-destinations-work/identity-handling.md) en el flujo de trabajo de activación.