---
title: Preguntas más frecuentes sobre audiencias
description: Encuentre respuestas a las preguntas frecuentes acerca de audiencias y otros conceptos relacionados con la segmentación.
source-git-commit: 9a72d85bfb592012b36826135e24d28983f92e40
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 1%

---


# Preguntas frecuentes

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite crear audiencias a través de definiciones de segmentos u otras fuentes a partir de su [!DNL Real-Time Customer Profile] datos. Estas audiencias se configuran de forma centralizada y se mantienen en Platform, y son fácilmente accesibles desde cualquier solución de Adobe. A continuación se muestra una lista de las preguntas más frecuentes sobre las audiencias y la segmentación.

## Audience Portal

En la siguiente sección se enumeran las preguntas relacionadas con Audience Portal.

### ¿Tengo acceso a Audience Portal y a Composición de audiencias?

Audience Portal y Audience Composition están disponibles para todos los clientes de Real-Time CDP Prime y Ultimate (ediciones B2C, B2B y B2P) y para los clientes de Journey Optimizer Select, Prime, Ultimate Starter y Ultimate.

En este momento, solo se admiten audiencias basadas en perfiles. En una versión posterior se añadirá compatibilidad con audiencias basadas en cuentas.

### ¿Las audiencias generadas previamente y generadas externamente son compatibles con Audience Portal?

Sí, las audiencias generadas previamente de forma externa son compatibles con Audience Portal. En este momento, puede importar una audiencia generada externamente a través de un archivo CSV. En el futuro, podrá añadir audiencias a través de conectores de origen por lotes o basados en streaming.

### ¿Puedo reconciliar los datos de audiencia generados externamente con un perfil existente en Platform?

Sí, la audiencia generada de forma externa se combinará con el perfil existente en Platform si coinciden los identificadores principales. Estos datos pueden tardar hasta 24 horas en conciliarse. Si los datos del perfil no existen, se creará un nuevo perfil a medida que se incorporen los datos.

## ¿Puedo utilizar una audiencia generada externamente para crear otras audiencias?

Sí, cualquier audiencia generada externamente aparecerá en el inventario de audiencias y se puede usar al crear audiencias en [Generador de segmentos](./ui/segment-builder.md).

### ¿Puedo utilizar atributos cargados externamente como parte de la segmentación?

No, no puedes. Los atributos de perfil están pensados para ser atributos de larga duración, mientras que los datos de audiencia generados externamente que se cargan solo contienen datos contextuales asociados con esa audiencia generada externamente.

Los datos contextuales de la audiencia generada externamente, o atributos de enriquecimiento, son **no** de larga duración, ya que su ciclo de vida está vinculado a la audiencia cargada. Como resultado, debido a su naturaleza transitoria, estos atributos de enriquecimiento son **no** disponible para su uso en la segmentación.

Sin embargo, al asignar audiencias a destinos por lotes o basados en archivos, puede utilizar estos atributos de enriquecimiento generados externamente para aumentar las audiencias y realizar más activaciones descendentes.

