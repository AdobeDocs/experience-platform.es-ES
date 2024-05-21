---
title: Preguntas más frecuentes sobre audiencias
description: Encuentre respuestas a las preguntas frecuentes acerca de audiencias y otros conceptos relacionados con la segmentación.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 6088dc06af6db2ce1a86a9638df23453184864b2
workflow-type: tm+mt
source-wordcount: '4056'
ht-degree: 0%

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

### ¿Qué permisos necesito tener para poder cargar audiencias generadas externamente?

Para cargar audiencias generadas externamente, debe tener los permisos de &quot;Ver segmentos&quot;, &quot;Administrar segmentos&quot; e &quot;Importar audiencias&quot;. No se requieren controles específicos basados en funciones para cargar audiencias generadas externamente.

### ¿Qué sucede cuando se carga una audiencia generada externamente?

Al cargar una audiencia generada externamente, se crean los siguientes elementos:

- Conjunto de datos
   - El conjunto de datos será visible dentro del inventario del conjunto de datos y su nombre será **igual** como el nombre de la audiencia generada externamente que ha cargado.
- Trabajo por lotes
   - Un trabajo por lotes **automáticamente** ejecutar al cargar una audiencia generada externamente. Esto significa que sí **no** Debe esperar a que se ejecute el trabajo de segmentación diario para activar la audiencia generada externamente.
- Esquema ad hoc
   - A **nuevo** Se creará un esquema XDM para utilizarlo con la audiencia generada externamente. Los campos de este esquema XDM tienen un espacio de nombres para su uso con el conjunto de datos también creado.

### ¿De qué se compone una audiencia generada externamente y qué sucede con estos datos cuando se importan en Platform?

Durante el flujo de trabajo de importación de audiencia externa, se debe especificar qué columna del archivo CSV corresponde con la columna **Identidad principal**. Un ejemplo de identidad principal incluye una dirección de correo electrónico, un ECID o un área de nombres de identidad personalizada específica de la organización.

Los datos asociados con esta columna de identidad principal son **solamente** datos adjuntos al perfil de. Si no hay perfiles que coincidan con los datos en la columna de identidad principal, se creará un nuevo perfil. Sin embargo, este perfil es esencialmente un perfil huérfano ya que **no** los atributos o eventos de experiencia están asociados a este perfil.

Se tienen en cuenta todos los demás datos de la audiencia generada externamente **atributos de carga útil**. Estos atributos pueden **solamente** se utilizarán para la personalización y el enriquecimiento durante la activación, y son **no** adjunto a un perfil. Sin embargo, estos atributos se almacenan en el lago de datos.

Aunque se puede hacer referencia a la audiencia generada externamente al crear audiencias con el Generador de segmentos, los atributos de perfil individuales **no puede** se utilizará.

### ¿Puedo reconciliar los datos de audiencia generados externamente con un perfil existente en Platform?

Sí, la audiencia generada de forma externa se combinará con el perfil existente en Platform si coinciden los identificadores principales. Estos datos pueden tardar hasta 24 horas en conciliarse. Si los datos del perfil no existen, se creará un nuevo perfil a medida que se incorporen los datos.

### ¿Puedo utilizar una audiencia generada externamente para crear otras audiencias?

Sí, cualquier audiencia generada externamente aparecerá en el inventario de audiencias y se puede usar al crear audiencias en [Generador de segmentos](./ui/segment-builder.md).

### ¿Puedo utilizar atributos cargados externamente como parte de la segmentación?

No, no puedes. Los atributos de perfil están pensados para ser atributos de larga duración, mientras que los datos de audiencia generados externamente que se cargan solo contienen datos contextuales asociados con esa audiencia generada externamente.

Los datos contextuales de la audiencia generada externamente, o atributos de enriquecimiento, son **no** de larga duración, ya que su ciclo de vida está vinculado a la audiencia cargada. Como resultado, debido a su naturaleza transitoria, estos atributos de enriquecimiento son **no** disponible para su uso en la segmentación.

