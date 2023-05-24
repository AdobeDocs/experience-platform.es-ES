---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía de usuario;guía de iu;guía de iu de segmentación;generador de segmentos;generador de segmentos;realizado;existente;existente;
solution: Experience Platform
title: Guía de IU del servicio de segmentación
description: El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario para crear y administrar definiciones de segmentos.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '2650'
ht-degree: 4%

---

# Guía de IU del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] proporciona una interfaz de usuario para crear y administrar definiciones de segmentos.

## Primeros pasos

El trabajo con definiciones de segmentos requiere la comprensión de los distintos [!DNL Experience Platform] servicios relacionados con la segmentación. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite dividir los datos almacenados en [!DNL Experience Platform] que se relaciona con individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permite la creación de perfiles de clientes mediante el puente de identidades de fuentes de datos dispares que se están ingiriendo en [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).

También es importante conocer dos términos clave que se utilizan a través de este documento y comprender la diferencia entre ellos:
- **Definición del segmento**: Conjunto de reglas utilizado para describir las características o los comportamientos clave de una audiencia objetivo.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento. Esto se puede crear a través de Adobe Experience Platform (audiencia generada por Platform) o de una fuente externa (audiencia generada externamente).

## Información general

En la IU del Experience Platform, seleccione **[!UICONTROL Segmentos]** en la navegación izquierda para abrir **[!UICONTROL Información general]** que muestra la [!UICONTROL Segmentos] panel.

>[!NOTE]
>
>Si su organización es nueva en Platform y aún no ha creado conjuntos de datos de perfil o políticas de combinación activos, la variable [!UICONTROL Segmentos] el panel no es visible. En su lugar, la variable [!UICONTROL Información general] La pestaña muestra vínculos y documentación para ayudarle a empezar a usar los segmentos.

### [!UICONTROL Segmentos] tablero {#segments-dashboard}

El **[!UICONTROL Segmentos]** El tablero describe las métricas clave relacionadas con los datos de segmentos de su organización.

Para obtener más información, visite la [guía del panel de segmentos](../../dashboards/guides/segments.md).

![Se muestra el panel de segmentos. Muestra varios widgets, incluido el tamaño de la audiencia, los perfiles por identidad, la superposición de identidad y la tendencia de cambio de tamaño de la audiencia.](../../dashboards/images/segments/dashboard-overview.png)

## Examinar {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Pérdida"
>abstract="La pérdida representa el porcentaje de perfiles que cambian dentro de una definición de segmento en comparación con la última vez que se ejecutó el trabajo del segmento."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Método de evaluación"
>abstract="Los métodos de evaluación de segmentos incluyen lote, streaming y Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Añadir todos los segmentos a la programación"
>abstract="Habilite para incluir todos los segmentos de evaluación por lotes en la actualización programada diaria. Deshabilite para eliminar todos los segmentos de la actualización programada."

Seleccione el **[!UICONTROL Examinar]** para ver una lista de todas las definiciones de segmentos de su organización.

![Se muestra la pantalla de exploración de segmentos. Se muestra una lista de todos los segmentos que pertenecen a la organización.](../images/ui/overview/segment-browse-all.png)

Esta vista muestra información sobre la definición del segmento, incluido el recuento de perfiles, la fecha de creación y la fecha de la última modificación.

Puede añadir campos adicionales a esta visualización seleccionando ![el icono de atributo de filtro](../images/ui/overview/filter-attribute.png). Estos campos adicionales incluyen desglose, método de evaluación e ID de trabajo.

Si se selecciona desglose, la visualización muestra un gráfico de barras que describe el porcentaje de perfiles que pertenecen a cada uno de los siguientes estados de perfiles calculados: [!UICONTROL Realizado] y [!UICONTROL Saliendo]. Además, el desglose que se muestra en la [!UICONTROL Examinar] es el desglose más preciso del estado del segmento. Si este número difiere de lo que se indica en la variable [!UICONTROL Información general] , debe utilizar los números de la pestaña [!UICONTROL Examinar] como la fuente de información correcta, ya que la variable [!UICONTROL Información general] los números de las pestañas solo se actualizan una vez al día.

