---
title: Preguntas más frecuentes sobre los atributos calculados
description: Encuentre respuestas a las preguntas más frecuentes acerca del uso de atributos calculados.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# Preguntas frecuentes

En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. A continuación se muestra una lista de las preguntas más frecuentes sobre los atributos calculados.

## ¿Cómo puedo obtener acceso a los atributos calculados?

Para obtener acceso a los atributos calculados, debe tener los permisos adecuados (**Ver atributos calculados** y **Administrar atributos calculados**). Para obtener más información sobre los permisos necesarios, lea la [documentación de control de acceso](../../access-control/home.md). Para obtener información sobre cómo aplicar estos permisos, lea la [guía de administración de permisos](../../access-control/ui/permissions.md).

## ¿Qué conjuntos de datos contribuyen a los cálculos de atributos calculados?

Los atributos calculados tienen en cuenta los conjuntos de datos de evento de experiencia habilitados para Perfil del cliente en tiempo real para calcular los atributos calculados.

## ¿Qué campos del modelo de datos de experiencia (XDM) se pueden utilizar para crear atributos calculados?

Todos los campos XDM del esquema de unión de Experience Event se pueden utilizar para crear atributos calculados.

## ¿Qué representan la &quot;última evaluación&quot; y el &quot;último estado de evaluación&quot;?

Última evaluación hace referencia a la marca de tiempo hasta la cual los eventos se consideran en la última ejecución correcta. El último estado de evaluación hace referencia a si la última ejecución de evaluación se realizó correctamente o no.

## ¿Puedo elegir la frecuencia de actualización? ¿Cómo se decide esto?