Sin embargo, al asignar audiencias a destinos por lotes o basados en archivos, puede utilizar estos atributos de enriquecimiento generados externamente para aumentar las audiencias y realizar más activaciones descendentes.

Para obtener más información acerca de esta capacidad, lea la guía de [activación de datos de audiencia en destinos de exportación de perfiles por lotes](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### ¿Existe una política de combinación específica para audiencias generadas externamente?

La política de combinación predeterminada específica de la organización se aplica automáticamente al cargar audiencias generadas externamente. Sin embargo, puede cambiar la política de combinación que se aplica a la audiencia generada externamente durante el flujo de trabajo de importación de audiencia.

### ¿Dónde puedo activar audiencias generadas externamente para?

Una audiencia generada externamente se puede asignar a cualquier destino RTCDP y se puede utilizar en campañas de Adobe Journey Optimizer.

### ¿Cuándo están listas las audiencias generadas externamente para su activación?

Si se activa en un destino de flujo continuo, los datos de la audiencia generada externamente estarán disponibles en un plazo de dos horas.

Si se activa en un destino por lotes, los datos de la audiencia generada externamente se sincronizarán con el siguiente trabajo de segmentación de 24 horas.

### ¿Puedo eliminar una audiencia generada externamente?

¡Sí! Las audiencias generadas externamente se pueden eliminar en Audience Portal.

### ¿Qué debo hacer si subo accidentalmente una audiencia generada externamente?

Si ha cargado accidentalmente una audiencia generada externamente y desea eliminar los datos, puede borrar los perfiles asociados con la audiencia cargando un archivo CSV con una fila y sin datos.

### ¿Cuánto tiempo duran las audiencias generadas externamente?

La caducidad de los datos actuales para las audiencias generadas de forma externa es **30 días**. Esta caducidad de datos se eligió para reducir la cantidad de datos sobrantes almacenados en su organización.

Una vez transcurrido el período de caducidad de los datos, el conjunto de datos asociado seguirá siendo visible dentro del inventario de conjuntos de datos, pero lo hará **no** poder activar la audiencia, y el recuento de perfiles se mostrará como cero.

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

## Estados del ciclo vital {#lifecycle-states}

En la siguiente sección se enumeran las preguntas relacionadas con los estados del ciclo vital y la administración del estado del ciclo vital en Audience Portal.

### ¿Qué representan los distintos estados del ciclo vital?

El siguiente gráfico explica los diferentes estados del ciclo vital, qué representan, dónde se pueden utilizar las audiencias con ese estado, así como el impacto en las protecciones de segmentación.

| Estado | Definición | ¿Visible en Audience Portal? | ¿Visible en destinos? | ¿Afecta a los límites de segmentación? | Impacto en las audiencias basadas en archivos | Impacto en la evaluación de audiencias | ¿Se puede usar dentro de otras audiencias? | Editable |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Borrador | Una audiencia en **Borrador** el estado es una audiencia que aún está en desarrollo y que aún no está lista para utilizarse en otros servicios. | Sí, pero se puede ocultar. | No | Sí | Se puede importar o actualizar durante el proceso de refinamiento. | Se puede evaluar para obtener recuentos de publicación precisos. | Sí, pero no se recomienda su uso. | Sí |
| Publicadas | Una audiencia en **Publicado** El estado es una audiencia lista para usar en todos los servicios descendentes. | Sí | Sí | Sí | Se puede importar o actualizar. | Se evalúa mediante segmentación por lotes, flujo continuo o de Edge. | Sí | Sí |
| Inactivo | Una audiencia en **Inactivo** El estado es una audiencia que no está en uso actualmente. Sigue existiendo dentro de Platform, pero lo hará **no** se puede utilizar hasta que se marque como borrador o se publique. | No, pero se puede mostrar. | No | No | Ya no se actualiza. | Platform ya no lo evalúa ni actualiza. | Sí | Sí |
| Eliminado | Una audiencia en **Eliminado** El estado es una audiencia que se ha eliminado. La eliminación real de los datos puede tardar hasta unos minutos en ejecutarse. | No | No | No | Se eliminan los datos subyacentes. | No se realiza ninguna evaluación ni ejecución de los datos una vez completada la eliminación. | No | No |

### ¿En qué estados puedo editar mis audiencias?

Las audiencias se pueden editar en los siguientes estados del ciclo vital:

- **Borrador**: Si una audiencia se edita en estado de borrador, permanecerá en estado de borrador a menos que se publique explícitamente.
- **Publicado**: Si una audiencia se edita en el estado publicado, seguirá publicándose y la audiencia se actualizará automáticamente.
- **Inactivo**: Si una audiencia se edita en estado inactivo, permanecerá inactiva. Esto significa que no se evaluará ni actualizará. Si necesita actualizar la audiencia, debe publicar la audiencia.

Una vez eliminada una audiencia, **no puede** no se puede editar.

### ¿A qué estados del ciclo vital puedo mover una audiencia?

Los posibles estados del ciclo de vida a los que se puede mover una audiencia dependen del estado actual de la audiencia.

![Diagrama que describe las posibles transiciones de estado del ciclo vital disponibles para las audiencias.](./images/faq/lifecycle-state-transition.png)

Si la audiencia está en estado de borrador, puede publicarla o eliminarla si la audiencia no tiene dependientes.

Si la audiencia está en el estado publicado, puede desactivarla o eliminarla si la audiencia no tiene dependientes.

Si la audiencia está en estado inactivo, puede volver a publicarla o eliminarla si la audiencia no tiene dependientes.

### ¿Hay advertencias para audiencias en determinados estados del ciclo vital?

Las audiencias en estado publicado solo se pueden mover a otro estado si la audiencia lo hace **no** tiene cualquier dependiente. Esto significa que si la audiencia se utiliza en un servicio descendente, no se puede desactivar ni eliminar.

Si se vuelve a publicar una audiencia que se evalúa mediante segmentación por lotes, es decir, cuando una audiencia pasa de inactiva a publicada, la audiencia se actualiza **después** el trabajo por lotes diario. Cuando se vuelva a publicar por primera vez, los perfiles y datos serán los siguientes **igual** como cuando la audiencia quedó inactiva.

### ¿Cómo puedo colocar una audiencia en estado de borrador?

El método para colocar una audiencia en el estado de borrador depende del origen de la audiencia.

Para las audiencias creadas con el Generador de segmentos, puede establecer la audiencia en el estado de borrador seleccionando &quot;[!UICONTROL Guardar como borrador]&quot; en el Generador de segmentos.

Para las audiencias creadas en Composición de audiencia, las audiencias se guardan automáticamente como borrador hasta su publicación.

Para las audiencias creadas externamente, las audiencias se publican automáticamente.

Una vez que una audiencia esté en el estado publicado, debe **no puede** vuelva a cambiar la audiencia original al estado de borrador. Sin embargo, si copia la audiencia, la audiencia recién copiada estará en estado de borrador.

### ¿Cómo puedo colocar una audiencia en el estado publicado?

Para las audiencias creadas con el Generador de segmentos o la Composición de audiencias, puede establecer la audiencia en el estado publicado seleccionando &quot;[!UICONTROL Publish]&quot; en sus respectivas IU.

Las audiencias creadas externamente se establecen automáticamente como publicadas.

### ¿Cómo puedo poner una audiencia en estado inactivo?

Puede poner una audiencia publicada en el estado inactivo abriendo el menú de acciones rápidas en Audience Portal y seleccionando &quot;[!UICONTROL Desactivar]&quot;.

### ¿Cómo puedo volver a publicar una audiencia?

>[!NOTE]
>
>El estado &quot;Volver a publicar&quot; es el mismo que el estado publicado para el comportamiento de audiencia.

Para volver a publicar una audiencia, seleccione una audiencia que esté en estado inactivo, abra el menú de acciones rápidas en Audience Portal y seleccione [!UICONTROL Publish].

### ¿Cómo puedo poner una audiencia en el estado eliminado?

>[!IMPORTANT]
>
>Solo puede eliminar audiencias que estén **no** se utiliza en cualquier activación descendente. Tampoco puede eliminar una audiencia a la que se haga referencia en otra audiencia. Si no puede eliminar su audiencia, asegúrese de que esté **no** utilizarlo en cualquier servicio descendente o como componente básico de otra audiencia.

Para poner una audiencia en el estado de eliminación, abra el menú de acciones rápidas en Audience Portal y seleccione [!UICONTROL Eliminar].

### ¿Hay alguna advertencia para las transiciones de estado del ciclo vital?

Sí, hay que tener en cuenta algunas advertencias cuando se utilizan audiencias en servicios descendentes, como Adobe Journey Optimizer, o audiencias no basadas en clientes, como audiencias basadas en cuentas.

En este momento, usted **debe** compruebe manualmente si la audiencia se utiliza en sentido descendente en Adobe Journey Optimizer, ya que este estado no se comprueba automáticamente en la actualidad.

Además, puede **debe** compruebe manualmente si la audiencia se utiliza como componente de una audiencia basada en cuentas, ya que este estado tampoco se comprueba automáticamente en este momento.

### ¿Afecta el uso de una audiencia como audiencia secundaria a las transiciones de estado del ciclo vital?

>[!NOTE]
>
>Una audiencia principal es una audiencia que **utiliza** otra audiencia como dependencia de la audiencia.
>
>Una audiencia secundaria es una audiencia que **se usa como** una dependencia para la audiencia.

Sí, el uso de una audiencia como audiencia secundaria afecta a las transiciones de estados del ciclo vital que pueden realizar la audiencia principal y la secundaria.

Para que una audiencia secundaria se mueva al estado publicado, seleccione toda su audiencia principal **debe** estar en estado publicado. Las audiencias principales se pueden publicar antes de publicar la audiencia secundaria o, si el usuario lo confirma, se pueden publicar automáticamente cuando se publica la audiencia secundaria.

Para que la audiencia principal se mueva al estado inactivo o eliminado, todas sus audiencias secundarias **debe** desactivarse o eliminarse.

### ¿Puedo hacer referencia a una audiencia que está en un estado de ciclo de vida diferente?

¡Sí! Si la audiencia está actualmente en estado de borrador, puede hacer referencia a audiencias en estado publicado o inactivo. Sin embargo, para publicar esta audiencia, debe **debe** publicar las demás audiencias principales.

## Inventario de audiencias

En la siguiente sección se enumeran las preguntas relacionadas con el inventario de audiencias dentro de Audience Portal.

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

El Generador de segmentos es más adecuado para la audiencia **creación** (para crear una audiencia desde cero), mientras que Composición de audiencia es más adecuada para la audiencia **depuración y personalización** (para crear nuevas audiencias basadas en una audiencia existente).

La siguiente tabla ilustra la diferencia entre los dos servicios:

| Generador de segmentos | Composición de público |
| --------------- | -------------------- |
| <ul><li>Generación de audiencias de un solo escenario</li><li>Crea los bloques básicos de audiencias a partir de datos de perfil, series temporales y de varias entidades</li><li>Se utiliza para crear **uno** audiencia</li></ul> | <ul><li>Generación de audiencias de varias fases mediante operaciones basadas en conjuntos</li><li>Utiliza las audiencias creadas por el Generador de segmentos y aplica opciones de enriquecimiento de datos como la clasificación de atributos de perfil y la división en subaudiencias</li><li>Se utiliza para crear **múltiple** audiencias a la vez</li></ul> |

Para obtener más información sobre el Generador de segmentos, lea la [Guía del Generador de segmentos](./ui/segment-builder.md). Para obtener más información sobre la composición de la audiencia, lea la [Guía de composición de audiencias](./ui/audience-composition.md).

### ¿Puedo utilizar audiencias generadas externamente en la composición de audiencias?

En este momento, no. Sin embargo, esta capacidad debería estar disponible en un futuro próximo.

### ¿Puedo enviar audiencias desde Composición de audiencia a todos los canales y destinos de flujo descendente?

En este momento, no. Actualmente, puede utilizar audiencias de Composición de audiencias en Campañas de Adobe Journey Optimizer y destinos de Real-Time CDP. En una versión futura se admitirán los Recorridos de Adobe Journey Optimizer.

### ¿Hay alguna barrera en el número de composiciones?

En este momento, solo puede tener **10** composiciones publicadas por zona protegida. Se prevé aumentar esta protección en una versión futura.

### ¿Cuáles son las barreras del flujo de trabajo para la composición de audiencias?

La colocación del componente de composición sigue una estructura rígida de la siguiente manera:

1. Usted **siempre** empiece con el [!UICONTROL Audiencia] para seleccionar su actividad de inicio. Puede tener un máximo de **uno** [!UICONTROL Audiencia] Bloque.
2. Si lo desea, puede añadir un [!UICONTROL Excluir] bloque que sigue al [!UICONTROL Audiencia] Bloque.
3. Si lo desea, puede añadir un [!UICONTROL Enriquecer] bloque que sigue al [!UICONTROL Excluir] Bloque. Solo puede utilizar **uno** [!UICONTROL Enriquecer] bloque por composición.
4. Si lo desea, puede agregar un [!UICONTROL Rango] o [!UICONTROL Split] Bloque. Puede **solamente** tenga uno de estos bloques por composición.
5. Usted **siempre** finalizar con un [!UICONTROL Guardar] para guardar la audiencia.

Además, las restricciones siguientes (?) aplicar al utilizar estos bloques:

- Bloque de división
   - Este bloque solo admite **Cadena** tipos de datos. El bloque Split sí **no** admite el tipo de datos fecha o booleano.
   - Además, este bloque sí **no** admiten atributos de enriquecimiento.
- Excluir bloque
   - Este bloque sí **no** admite el tipo de datos fecha o booleano.
- Bloque de clasificación
   - Este bloque sí **no** admiten atributos de enriquecimiento.

Para obtener más información sobre el uso de Composición de audiencia, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md).

