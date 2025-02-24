---
keywords: Experience Platform;inicio;temas populares;Editor de consultas;editor de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Guía de IU del Editor de consultas
description: El Editor de consultas es una herramienta interactiva proporcionada por el Servicio de consultas de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas de datos de experiencia del cliente en la interfaz de usuario de Experience Platform. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: e1ecdb5d701093d9c73b6a05dad9a4dd848e0083
workflow-type: tm+mt
source-wordcount: '2745'
ht-degree: 0%

---

# Guía de IU del Editor de consultas

El Editor de consultas es una herramienta interactiva proporcionada por el Servicio de consultas de Adobe Experience Platform, que le permite escribir, validar y ejecutar consultas para datos de experiencia del cliente en la interfaz de usuario de [!DNL Experience Platform]. El Editor de consultas admite el desarrollo de consultas para análisis y exploración de datos, y permite ejecutar consultas interactivas con fines de desarrollo, así como consultas no interactivas para rellenar conjuntos de datos en [!DNL Experience Platform].

Para obtener más información acerca de los conceptos y características del servicio de consultas, vea [Introducción al servicio de consultas](../home.md). Para obtener más información sobre cómo navegar por la interfaz de usuario del servicio de consultas en [!DNL Platform], consulte la [descripción general de la interfaz de usuario del servicio de consultas](./overview.md).

## Introducción {#getting-started}

El Editor de consultas permite una ejecución flexible de las consultas conectándose al Servicio de consultas, y las consultas sólo se ejecutan mientras está activa esta conexión.

## Acceso al Editor de consultas {#accessing-query-editor}

En la interfaz de usuario [!DNL Experience Platform], seleccione **[!UICONTROL Consultas]** en el menú de navegación de la izquierda para abrir el área de trabajo del servicio de consultas. A continuación, para empezar a escribir consultas, seleccione **[!UICONTROL Crear consulta]** en la parte superior derecha de la pantalla. Este vínculo está disponible en cualquiera de las páginas del espacio de trabajo del servicio de consultas.

![Ficha de información general de Queries Workspace con Crear consulta resaltada.](../images/ui/query-editor/create-query.png)

### Conectando con el servicio de consultas {#connecting-to-query-service}

El Editor de consultas tarda unos segundos en inicializarse y conectarse al Servicio de consultas cuando se abre. La consola le indica cuándo está conectada, como se muestra a continuación. Si intenta ejecutar una consulta antes de que el editor se haya conectado, retrasará la ejecución hasta que se complete la conexión.

![Salida de consola del Editor de consultas tras la conexión inicial.](../images/ui/query-editor/connect.png)

### Cómo se ejecutan las consultas desde el Editor de consultas {#run-a-query}

Las consultas ejecutadas desde el Editor de consultas se ejecutan de forma interactiva, lo que significa que si cierra el explorador o sale, la consulta se cancela. Lo mismo ocurre con las consultas realizadas para generar conjuntos de datos a partir de resultados de consultas.

## Creación de consultas mediante el Editor de consultas mejorado {#query-authoring}

Con el Editor de consultas, puede escribir, ejecutar y guardar consultas para datos de experiencia del cliente. Todas las consultas ejecutadas o guardadas en el Editor de consultas están disponibles para todos los usuarios de su organización con acceso al Servicio de consultas.

### Selector de base de datos {#database-selector}

Seleccione una base de datos para consultar en el menú desplegable de la parte superior derecha del Editor de consultas. La base de datos seleccionada se muestra en la lista desplegable.

![Se resaltó el Editor de consultas con el menú desplegable de base de datos.](../images/ui/query-editor/database-dropdown.png)

### Configuración {#settings}

Un icono de configuración sobre el campo de entrada del Editor de consultas incluye una opción para habilitar/deshabilitar el tema oscuro o para deshabilitar/habilitar el autocompletado.

>[!TIP]
>
>Puede [!UICONTROL Deshabilitar sintaxis para autocompletar] al crear una consulta sin perder el progreso.

Para habilitar los temas oscuros o claros, seleccione el icono de configuración (![Un icono de configuración.](/help/images/icons/settings.png)) seguido de la opción en el menú desplegable que aparece.

![Se resaltó el Editor de consultas con el icono de configuración y la opción de menú desplegable Habilitar tema oscuro.](../images/ui/query-editor/query-editor-settings.png)

#### Completar automáticamente {#auto-complete}

El Editor de consultas sugiere automáticamente palabras clave SQL potenciales junto con detalles de tabla o columna para la consulta a medida que la escribe. La función de autocompletar está habilitada de forma predeterminada y se puede deshabilitar o habilitar en cualquier momento desde la configuración del Editor de consultas.