Para obtener más información acerca de esta capacidad, lea la guía de [activación de datos de audiencia en destinos de exportación de perfiles por lotes](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### ¿Puedo activar audiencias generadas externamente en Adobe Journey Optimizer?

En este momento, no. Sin embargo, esta capacidad estará disponible en un futuro próximo.

### ¿Puedo eliminar una audiencia generada externamente?

En este momento, no. En su lugar, puede desactivar o archivar esta audiencia. En este estado, los perfiles **testamento** permanecer activo para su uso en aplicaciones de flujo descendente. En una versión posterior se añadirá compatibilidad para eliminar audiencias generadas externamente.

### ¿Qué representan los distintos estados del ciclo vital?

El siguiente gráfico explica los diferentes estados del ciclo vital, qué representan, dónde se pueden utilizar las audiencias con ese estado, así como el impacto en las protecciones de segmentación.

| Estado | Definición | ¿Visible en Audience Portal? | ¿Visible en destinos? | ¿Afecta a los límites de segmentación? | Impacto en las audiencias basadas en archivos | Impacto en la evaluación de audiencias | ¿Se puede usar dentro de otras audiencias? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Borrador | Una audiencia en **Borrador** el estado es una audiencia que aún está en desarrollo y que aún no está lista para utilizarse en otros servicios. | Sí, pero se puede ocultar. | No | Sí | Se puede importar o actualizar durante el proceso de refinamiento. | Se puede evaluar para obtener recuentos de publicación precisos. | Sí, pero no se recomienda su uso. |
| Publicadas | Una audiencia en **Publicado** El estado es una audiencia lista para usar en todos los servicios descendentes. | Sí | Sí | Sí | Se puede importar o actualizar. | Se evalúa mediante segmentación por lotes, flujo continuo o de Edge. | Sí |
| Inactivo | Una audiencia en **Inactivo** El estado es una audiencia que no está en uso actualmente. Sigue existiendo dentro de Platform, pero lo hará **no** se puede utilizar hasta que se marque como borrador o se publique. | No, pero se puede mostrar. | No | No | No ya no se actualiza. | Platform ya no lo evalúa ni actualiza. | Sí |
| Eliminado | Una audiencia en **Eliminado** El estado es una audiencia que se ha eliminado. La eliminación real de los datos puede tardar hasta unos minutos en ejecutarse. | No | No | No | Se eliminan los datos subyacentes. | No se realiza ninguna evaluación ni ejecución de los datos una vez completada la eliminación. | No |

### ¿Cómo interactúan Audience Portal y Composición de audiencias con la versión de los datos de socios de Real-Time CDP?

Audience Portal y Composición de audiencias interactuarán con los datos de los socios de dos formas:

1. Si introduce una lista de clientes potenciales proporcionada por el socio utilizando la clase y el flujo de trabajo Perfil de clientes potenciales, se conservarán los clientes potenciales **por separado** de combinar perfiles de clientes en el servicio de perfiles. Como resultado, esto significa que las listas de clientes potenciales **no** aparecen en Audience Portal o en Composición de audiencia para su uso.
2. Si utiliza atributos proporcionados por el socio para enriquecer **existente** perfiles de origen, esas audiencias enriquecidas con datos de socios **testamento** aparecen tanto en Audience Portal como en Composición de audiencia para su uso.

### ¿Cómo puedo usar atributos adicionales con mis audiencias?

Con las audiencias, hay **dos** diferentes tipos de atributos adicionales que puede añadir: atributos de carga útil (contextuales) y atributos de enriquecimiento.

Los atributos de carga útil son atributos que se incorporan como parte de la carga CSV de una audiencia generada externamente. Estos atributos son **no** se incorpora en el Perfil del cliente en tiempo real, pero se puede utilizar como parte de un destino descendente.

Los atributos de enriquecimiento son atributos que provienen de un conjunto de datos y se unen a una audiencia en Composición de audiencia. Actualmente, estos atributos solo se pueden utilizar en campañas de Adobe Journey Optimizer. La compatibilidad con los recorridos de Adobe Journey Optimizer estará disponible próximamente y la compatibilidad con los destinos descendentes estará pendiente de una versión futura.

| Canal de activación | Audiencias de carga personalizada en CSV | Audiencias de la composición de audiencias |
| --- | --- | --- |
| Destinos de Real-Time CDP | Se pueden activar tanto los atributos de carga útil como las audiencias. | Solo se puede activar la audiencia. Atributos de enriquecimiento **no puede** se activará. |
| Adobe Journey Optimizer Campaigns | Ni los atributos de audiencia ni los de carga útil pueden activarse. | Se pueden activar tanto la audiencia como los atributos de ampliación. |

## Inventario de audiencias

En las secciones siguientes se enumeran las preguntas relacionadas con el inventario de audiencias dentro de Audience Portal.

### ¿Necesito permisos adicionales para utilizar las funciones del inventario de audiencias?

No, tú no. Siempre que tenga permisos de edición para audiencias, podrá crear, actualizar y administrar sus carpetas y etiquetas dentro del Portal de audiencias. Para obtener más información sobre la administración de permisos, lea la [guía de administración de permisos](../access-control/ui/permissions.md).

### ¿Hay un límite en el número de carpetas que puedo crear?

No, no hay límite en el número de carpetas que puede crear. Para obtener más información sobre las carpetas, lea la [sección inventario de audiencias](./ui/overview.md#folders) de la Información general sobre la IU del Servicio de segmentación.

### ¿Hay un límite en el número de etiquetas que se pueden añadir a una audiencia?

No, no hay límite en el número de etiquetas que se pueden añadir a una audiencia. Para obtener más información sobre las etiquetas, lea la [sección inventario de audiencias](./ui/overview.md#tags) de la Información general sobre la IU del Servicio de segmentación.

### ¿Hay un límite en el número de etiquetas que puedo crear?

No, no hay límite en el número de etiquetas que puede crear. Sin embargo, puede crear un máximo de **100** categorías que se aplicarán a las etiquetas. Para obtener más información sobre la administración de etiquetas, lea la [Guía de administración de etiquetas](../administrative-tags/ui/managing-tags.md).

### Cuando busco una audiencia por nombre o etiqueta en una carpeta principal, ¿puedo también buscar en las carpetas secundarias relacionadas?

No, este comportamiento no es compatible. Sin embargo, puede cambiar la vista de inventario de audiencias para que mire **Todas las audiencias**, luego busque en todas las carpetas. Para obtener más información sobre el uso de la búsqueda en el inventario de audiencias, lea la [sección de búsqueda](./ui/overview.md#search) de la Información general sobre la IU del Servicio de segmentación.

### ¿Puedo asignar automáticamente una audiencia a una carpeta en el momento de la creación?

En este momento, no. Sin embargo, esta capacidad puede estar disponible en el futuro.

### ¿Puedo mover varias audiencias a una carpeta al mismo tiempo?

En este momento, no. Sin embargo, esta capacidad puede estar disponible en el futuro.

## Composición de público

En la siguiente sección se enumeran las preguntas relacionadas con la Composición de audiencias.

### ¿Cuándo debo usar Composición de audiencia en lugar de usar el Generador de segmentos?

Tanto la Composición de audiencias como el Generador de segmentos tienen una función importante en la creación de audiencias en Platform.

El Generador de segmentos es más adecuado para la audiencia **creación** (para crear una audiencia desde cero), mientras que Composición de audiencia es más adecuada para la audiencia **depuración** (para crear nuevas audiencias basadas en una audiencia existente).

La siguiente tabla ilustra la diferencia entre los dos servicios:

| Generador de segmentos | Composición de público |
| --------------- | -------------------- |
| <ul><li>Generación de audiencias de un solo escenario</li><li>Crea los bloques básicos de audiencias a partir de datos de perfil, series temporales y de varias entidades</li><li>Se utiliza para crear **uno** audiencia</li></ul> | <ul><li>Generación de audiencias de varias fases mediante operaciones basadas en conjuntos</li><li>Utiliza las audiencias creadas por el Generador de segmentos y aplica opciones de enriquecimiento de datos como la clasificación de atributos de perfil</li><li>Se utiliza para crear **múltiple** audiencias a la vez</li></ul> |

Para obtener más información sobre el Generador de segmentos, lea la [Guía del Generador de segmentos](./ui/segment-builder.md). Para obtener más información sobre la composición de la audiencia, lea la [Guía de composición de audiencias](./ui/audience-composition.md).

### ¿Puedo utilizar audiencias generadas externamente en la composición de audiencias?

En este momento, no. Sin embargo, esta capacidad debería estar disponible en un futuro próximo.

### ¿Puedo enviar audiencias desde Composición de audiencia a todos los canales y destinos de flujo descendente?

En este momento, no. Actualmente, puede utilizar audiencias de Composición de audiencias en Campañas de Adobe Journey Optimizer y destinos de CDP en tiempo real. En una versión futura se admitirán los Recorridos de Adobe Journey Optimizer.

### ¿Hay alguna barrera en el número de composiciones?

En este momento, solo puede tener **10** composiciones publicadas por zona protegida. Se prevé aumentar esta protección en una versión futura.

### ¿Cuáles son las barreras del flujo de trabajo para la composición de audiencias?

La colocación del componente de composición sigue una estructura rígida de la siguiente manera:

1. Usted **siempre** empiece con el [!UICONTROL Audiencia] para seleccionar su actividad de inicio. Puede tener un máximo de **uno** [!UICONTROL Audiencia] Bloque.
2. Si lo desea, puede añadir un [!UICONTROL Excluir] bloque que sigue al [!UICONTROL Audiencia] Bloque.
3. Si lo desea, puede añadir un [!UICONTROL Enriquecer] bloque que sigue al [!UICONTROL Excluir] Bloque.
4. Si lo desea, puede agregar un [!UICONTROL Rango] o [!UICONTROL Split] Bloque. Puede **solamente** tenga uno de estos bloques por composición.
5. Usted **siempre** finalizar con un [!UICONTROL Guardar] para guardar la audiencia.

Para obtener más información sobre el uso de Composición de audiencia, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md).

### ¿Puedo usar una composición de audiencia en otra composición?

No, audiencias creadas con Composición de audiencia **no puede** se utilizará como entrada en otra composición de audiencia.

### ¿Cómo funciona la división en Composición de audiencias?

La división de audiencias permite subdividir aún más la audiencia en grupos más pequeños. Esta división fuerza la exclusividad mutua entre los grupos. Esto significa que si un registro cumple los criterios de varias rutas divididas, se le asigna la variable **primero** ruta desde la izquierda y **no** asignado a cualquiera de las otras rutas.

Para obtener más información sobre el bloque Split, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md#split).

### ¿Puedo utilizar todos los tipos de segmentación en el flujo de trabajo de Composición de audiencia?

Sí, todos los tipos de segmentación ([segmentación por lotes, segmentación de streaming y segmentación de edge](./home.md#evaluate-segments)) son compatibles con el flujo de trabajo de Composición de audiencia. Sin embargo, dado que las composiciones actualmente solo se ejecutan una vez al día, incluso si se incluyen audiencias evaluadas por streaming o por Edge, el resultado se basará en la pertenencia de la audiencia en el momento en que se ejecutó la composición.

## ¿Cómo puedo confirmar la pertenencia de un perfil a una audiencia?

Para confirmar la pertenencia de un perfil a la audiencia, visite la página de detalles del perfil que desee confirmar. Seleccionar **[!UICONTROL Atributos]**, seguido de **[!UICONTROL Ver JSON]**, y puede confirmar que la variable `segmentMembership` contiene el ID de la audiencia.