La frecuencia de actualización se determina automáticamente en función del período retroactivo del atributo calculado. Para obtener más información al respecto, lea la [sección de período retrospectivo](./overview.md#lookback-periods) de la descripción general de los atributos calculados.

## ¿En qué afecta a los cálculos la caducidad de los datos de Experience Event?

Los cálculos de atributos calculados se rellenan con la duración de retrospectiva definida en la primera evaluación y se actualizan en función de los eventos incrementales para las actualizaciones posteriores. Como resultado, estos cálculos son **no** se ve afectado por la caducidad de los datos de Experience Event de los datos antiguos después de la primera evaluación.

Por ejemplo, si crea un atributo calculado que se evalúa mensualmente con un periodo retrospectivo de tres meses, para la primera evaluación, el atributo calculado calculará para todos los eventos dentro de ese periodo retrospectivo de tres meses. Incluso si el conjunto de datos de evento de experiencia tiene una caducidad de datos de un mes, esta caducidad de datos **no** afectan a la actualización mensual de atributos calculados, ya que la ejecución de evaluación del mes siguiente acumulará eventos de forma incremental y actualizará el cálculo.

>[!NOTE]
>
>Datos caducados **no puede** Rellenarse más tarde con un atributo calculado. Caducidad de datos del conjunto de datos de eventos **mayo** se ha limitado la capacidad de validar el valor del atributo calculado en un momento posterior. Para validar el valor de atributo calculado, el periodo retroactivo debe permanecer **dentro** los límites de la caducidad de los datos.

## ¿Puedo crear un atributo calculado basado en otro atributo calculado?

Dado que los atributos calculados se crean mediante campos de Evento de experiencia y residen en un campo de Perfil, no hay forma de utilizar directamente un atributo calculado para crear otro atributo calculado.

## ¿Hay algún límite en el número de atributos calculados que puedo crear?

Sí, hay un límite en el número de atributos calculados que puede crear. Consulte la descripción del producto o póngase en contacto con el equipo de cuenta de Adobe para obtener más información.

## ¿Hay alguna consecuencia en sentido descendente de la desactivación de un atributo calculado?

Antes de deshabilitar el atributo calculado, debe hacer lo siguiente **debería** elimínelos de sus sistemas descendentes (como la segmentación, los recorridos o los destinos), ya que puede haber complicaciones que surjan si no se eliminan.

## ¿Qué sucede cuando se deshabilita un atributo calculado? {#inactive-status}

Cuando un atributo calculado está deshabilitado o inactivo, ya no se actualiza. Como resultado, este atributo calculado **no puede** se utilizará en la búsqueda de perfiles u otros usos posteriores.

## ¿Cómo ayudan los atributos calculados a impulsar la participación?

Los atributos calculados impulsan el enriquecimiento de perfiles al añadir los atributos de evento a un nivel de perfil combinado. Por ejemplo, puede personalizar los correos electrónicos de marketing con el último producto visualizado.

## ¿Con qué frecuencia se evalúan los atributos calculados? ¿Está relacionado con el programa de evaluación de audiencias?

Los atributos calculados se evalúan en una **lote** frecuencia que es **independiente** Consulte la programación de la evaluación de audiencia, destino y recorrido. Esto significa que, independientemente del tipo de segmentación (segmentación por lotes o segmentación por flujo continuo), el atributo calculado se evalúa según su propia programación (por hora, diariamente, semanalmente o mensualmente).

La primera evaluación del atributo calculado se produce dentro de las 24 horas siguientes a su **creación**. Las evaluaciones por lotes subsiguientes se producen cada hora, cada día, cada semana o cada mes, según el periodo retrospectivo definido.

Por ejemplo, si se realiza una primera evaluación a las 12:00 UTC del 9 de octubre, las evaluaciones posteriores se producirían en los momentos siguientes:

- Próxima actualización diaria: 12:00 UTC el 10 de octubre
- Próxima actualización semanal: 12:00 UTC el 15 de octubre
- Próxima actualización mensual: 12:00 UTC el 1 de noviembre

>[!IMPORTANT]
>
>Este solo es el caso si la actualización rápida es **no** activado. Para obtener información sobre cómo cambia el período retroactivo cuando la actualización rápida está habilitada, lea la [sección de actualización rápida](./overview.md#fast-refresh).

Tanto la **semanalmente** y **mensualmente** las actualizaciones se realizan al principio del **semana natural** (el domingo de la nueva semana) o el comienzo de la **mes natural** (el primero del nuevo mes), a diferencia de exactamente una semana o un mes después de la primera fecha de evaluación.

>[!NOTE]
>
>El valor de atributo calculado es **no** se actualiza inmediatamente en el perfil después de cada ejecución de evaluación. Para asegurarse de que el valor actualizado esté en los perfiles, debe considerar un búfer de unas pocas horas entre el tiempo de evaluación y el uso de atributos calculados. La programación de actualización de atributos calculada es **determinado por el sistema** y **no puede** no se puede modificar. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe.

## ¿Cómo interactúan los atributos calculados con las audiencias evaluadas mediante la segmentación de flujo continuo?

Si una audiencia evaluada por segmentación de flujo continuo utiliza un atributo calculado, tomará el **último valor** del atributo calculado mientras se evalúa la audiencia. Por ejemplo, si la audiencia busca eventos de compra, la audiencia hará referencia al último valor de atributo calculado evaluado cuando se produzca el evento de compra.

## ¿Puedo utilizar atributos calculados en Edge?

Al igual que cualquier otro atributo de perfil, los atributos calculados están disponibles y se pueden utilizar en perímetros. Los atributos calculados son los siguientes **no** calculado en edge.

## ¿Cómo se aplican las etiquetas de uso de datos en los atributos calculados?

Los atributos calculados derivan automáticamente las etiquetas de uso de datos de los campos y conjuntos de datos de origen que se utilizaron para definir los atributos calculados. Esto garantiza que los datos de comportamiento se utilicen correctamente.

## ¿Cómo se utilizan los atributos calculados con Adobe Journey Optimizer?

Para utilizar atributos calculados en recorridos, debe añadir el `SystemComputedAttributes` grupo de campos al origen de datos del Experience Platform. Para obtener más información sobre la configuración de la fuente de datos de Experience Platform, lea la [Guía de fuente de datos de Adobe Experience Platform](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html).
