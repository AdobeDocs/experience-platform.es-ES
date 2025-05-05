---
title: Preguntas más frecuentes sobre audiencias
description: Encuentre respuestas a las preguntas frecuentes acerca de audiencias y otros conceptos relacionados con la segmentación.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '4842'
ht-degree: 2%

---

# Preguntas frecuentes

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API RESTful que le permiten crear audiencias a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estas audiencias se configuran de forma centralizada y se mantienen en Experience Platform, y cualquier solución de Adobe puede acceder a ellas fácilmente. A continuación se muestra una lista de las preguntas más frecuentes sobre las audiencias y la segmentación.

## Audience Portal

En la siguiente sección se enumeran las preguntas relacionadas con Audience Portal.

### ¿Tengo acceso a Audience Portal y a Composición de audiencias?

El portal de audiencias y la composición de audiencias están disponibles para todos los clientes de Real-Time CDP Prime y Ultimate (ediciones B2C, B2B y B2P) y para los clientes de Journey Optimizer Select, Prime, Ultimate Starter y Ultimate.

En este momento, solo se admiten audiencias basadas en perfiles. En una versión posterior se añadirá compatibilidad con audiencias basadas en cuentas.

### ¿Las audiencias generadas previamente y generadas externamente son compatibles con Audience Portal?

Sí, las audiencias generadas previamente de forma externa son compatibles con Audience Portal. En este momento, puede importar una audiencia generada externamente a través de un archivo CSV. En el futuro, podrá añadir audiencias a través de conectores de origen por lotes o basados en streaming.

### ¿Qué permisos necesito tener para poder cargar audiencias generadas externamente?

Para cargar audiencias generadas externamente, debe tener los permisos de &quot;Ver segmentos&quot;, &quot;Administrar segmentos&quot; e &quot;Importar audiencias&quot;. No se requieren controles específicos basados en funciones para cargar audiencias generadas externamente.

### ¿Qué sucede cuando se carga una audiencia generada externamente?

Al cargar una audiencia generada externamente, se crea un conjunto de datos y este se puede ver en el inventario de conjuntos de datos. El nombre del conjunto de datos será **igual** que el nombre de la audiencia generada externamente que usted subió.

### ¿De qué se compone una audiencia generada externamente y qué sucede con estos datos cuando se importan a Experience Platform?

Durante el flujo de trabajo de importación de audiencia externa, debe especificar qué columna del archivo CSV corresponde con la **Identidad principal**. Un ejemplo de identidad principal incluye una dirección de correo electrónico, un ECID o un área de nombres de identidad personalizada específica de la organización.

Los datos asociados con esta columna de identidad principal son los **únicos** datos adjuntos al perfil. Si no hay perfiles que coincidan con los datos en la columna de identidad principal, se creará un nuevo perfil. Sin embargo, este perfil es esencialmente un perfil huérfano, ya que **no** atributos o eventos de experiencia están asociados a este perfil.

El resto de los datos de la audiencia generada externamente se consideran **atributos de carga útil**. Estos atributos **solo** se pueden usar para la personalización y el enriquecimiento durante la activación, y **no** están adjuntos a un perfil. Sin embargo, estos atributos se almacenan en el lago de datos.

Aunque se puede hacer referencia a la audiencia generada externamente al crear audiencias mediante el Generador de segmentos, no se pueden usar los atributos de perfil individuales **not**.

### ¿Puedo reconciliar los datos de audiencia generados externamente con un perfil existente en Experience Platform?

Sí, la audiencia generada de forma externa se combinará con el perfil existente en Experience Platform si coinciden los identificadores principales. Estos datos pueden tardar hasta 24 horas en conciliarse. Si los datos del perfil no existen, se creará un nuevo perfil a medida que se incorporen los datos.

### ¿Cómo se respetan las preferencias de consentimiento del cliente para las audiencias generadas externamente que se importan en Audience Portal?{#consent}

A medida que los datos del cliente se capturan desde varios canales, la identificación de identidades y las políticas de combinación permiten que estos datos se consoliden en un único perfil del cliente en tiempo real. La información sobre las preferencias de consentimiento de los clientes se almacena y evalúa a nivel de perfil.

Los destinos descendentes comprueban cada perfil para obtener información de consentimiento antes de la activación. La información de consentimiento de cada perfil se compara con los requisitos de consentimiento para un destino en particular. Si el perfil no cumple los requisitos, no se envía a un destino.

