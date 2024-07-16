---
title: Comportamiento de exportación de perfil
description: Descubra cómo varía el comportamiento de exportación de perfiles entre los distintos patrones de integración admitidos en los destinos de Experience Platform.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '2931'
ht-degree: 0%

---

# Comportamiento de exportación de perfil para diferentes tipos de destino

Existen varios tipos de destinos en Experience Platform, como se muestra en el diagrama siguiente. Estos destinos tienen patrones de exportación ligeramente diferentes con respecto a los déclencheur que se exportan y a lo que se incluye en una exportación, tal como se describe en las secciones siguientes.

>[!IMPORTANT]
>
>Esta página de documentación solo describe el comportamiento de exportación de perfiles para las conexiones resaltadas en la parte inferior del diagrama.

![Diagrama de tipos de destinos](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Agregación de mensajes en destinos de flujo continuo

Antes de profundizar en información específica por tipo de destino, es importante comprender el concepto de agregación de mensajes para *destinos de streaming*.

Los destinos de Experience Platform exportan datos a integraciones basadas en API como llamadas HTTPS. Una vez que otros servicios ascendentes notifican al servicio de destinos que los perfiles se han actualizado como resultado de la ingesta por lotes, la ingesta por transmisión, la segmentación por lotes, la segmentación por transmisión o los cambios en el gráfico de identidad, los datos se exportan y se envían a los destinos de transmisión.

Los perfiles se agregan en mensajes HTTPS antes de enviarse a los extremos de la API de destino.

Tome como ejemplo el [destino de Facebook](/help/destinations/catalog/social/facebook.md) con una directiva de *[agregación configurable](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*; los datos se envían de forma agregada, donde el servicio de destinos toma todos los datos entrantes del servicio de perfil en sentido ascendente y los agrega mediante una de las siguientes opciones, antes de enviarlos a Facebook:

* Número de registros (máximo de 10 000) o
* Intervalo de ventana de tiempo (300 segundos)

Cualquiera de los umbrales anteriores se cumple primero como déclencheur para exportarse a Facebook. Por lo tanto, en el tablero [!DNL Facebook Custom Audiences], es posible que vea audiencias que llegan desde Experience Platform en incrementos de 10 000 registros. Es posible que vea 10 000 registros cada 2-3 minutos, porque los datos se procesan y agregan más rápido que el intervalo de exportación de 300 segundos y se envían más rápido, por lo que cada 2-3 minutos, aproximadamente, hasta que se hayan procesado todos los registros. Si no hay registros suficientes para constituir un lote de 10 000, el número actual de registros se enviará tal cual cuando se alcance el umbral de la ventana de tiempo, por lo que es posible que también vea lotes más pequeños enviados a Facebook.

Otro ejemplo: considere el [destino de la API HTTP](/help/destinations/catalog/streaming/http-destination.md), que tiene una directiva *[agregación de mejor esfuerzo](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*, con `maxUsersPerRequest: 10`. Esto significa que se agregarán un máximo de diez perfiles antes de activar una llamada HTTP a este destino, pero Experience Platform intenta enviar perfiles al destino en cuanto el servicio de destinos recibe información de reevaluación actualizada de un servicio ascendente.

La directiva de agregación se puede configurar y los desarrolladores de destino pueden decidir cómo configurar la directiva de agregación para satisfacer de la mejor manera las limitaciones de velocidad de los extremos de API descendentes. Obtenga más información acerca de [política de agregación](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) en la documentación del Destination SDK.

## Destinos de exportación de perfiles de streaming (empresa) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Los destinos empresariales solo están disponibles para los clientes de [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es).

Los [destinos empresariales](/help/destinations/destination-types.md#streaming-profile-export) de Experience Platform son Amazon Kinesis, Azure Event Hubs y la API de HTTP.

Experience Platform optimiza el comportamiento de exportación de perfiles a su destino empresarial para exportar solo datos a su punto final de API cuando se han producido actualizaciones relevantes en un perfil tras la calificación de la audiencia u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó por un cambio en [pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) para al menos una de las audiencias asignadas al destino. Por ejemplo, el perfil cumple los requisitos de una de las audiencias asignadas al destino o ha salido de una de las audiencias asignadas al destino.
* La actualización de perfil se determinó mediante un cambio en el [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md). Por ejemplo, a un perfil que ya estaba cualificado para una de las audiencias asignadas al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si una audiencia asignada al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación

Con respecto a los datos que se exportan para un perfil determinado, es importante entender los dos conceptos diferentes de *qué determina una exportación de datos a su destino empresarial* y *qué datos se incluyen en la exportación*.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y audiencias asignados sirven de referencia para una exportación de destino. Esto significa que si alguna audiencia asignada cambia de estado (de `null` a `realized` o de `realized` a `exiting`) o si se actualiza algún atributo asignado, se iniciará una exportación de destino.</li><li>Dado que las identidades no se pueden asignar actualmente a destinos empresariales, los cambios en cualquier identidad de un perfil determinado también determinan las exportaciones de destino.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, independientemente de si es el mismo valor o no. Esto significa que la sobrescritura de un atributo se considera un cambio aunque el valor en sí no haya cambiado.</li></ul> | <ul><li>El objeto `segmentMembership` incluye la audiencia asignada en el flujo de datos de activación, para la cual el estado del perfil ha cambiado después de un evento de calificación o salida de audiencia. Tenga en cuenta que otras audiencias sin asignar para las que el perfil cumple los requisitos pueden formar parte de la exportación de destino, si estas audiencias pertenecen a la misma [política de combinación](/help/profile/merge-policies/overview.md) que la audiencia asignada en el flujo de datos de activación. </li><li>También se incluyen todas las identidades del objeto `identityMap` (actualmente, el Experience Platform no admite la asignación de identidades en el destino de Enterprise).</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Los destinos empresariales transmiten datos de relleno al activar perfiles en un destino. Esto significa que la primera exportación de datos después de configurar un flujo de trabajo de activación a un destino incluye perfiles cualificados para la audiencia activada antes de que la audiencia se asigne al destino.

>[!BEGINSHADEBOX]

Por ejemplo, considere este flujo de datos para un destino HTTP en el que se seleccionen tres audiencias en el flujo de datos y se asignen cuatro atributos al destino.

![flujo de datos de destino empresarial](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que califique para uno de los *tres segmentos asignados* o que salga de él. Sin embargo, en la exportación de datos, en el objeto `segmentMembership` podrían aparecer otras audiencias no asignadas, si ese perfil en particular es miembro de ellas y si comparten la misma política de combinación que la audiencia que activó la exportación. Si un perfil cumple los requisitos para la audiencia de **Cliente con DeLorean Cars**, pero también es miembro de los segmentos de **Película de &quot;Regreso al futuro&quot; vista** y **Aficionados a la ciencia ficción**, entonces estas otras dos audiencias también estarán presentes en el objeto `segmentMembership` de la exportación de datos, aunque no estén asignadas en el flujo de datos, si comparten la misma política de combinación con el segmento **Cliente con DeLorean Cars**.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los cuatro atributos asignados anteriormente determinará una exportación de destino y cualquiera de los cuatro atributos asignados presentes en el perfil estará presente en la exportación de datos.

>[!ENDSHADEBOX]

>[!TIP]
>
> Puede ver ejemplos de datos exportados a varios destinos empresariales en las páginas de documentación de destino de [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data) y [HTTP API](/help/destinations/catalog/streaming/http-destination.md#exported-data).

## Destinos basados en API de streaming {#streaming-api-based-destinations}

El comportamiento de exportación de perfiles para destinos de streaming como Facebook, Trade Desk y otras integraciones basadas en API es muy similar al comportamiento descrito anteriormente para destinos empresariales.

Algunos ejemplos de destinos de streaming son los destinos que pertenecen a las [categorías sociales y publicitarias](/help/destinations/destination-types.md#categories) del catálogo.

Experience Platform optimiza el comportamiento de exportación de perfiles a su destino de streaming para exportar solo datos a destinos de streaming basados en API cuando se han producido actualizaciones relevantes en un perfil tras la calificación de la audiencia u otros eventos significativos. Los perfiles se exportan al destino en las siguientes situaciones:

* La actualización de perfil se determinó por un cambio en [pertenencia a audiencias](/help/xdm/field-groups/profile/segmentation.md) para al menos una de las audiencias asignadas al destino. Por ejemplo, el perfil cumple los requisitos de una de las audiencias asignadas al destino o ha salido de una de las audiencias asignadas al destino.
* La actualización de perfil se determinó mediante un cambio en el [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md) para un área de nombres de identidad que está marcado para la exportación para esta instancia de destino. Por ejemplo, a un perfil que ya estaba cualificado para una de las audiencias asignadas al destino se le ha añadido una nueva identidad en el atributo del mapa de identidad.
* La actualización de perfil estaba determinada por un cambio en los atributos de al menos uno de los atributos asignados al destino. Por ejemplo, uno de los atributos asignados al destino en el paso de asignación se agrega a un perfil.
* El consentimiento cambia para un perfil cuando se configura la aplicación del consentimiento automatizado y un perfil se excluye. La aplicación automática del consentimiento enviará un evento de salida de audiencia al destino para que el perfil no se incluya en ningún objetivo en el destino.

En todos los casos descritos anteriormente, solo los perfiles en los que se han producido actualizaciones relevantes se exportan a su destino. Por ejemplo, si una audiencia asignada al flujo de destino tiene cien miembros y cinco perfiles nuevos cumplen los requisitos para el segmento, la exportación a su destino es incremental y solo incluye los cinco perfiles nuevos.

Tenga en cuenta que todos los atributos asignados se exportan para un perfil, independientemente de dónde se encuentren los cambios. Por lo tanto, en el ejemplo anterior, todos los atributos asignados para esos cinco nuevos perfiles se exportarán incluso si los atributos en sí no han cambiado.

### Qué determina una exportación de datos y qué se incluye en la exportación

Con respecto a los datos que se exportan para un perfil determinado, es importante comprender los dos conceptos diferentes de lo que determina una exportación de datos a su destino de API de flujo continuo y qué datos se incluyen en la exportación.

| Qué determina una exportación de destino | Qué se incluye en la exportación de destino |
|---------|----------|
| <ul><li>Los atributos y audiencias asignados sirven de referencia para una exportación de destino. Esto significa que si alguna audiencia asignada cambia de estado (de `null` a `realized` o de `realized` a `exiting`) o si se actualiza algún atributo asignado, se iniciará una exportación de destino.</li><li>Un cambio en el mapa de identidad se define como una identidad que se agrega o elimina para el [gráfico de identidad](/help/identity-service/features/identity-graph-viewer.md) del perfil, para áreas de nombres de identidad que se asignan para la exportación.</li><li>Un cambio para un atributo se define como cualquier actualización del atributo, para atributos asignados al destino.</li></ul> | <ul><li>Las audiencias asignadas al destino y que han cambiado se incluirán en el objeto `segmentMembership`. En algunos casos, se pueden exportar utilizando varias llamadas. Además, en algunos casos, es posible que algunas audiencias que no han cambiado también se incluyan en la llamada. En cualquier caso, solo se exportarán las audiencias asignadas.</li><li>Todas las identidades de las áreas de nombres asignadas al destino en el objeto `identityMap` también se incluyen</li><li>En la exportación de destino solo se incluyen los atributos asignados.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Los destinos de API de streaming transmiten los datos de relleno al activar perfiles a un destino. Esto significa que la primera exportación de datos después de configurar un flujo de trabajo de activación a un destino incluye perfiles cualificados para la audiencia activada antes de que la audiencia se asigne al destino.

>[!BEGINSHADEBOX]

Por ejemplo, considere este flujo de datos a un destino de streaming en el que se seleccionen tres audiencias en el flujo de datos.

![flujo de datos de destino de streaming](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Una exportación de perfil al destino puede determinarse mediante un perfil que cumpla los requisitos de uno de los tres segmentos asignados o que salga de él. Si un perfil cumple los requisitos para el segmento **Cliente con DeLorean Cars**, se exportará un déclencheur. Las otras audiencias (**Ciudad - Dallas** y **Sitio básico activo**) podrían exportarse también en caso de que el perfil tenga esa audiencia presente con uno de los estados posibles (`realized` o `exited`). Las audiencias que no estén asignadas (como **fans de ciencia ficción**) no se exportarán.

Desde el punto de vista de los atributos de perfil, cualquier cambio en los tres atributos asignados anteriormente determinará una exportación de destino.

>[!ENDSHADEBOX]

## Destinos por lotes (basados en archivos) {#file-based-destinations}

Al exportar perfiles a [destinos basados en archivos](/help/destinations/destination-types.md#file-based) en Experience Platform, existen tres tipos de programaciones (enumeradas a continuación) y dos opciones de exportación de archivos (archivos completos o incrementales) que puede utilizar. Todos estos ajustes se establecen en un nivel de audiencia, incluso cuando se asignan varias audiencias a un único flujo de datos de destino.

* Exportaciones programadas: configure un destino, añada uno o más segmentos, seleccione si desea exportar archivos completos o incrementales y seleccione una hora determinada cada día o varias veces al día en las que se deben exportar los archivos. Por ejemplo, un tiempo de exportación de 5 p. m. significa que los perfiles cualificados para la audiencia se exportarán a las 5 p. m.
* Después de la evaluación de segmentos: la exportación se activa inmediatamente después de que se ejecute el trabajo diario de evaluación de audiencias. Esto significa que los números de perfil exportados en el archivo están lo más cerca posible de la población evaluada más reciente del segmento.
* Exportaciones a petición ([exportar archivo ahora](/help/destinations/ui/export-file-now.md)): en función del trabajo de evaluación de audiencia más reciente, se exporta un archivo completo una vez además de las exportaciones programadas regularmente.

En cualquiera de las situaciones de exportación anteriores, los archivos exportados incluyen los perfiles aptos para la exportación, junto con las columnas seleccionadas como atributos XDM para la exportación.

>[!TIP]
>
>Cuando una audiencia de streaming se asigna a un destino por lotes, existe una mayor probabilidad de que el número de perfiles del archivo exportado sea más cercano al número de usuarios del segmento. Esto se debe a que hay una mayor probabilidad de que la última evaluación de audiencia se haya ejecutado más cerca del tiempo de exportación.

### Exportaciones incrementales de archivos {#incremental-file-exports}

No todas las actualizaciones de un perfil cumplen los requisitos para que un perfil se incluya en las exportaciones de archivos incrementales. Por ejemplo, si un atributo se añadió o se eliminó de un perfil, eso no incluye el perfil en la exportación. Solo los perfiles cuyo atributo `segmentMembership` haya cambiado se incluirán en los archivos exportados. En otras palabras, solo se incluye en las exportaciones de archivos incrementales si el perfil pasa a formar parte de la audiencia o se elimina de la audiencia.

Del mismo modo, si se agrega una nueva identidad (nueva dirección de correo electrónico, número de teléfono, ECID, etc.) a un perfil en el [gráfico de identidad](/help/identity-service/features/identity-graph-viewer.md), eso no representa un motivo para incluir el perfil en una nueva exportación de archivo incremental.

Si se añade una nueva audiencia a una asignación de destino, eso no afecta a las cualificaciones y exportaciones de otro segmento. Las programaciones de exportación se configuran individualmente por audiencia y los archivos se exportan por separado para cada segmento, incluso si las audiencias se han agregado al mismo flujo de datos de destino.

>[!BEGINSHADEBOX]

Por ejemplo, en la configuración de exportación que se muestra a continuación, cuando una audiencia exporta actualizaciones de archivo incrementales, tenga en cuenta las siguientes circunstancias en las que un perfil se incluye en una exportación de archivo incremental o no:

![Exportar configuración con varios atributos seleccionados.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Se incluye un perfil en una exportación de archivo incremental cuando cumple los requisitos o no para el segmento.
* Se incluye un perfil *no* en una exportación de archivo incremental cuando se agrega un nuevo número de teléfono al gráfico de identidad.
* Se incluye un perfil *no* en una exportación de archivo incremental cuando el valor de cualquiera de los campos XDM asignados como `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` se actualiza en un perfil.
* Siempre que el campo XDM `segmentMembership.status` se asigne en el flujo de trabajo de activación de destino, los perfiles que salen de la audiencia también se incluyen en los archivos incrementales exportados, con un estado `exited`.

>[!ENDSHADEBOX]

### Qué determina una exportación de datos y qué se incluye en la exportación

En función de la información de la sección anterior, el comportamiento de exportación de perfiles a destinos basados en archivos se puede resumir como se describe a continuación:

**Exportaciones de archivos completas**

La población activa completa de la audiencia se exporta todos los días.

| Qué determina una exportación de destino | Qué se incluye en el archivo exportado |
|---------|----------|
| <ul><li>La programación de exportación establecida en la interfaz de usuario o la API y la acción del usuario (al seleccionar [Exportar archivo ahora](/help/destinations/ui/export-file-now.md) en la interfaz de usuario o al usar la [API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) determinan el inicio de una exportación de destino.</li></ul> | En las exportaciones de archivos completas, se incluye con cada exportación de archivo toda la población de perfiles activos de un segmento, según la última evaluación de audiencia. Los valores más recientes para cada atributo XDM seleccionado para la exportación también se incluyen como columnas en cada archivo. Tenga en cuenta que los perfiles en estado de salida no se incluyen en la exportación del archivo. |

{style="table-layout:fixed"}

**Exportaciones incrementales de archivos**

En la primera exportación de archivos después de configurar el flujo de trabajo de activación, se exporta toda la población de la audiencia. En las exportaciones posteriores, solo se exportan los perfiles modificados.

| Qué determina una exportación de destino | Qué se incluye en el archivo exportado |
|---------|----------|
| <ul><li>La programación de exportación establecida en la interfaz de usuario o la API determina el inicio de una exportación de destino.</li><li>Cualquier cambio en el abono de audiencia de un perfil, independientemente de si cumple o no los requisitos para pertenecer al segmento, califica un perfil para incluirlo en las exportaciones incrementales. Los cambios en los atributos o en los mapas de identidad de un perfil *no* cumplen los requisitos para que un perfil se incluya en las exportaciones incrementales.</li></ul> | <p>Los perfiles para los que ha cambiado la pertenencia a la audiencia, junto con la información más reciente de cada atributo XDM seleccionado para la exportación.</p><p>Los perfiles con el estado saliente se incluyen en las exportaciones de destino si el campo XDM `segmentMembership.status` está seleccionado en el paso de asignación.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Como recordatorio, los cambios en los valores de atributos o en los mapas de identidad de un perfil no califican un perfil para incluirlo en una exportación de archivo incremental.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe qué ver en las exportaciones de perfiles a destinos de flujo continuo, empresariales y basados en archivos.

A continuación, puede leer cómo se gestionan las [identidades](/help/destinations/how-destinations-work/identity-handling.md) en el flujo de trabajo de activación.