La configuración de autocompletar es por usuario y se recuerda por los inicios de sesión consecutivos de ese usuario. Al deshabilitar esta función, se detienen varios comandos de metadatos y se proporcionan recomendaciones que generalmente benefician la velocidad del autor al editar consultas.


### Ejecutar varias consultas secuenciales {#execute-multiple-sequential-queries}

Utilice el Editor de consultas mejorado para escribir más de una consulta y ejecutar todas las consultas de forma secuencial. La ejecución de varias consultas en una secuencia genera cada una una una entrada de registro. Sin embargo, solo se muestran los resultados de la primera consulta en la consola del Editor de consultas. Consulte el registro de consultas si necesita solucionar problemas o confirmar las consultas que se ejecutaron. Consulte la [documentación de registros de consulta](./query-logs.md) para obtener más información.

>[!NOTE]
> 
>Si se ejecuta una consulta CTAS después de la primera consulta en el Editor de consultas, se seguirá creando una tabla, pero no habrá resultados en la consola del Editor de consultas.

### Ejecutar consulta seleccionada {#execute-selected-query}

Si ha escrito varias consultas pero sólo necesita ejecutar una, puede resaltar la consulta elegida y seleccionar
[!UICONTROL Ejecutar consulta seleccionada] icono. Este icono está desactivado de forma predeterminada hasta que seleccione una sintaxis de consulta en el editor.

![Se ha resaltado el editor de consultas con el icono [!UICONTROL Ejecutar consulta seleccionada].](../images/ui/query-editor/run-selected-query.png)

### Cancelar sesión del Editor de consultas {#cancel-query}

Tome el control de la ejecución de consultas y mejore su productividad cancelando consultas de larga duración. Esta acción borra el Editor de consultas durante la ejecución de una consulta. Tenga en cuenta que la consulta sigue ejecutándose en segundo plano. Si es una consulta CTAS, seguirá generando un conjunto de datos de salida. Para cancelar la ejecución en el editor y continuar maquetando una instrucción SQL, seleccione **[!UICONTROL Cancelar consulta]** después de ejecutar una consulta.

![Se resaltó el editor de consultas con [!UICONTROL Cancelar consulta].](../images/ui/query-editor/cancel-query-run.png)

Aparecerá un cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Confirmar]** para cancelar la ejecución de la consulta.