Cuando se incorpora una audiencia externa en Audience Portal, se une a perfiles existentes mediante un ID principal como correo electrónico o ECID. Como resultado, las políticas de consentimiento existentes permanecerán en vigor durante toda la activación.

Tenga en cuenta que **no** debe incluir información de consentimiento con audiencias generadas externamente, ya que las variables de carga útil **no** están almacenadas en el almacén de perfiles, sino en el lago de datos. En su lugar, **debe** utilizar un canal de ingesta de Adobe Experience Platform donde se importen los datos del perfil.

### ¿Puedo utilizar una audiencia generada externamente para crear otras audiencias?

Sí, cualquier audiencia generada externamente aparecerá en el inventario de audiencias y se puede usar al crear audiencias en [Generador de segmentos](./ui/segment-builder.md).

### ¿Con qué frecuencia se evalúan las audiencias generadas externamente?

Las audiencias generadas externamente son **solamente** evaluadas durante el tiempo de la importación. Dado que los atributos asociados a estas audiencias de importación no son duraderos y son **no** parte del almacén de perfiles, la única vez que se actualizará una audiencia generada externamente es si la audiencia existente se actualiza manualmente.

### ¿Puedo utilizar atributos cargados externamente como parte de la segmentación?

No, no puedes. Los atributos de perfil están pensados para ser atributos de larga duración, mientras que los datos de audiencia generados externamente que se cargan solo contienen datos contextuales asociados con esa audiencia generada externamente.

Los datos contextuales de la audiencia generada externamente, o atributos de enriquecimiento, son **no** de larga duración, ya que su ciclo de vida está vinculado a la audiencia cargada. Como resultado, debido a su naturaleza transitoria, estos atributos de enriquecimiento están **no** disponibles para su uso en la segmentación.

Sin embargo, al asignar audiencias a destinos por lotes o basados en archivos, puede utilizar estos atributos de enriquecimiento generados externamente para aumentar las audiencias y realizar más activaciones descendentes.

