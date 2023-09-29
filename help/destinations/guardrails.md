---
keywords: Experience Platform;activación;solución de problemas;protecciones;directrices;límite
title: Protecciones predeterminadas para los datos de activación
solution: Experience Platform
product: experience platform
type: Documentation
description: Obtenga más información acerca del uso predeterminado y los límites de velocidad de activación de datos.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: d8e7b5daf72afab8e0a980e35b18a9986a19387d
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 2%

---

# Protecciones para los datos de activación

Esta página proporciona límites predeterminados de uso y velocidad con respecto al comportamiento de activación. Al revisar las siguientes protecciones, se da por hecho que ha [conectado a destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.
>* Los límites descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones.
>* Según las limitaciones descendentes individuales, algunos destinos pueden tener protecciones más estrictas que las documentadas en esta página. Asegúrese de comprobar también el [catalogar](/help/destinations/catalog/overview.md) del destino al que se están conectando y activando los datos.

## Tipos de límite {#limit-types}

Existen dos tipos de límites predeterminados en este documento:

* **Límite leve:** Es posible ir más allá de un límite flexible, aunque los límites flexibles proporcionan una guía recomendada para el rendimiento del sistema.
* **Límite estricto:** Un límite estricto proporciona un máximo absoluto. La interfaz de usuario o la API de Experience Platform no permiten superar este límite o se devuelve un error si se supera.


## Límites de activación {#activation-limits}

Las siguientes protecciones proporcionan límites recomendados al activar datos del perfil del cliente en tiempo real en los destinos.

### Protecciones generales de activación {#general-activation-guardrails}

Las protecciones que se indican a continuación se aplican generalmente a la activación mediante [todos los tipos de destino](/help/destinations/destination-types.md#destination-types).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de audiencias a un solo destino | 250 | Leve | La recomendación es asignar un máximo de 250 audiencias a un solo destino en un flujo de datos. <br><br> Si necesita activar más de 250 audiencias en un destino, puede hacer lo siguiente: <ul><li> Anule la asignación de audiencias que ya no desee activar, o</li><li>Cree un nuevo flujo de datos al destino deseado y asigne las audiencias a este nuevo flujo de datos.</li></ul> <br> Tenga en cuenta que en el caso de algunos destinos, se puede limitar a menos de 250 audiencias asignadas al destino. Estos destinos se indican más adelante en la página, en sus secciones respectivas. |
| Número máximo de atributos asignados a un destino | 50 | Leve | En el caso de varios destinos y tipos de destino, puede seleccionar atributos e identidades de perfil para asignar para la exportación. Para obtener un rendimiento óptimo, se debe asignar un máximo de 50 atributos en un flujo de datos a un destino. |
| Número máximo de destinos | 100 | Grave | Puede crear un máximo de 100 destinos a los que puede conectar y activar datos, *por zona protegida*. [Destinos de personalización de Edge (personalización personalizada)](#edge-destinations-activation) puede constituir un máximo de 10 de los 100 destinos recomendados. |
| Tipo de datos activados en los destinos | Datos de perfil, incluidas identidades y mapa de identidad | Grave | Actualmente, solo es posible exportar *atributos de registro de perfil* a destinos. Los atributos XDM que describen datos de evento no son compatibles con la exportación en este momento. |
| Tipo de datos activados para destinos: compatibilidad con atributos de matriz y asignación | No disponible | Grave | En este momento, lo es **no** posible para exportar *atributos de matriz o asignación* a destinos. La excepción a esta regla es la [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md), que se exporta en las activaciones de flujo continuo y basadas en archivos. |

{style="table-layout:auto"}

### Activación de streaming {#streaming-activation}

Las siguientes protecciones se aplican a la activación mediante [destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número de activaciones (mensajes HTTP con exportaciones de perfil) por segundo | N/A | - | Actualmente no hay límite en el número de mensajes por segundo enviados desde el Experience Platform a los extremos de API de los destinos del socio. <br> Los límites o latencias los dicta el extremo al que el Experience Platform envía datos. Asegúrese de comprobar también el [catalogar](/help/destinations/catalog/overview.md) del destino al que se están conectando y activando los datos. |

{style="table-layout:auto"}

### Activación por lotes (basada en archivos) {#batch-file-based-activation}

Las siguientes protecciones se aplican a la activación mediante [destinos por lotes (basados en archivos)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Frecuencia de activación | Una exportación completa diaria o exportaciones incrementales más frecuentes cada 3, 6, 8 o 12 horas. | Grave | Lea el [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) secciones de documentación para obtener más información sobre los incrementos de frecuencia para las exportaciones por lotes. |
| Número máximo de audiencias que pueden exportarse a una hora determinada | 100 | Leve | Se recomienda añadir un máximo de 100 audiencias a los flujos de datos de destino por lotes. |
| Número máximo de filas (registros) por archivo que activar | 5 millones | Grave | Adobe Experience Platform divide automáticamente los archivos exportados en 5 millones de registros (filas) por archivo. Cada fila representa un perfil. Los nombres de los archivos divididos se anexan con un número que indica que el archivo forma parte de una exportación más grande, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obtener más información, lea la [sección de programación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) del tutorial activar destinos por lotes. |

{style="table-layout:auto"}

### Activación ad hoc {#ad-hoc-activation}

Las siguientes limitaciones se aplican al [activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md) método.

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Audiencias activadas por trabajo de activación ad hoc | 80 | Grave | Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 audiencias. Si se intentan activar más de 80 audiencias por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones. |
| Trabajos de activación ad hoc simultáneos por audiencia | 1 | Grave | No ejecute más de un trabajo de activación ad hoc simultáneo por audiencia. |

{style="table-layout:auto"}

### Activación de destinos de personalización de Edge {#edge-destinations-activation}

Las siguientes protecciones se aplican a la activación mediante [destinos de personalización de edge](/help/destinations/destination-types.md#streaming-profile-export).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [Personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos | 10 | Leve | Puede configurar flujos de datos a 10 destinos de personalización personalizados por zona protegida. |
| Número máximo de atributos asignados a un destino de personalización por zona protegida | 30 | Grave | Se puede asignar un máximo de 30 atributos en un flujo de datos a un destino de personalización por zona protegida. |
| Número máximo de audiencias asignadas a un único [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destino | 50 | Leve | Puede activar un máximo de 50 audiencias en un flujo de activación para un único destino de Adobe Target. |

{style="table-layout:auto"}

### Exportaciones de conjuntos de datos {#dataset-exports}

Las exportaciones de conjuntos de datos son compatibles actualmente con un **[!UICONTROL Primero Completo y luego Incremental]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). Las barreras descritas en esta sección *aplicar a la primera exportación completa* que se produce después de configurar un flujo de trabajo de exportación de conjuntos de datos.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Tipos de conjuntos de datos {#dataset-types}

Las protecciones de exportación del conjunto de datos se aplican a dos tipos de conjuntos de datos exportados desde Experience Platform, como se describe a continuación:

**Conjuntos de datos basados en el esquema de eventos de experiencia XDM**
En el caso de los conjuntos de datos basados en el esquema de eventos de experiencia XDM, el esquema del conjunto de datos incluye un nivel superior *timestamp* columna. Los datos se incorporan de forma exclusiva con datos anexados.

**Conjuntos de datos basados en el esquema Perfil individual XDM**
En el caso de los conjuntos de datos basados en el esquema Perfil individual de XDM, el esquema del conjunto de datos no incluye un nivel superior *timestamp* columna. Los datos se incorporan de forma actualizada.

La protección suave siguiente se aplica a todos los conjuntos de datos exportados fuera de Experience Platform. Revise también las protecciones rígidas más abajo, específicas para diferentes tipos de compresión y conjuntos de datos.

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño de los conjuntos de datos exportados | 5 mil millones de registros | Leve | El límite descrito aquí para las exportaciones de conjuntos de datos es un *barandilla suave*. Por ejemplo, aunque la interfaz de usuario no le impedirá exportar conjuntos de datos de más de 5000 millones de registros, el comportamiento es impredecible y las exportaciones podrían fallar o tener una latencia de exportación muy larga. |

{style="table-layout:auto"}

#### Protecciones para exportaciones de conjuntos de datos programados

Para exportaciones de conjuntos de datos programadas o recurrentes, las protecciones siguientes son idénticas para los dos formatos del archivo exportado (JSON o parquet) y se agrupan por tipo de conjunto de datos.

>[!WARNING]
>
>Las exportaciones a archivos JSON solo se admiten en modo comprimido.

| Tipo de conjunto de datos | Barrera | Tipo de protección | Descripción |
---------|----------|---------|-------|
| Conjuntos de datos basados en **Esquema de eventos de experiencia XDM** | Últimos 365 días de datos | Grave | Se exportan los datos del último año natural. |
| Conjuntos de datos basados en **Esquema de perfil individual de XDM** | Diez mil millones de registros en todos los archivos exportados de un flujo de datos | Grave | El recuento de registros del conjunto de datos debe ser inferior a diez mil millones para archivos JSON o parquet comprimidos y un millón para archivos de parquet no comprimidos; de lo contrario, la exportación falla. Reduzca el tamaño del conjunto de datos que está intentando exportar si supera el umbral permitido. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Más información sobre [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md).


### protecciones de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que Experience Platform envíe datos de audiencia y perfil a su punto de conexión, en función de los datos y los formatos de autenticación de su elección. Las siguientes protecciones se aplican a los destinos configurados con Destination SDK.

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Leve | Puede crear un máximo de 5 destinos privados por lotes o de flujo continuo personalizados utilizando Destination SDK. Póngase en contacto con un representante de atención personalizada si necesita crear más de 5 de estos destinos. |
| Política de exportación de perfiles para el Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 1.800 y máximo 3.600)</li><li>`maxNumEventsInBatch` (mínimo 1 000, máximo 10 000)</li></ul> | Grave | Al usar el [agregación configurable](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) para su destino, tenga en cuenta los valores mínimos y máximos que determinan la frecuencia con la que se envían mensajes HTTP a su destino basado en API y cuántos perfiles deben incluir los mensajes. |

{style="table-layout:auto"}

### Política de restricción y reintento de destino {#destination-throttling-and-retry-policy}

Detalles sobre los umbrales de restricción o las limitaciones para determinados destinos. Esta sección también proporciona información sobre la directiva de reintentos para destinos.

| Tipo de destino | Descripción |
| --- | --- |
| Destinos empresariales (API HTTP, Amazon Kinesis, Azure EventHubs) | En el 95 por ciento de los casos, Experience Platform intenta ofrecer una latencia de rendimiento de menos de 10 minutos para los mensajes enviados correctamente con una tasa de menos de 10 000 solicitudes por segundo para cada flujo de datos a un destino empresarial. <br> En caso de solicitudes fallidas al destino de empresa, Experience Platform almacena las solicitudes fallidas y las reintenta dos veces para enviarlas al punto de conexión. |

{style="table-layout:auto"}

## Protecciones para otros servicios de Experience Platform {#guardrails-other-services}

Ver información de protecciones para otros servicios de Experience Platform:

* Protecciones para [ingesta de datos](/help/ingestion/guardrails.md)
* Protecciones para [[!DNL Identity Service] datos](/help/identity-service/guardrails.md)
* Protecciones para [[!DNL Real-Time Customer Profile] datos](/help/profile/guardrails.md)
* Protecciones para [[!DNL Query Service] datos](/help/query-service/guardrails.md)