![Cuadro de diálogo de confirmación Cancelar consulta con Confirmar resaltado.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Recuento de resultados {#result-count}

El Editor de consultas tiene un resultado máximo de 50 000 filas. Puede elegir el número de filas que se muestran a la vez en la consola del Editor de consultas. Para cambiar el número de filas que se muestran en la consola, seleccione la lista desplegable **[!UICONTROL Recuento de resultados]** y elija entre las opciones 50, 100, 150, 300, 500 y 1000.

>[!NOTE]
>
>Como la IU de Platform puede admitir hasta 1000 filas, se omite el paso de un valor LIMIT superior a 1000.

![Editor de consultas con la lista desplegable Recuento de resultados resaltada.](../images/ui/query-editor/result-count.png)

## Escritura de consultas {#writing-queries}

[!UICONTROL Editor de consultas] está organizado para que escribir consultas sea lo más fácil posible. La captura de pantalla siguiente muestra cómo aparece el editor en la interfaz de usuario, con el campo de entrada SQL y **Reproducir** resaltado.

![Editor de consultas con el campo de entrada SQL y Reproducir resaltado.](../images/ui/query-editor/editor.png)

Para minimizar el tiempo de desarrollo, se recomienda desarrollar las consultas con límites en la cantidad de filas devueltas. Por ejemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Después de comprobar que la consulta produce el resultado esperado, quite los límites y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado.

## Herramientas de escritura en el Editor de consultas {#writing-tools}

Utilice las herramientas de escritura del Editor de consultas para mejorar el proceso de creación de consultas. Las funciones incluyen opciones para dar formato al texto, copiar SQL, administrar detalles de consultas y guardar o programar el trabajo a medida que avanza.

### Formatear texto {#format-text}

La característica [!UICONTROL Formato de texto] hace que la consulta sea más legible al agregar un estilo de sintaxis estandarizado. Seleccione **[!UICONTROL Dar formato al texto]** para estandarizar todo el texto dentro del Editor de consultas.

>[!NOTE]
>
>La característica [!UICONTROL Dar formato al texto] no funciona con bloques anónimos. Para obtener información sobre cómo encadenar una o varias instrucciones SQL secuencialmente, consulte la [documentación de bloques anónimos](../key-concepts/anonymous-block.md).

![El editor de consultas con [!UICONTROL texto de formato] y las instrucciones SQL resaltadas.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### Copiar SQL {#copy-sql}

Seleccione el icono Copiar para copiar SQL desde el Editor de consultas al portapapeles. Esta función de copia está disponible tanto para plantillas de consulta como para consultas recién creadas en el Editor de consultas.

![Área de trabajo de consultas con una plantilla de consulta de ejemplo con el icono de copia resaltado.](../images/ui/query-editor/copy-sql.png)

### Detalles de consulta {#query-details}

Para ver una consulta en el Editor de consultas, seleccione cualquier plantilla guardada de la ficha [!UICONTROL Plantillas]. El panel de detalles de la consulta proporciona más información y herramientas para administrar la consulta seleccionada. También muestra metadatos útiles, como la última vez que se modificó la consulta y quién la modificó, si corresponde.

>[!NOTE]
>
>Las opciones [!UICONTROL Ver programación], [!UICONTROL Agregar programación] y [!UICONTROL Eliminar consulta] solo están disponibles después de que la consulta se haya guardado como plantilla. La opción [!UICONTROL Agregar programación] le lleva directamente al generador de programaciones desde el Editor de consultas. La opción [!UICONTROL Ver programación] le lleva directamente al inventario de programación para esa consulta. Consulte la documentación de programaciones de consultas para obtener información sobre cómo [crear programaciones de consultas en la interfaz de usuario](./query-schedules.md#create-schedule).

![Editor de consultas con el panel de detalles de la consulta resaltado.](../images/ui/query-editor/query-details.png)

Desde el panel de detalles puede generar un conjunto de datos de salida directamente desde la interfaz de usuario, eliminar o asignar un nombre a la consulta mostrada, ver la programación de ejecución de la consulta y agregar la consulta a una programación.

Para generar un conjunto de datos de salida, seleccione **[!UICONTROL Ejecutar como CTAS]**. Aparecerá el cuadro de diálogo **[!UICONTROL Introducir detalles del conjunto de datos de salida]**. Escriba un nombre y una descripción y, a continuación, seleccione **[!UICONTROL Ejecutar como CTAS]**. El nuevo conjunto de datos se muestra en la ficha Examinar **[!UICONTROL Conjuntos de datos]**. Consulte [la documentación de la vista de conjuntos de datos](../../catalog/datasets/user-guide.md#view-datasets) para obtener más información sobre los conjuntos de datos disponibles para su organización.

>[!NOTE]
>
>La opción [!UICONTROL Ejecutar como CTAS] solo está disponible si la consulta se ha programado **no**.

![Cuadro de diálogo [!UICONTROL Introducir detalles del conjunto de datos de salida].](../images/ui/query-editor/output-dataset-details.png)

Después de ejecutar la acción **[!UICONTROL Ejecutar como CTAS]**, aparece un mensaje de confirmación para notificarle que la acción se ha realizado correctamente. Este mensaje emergente contiene un vínculo que proporciona una forma cómoda de desplazarse al espacio de trabajo de registros de consultas. Consulte la [documentación de registros de consultas](./query-logs.md) para obtener más información sobre los registros de consultas.

### Guardar consultas {#saving-queries}

El Editor de consultas proporciona una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Para guardar una consulta, selecciona **[!UICONTROL Guardar]** en la esquina superior derecha del Editor de consultas. Para poder guardar una consulta, se debe proporcionar un nombre para la consulta mediante el panel **[!UICONTROL Detalles de la consulta]**.

>[!NOTE]
>
>Las consultas con nombre y guardadas en mediante el Editor de consultas están disponibles como plantillas en la ficha [!UICONTROL Plantillas] del panel de consultas. Consulte la [documentación de plantillas](./query-templates.md) para obtener más información.

Al guardar una consulta en el Editor de consultas, aparece un mensaje de confirmación para notificarle que la acción se ha realizado correctamente. Este mensaje emergente contiene un vínculo que proporciona una forma cómoda de desplazarse al espacio de trabajo de programación de consultas. Consulte la [documentación de consultas de programación](./query-schedules.md) para obtener información sobre cómo ejecutar consultas en una cadencia personalizada.

### Consultas programadas {#scheduled-queries}

Las consultas que se han guardado como plantilla se pueden programar desde el Editor de consultas. La programación de consultas permite automatizar las ejecuciones de consultas en una cadencia personalizada. Puede programar consultas en función de la frecuencia, la fecha y la hora, y también elegir un conjunto de datos de salida para los resultados si es necesario. Las programaciones de consultas también se pueden deshabilitar o eliminar a través de la interfaz de usuario.

Las programaciones se establecen en el Editor de consultas. Al utilizar el Editor de consultas, solo puede agregar una programación a una consulta que ya se ha creado y guardado. La misma limitación no se aplica a la API del servicio de consultas.

>[!NOTE]
>
>Las consultas programadas que generan diez ejecuciones consecutivas se ponen automáticamente en estado [!UICONTROL En cuarentena]. Una consulta con este estado requiere su intervención para que se puedan llevar a cabo más ejecuciones. Consulte la documentación de [consultas en cuarentena](./monitor-queries.md#quarantined-queries) para obtener más información.

Consulte la documentación de programaciones de consultas para obtener información sobre cómo [crear programaciones de consultas en la interfaz de usuario](./query-schedules.md). Como alternativa, para aprender a agregar programaciones mediante la API, lea la [guía de extremo de consultas programadas](../api/scheduled-queries.md).

Todas las consultas programadas se agregan a la lista en la ficha [!UICONTROL Consultas programadas]. Desde ese espacio de trabajo, puede monitorizar el estado de todos los trabajos de consulta programados a través de la interfaz de usuario. En la ficha [!UICONTROL Consultas programadas], puede encontrar información importante acerca de las ejecuciones de consultas y la suscripción a alertas. La información disponible incluye el estado, los detalles de la programación y los mensajes/códigos de error si falla una ejecución. Consulte el [documento Supervisión de consultas programadas](./monitor-queries.md) para obtener más información.


### Cómo encontrar consultas anteriores {#previous-queries}

Todas las consultas ejecutadas desde el Editor de consultas se capturan en la Tabla de registro. Puede utilizar la funcionalidad de búsqueda en la pestaña **[!UICONTROL Log]** para encontrar ejecuciones de consulta. Las consultas guardadas se muestran en la ficha **[!UICONTROL Plantillas]**.

Si se programó una consulta, entonces la ficha [!UICONTROL Consultas programadas] proporciona una visibilidad mejorada a través de la interfaz de usuario para esos trabajos de consulta. Consulte la [documentación de supervisión de consultas](./monitor-queries.md) para obtener más información.

>[!NOTE]
>
>El registro no guarda las consultas que no se ejecutan. Para que la consulta esté disponible en el servicio de consultas, debe ejecutarse o guardarse en el Editor de consultas.

### [!BADGE Disponibilidad limitada]{type=Informative} Explorador de objetos {#object-browser}

>[!AVAILABILITY]
>
El carril de navegación del conjunto de datos solo está disponible para los clientes de Data Distiller. Es posible que la IU de Platform no contenga el carril izquierdo de navegación del conjunto de datos. Otras imágenes de este documento pueden no reflejar el carril de navegación del conjunto de datos. Póngase en contacto con su representante de Adobe para obtener más información.<br>
Actualmente, el Examinador de objetos sólo está disponible en **versión limitada**. Póngase en contacto con su representante de Adobe para obtener acceso anticipado a la versión.

Utilice el explorador de objetos para buscar y filtrar conjuntos de datos fácilmente. El explorador de objetos reduce el tiempo empleado en buscar tablas y conjuntos de datos en entornos grandes con numerosos conjuntos de datos. Con un acceso optimizado a los datos y metadatos relevantes, puede centrarse más en la creación de consultas y menos en la navegación.

Para explorar la base de datos con el explorador de objetos, escriba un nombre de tabla en el campo de búsqueda o seleccione **[!UICONTROL Tablas]** para expandir la lista de tablas y conjuntos de datos disponibles. Al utilizar el campo de búsqueda, la lista de tablas disponibles se filtra dinámicamente en función de la entrada.

Todos los conjuntos de datos contenidos en [su base de datos seleccionada](#database-dropdown) se muestran en un carril de navegación a la izquierda del Editor de consultas.

![Carril de navegación del conjunto de datos del Editor de consultas con la entrada de búsqueda resaltada.](../images/ui/query-editor/search-tables.png)

El esquema mostrado en el explorador de objetos es un esquema observable. Esto significa que puede utilizarlo para monitorizar los cambios y las actualizaciones en tiempo real a medida que los cambios sean visibles inmediatamente. Los esquemas observables ayudan a garantizar la sincronización de datos y ayudan con las tareas de depuración o análisis.

#### Limitación actual {#current-limitation}

El sistema procesa las consultas de forma secuencial, lo que significa que solo se puede ejecutar una consulta a la vez. Mientras una consulta está en curso, no se puede acceder a tablas adicionales en el panel de navegación izquierdo.

#### Acceso a metadatos de tabla {#table-metadata}

Además de las búsquedas rápidas, ahora puede acceder fácilmente a los metadatos de cualquier tabla seleccionando el icono &quot;i&quot; junto al nombre de la tabla. Esto proporciona información detallada acerca de la tabla seleccionada, que le ayuda a tomar decisiones informadas al escribir consultas.

![Carril de navegación del conjunto de datos del Editor de consultas con la entrada de búsqueda resaltada.](../images/ui/query-editor/table-metadata.png)

#### Explorar tablas secundarias

Para explorar tablas secundarias o vinculadas, seleccione la flecha desplegable junto al nombre de una tabla en la lista. Esto expande la tabla para mostrar cualquier tabla secundaria asociada, proporciona una vista clara de la estructura de datos y permite construcciones de consulta más complejas. El icono situado junto al nombre del campo indica el tipo de datos de la columna, to le ayudará a identificarlo durante consultas complejas.

![Editor de consultas que muestra la lista de tablas filtradas.](../images/ui/query-editor/child-table-list.png)

## Ejecución de consultas mediante el Editor de consultas {#executing-queries}

Para ejecutar una consulta en el Editor de consultas, puede escribir SQL en el editor o cargar una consulta anterior desde la ficha **[!UICONTROL Registro]** o **[!UICONTROL Plantillas]** y seleccionar **Reproducir**. El estado de ejecución de la consulta se muestra en la ficha **[!UICONTROL Consola]** a continuación y los datos de salida en la ficha **[!UICONTROL Resultados]**.

### Consola {#console}

La consola proporciona información sobre el estado y el funcionamiento del servicio de consultas. La consola muestra el estado de conexión al servicio de consultas, las operaciones de consulta que se están ejecutando y los mensajes de error que resulten de esas consultas.

![La ficha Consola de la consola del Editor de consultas.](../images/ui/query-editor/console.png)

>[!NOTE]
>
La consola solo muestra los errores resultantes de la ejecución de una consulta. No muestra los errores de validación de consultas que se producen antes de ejecutar una consulta.

### Resultados de consulta {#query-results}

Una vez finalizada una consulta, los resultados se muestran en la ficha **[!UICONTROL Resultados]**, junto a la ficha **[!UICONTROL Consola]**. Esta vista muestra el resultado tabular de la consulta, mostrando entre 50 y 1000 filas de resultados según el [recuento de resultados](#result-count) seleccionado. Esta vista le permite comprobar que la consulta produce el resultado esperado. Para generar un conjunto de datos con la consulta, quite los límites de las filas devueltas y ejecute la consulta con `CREATE TABLE tablename AS SELECT` para generar un conjunto de datos con el resultado. Consulte el [tutorial de generación de conjuntos de datos](./create-datasets.md) para obtener instrucciones sobre cómo generar un conjunto de datos a partir de los resultados de la consulta en el Editor de consultas.

![La ficha Resultados de la consola del Editor de consultas muestra los resultados de una ejecución de consulta.](../images/ui/query-editor/query-results.png)

## Ejemplos {#examples}

El servicio de consulta proporciona soluciones para una variedad de casos de uso en industrias y escenarios empresariales. Estos ejemplos demuestran la flexibilidad y el impacto del servicio para abordar diversas necesidades. Para [descubrir cómo el servicio de consultas puede aportar valor a sus necesidades comerciales específicas](../use-cases/overview.md), explore la colección completa de documentos de casos de uso. Aprenda a utilizar el servicio de consulta para proporcionar perspectivas y soluciones que mejoren la eficacia operativa y el éxito empresarial.

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## Tutorial en vídeo de ejecución de consultas con el servicio de consultas {#query-tutorial-video}

El siguiente vídeo muestra cómo ejecutar consultas en la interfaz de Adobe Experience Platform y en un cliente SQL. En el vídeo también se muestra el uso de propiedades individuales en un objeto XDM, funciones definidas por Adobe y cómo utilizar CREATE TABLE AS SELECT (CTAS) como consultas.

>[!NOTE]
>
La interfaz de usuario que se muestra en el vídeo está obsoleta, pero la lógica utilizada en el flujo de trabajo sigue siendo la misma.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Pasos siguientes

Ahora que sabe qué características están disponibles en el Editor de consultas y cómo navegar por la aplicación, puede empezar a crear sus propias consultas directamente en [!DNL Platform]. Para obtener más información sobre la ejecución de consultas SQL en conjuntos de datos de [!DNL Data Lake], consulte la guía sobre [ejecución de consultas](../best-practices/writing-queries.md).