Para obtener más información acerca de esta funcionalidad, lea la guía sobre [activación de datos de audiencia en destinos de exportación de perfiles por lotes](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### ¿Existe una política de combinación específica para audiencias generadas externamente?

La política de combinación predeterminada específica de la organización se aplica automáticamente al cargar audiencias generadas externamente. Sin embargo, puede cambiar la política de combinación que se aplica a la audiencia generada externamente durante el flujo de trabajo de importación de audiencia.

### ¿Dónde puedo activar audiencias generadas externamente para?

Una audiencia generada de forma externa se puede asignar a cualquier destino y se puede utilizar en campañas y recorridos de Adobe Journey Optimizer.

### ¿Puedo eliminar una audiencia generada externamente?

¡Sí! Las audiencias generadas externamente se pueden eliminar en Audience Portal.

### ¿Qué debo hacer si subo accidentalmente una audiencia generada externamente?

Si ha cargado accidentalmente una audiencia generada externamente y desea eliminar los datos, puede borrar los perfiles asociados con la audiencia cargando un archivo CSV con una fila y sin datos.

### ¿Cuánto tiempo duran las audiencias generadas externamente?

La caducidad de los datos actuales para las audiencias generadas externamente es de **30 días**. Esta caducidad de datos se eligió para reducir la cantidad de datos sobrantes almacenados en su organización.

Una vez transcurrido el período de caducidad de los datos, el conjunto de datos asociado seguirá visible en el inventario de conjuntos de datos, pero **no** podrá activar la audiencia y el recuento de perfiles se mostrará como cero.

### ¿Hay un número máximo de audiencias generadas externamente que pueda importar?

No hay límite en el número de audiencias generadas externamente que puede importar. Sin embargo, tenga en cuenta que las audiencias importadas **do** cuentan en el límite general de audiencias.

### ¿Cómo interactúan Audience Portal y Composición de audiencias con la versión de los datos de socios de Real-Time CDP?

Audience Portal y Composición de audiencias interactuarán con los datos de los socios de dos formas:

1. Si ingiere una lista de clientes potenciales proporcionada por el socio mediante la clase y el flujo de trabajo Perfil de cliente potencial, los clientes potenciales se mantendrán **por separado** de la combinación de perfiles de cliente en el servicio de perfil. Como resultado, esto significa que las listas de clientes potenciales **no** aparecerán en el Portal de audiencias o en la Composición de audiencias para su uso.
2. Si está aprovechando atributos proporcionados por el socio para enriquecer perfiles de origen de **existing**, esas audiencias enriquecidas con datos del socio **aparecerán** en Audience Portal y en Composición de audiencia para su uso.

### ¿Cómo puedo usar atributos adicionales con mis audiencias?

Con las audiencias, hay **dos** tipos diferentes de atributos adicionales que puede agregar: atributos de carga útil (contextuales) y atributos de enriquecimiento.

Los atributos de carga útil son atributos que se incorporan como parte de la carga CSV de una audiencia generada externamente. Estos atributos son **no** introducidos en el perfil del cliente en tiempo real, pero pueden usarse como parte de un destino descendente.

Los atributos de enriquecimiento son atributos que provienen de un conjunto de datos y se unen a una audiencia en Composición de audiencia. Actualmente, estos atributos solo se pueden utilizar en campañas de Adobe Journey Optimizer. La compatibilidad con los recorridos de Adobe Journey Optimizer estará disponible próximamente y la compatibilidad con los destinos descendentes estará pendiente de una versión futura.

| Canal de activación | Audiencias de carga personalizada en CSV | Audiencias de la composición de audiencias |
| --- | --- | --- |
| Destinos de Real-Time CDP | Se pueden activar tanto los atributos de carga útil como las audiencias. | Solo se puede activar la audiencia. No se pueden activar los atributos de enriquecimiento **1&rbrace;.** |
| Adobe Journey Optimizer Campaigns | Ni los atributos de audiencia ni los de carga útil pueden activarse. | Se pueden activar tanto la audiencia como los atributos de ampliación. |

## Estados del ciclo vital {#lifecycle-states}

En la siguiente sección se enumeran las preguntas relacionadas con los estados del ciclo vital y la administración del estado del ciclo vital en Audience Portal.

### ¿Qué representan los distintos estados del ciclo vital?

El siguiente gráfico explica los diferentes estados del ciclo vital, qué representan, dónde se pueden utilizar las audiencias con ese estado, así como el impacto en las protecciones de segmentación.

| Estado | Definición | ¿Visible en Audience Portal? | ¿Visible en destinos? | ¿Afecta a los límites de segmentación? | Impacto en las audiencias basadas en archivos | Impacto en la evaluación de audiencias | ¿Se puede usar dentro de otras audiencias? | Editable |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Borrador | Una audiencia con el estado **Borrador** es una audiencia que aún está en desarrollo y no está lista para utilizarse en otros servicios. | Sí, pero se puede ocultar. | No | Sí | Se puede importar o actualizar durante el proceso de refinamiento. | Evaluado para obtener recuentos de publicación precisos. | Sí, pero no se recomienda su uso. | Sí |
| Publicadas | Una audiencia con el estado **Publicado** es una audiencia lista para usar en todos los servicios descendentes. | Sí | Sí | Sí | Se puede importar o actualizar. | Se evalúa mediante segmentación por lotes, flujo continuo o de Edge. | Sí | Sí |
| Inactivo | Una audiencia con el estado **Inactiva** es una audiencia que no está en uso actualmente. Sigue existiendo en Experience Platform, pero **no** se podrá usar hasta que se marque como borrador o se publique. | No, pero se puede mostrar. | No | No | Ya no se actualiza. | Experience Platform ya no lo evalúa ni actualiza. | No | Sí |
| Eliminado | Una audiencia con el estado **Eliminado** es una audiencia que se ha eliminado. La eliminación real de los datos puede tardar hasta unos minutos en ejecutarse. | No | No | No | Se eliminan los datos subyacentes. | No se realiza ninguna evaluación ni ejecución de los datos una vez completada la eliminación. | No | No |

### ¿En qué estados puedo editar mis audiencias?

Las audiencias se pueden editar en los siguientes estados del ciclo vital:

- **Borrador**: Si una audiencia se edita en estado de borrador, permanecerá en estado de borrador a menos que se publique explícitamente.
- **Publicada**: Si una audiencia se edita en el estado publicado, permanecerá publicada y la audiencia se actualizará automáticamente.
- **Inactiva**: si una audiencia se edita en estado inactivo, permanecerá inactiva. Esto significa que no se evaluará ni actualizará. Si necesita actualizar la audiencia, debe publicar la audiencia.

Una vez eliminada una audiencia, **no se puede** editar.

### ¿A qué estados del ciclo vital puedo mover una audiencia?

Los posibles estados del ciclo de vida a los que se puede mover una audiencia dependen del estado actual de la audiencia.

![Diagrama que describe las posibles transiciones de estado del ciclo vital disponibles para las audiencias.](./images/faq/lifecycle-state-transition.png)

Si la audiencia está en estado de borrador, puede publicarla o eliminarla si la audiencia no tiene dependientes.

Si la audiencia está en el estado publicado, puede desactivarla o eliminarla si la audiencia no tiene dependientes.

Si la audiencia está en estado inactivo, puede volver a publicarla o eliminarla si la audiencia no tiene dependientes.

### ¿Hay advertencias para audiencias en determinados estados del ciclo vital?

Las audiencias en el estado publicado solo se pueden mover a otro estado si la audiencia **no** tiene dependientes. Esto significa que si la audiencia se utiliza en un servicio descendente, no se puede desactivar ni eliminar.

Si se vuelve a publicar una audiencia que se evalúa mediante segmentación por lotes, es decir, cuando una audiencia pasa de inactiva a publicada, la audiencia actualizará **después** del trabajo por lotes diario. Cuando se vuelva a publicar por primera vez, los perfiles y los datos serán **iguales** que cuando la audiencia se inactiva.

### ¿Cómo puedo colocar una audiencia en estado de borrador?

El método para colocar una audiencia en el estado de borrador depende del origen de la audiencia.

Para las audiencias creadas con el Generador de segmentos, puede establecer la audiencia en el estado de borrador seleccionando &quot;[!UICONTROL Guardar como borrador]&quot; en el Generador de segmentos.

Para las audiencias creadas en Composición de audiencia, las audiencias se guardan automáticamente como borrador hasta su publicación.

Para las audiencias creadas externamente, las audiencias se publican automáticamente.

Una vez que una audiencia se encuentra en el estado publicado, **no puede** volver a cambiar la audiencia original al estado de borrador. Sin embargo, si copia la audiencia, la audiencia recién copiada estará en estado de borrador.

### ¿Cómo puedo colocar una audiencia en el estado publicado?

Para las audiencias creadas con el Generador de segmentos o la Composición de audiencias, puede establecer la audiencia en el estado publicado seleccionando &quot;[!UICONTROL Publicar]&quot; en sus respectivas interfaces de usuario.

Las audiencias creadas externamente se establecen automáticamente como publicadas.

### ¿Cómo puedo poner una audiencia en estado inactivo?

Puede poner una audiencia publicada en el estado inactivo abriendo el menú de acciones rápidas en Audience Portal y seleccionando &quot;[!UICONTROL Desactivar]&quot;.

### ¿Cómo puedo volver a publicar una audiencia?

>[!NOTE]
>
>El estado &quot;Volver a publicar&quot; es el mismo que el estado publicado para el comportamiento de audiencia.

Para volver a publicar una audiencia, seleccione una audiencia que esté en estado inactivo, abra el menú de acciones rápidas en Audience Portal y seleccione [!UICONTROL Publicar].

### ¿Cómo puedo poner una audiencia en el estado eliminado?

>[!IMPORTANT]
>
>Solo puede eliminar audiencias que sean **no** utilizadas en activaciones posteriores. Tampoco puede eliminar una audiencia a la que se haga referencia en otra audiencia. Si no puedes eliminar tu audiencia, asegúrate de que **no** la esté usando en ningún servicio descendente o como componente básico de otra audiencia.

Para poner una audiencia en el estado de eliminación, abra el menú de acciones rápidas en Audience Portal y seleccione [!UICONTROL Eliminar].

### ¿Hay alguna advertencia para las transiciones de estado del ciclo vital?

Sí, hay que tener en cuenta algunas advertencias cuando se utilizan audiencias en servicios descendentes, como Adobe Journey Optimizer, o audiencias no basadas en clientes, como audiencias basadas en cuentas.

En este momento, **debe** comprobar manualmente si la audiencia se utiliza en el flujo descendente en Adobe Journey Optimizer, ya que este estado no se comprueba automáticamente en este momento.

Además, **debe** comprobar manualmente si la audiencia se usa como componente de una audiencia basada en cuentas, ya que este estado tampoco se comprueba automáticamente en este momento.

### ¿Qué sucede cuando copio una audiencia? {#copy}

Al copiar una audiencia, la nueva estará en estado de borrador y conservará las mismas carpetas, etiquetas y etiquetas que se aplicaron a la audiencia original.

### ¿Afecta el uso de una audiencia como audiencia secundaria a las transiciones de estado del ciclo vital?

>[!NOTE]
>
>Una audiencia principal es una audiencia que **usa** otra audiencia como dependencia de la audiencia.
>
>Una audiencia secundaria es una audiencia **que se usa como** dependencia de la audiencia.

Sí, el uso de una audiencia como audiencia secundaria afecta a las transiciones de estados del ciclo vital que pueden realizar la audiencia principal y la secundaria.

Para que una audiencia secundaria se mueva al estado publicado, toda su audiencia principal **debe** estar en el estado publicado. Las audiencias principales se pueden publicar antes de publicar la audiencia secundaria o, si el usuario lo confirma, se pueden publicar automáticamente cuando se publica la audiencia secundaria.

Para que la audiencia principal se mueva al estado inactivo o eliminado, todas sus audiencias secundarias **deben** desactivarse o eliminarse.

### ¿Puedo hacer referencia a una audiencia que está en un estado de ciclo de vida diferente?

¡Sí! Si la audiencia está actualmente en estado de borrador, puede hacer referencia a las audiencias en estado de borrador o publicado. Sin embargo, para publicar esta audiencia, **debe** publicar las otras audiencias principales.

## Inventario de audiencias

En la siguiente sección se enumeran las preguntas relacionadas con el inventario de audiencias dentro de Audience Portal.

### ¿Necesito permisos adicionales para utilizar las funciones del inventario de audiencias?

No, tú no. Siempre que tenga permisos de edición para audiencias, podrá crear, actualizar y administrar sus carpetas y etiquetas dentro del Portal de audiencias. Para obtener más información sobre la administración de permisos, lea la [guía de administración de permisos](../access-control/ui/permissions.md).

### ¿Hay un límite en el número de carpetas que puedo crear?

No, no hay límite en el número de carpetas que puede crear. Para obtener más información sobre las carpetas, lea la [sección de inventario de audiencias](./ui/audience-portal.md#folders) de la descripción general de la interfaz de usuario del servicio de segmentación.

### ¿Hay un límite en el número de etiquetas que se pueden añadir a una audiencia?

No, no hay límite en el número de etiquetas que se pueden añadir a una audiencia. Para obtener más información sobre las etiquetas, lea la [sección de inventario de audiencias](./ui/audience-portal.md#tags) de la descripción general de la interfaz de usuario del servicio de segmentación.

### ¿Hay un límite en el número de etiquetas que puedo crear?

No, no hay límite en el número de etiquetas que puede crear. Sin embargo, puede crear un máximo de **100** categorías para aplicar a las etiquetas. Para obtener más información acerca de la administración de etiquetas, lea la [Guía de administración de etiquetas](../administrative-tags/ui/managing-tags.md).

### Cuando busco una audiencia por nombre o etiqueta en una carpeta principal, ¿puedo también buscar en las carpetas secundarias relacionadas?

No, este comportamiento no es compatible. Sin embargo, puede cambiar la vista de inventario de audiencias para ver **Todas las audiencias** y luego buscar en todas las carpetas. Para obtener más información sobre cómo usar la búsqueda en el inventario de audiencias, lea la [sección de búsqueda](./ui/audience-portal.md#search) de la descripción general de la interfaz de usuario del servicio de segmentación.

### ¿Puedo asignar automáticamente una audiencia a una carpeta en el momento de la creación?

En este momento, no. Sin embargo, esta capacidad puede estar disponible en el futuro.

### ¿Puedo mover varias audiencias a una carpeta al mismo tiempo?

En este momento, no. Sin embargo, esta capacidad puede estar disponible en el futuro.

## Composición de público

En la siguiente sección se enumeran las preguntas relacionadas con la Composición de audiencias.

### ¿Cuándo debo usar Composición de audiencia en lugar de usar el Generador de segmentos?

Tanto la Composición de audiencias como el Generador de segmentos tienen una función importante en la creación de audiencias en Experience Platform.

El Generador de segmentos es más adecuado para la audiencia **creación** (para crear una audiencia desde cero), mientras que la Composición de audiencias es más adecuada para la audiencia **depuración y personalización** (para crear nuevas audiencias basadas en una audiencia existente).

La siguiente tabla ilustra la diferencia entre los dos servicios:

| Generador de segmentos | Composición de público |
| --------------- | -------------------- |
| <ul><li>Generación de audiencias de un solo escenario</li><li>Crea los bloques básicos de audiencias a partir de datos de perfil, series temporales y de varias entidades</li><li>Se utilizó para crear la audiencia **one**</li></ul> | <ul><li>Generación de audiencias de varias fases mediante operaciones basadas en conjuntos</li><li>Utiliza las audiencias creadas por el Generador de segmentos y aplica opciones de enriquecimiento de datos como la clasificación de atributos de perfil y la división en subaudiencias</li><li>Se usa para crear **múltiples** audiencias a la vez</li></ul> |

Para obtener más información sobre el Generador de segmentos, lea la [guía del Generador de segmentos](./ui/segment-builder.md). Para obtener más información sobre la composición de audiencias, lea la [guía de composición de audiencias](./ui/audience-composition.md).

### ¿Puedo utilizar audiencias generadas externamente en la composición de audiencias?

En este momento, no. Sin embargo, esta capacidad debería estar disponible en un futuro próximo.

### ¿Puedo enviar audiencias desde Composición de audiencia a todos los canales y destinos de flujo descendente?

En este momento, no. Actualmente, puede utilizar audiencias de Composición de audiencias en Campañas de Adobe Journey Optimizer y destinos de Real-Time CDP. En una versión futura se admitirán los Recorridos de Adobe Journey Optimizer.

### ¿Hay alguna barrera en el número de composiciones?

En este momento, solo puede tener **10** composiciones publicadas por zona protegida. Se prevé aumentar esta protección en una versión futura.

### ¿Cuáles son las barreras del flujo de trabajo para la composición de audiencias?

La colocación del componente de composición sigue una estructura rígida de la siguiente manera:

1. Usted **siempre** comienza con el bloque [!UICONTROL Audiencia] para seleccionar su actividad de inicio. Puede tener un máximo de **un** bloque de [!UICONTROL Audiencia].
2. Opcionalmente, puede agregar un bloque [!UICONTROL Exclude] que sigue al bloque [!UICONTROL Audience].
3. Opcionalmente, puede agregar un bloque [!UICONTROL Enrich] que sigue al bloque [!UICONTROL Exclude]. Solo puedes usar **un** bloque [!UICONTROL Enrich] por composición.
4. Si lo desea, puede agregar un bloque de [!UICONTROL Clasificación] o [!UICONTROL División]. Puede **solamente** tener uno de estos bloques por composición.
5. Usted **siempre** termina con un bloque [!UICONTROL Guardar] para guardar su audiencia.

Además, las restricciones siguientes (?) aplicar al utilizar estos bloques:

- Bloque de división
   - Este bloque solo admite tipos de datos **String**. El bloque dividido **no** admite el tipo de datos booleano o de fecha.
   - Además, este bloque **no** admite atributos de enriquecimiento.
- Excluir bloque
   - Este bloque **no** admite el tipo de datos booleano o de fecha.
- Bloque de clasificación
   - Este bloque **no** admite atributos de enriquecimiento.

Para obtener más información acerca del uso de Composición de audiencia, lea la [guía de la interfaz de usuario de la Composición de audiencia](./ui/audience-composition.md).

### ¿Cuándo se guardan y evalúan las audiencias creadas con Composición de audiencia?

Las audiencias se guardan automáticamente al crearlas en Composición de audiencia. La hora de creación de la audiencia es la primera vez que se realiza este guardado automático.

Una vez creada la composición de audiencias, pueden pasar hasta 48 horas hasta que se evalúe y active para su uso en servicios descendentes como un destino de Real-Time CDP o un canal de Adobe Journey Optimizer.

### ¿Cuándo puedo utilizar la audiencia que he creado?

La audiencia creada en Composición de audiencias **se mostrará inmediatamente** en el Portal de audiencias. Sin embargo, para utilizarlo en Adobe Journey Optimizer, debe esperar al menos 24 horas después de la evaluación.

### ¿Los trabajos de evaluación son visibles dentro de la sección de monitorización?

En este momento, los trabajos de evaluación **no** se muestran en la interfaz de usuario de supervisión.

### ¿Puedo usar una composición de audiencia en otra composición?

No, las audiencias creadas con Composición de audiencia **no se pueden** usar como entrada en otra composición de audiencia.

### ¿Cómo funciona la división en Composición de audiencias?

La división de audiencias permite subdividir aún más la audiencia en grupos más pequeños.

Al dividir por atributo, existe exclusividad mutua entre los grupos. Esto significa que si un registro cumple los criterios de varias rutas de acceso divididas, se le asignará la ruta **first** desde la izquierda y **no** se asignará a ninguna de las otras rutas.

Al dividir por porcentaje, las divisiones se **realizan de forma aleatoria**. Esto significa que los perfiles se asignan aleatoriamente a cada ruta.

Para obtener más información sobre el bloque dividido, lea la [guía de la interfaz de usuario de la composición de audiencias](./ui/audience-composition.md#split).

### ¿Puedo utilizar todos los tipos de segmentación en el flujo de trabajo de Composición de audiencia?

Sí, todos los tipos de segmentación ([segmentación por lotes, segmentación por flujo continuo y segmentación de perímetros](./home.md#evaluate-segments)) son compatibles con el flujo de trabajo de composición de audiencias. Sin embargo, dado que las composiciones actualmente solo se ejecutan una vez al día, incluso si se incluyen audiencias evaluadas por streaming o por Edge, el resultado se basará en la pertenencia de la audiencia en el momento en que se ejecutó la composición.

## Abono de público

En la siguiente sección se enumeran las preguntas relacionadas con la pertenencia a audiencias.

### ¿Cómo puedo confirmar la pertenencia de un perfil a una audiencia?

Para confirmar la pertenencia de un perfil a la audiencia, visite la página de detalles del perfil que desee confirmar. Seleccione **[!UICONTROL Atributos]**, seguido de **[!UICONTROL Ver JSON]**, y podrá confirmar que el objeto `segmentMembership` contiene el ID de la audiencia.

### ¿Puede la pertenencia a audiencias oscilar entre la pertenencia ideal y la real?

Sí, la pertenencia a audiencias puede variar entre la pertenencia ideal y la real si se evalúa una audiencia con la segmentación por secuencias **y**. Esa audiencia se basa en una audiencia evaluada mediante segmentación por lotes.

Por ejemplo, si la audiencia A se basa en la audiencia B y la audiencia B se evalúa mediante segmentación por lotes, ya que la audiencia B solo se actualiza cada 24 horas, la audiencia A se alejará más de los datos reales hasta que se vuelva a sincronizar con las actualizaciones de la audiencia B.

## Segmentación por lotes {#batch-segmentation}

En la siguiente sección se enumeran las preguntas relacionadas con la segmentación por lotes.

### ¿Cómo resuelve la segmentación por lotes la pertenencia a perfiles?

Las audiencias evaluadas mediante la segmentación por lotes se resuelven a diario y los resultados de los miembros de la audiencia se registran en el atributo `segmentMembership` del perfil. Las búsquedas de perfiles generan una nueva versión del perfil en el momento de la búsqueda, pero **no** actualiza los resultados de segmentación por lotes.

Como resultado, cuando se realizan cambios en el perfil, como combinar dos perfiles, estos cambios **aparecerán** en el perfil cuando se busquen, pero **no** se reflejarán en el atributo `segmentMembership` hasta que el trabajo de evaluación de segmentos se haya ejecutado de nuevo.

Por ejemplo, supongamos que ha creado dos audiencias mutuamente exclusivas: la audiencia A es para personas que viven en Washington y la audiencia B es para personas que **no** viven en Washington. Existen dos perfiles: el perfil 1 de una persona que vive en Washington y el perfil 2 de una persona que vive en Oregón.

Cuando se ejecute el trabajo de evaluación de segmentación por lotes, el perfil 1 irá a la Audiencia A, mientras que el perfil 2 irá a la Audiencia B. Más adelante, pero antes de que se ejecute el trabajo de evaluación de segmentación por lotes del día siguiente, entrará en Experience Platform un evento que reconcilie los dos perfiles. Como resultado, se crea un único perfil combinado que contiene los perfiles 1 y 2.

Hasta que se ejecute el siguiente trabajo de evaluación de segmentos por lotes, el nuevo perfil combinado tendrá pertenencia a audiencia en **tanto el perfil 1 como el perfil 2 de**. Como resultado, esto significa que será miembro de **tanto de** audiencia A como de la audiencia B, a pesar de que estas audiencias tienen definiciones contradictorias. Para el usuario final, esta es **exactamente la misma situación** que antes de que se conectaran los perfiles, ya que siempre había solo una persona involucrada y Experience Platform simplemente **no** tenía suficiente información para conectar los dos perfiles.

Si usa la búsqueda de perfiles para recuperar el perfil recién creado y observar su pertenencia a audiencias, se mostrará que es miembro de **tanto de la audiencia A como de la audiencia B**, a pesar de que ambas audiencias tienen definiciones contradictorias. Una vez que se ejecute el trabajo diario de evaluación de segmentación por lotes, el abono a audiencia se actualizará para reflejar este estado actualizado de datos de perfil.

Si necesita más resolución de audiencia en tiempo real, utilice streaming o segmentación de Edge.

### ¿Cuánto tiempo tardan los datos de streaming en estar disponibles en los flujos de trabajo de segmentación por lotes?

Los datos de streaming pueden tardar hasta tres horas en estar disponibles en los flujos de trabajo de segmentación por lotes.

Por ejemplo, si un trabajo de segmentación por lotes se ejecuta a las 9 p. m., se garantiza que contendrá datos ingeridos por streaming de **hasta las** 6 p. m. Se incluirán los datos ingeridos por streaming que se ingirieron después de las 6 p. m. pero antes de las 9 p. m. **puede**.

## Segmentación de Edge {#edge-segmentation}

En la siguiente sección se enumeran las preguntas relacionadas con la segmentación de Edge.

### ¿Cuánto tiempo tarda una definición de segmento en estar disponible en Edge Network?

Una definición de segmento tarda hasta una hora en estar disponible en Edge Network.

## Segmentación de streaming {#streaming-segmentation}

En la siguiente sección se enumeran las preguntas relacionadas con la segmentación de flujo continuo.

### ¿La &quot;descalificación&quot; de la segmentación de streaming también se produce en tiempo real?

En la mayoría de los casos, la descalificación de la segmentación de streaming se produce en tiempo real. Sin embargo, los segmentos de streaming que usan segmentos de segmentos **no** descalifican en tiempo real, en lugar de descalificar después de 24 horas.

### ¿En qué datos funciona la segmentación por streaming?

La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los datos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión. Los eventos transmitidos al sistema con una marca de tiempo de más de 24 horas se procesarán en el trabajo por lotes siguiente.

### ¿Cómo se definen los segmentos como segmentación por lotes o de flujo continuo?

Una definición de segmento se define como segmentación por lotes, por secuencias o perimetral basada en una combinación de tipo de consulta y duración del historial de eventos. Se puede encontrar una lista de los segmentos que se evaluarán como una definición de segmento de flujo continuo en la [sección de tipos de consulta de segmentación de flujo continuo](#query-types).

Tenga en cuenta que si una definición de segmento contiene **both** una expresión `inSegment` y una cadena de evento único directa, no puede calificar para la segmentación de flujo continuo. Si desea que esta definición de segmento cumpla los requisitos de la segmentación de flujo continuo, debe convertir la cadena de evento único directo en su propio segmento.

### ¿Por qué sigue aumentando el número de segmentos &quot;cualificados totales&quot; mientras que el número de &quot;últimos X días&quot; permanece en cero dentro de la sección de detalles de definición del segmento?

El número total de segmentos cualificados se obtiene del trabajo de segmentación diario, que incluye audiencias que cumplen los requisitos para los segmentos por lotes y de flujo continuo. Este valor se muestra para los segmentos por lotes y de flujo continuo.

El número bajo los &quot;últimos X días&quot; **solo** incluye audiencias que se califican en la segmentación por transmisión y **solo** aumenta si ha transmitido datos al sistema y cuenta para esa definición de transmisión. Este valor se muestra **solamente** para los segmentos de streaming. Como resultado, este valor **may** se muestra como 0 para los segmentos por lotes.

Como resultado, si ve que el número bajo &quot;Últimos X días&quot; es cero y el gráfico de líneas también informa cero, tiene **no** transmitido ningún perfil al sistema que calificaría para ese segmento.

### ¿Cuánto tiempo tarda una definición de segmento en estar disponible?

Una definición de segmento tarda hasta una hora en estar disponible.

### ¿Existen limitaciones a los datos que se transmiten en?

Para que los datos transmitidos se usen en la segmentación de flujo continuo, **debe** haber un espacio entre los eventos transmitidos. Si se transmiten demasiados eventos en el mismo segundo, Experience Platform tratará estos eventos como datos generados por bots y se descartarán. Como práctica recomendada, debe tener **al menos** cinco segundos entre los datos de evento para asegurarse de que los datos se utilizan correctamente.