| Estado | Descripción |
| ------ | ----------- |
| Realizado | El recuento de perfiles que cumplen los requisitos para el segmento en las últimas 24 horas. Por lo tanto, el número de perfiles que cumplen los requisitos para el segmento desde la última vez que se ejecutó el trabajo de segmento por lotes. |
| Saliendo | El recuento de perfiles que abandonaron el segmento en las últimas 24 horas. Por lo tanto, el número de perfiles que ya no cumplen los requisitos para el segmento desde la última vez que se ejecutó el trabajo de segmentación por lotes. |

El método de evaluación puede ser streaming, por lotes o Edge. Los segmentos de flujo continuo se evalúan constantemente a medida que los datos entran en el sistema. Los segmentos por lotes se evalúan de acuerdo con una programación establecida. Los segmentos de Edge se evalúan en tiempo real, lo que permite casos de uso de personalización de la misma página y de la siguiente.

![Se resaltan los segmentos de la página de navegación de segmentos.](../images/ui/overview/segment-browse-segments.png)

En la parte superior de la página hay opciones para agregar todos los segmentos a una programación y crear un nuevo segmento.

Alternar **[!UICONTROL Añadir todos los segmentos a la programación]** habilitará la segmentación programada. Encontrará más información sobre la segmentación programada en la [sección segmentación programada de esta guía del usuario](#scheduled-segmentation).

Seleccionar **[!UICONTROL Crear segmento]** le llevará al Generador de segmentos. Para obtener más información sobre la creación de segmentos, lea la sección sobre [creación de segmentos en la guía del usuario](#create-segment).

![La barra de navegación superior de la página de navegación de segmentos está resaltada. Esta barra contiene un botón para añadir todos los segmentos a una programación y un botón para crear un segmento.](../images/ui/overview/segment-browse-top.png)

La barra lateral derecha contiene información sobre todos los segmentos de la organización, con el número total de segmentos, la última fecha de evaluación, la siguiente fecha de evaluación y un desglose de los segmentos por método de evaluación.

![La barra lateral derecha de la página de navegación de segmentos está resaltada. Se muestra información sobre los segmentos de la organización. Incluye información como el número total de segmentos, la última hora de evaluación, la siguiente hora de evaluación, así como un desglose de los diferentes tipos de segmentos.](../images/ui/overview/segment-browse-segment-info.png)

Al seleccionar la fila de la definición del segmento, se proporciona un resumen de la definición del segmento, incluidas las opciones para editar o eliminar el segmento, activar el segmento en un destino, la audiencia cualificada para el segmento, el tamaño total de la audiencia, además del nombre, la descripción, el método de evaluación, la fecha de creación y la fecha de la última modificación del segmento.

>[!NOTE]
>
> Lo hará **no** poder eliminar un segmento que se utilice en una activación de destino.

![Se muestran los detalles del segmento seleccionado. Esto incluye detalles sobre el número de perfiles cualificados, el desglose porcentual de perfiles cualificados comparados con los perfiles totales, la última fecha de evaluación.](../images/ui/overview/segment-browse-details.png)

## Detalles de definición del segmento {#segment-details}

Para ver más detalles acerca de una definición de segmento específica, seleccione el nombre de un segmento dentro de la variable **[!UICONTROL Examinar]** pestaña.

Aparecerá la página de detalles del segmento. En la parte superior, hay un resumen de la definición del segmento, información sobre el tamaño de audiencia apto, así como los destinos para los que está activado el segmento.

![Se muestra la página de detalles de la definición del segmento. Se resaltan las tarjetas de resumen del segmento, audiencia total en el segmento y destinos activados.](../images/ui/overview/segment-details-summary.png)

### Resumen de segmentos {#segment-summary}

El **[!UICONTROL Resumen de segmentos]** proporciona información como el ID, el nombre, la descripción y los detalles de los atributos.

Además, tiene la opción de activar el segmento en un destino o editarlo. Seleccionar **[!UICONTROL Activar en destino]** le permitirá activar el segmento en un destino. Para obtener información más detallada sobre cómo activar un segmento en un destino, lea la [información general de activación](../../destinations/ui/activation-overview.md).

![El botón Activar en destino aparece resaltado.](../images/ui/overview/segment-details-activate.png)

Seleccionar **[!UICONTROL Editar segmento]** le llevará a la [!DNL Segment Builder]. Para obtener información más detallada sobre el uso de [!DNL Segment Builder] espacio de trabajo, lea la [[!DNL Segment Builder] guía del usuario](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Audiencia total en el segmento

El **[!UICONTROL Audiencia total en el segmento]** Esta sección muestra el número total de perfiles aptos para el segmento.

Las estimaciones se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de 1 millón de entidades en su almacén de perfiles, se utiliza el conjunto de datos completo; para entre 1 y 20 millones de entidades, se utiliza 1 millón de entidades; y para más de 20 millones de entidades, se utiliza el 5% del total de entidades. Encontrará más información sobre la generación de estimaciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de segmentos.

### Destinos activados

El **[!UICONTROL Destinos activados]** Esta sección muestra los destinos para los que está activado este segmento.

>[!NOTE]
>
> Los destinos son una función disponible con [!DNL Adobe Real-Time Customer Data Platform]y permiten exportar datos a plataformas externas. Para obtener más información sobre los destinos, lea la [información general sobre destinos](../../destinations/home.md). Para obtener información sobre cómo activar un segmento en un destino, consulte [información general de activación](../../destinations/ui/activation-overview.md).

### Muestras de perfil

A continuación se muestra un muestreo de perfiles aptos para el segmento, con información detallada, incluida la [!DNL Profile] ID, nombre, apellidos y correo electrónico personal.

La forma en que se activa el muestreo de datos depende del método de ingesta.

Para la ingesta por lotes, el almacén de perfiles se analiza automáticamente cada quince minutos para ver si un nuevo lote se ha ingerido correctamente desde que se ejecutó el último trabajo de muestreo. En ese caso, se analiza posteriormente el almacén de perfiles para ver si ha habido al menos un cambio del 5 % en el número de registros. Si se cumplen estas condiciones, se activa un nuevo trabajo de muestreo.

Para la ingesta de transmisión, el almacén de perfiles se analiza automáticamente cada hora para ver si ha habido al menos un cambio del 5 % en el número de registros. Si se cumple esta condición, se activa un nuevo trabajo de muestreo.

El tamaño de la muestra de la exploración depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades en el almacén de perfiles | Tamaño de muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Información más detallada sobre cada [!DNL Profile] se puede ver seleccionando la variable [!DNL Profile] ID. Para obtener más información sobre los detalles de un perfil, lea la [[!DNL Real-Time Customer Profile] guía del usuario](../../profile/ui/user-guide.md#profile-detail).

![Se resaltan los perfiles de muestra para la definición del segmento. La información del perfil de ejemplo incluye el ID de perfil, el nombre, los apellidos y el correo electrónico de la persona.](../images/ui/overview/segment-details-profiles.png)

## Creación de segmentos {#create-segment}

Seleccionar **[!UICONTROL Crear segmento]** en la esquina superior derecha se abre la [!DNL Segment Builder] Workspace, donde puede empezar a crear una definición de segmento.

![En la página de exploración de segmentos, se resalta el botón Crear segmento.](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] workspace

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.

Para obtener información más detallada sobre el uso de [!DNL Segment Builder] espacio de trabajo, lea la [[!DNL Segment Builder] guía del usuario](./segment-builder.md).

![Se muestra el espacio de trabajo del Generador de segmentos.](../images/ui/overview/segment-builder.png)

## Segmentación programada {#scheduled-segmentation}

Una vez creadas las definiciones de segmentos, puede evaluarlas mediante una evaluación bajo demanda o programada (continua). Evaluación significa mudarse [!DNL Real-Time Customer Profile] datos a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creadas, las audiencias se guardan y almacenan para que se puedan exportar con [!DNL Experience Platform] API.

La evaluación bajo demanda implica utilizar la API para realizar evaluaciones y generar audiencias según sea necesario, mientras que la evaluación programada (también conocida como &quot;segmentación programada&quot;) le permite crear una programación recurrente para evaluar definiciones de segmentos a una hora específica (como máximo, una vez al día).

### Habilitar la segmentación programada {#enable-scheduled-segmentation}

Puede habilitar las definiciones de segmentos para la evaluación programada mediante la interfaz de usuario o la API. En la interfaz de usuario de, vuelva a **[!UICONTROL Examinar]** pestaña dentro de **[!UICONTROL Segmentos]** y activar **[!UICONTROL Añadir todos los segmentos a la programación]**. Esto hará que todos los segmentos se evalúen según la programación establecida por su organización.

>[!NOTE]
>
>La evaluación programada se puede habilitar para zonas protegidas con un máximo de cinco (5) políticas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco políticas de combinación para [!DNL XDM Individual Profile] en un solo entorno de zona protegida, no podrá utilizar la evaluación programada.

Actualmente, los horarios solo se pueden crear con la API. Para ver los pasos detallados sobre la creación, edición y trabajo con programaciones mediante la API, siga el tutorial para evaluar y acceder a los resultados de los segmentos, específicamente la sección sobre [evaluación programada mediante la API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![El conmutador a Añadir todos los segmentos a una programación se resalta en la página Exploración de segmentos.](../images/ui/overview/segment-browse-scheduled.png)

## Audiencias {#audiences}

>[!IMPORTANT]
>
>Actualmente, la funcionalidad de audiencias está en versión beta limitada y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Seleccione el **[!UICONTROL Audiencias]** para ver una lista de todas las audiencias de su organización.

![Una lista de audiencias para su organización.](../images/ui/overview/list-audiences.png)

De forma predeterminada, esta vista muestra información sobre las audiencias, incluido el nombre, el recuento de perfiles, el origen, la fecha de creación y la fecha de la última modificación.

Puede seleccionar el ![Personalizar tabla](../images/ui/overview/customize-table.png) para cambiar los campos que se muestran.

![Se resalta el botón Personalizar tabla. Al seleccionar este botón, puede personalizar los campos que se muestran en la página de exploración Audiencias.](../images/ui/overview/select-customize-table.png)

Aparece una ventana emergente que enumera todos los campos que se pueden mostrar en la tabla.

![Atributos que se pueden mostrar en la sección Examinar audiencias.](../images/ui/overview/customize-table-attributes.png)

| Campo | Descripción |
| ----- | ----------- | 
| [!UICONTROL Nombre] | El nombre de la audiencia. |
| [!UICONTROL Recuento de perfiles] | Número total de perfiles aptos para la audiencia. |
| [!UICONTROL Origen] | El origen de la audiencia. Si esta audiencia fue generada por Platform, tendrá un origen de Servicio de segmentación. |
| [!UICONTROL Estado del ciclo vital] | El estado de la audiencia. Los valores posibles para este campo incluyen `Draft`, `Published`, y `Archived`. |
| [!UICONTROL Frecuencia de actualización] | Un valor que indica la frecuencia con la que se actualizan los datos de la audiencia. Los valores posibles para este campo incluyen `On Demand`, `Scheduled`, y `Continuous`. |
| [!UICONTROL Actualizado por última vez por] | El nombre de la persona que actualizó la audiencia por última vez. |
| [!UICONTROL Creado] | La hora y la fecha de creación de la audiencia. |
| [!UICONTROL Última actualización] | Fecha y hora en la que se creó la audiencia por última vez. |
| [!UICONTROL Etiquetas de acceso] | Las etiquetas de acceso para la audiencia. Las etiquetas de acceso le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Estas etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Para obtener más información sobre las etiquetas de acceso, lea la documentación sobre [administración de etiquetas](../../access-control/abac/ui/labels.md). |

Puede seleccionar **[!UICONTROL Crear audiencia]** para crear una audiencia.

![El botón Crear audiencia aparece resaltado y muestra dónde seleccionar para crear una audiencia.](../images/ui/overview/create-audience.png)

Aparece una ventana emergente que le permite elegir entre componer una audiencia o crear reglas.

![Una ventana emergente que muestra los dos tipos de audiencias que puede crear.](../images/ui/overview/create-audience-type.png)

Seleccionar **[!UICONTROL Componer audiencias]** le lleva al Generador de audiencias. Para obtener más información sobre la creación de audiencias, lea la [Guía del Generador de audiencias](./audience-builder.md).

Seleccionar **[!UICONTROL Generar regla]** le lleva al Generador de segmentos. Para obtener más información sobre la creación de segmentos, lea la [Guía del Generador de segmentos](./segment-builder.md)

## Detalles de audiencia {#audience-details}

Para ver más detalles acerca de una audiencia específica, seleccione el nombre de una audiencia dentro de la [!UICONTROL Audiencias] pestaña.

Aparecerá la página de detalles de la audiencia. Esta página difiere en detalles en función de si la audiencia se generó con Adobe Experience Platform o desde una fuente externa como Audience Orchestration.

### Audiencia generada por Platform

Para obtener más información sobre las audiencias generadas por Platform, lea la [sección de resumen del segmento](#segment-summary).

### Audiencia generada externamente

En la parte superior de la página de detalles de la audiencia encontrará un resumen de la audiencia y detalles sobre el conjunto de datos en el que se guarda la audiencia.

![Los detalles proporcionados para una audiencia generada externamente.](../images/ui/overview/externally-generated-audience.png)

El **[!UICONTROL Resumen de audiencia]** proporciona información como el ID, el nombre, la descripción y los detalles de los atributos.

El **[!UICONTROL Detalles del conjunto de datos]** proporciona información como el nombre, la descripción, el nombre de tabla, el origen y el esquema. Puede seleccionar **[!UICONTROL Ver conjunto de datos]** para ver más información sobre el conjunto de datos.

| Campo | Descripción |
| ----- | ----------- |
| [!UICONTROL Nombre] | El nombre del conjunto de datos. |
| [!UICONTROL Descripción] | La descripción del conjunto de datos. |
| [!UICONTROL Nombre de tabla] | Nombre de tabla del conjunto de datos. |
| [!UICONTROL Fuente] | Origen del conjunto de datos. Para audiencias generadas externamente, este valor es **Esquema**. |
| [!UICONTROL Esquema] | El tipo de esquema XDM al que corresponde el conjunto de datos. |

Para obtener más información sobre los conjuntos de datos, lea la [información general del conjunto de datos](../../catalog/datasets/overview.md).

## Segmentación de streaming {#streaming-segmentation}

La segmentación por streaming es la capacidad de segmentación de [!DNL Platform] en tiempo casi real, mientras se centra en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos llegan a [!DNL Platform], aliviando la necesidad de programar y ejecutar trabajos de segmentación.

Encontrará más información sobre la segmentación de flujo continuo en la [guía del usuario de segmentación de streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Para que la segmentación de streaming funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre la activación de la segmentación programada, consulte [la sección segmentación de streaming en esta guía del usuario](#scheduled-segmentation).

## Segmentación de Edge {#edge-segmentation}

La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea en Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente.

Puede encontrar más información acerca de la segmentación de Edge en la [guía de IU de segmentación de Edge](./edge-segmentation.md)

## Infracciones de directiva

>[!NOTE]
>
>Las infracciones de directivas sólo se aplican si está creando un segmento que se ha asignado a un destino.

Una vez que haya terminado de crear su segmento, el control de datos de Adobe Experience Platform analizará el segmento para asegurarse de que no haya infracciones de directivas dentro del segmento. Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información.

![Se muestran las violaciones de política para el segmento.](../images/ui/overview/segment-dule-policy-violations.png)

## Pasos siguientes y recursos adicionales {#next-steps}

El [!DNL Segmentation Service] La interfaz de usuario de proporciona un flujo de trabajo enriquecido que le permite aislar audiencias comercializables de [!DNL Real-Time Customer Profile] datos.

Para obtener más información acerca de [!DNL Segmentation Service], siga leyendo la documentación. Para aprender a utilizar [!DNL Segmentation Service] API, lea la [[!DNL Segmentation Service] guía para desarrolladores](../api/overview.md).