### ¿Cuándo se guardan y evalúan las audiencias creadas con Composición de audiencia?

Las audiencias se guardan automáticamente al crearlas en Composición de audiencia. La hora de creación de la audiencia es la primera vez que se realiza este guardado automático.

Una vez creada la audiencia, puede tardar hasta 24 horas en evaluarse.

### ¿Cuándo puedo utilizar la audiencia que he creado?

La audiencia creada en Composición de audiencia hará lo siguiente **inmediatamente** se muestran en Audience Portal. Sin embargo, para utilizarlo en Adobe Journey Optimizer, debe esperar al menos 24 horas después de la evaluación.

### ¿Los trabajos de evaluación son visibles dentro de la sección de monitorización?

En este momento, los trabajos de evaluación son **no** se muestra en la interfaz de usuario de monitorización.

### ¿Puedo usar una composición de audiencia en otra composición?

No, audiencias creadas con Composición de audiencia **no puede** se utilizará como entrada en otra composición de audiencia.

### ¿Cómo funciona la división en Composición de audiencias?

La división de audiencias permite subdividir aún más la audiencia en grupos más pequeños.

Al dividir por atributo, existe exclusividad mutua entre los grupos. Esto significa que si un registro cumple los criterios de varias rutas divididas, se le asigna la variable **primero** ruta desde la izquierda y **no** asignado a cualquiera de las otras rutas.

