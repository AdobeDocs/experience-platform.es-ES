---
title: Uso de licencias y capacidad
description: Obtenga información sobre el uso de licencias y los límites de capacidad en Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 5520e449b4cbe45eb9664ce3c913dd5d544e088c
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 6%

---


# Uso de licencias y capacidades

>[!AVAILABILITY]
>
>Para utilizar esta función, debe tener los siguientes permisos:
>
>- **Ver tablero de uso de licencias**
>   - Este permiso le permite **ver** el inicio de capacidad.
>- **Administrar zonas protegidas**
>   - Este permiso le permite **editar** sus asignaciones de capacidad.
>   - Además, **debe** tener acceso asignado a todas las zonas protegidas para editar la capacidad de **cualquier** zona protegida.
>
>Encontrará más información sobre los permisos de Experience Platform en la [descripción general del control de acceso](/help/access-control/home.md#permissions)
>
>Además, si ha adquirido la segmentación de flujo de alto rendimiento, **no** podrá asignar sus capacidades mediante Capacity. Para actualizar sus capacidades, póngase en contacto con el Servicio de atención al cliente de Adobe.

En Adobe Experience Platform, las capacidades le permiten saber si su organización ha superado alguna de sus protecciones y le proporcionan información sobre cómo solucionar estos problemas.

Para obtener más información sobre las protecciones en Experience Platform, lea [Información general sobre las protecciones de Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamiento de capacidad {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Rendimiento de streaming"
>abstract="El valor de rendimiento de streaming mide los eventos de entrada máximos combinados por segundo para la ingesta de streaming al servicio Perfil, en sus zonas protegidas de producción y desarrollo."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Recuento de público de streaming"
>abstract="Número máximo de públicos de streaming por zona protegida. Este número incluye el número de públicos de Edge que tiene en su zona protegida."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Públicos de Edge"
>abstract="Número máximo de públicos de Edge por zona protegida."

Actualmente, Capacity admite los siguientes servicios:

- Segmentación de streaming
- Ingesta por streaming

Dentro de estos servicios, se rastrean las siguientes barreras:

- El número máximo de audiencias de streaming es de 500
   - De estas 500 audiencias de streaming, el número máximo de audiencias de Edge es de 150
- El rendimiento inicial combinado para la ingesta de transmisión es de 1500 registros por segundo (rps)
   - Este rendimiento de flujo combinado mide los eventos de entrada máximos combinados por segundo para la transmisión de la ingesta al Perfil del cliente en tiempo real en los entornos limitados de producción y desarrollo.
   - Puede adquirir compatibilidad adicional con la segmentación de flujo continuo de hasta 13 500 registros por segundo. Encontrará más información sobre la compra de derechos adicionales en la [descripción del producto de Real-Time CDP](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

La capacidad de audiencia está en el nivel de **espacio aislado**. Esto significa que, para cada zona protegida que tenga en su organización, puede tener 500 audiencias de streaming, de las cuales 150 pueden ser audiencias de Edge.

La capacidad de rendimiento de flujo continuo está en el nivel de **organización** y se puede distribuir a cada zona protegida. Por ejemplo, con el rendimiento de 1500 rps para la ingesta de transmisión, puede establecer su zona protegida de producción en 1300 rps y su zona protegida de desarrollo en 200 rps.

Experience Platform calcula el rendimiento de la zona protegida en intervalos móviles de 15 minutos. Este rendimiento se mide en tiempo real y los datos se actualizan cada 60 segundos.

Si el uso alcanza el 80 % y el 90 % de la capacidad con licencia, Experience Platform emitirá una alerta en la que notificará que está alcanzando el máximo de la capacidad especificada. Puede modificar la configuración para personalizar el porcentaje de capacidad para recibir la alerta o eliminarla por completo.

Si su uso supera el 100% de su capacidad con licencia, se considerará que ha incumplido su capacidad. En este punto, experimentará latencia de rendimiento y se garantizarán los objetivos de nivel de servicio (SLT, por sus siglas en inglés) **no**.

## Acceso {#access}

Para acceder al resumen de Capacity, seleccione **[!UICONTROL License usage]** seguido de **[!UICONTROL Capacity]**.

![El método para acceder a la sección Capacity está resaltado.](/help/landing/images/capacity/access-capacity.png)

Se muestra la página de información general de capacidad, con información que incluye un historial de alertas y detalles de las capacidades de su organización.

![La página de descripción general de capacidad se muestra en su totalidad, con el historial de alertas y las secciones de detalles de capacidad.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Historial de alertas {#alert-history}

La sección **[!UICONTROL Alert history]** muestra una lista de las brechas de capacidad más recientes dentro de su organización.

![Se muestra la sección Historial de alertas.](/help/landing/images/capacity/alert-history.png)

| Nombre de columna | Descripción |
| ----------- | ----------- |
| Zona protegida | Nombre de la zona protegida en la que se produjo la infracción de capacidad. |
| Alerta | La capacidad que se ha incumplido en la zona protegida. |
| Marca de tiempo | Los datos y la hora en que se produjo la infracción. |

Para ver un historial completo de las alertas de su organización, seleccione el ![icono de tres puntos](/help/images/icons/more.png), seguido de **[!UICONTROL View all]**.

![Se muestra el historial completo de alertas de una organización.](/help/landing/images/capacity/full-alert-history.png)

### Detalles de capacidad {#capacity-details}

La sección Detalles de capacidad describe la información sobre las capacidades de su organización. En esta sección, puede filtrar por zona protegida y cambiar el periodo de retrospectiva.

![Se resaltan el selector de zona protegida y el selector de fechas para el período retroactivo.](/help/landing/images/capacity/filter-sandbox-and-date.png)

Actualmente, muestra información de capacidad sobre el rendimiento de flujo continuo, las audiencias de flujo continuo y las audiencias de Edge.

#### Rendimiento de streaming {#streaming-throughput}

La sección rendimiento de flujo continuo muestra información sobre el rendimiento de flujo continuo dentro de los entornos limitados de la organización. El valor de rendimiento de flujo continuo mide los eventos de entrada máximos combinados por segundo para la transmisión de la ingesta al servicio de perfil.

![Se muestra la sección de rendimiento de flujo continuo dentro de la página de detalles de capacidad.](/help/landing/images/capacity/streaming-throughput-section.png)

| Nombre de columna | Descripción |
| ----------- | ----------- |
| Zona protegida | Nombre de la zona protegida. |
| Servicios | El servicio que utiliza la zona protegida. Actualmente, el único valor admitido es Profile. |
| Uso (máximo) | El rendimiento máximo de flujo de datos en la zona protegida dentro del período retrospectivo seleccionado. |
| Capacidad | El rendimiento máximo de flujo máximo para la zona protegida. |
| Infracción | Si se ha producido una infracción, el tipo de infracción para el rendimiento de flujo continuo. |
| Acciones recomendadas | Una columna que describe la acción recomendada para mitigar la infracción. |

Puede seleccionar la zona protegida individual para ver una vista más detallada del rendimiento de flujo de la zona protegida.

![Se ha resaltado una zona protegida dentro de la sección de rendimiento de flujo continuo.](/help/landing/images/capacity/select-sandbox.png)

Se muestra la página Detalles del rendimiento de flujo continuo. Puede ver un gráfico que muestra el rendimiento de la solicitud en comparación con el límite de capacidad, una lista de los entornos limitados y su rendimiento, así como un botón para asignar las capacidades de su organización.

![Se muestra la página de rendimiento de flujo continuo, con información detallada sobre el rendimiento de flujo para la zona protegida seleccionada.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Para actualizar las capacidades de rendimiento de flujo continuo de la organización, seleccione **[!UICONTROL Allocate capacities]**.

![El botón Asignar capacidades está resaltado en la página de detalles de rendimiento de flujo continuo.](/help/landing/images/capacity/select-allocate.png)

Aparecerá la página de asignación. En esta página, puede establecer las capacidades de sus diferentes entornos limitados. La suma de todas las capacidades **debe** es igual al total de capacidad de la organización.

![Se muestra la página de asignación de capacidad.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>Solo puede establecer la nueva capacidad en pedidos de **100**. Por ejemplo, puede establecer el valor de la nueva capacidad de la zona protegida en 300 o 500, pero **no puede** establecer este valor en 450.
>
>Si el valor no está en el orden de 100, se redondea hacia arriba o hacia abajo en consecuencia.

Después de actualizar las asignaciones de capacidad, seleccione **[!UICONTROL Save]** para finalizar las actualizaciones. Tenga en cuenta que los cambios pueden tardar hasta 10 minutos en reflejarse en su organización.

#### Recuento de público {#audience-count}

Las secciones **[!UICONTROL Streaming audience count]** y **[!UICONTROL Edge audience count]** muestran el número de audiencias de streaming y de Edge dentro de la zona protegida, así como la cantidad máxima de audiencias de streaming y Edge permitidas dentro de la zona protegida.

![Se muestran las secciones Recuentos de audiencias.](/help/landing/images/capacity/audience-count.png)

| Nombre de columna | Descripción |
| ----------- | ----------- |
| Zona protegida | Nombre de la zona protegida. |
| Servicios | El servicio que se está utilizando para la zona protegida. |
| Uso | El número de audiencias del tipo enumerado que se encuentran en la zona protegida. |
| Capacidad | Número máximo de audiencias del tipo enumerado que se permiten en la zona protegida. |

## Prácticas recomendadas de rendimiento de streaming {#suggestions}

Puede resolver las violaciones del rendimiento del flujo continuo adoptando una de las siguientes recomendaciones:

1. Aumente la capacidad asignada para la zona protegida.
2. Identifique los flujos de datos de alto rendimiento en el [panel de supervisión](/help/dataflows/ui/monitor-streaming-profile.md) y aplique restricciones o filtros en relación con estos flujos de datos si es necesario.
3. Optimice la ingesta utilizando la ingesta por lotes para casos de uso de menor latencia.

Además, puede consultar los flujos de datos y ver si puede optimizar su estrategia de datos.

| Factor contribuyente | Qué es | Impacto en los casos de uso | Prácticas recomendadas |
| --- | --- | --- | --- |
| Conversión de lote a flujo continuo | Las cargas de trabajo por lotes convertidas en flujo continuo pueden aumentar significativamente el rendimiento, lo que afecta al rendimiento y a la asignación de recursos. Por ejemplo, realizar una actualización de perfil masiva después de un evento sin límites de velocidad. | Las estrategias de streaming no son necesarias para los casos de uso por lotes cuando no se requiere un procesamiento de baja latencia. | Evaluar los requisitos de casos de uso. Para el marketing saliente por lotes, considere la posibilidad de usar [ingesta por lotes](/help/ingestion/batch-ingestion/overview.md) en lugar de la transmisión para administrar la ingesta de datos de manera más eficiente. |
| Ingesta de datos innecesaria | La ingesta de datos no necesarios para la personalización aumenta el rendimiento sin añadir valor y desperdiciar recursos. Por ejemplo, la ingesta de todo el tráfico de análisis en perfiles independientemente de la relevancia. | El exceso de datos no relevantes crea ruido, lo que dificulta la identificación de puntos de datos impactantes. También puede causar fricción al definir y administrar audiencias y perfiles. | Introduzca solo los datos necesarios para sus casos de uso. Asegúrese de filtrar los datos innecesarios.<ul><li>**Adobe Analytics**: Use [filtrado de nivel de fila](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) para optimizar la ingesta de datos.</li><li>**Fuentes**: use la [[!DNL Flow Service] API para filtrar datos de nivel de fila](/help/sources/tutorials/api/filter.md) para fuentes compatibles como [!DNL Snowflake] y [!DNL Google BigQuery].</li></li>**Flujo de datos de Edge**: configure [flujos de datos dinámicos](/help/datastreams/configure-dynamic-datastream.md) para realizar el filtrado de nivel de fila del tráfico proveniente del SDK web.</li></ul> |

## Vídeo introductorio {#video}

El siguiente vídeo proporciona información general sobre Capacity.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Preguntas frecuentes {#faq}

En la siguiente sección se describen las preguntas más frecuentes sobre las capacidades de Capacity.

### ¿Puedo tener un límite máximo de rendimiento combinado que suma menos de mi objetivo máximo?

+++ Respuesta

No. El límite máximo de rendimiento combinado **debe** sumarse a la protección de su organización.

+++

### ¿Qué sucede si excedo mis capacidades máximas?

+++ Respuesta

Esto depende de la capacidad que se exceda.

Actualmente, si supera la cantidad máxima de audiencias permitidas, las audiencias excesivas no se verán afectadas. Sin embargo, la capacidad de crear nuevas audiencias puede estar restringida en el futuro.

Si supera el rendimiento de flujo continuo, experimentará latencia de rendimiento en la ingesta y segmentación.

+++

### ¿Por qué debo adherir a mis capacidades máximas?

+++ Respuesta

Trabajar dentro de sus capacidades máximas garantiza que sus datos permanezcan consistentes y que su integridad de datos se mantenga intacta.

Garantiza un rendimiento coherente durante los eventos de mayor actividad, evitando problemas técnicos que podrían afectar negativamente al rendimiento del sistema y afectar a las experiencias de los clientes que siguen el flujo de trabajo, lo que a la larga mejora la higiene de los datos y el rendimiento general del sistema.

+++

### ¿Cuáles son las prácticas recomendadas para administrar el rendimiento de la ingesta de transmisión?

+++ Respuesta

Para administrar mejor el rendimiento de la ingesta de transmisión, debe evaluar los conjuntos de datos para asegurarse de que priorizan los datos necesarios para la personalización.


Si no se requiere procesamiento en tiempo real, debe utilizar la ingesta por lotes en lugar de la ingesta por flujo continuo.

+++
