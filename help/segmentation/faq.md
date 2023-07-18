---
title: Preguntas más frecuentes sobre audiencias
description: Encuentre respuestas a las preguntas frecuentes acerca de las audiencias.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Preguntas frecuentes

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permite crear audiencias a través de definiciones de segmentos u otras fuentes a partir de su [!DNL Real-Time Customer Profile] datos. Estas audiencias se configuran de forma centralizada y se mantienen en Platform, y son fácilmente accesibles desde cualquier solución de Adobe. A continuación se muestra una lista de las preguntas más frecuentes sobre las audiencias y la segmentación.

## ¿Tengo acceso a Audience Portal y a Composición de audiencias?

Audience Portal y Audience Composition están disponibles para todos los clientes de Real-Time CDP Prime y Ultimate (ediciones B2C, B2B y B2P) y para los clientes de Journey Optimizer Select, Prime, Ultimate Starter y Ultimate.

En este momento, solo se admiten audiencias basadas en perfiles. En una versión posterior se añadirá compatibilidad con audiencias basadas en cuentas.

## ¿Las audiencias generadas previamente y generadas externamente son compatibles con Audience Portal?

Sí, las audiencias generadas previamente de forma externa son compatibles con Audience Portal. En este momento, puede importar una audiencia generada externamente a través de un archivo CSV. En el futuro, podrá añadir audiencias a través de conectores de origen por lotes o basados en streaming.

## ¿Puedo reconciliar los datos de audiencia generados externamente con un perfil existente en Platform?

Sí, la audiencia generada de forma externa se combinará con el perfil existente en Platform si coinciden los identificadores principales. Estos datos pueden tardar hasta 24 horas en conciliarse. Si los datos del perfil no existen, se creará un nuevo perfil a medida que se incorporen los datos.

## ¿Puedo utilizar una audiencia generada externamente para crear otras audiencias?

Sí, cualquier audiencia generada externamente aparecerá en el inventario de audiencias y se puede usar al crear audiencias en [Generador de segmentos](./ui/segment-builder.md).

## ¿Puedo utilizar atributos cargados externamente como parte de la segmentación?

No, no puedes. Los atributos de perfil están pensados para ser atributos de larga duración, mientras que los datos de audiencia generados externamente que se cargan solo contienen datos contextuales asociados con esa audiencia generada externamente.

Los datos contextuales de la audiencia generada externamente, o atributos de enriquecimiento, son **no** de larga duración, ya que su ciclo de vida está vinculado a la audiencia cargada. Como resultado, debido a su naturaleza transitoria, estos atributos de enriquecimiento son **no** disponible para su uso en la segmentación.

Sin embargo, al asignar audiencias a destinos por lotes o basados en archivos, puede utilizar estos atributos de enriquecimiento generados externamente para aumentar las audiencias y realizar más activaciones descendentes.

Para obtener más información acerca de esta capacidad, lea la guía de [activación de datos de audiencia en destinos de exportación de perfiles por lotes](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## ¿Puedo activar audiencias generadas externamente en Adobe Journey Optimizer?

En este momento, no. Sin embargo, esta capacidad estará disponible en un futuro próximo.

## ¿Puedo eliminar una audiencia generada externamente?

En este momento, no. En su lugar, puede desactivar o archivar esta audiencia. En este estado, los perfiles **testamento** permanecer activo para su uso en aplicaciones de flujo descendente. En una versión posterior se añadirá compatibilidad para eliminar audiencias generadas externamente.

## ¿Cómo interactúan Audience Portal y Composición de audiencias con la versión de los datos de socios de Real-Time CDP?

Audience Portal y Composición de audiencias interactuarán con los datos de los socios de dos formas:

1. Si introduce una lista de clientes potenciales proporcionada por el socio utilizando la clase y el flujo de trabajo Perfil de clientes potenciales, se conservarán los clientes potenciales **por separado** de combinar perfiles de clientes en el servicio de perfiles. Como resultado, esto significa que las listas de clientes potenciales **no** aparecen en Audience Portal o en Composición de audiencia para su uso.
2. Si utiliza atributos proporcionados por el socio para enriquecer **existente** perfiles de origen, esas audiencias enriquecidas con datos de socios **testamento** aparecen tanto en Audience Portal como en Composición de audiencia para su uso.

## ¿Puedo utilizar audiencias generadas externamente en la composición de audiencias?

En este momento, no. Sin embargo, esta capacidad debería estar disponible en un futuro próximo.

## ¿Puedo enviar audiencias desde Composición de audiencia a todos los canales y destinos de flujo descendente?

En este momento, no. Actualmente, puede utilizar audiencias de Composición de audiencias en Campañas de Adobe Journey Optimizer y destinos de CDP en tiempo real. En una versión futura se admitirán los Recorridos de Adobe Journey Optimizer.

## ¿Hay alguna barrera en el número de composiciones?

En este momento, solo puede tener **10** composiciones publicadas por zona protegida. Se prevé aumentar esta protección en una versión futura.

## ¿Cuáles son las barreras del flujo de trabajo para la composición de audiencias?

La colocación del componente de composición sigue una estructura rígida de la siguiente manera:

1. Usted **siempre** empiece con el [!UICONTROL Audiencia] para seleccionar su actividad de inicio. Puede tener un máximo de **uno** [!UICONTROL Audiencia] Bloque.
2. Si lo desea, puede añadir un [!UICONTROL Excluir] bloque que sigue al [!UICONTROL Audiencia] Bloque.
3. Si lo desea, puede añadir un [!UICONTROL Enriquecer] bloque que sigue al [!UICONTROL Excluir] Bloque.
4. Si lo desea, puede agregar un [!UICONTROL Rango] o [!UICONTROL Split] Bloque. Puede **solamente** tenga uno de estos bloques por composición.
5. Usted **siempre** finalizar con un [!UICONTROL Guardar] para guardar la audiencia.

Para obtener más información sobre el uso de Composición de audiencia, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md).

## ¿Puedo usar una composición de audiencia en otra composición?

No, audiencias creadas con Composición de audiencia **no puede** se utilizará como entrada en otra composición de audiencia.

## ¿Cómo funciona la división en Composición de audiencias?

La división de audiencias permite subdividir aún más la audiencia en grupos más pequeños. Esta división fuerza la exclusividad mutua entre los grupos. Esto significa que si un registro cumple los criterios de varias rutas divididas, se le asigna la variable **primero** ruta desde la izquierda y **no** asignado a cualquiera de las otras rutas.

Para obtener más información sobre el bloque Split, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md#split).

## ¿Puedo utilizar todos los tipos de segmentación en el flujo de trabajo de Composición de audiencia?

Sí, todos los tipos de segmentación ([segmentación por lotes, segmentación de streaming y segmentación de edge](./home.md#evaluate-segments)) son compatibles con el flujo de trabajo de Composición de audiencia. Sin embargo, dado que las composiciones actualmente solo se ejecutan una vez al día, incluso si se incluyen audiencias evaluadas por streaming o por Edge, el resultado se basará en la pertenencia de la audiencia en el momento en que se ejecutó la composición.

## ¿Cómo puedo confirmar la pertenencia de un perfil a una audiencia?

Para confirmar la pertenencia de un perfil a la audiencia, visite la página de detalles del perfil que desee confirmar. Seleccionar **[!UICONTROL Atributos]**, seguido de **[!UICONTROL Ver JSON]**, y puede confirmar que la variable `segmentMembership` contiene el ID de la audiencia.