Al dividir por porcentaje, las divisiones son **aleatoriamente** hecho. Esto significa que los perfiles se asignan aleatoriamente a cada ruta. La división es **no** persistente, de modo que el perfil podría estar en una subaudiencia diferente en cada evaluación.

Para obtener más información sobre el bloque Split, lea la [Guía de IU de composición de audiencia](./ui/audience-composition.md#split).

### ¿Puedo utilizar todos los tipos de segmentación en el flujo de trabajo de Composición de audiencia?

Sí, todos los tipos de segmentación ([segmentación por lotes, segmentación de streaming y segmentación de edge](./home.md#evaluate-segments)) son compatibles con el flujo de trabajo de Composición de audiencia. Sin embargo, dado que las composiciones actualmente solo se ejecutan una vez al día, incluso si se incluyen audiencias evaluadas por streaming o por Edge, el resultado se basará en la pertenencia de la audiencia en el momento en que se ejecutó la composición.

## Abono a audiencia

En la siguiente sección se enumeran las preguntas relacionadas con la pertenencia a audiencias.

### ¿Cómo puedo confirmar la pertenencia de un perfil a una audiencia?

Para confirmar la pertenencia de un perfil a la audiencia, visite la página de detalles del perfil que desee confirmar. Seleccionar **[!UICONTROL Atributos]**, seguido de **[!UICONTROL Ver JSON]**, y puede confirmar que la variable `segmentMembership` contiene el ID de la audiencia.

### ¿Cómo resuelve la segmentación por lotes la pertenencia a perfiles?

Las audiencias evaluadas mediante la segmentación por lotes se resuelven a diario y los resultados de los miembros de la audiencia se registran en el `segmentMembership` atributo. Las búsquedas de perfiles generan una versión nueva del perfil en el momento de la búsqueda, pero no lo hace **no** actualice los resultados de segmentación por lotes.

Como resultado, cuando se realizan cambios en el perfil, como la combinación de dos perfiles, estos cambios **testamento** aparecen en el perfil cuando se busca, pero **no** se reflejará en la `segmentMembership` hasta que el trabajo de evaluación de segmentos se haya ejecutado de nuevo.

Por ejemplo, supongamos que ha creado dos audiencias mutuamente excluyentes: la audiencia A es para personas que viven en Washington y la audiencia B es para personas que viven en Washington **no** Vivo en Washington. Existen dos perfiles: el perfil 1 de una persona que vive en Washington y el perfil 2 de una persona que vive en Oregón.

Cuando se ejecute el trabajo de evaluación de segmentación por lotes, el perfil 1 irá a la Audiencia A, mientras que el perfil 2 irá a la Audiencia B. Más adelante, pero antes de que se ejecute el trabajo de evaluación de segmentación por lotes del día siguiente, entrará en Platform un evento que reconcilie los dos perfiles. Como resultado, se crea un único perfil combinado que contiene los perfiles 1 y 2.

Hasta que se ejecute el siguiente trabajo de evaluación de segmentos por lotes, el nuevo perfil combinado tendrá pertenencia a audiencia en **ambos** perfil 1 y perfil 2. Como resultado, esto significa que será un miembro de **ambos** Audiencia A y Audiencia B, a pesar de que estas audiencias tienen definiciones contradictorias. Para el usuario final, esta es la **exactamente la misma situación** como antes de que los perfiles estuvieran conectados, ya que siempre solo había una persona involucrada, y Platform lo hizo **no** Tener información suficiente para conectar los dos perfiles.

Si utiliza la búsqueda de perfiles para recuperar el perfil recién creado y observar su pertenencia a audiencias, se mostrará que es miembro de **ambos** Audiencia A y Audiencia B, a pesar de que ambas audiencias tienen definiciones contradictorias. Una vez que se ejecute el trabajo diario de evaluación de segmentación por lotes, el abono a audiencia se actualizará para reflejar este estado actualizado de datos de perfil.

Si necesita más resolución de audiencia en tiempo real, utilice streaming o segmentación de Edge.

### ¿Cuánto tiempo tardan los datos de streaming en estar disponibles en los flujos de trabajo de segmentación por lotes?

Los datos de streaming pueden tardar hasta tres horas en estar disponibles en los flujos de trabajo de segmentación por lotes.

Por ejemplo, si un trabajo de segmentación por lotes se ejecuta a las 21:00, se garantiza que contiene datos ingeridos de flujo continuo **hasta** 18H. Transmisión de datos introducidos después de las 18:00 pero antes de las 21:00 **mayo** ser incluido.

