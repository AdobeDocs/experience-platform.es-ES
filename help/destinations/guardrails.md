---
keywords: Experience Platform;activación;solución de problemas;protecciones;directrices;límite
title: Protecciones predeterminadas para la activación de datos
solution: Experience Platform
product: experience platform
type: Documentation
description: Obtenga más información acerca del uso predeterminado y los límites de velocidad de activación de datos.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 8a1ac01c503bd1e5b9873714514d438b22f45cfb
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 2%

---

# Protecciones para la activación de datos

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

Esta página proporciona límites predeterminados de uso y velocidad con respecto al comportamiento de activación. Al revisar las siguientes protecciones, se supone que se ha [conectado correctamente a los destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante del servicio de atención al cliente.
>* Los límites descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones.
>* Según las limitaciones descendentes individuales, algunos destinos pueden tener protecciones más estrictas que las documentadas en esta página. Asegúrese de consultar también la página [catálogo](/help/destinations/catalog/overview.md) del destino al que se está conectando y activando los datos.

## Tipos de protección {#limit-types}

Existen dos tipos de límites predeterminados en este documento:

| Tipo de protección | Descripción |
|----------|---------|
| **Protección de rendimiento (límite leve)** | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso. Al superar las barreras de rendimiento, puede experimentar una degradación y latencia del rendimiento. Adobe no es responsable de esta degradación del rendimiento. Los clientes que exceden de manera consistente una protección de rendimiento pueden optar por licenciar capacidad adicional para evitar la degradación del rendimiento. |
| **Protecciones impuestas por el sistema (límite estricto)** | La interfaz de usuario o la API de Real-Time CDP aplican las protecciones impuestas por el sistema. Estos son límites que no se pueden superar, ya que la IU y la API le bloquearán el acceso o devolverán un error. |

{style="table-layout:auto"}


## Límites de activación {#activation-limits}

Las siguientes protecciones proporcionan límites recomendados al activar datos del perfil del cliente en tiempo real en los destinos.

### Protecciones generales de activación {#general-activation-guardrails}

Las protecciones siguientes generalmente se aplican a la activación mediante [todos los tipos de destino](/help/destinations/destination-types.md#destination-types).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de audiencias a un solo destino | 250 | Protección de rendimiento | La recomendación es asignar un máximo de 250 audiencias a un solo destino en un flujo de datos. <br><br> Si necesita activar más de 250 audiencias en un destino, puede: <ul><li> Anule la asignación de audiencias que ya no desee activar, o</li><li>Cree un nuevo flujo de datos al destino deseado y asigne las audiencias a este nuevo flujo de datos.</li></ul> <br> Tenga en cuenta que en el caso de algunos destinos, se puede limitar a menos de 250 audiencias asignadas al destino. Estos destinos se indican más adelante en la página, en sus secciones respectivas. |
| Número máximo de atributos asignados a un destino | 50 | Protección de rendimiento | En el caso de varios destinos y tipos de destino, puede seleccionar atributos e identidades de perfil para asignar para la exportación. Para obtener un rendimiento óptimo, se debe asignar un máximo de 50 atributos en un flujo de datos a un destino. |
| Número máximo de destinos | 100 | Protección impuesta por el sistema | Puede crear un máximo de 100 destinos a los que conectar y activar datos, *por espacio aislado*. [Los destinos de personalización de Edge (personalización personalizada)](#edge-destinations-activation) pueden constituir un máximo de 10 de los 100 destinos recomendados. |
| Tipo de datos activados en los destinos | Datos de perfil, incluidas identidades y mapa de identidad | Protección impuesta por el sistema | Actualmente, solo es posible exportar *atributos de registro de perfil* a destinos. Los atributos XDM que describen datos de evento no son compatibles con la exportación en este momento. |
| Tipo de datos activados para destinos: compatibilidad con atributos de matriz y asignación | Disponible parcialmente | Protección impuesta por el sistema | Puede exportar atributos de matriz a [destinos basados en archivos](/help/destinations/destination-types.md#file-based). [Más información](/help/destinations/ui/export-arrays-maps-objects.md) sobre la nueva funcionalidad. |

{style="table-layout:auto"}

### Activación de streaming {#streaming-activation}

Las siguientes protecciones se aplican a la activación a través de [destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número de activaciones (mensajes HTTP con exportaciones de perfil) por segundo | N/A | - | Actualmente no hay límite en el número de mensajes por segundo enviados desde Experience Platform a los extremos de API de los destinos del socio. <br>: los límites o latencias los dicta el extremo al que Experience Platform envía datos. Asegúrese de consultar también la página [catálogo](/help/destinations/catalog/overview.md) del destino al que se está conectando y activando los datos. |

{style="table-layout:auto"}

### Activación por lotes (basada en archivos) {#batch-file-based-activation}

Las siguientes protecciones se aplican a la activación mediante [destinos por lotes (basados en archivos)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Frecuencia de activación | Una exportación completa diaria o exportaciones incrementales más frecuentes cada 3, 6, 8 o 12 horas. | Protección impuesta por el sistema | Lea las secciones de la documentación [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) para obtener más información sobre los incrementos de frecuencia para las exportaciones por lotes. |
| Número máximo de audiencias que pueden exportarse a una hora determinada | 100 | Protección de rendimiento | Se recomienda añadir un máximo de 100 audiencias a los flujos de datos de destino por lotes. |
| Número máximo de filas (registros) por archivo que activar | 5 millones | Protección impuesta por el sistema | Adobe Experience Platform divide automáticamente los archivos exportados en 5 millones de registros (filas) por archivo. Cada fila representa un perfil. Los nombres de los archivos divididos se anexan con un número que indica que el archivo forma parte de una exportación mayor, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obtener más información, lea la [sección de programación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) del tutorial para activar destinos por lotes. |
| Número máximo de audiencias de carga personalizadas para activar en un flujo de datos | 10 | Protección impuesta por el sistema | Al activar [audiencias de carga personalizadas](/help/segmentation/ui/audience-portal.md#import-audience) en destinos basados en archivos por lotes, hay un límite de 10 de esas audiencias que puede activar en un flujo de datos. Obtenga más información sobre el flujo de trabajo para [activar audiencias de carga personalizadas en destinos basados en archivos por lotes](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences). |

{style="table-layout:auto"}

### Activación ad hoc {#ad-hoc-activation}

Las siguientes protecciones se aplican al método [activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Audiencias activadas por trabajo de activación ad hoc | 80 | Protección impuesta por el sistema | Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 audiencias. Si se intentan activar más de 80 audiencias por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones. |
| Trabajos de activación ad hoc simultáneos por audiencia | 1 | Protección impuesta por el sistema | No ejecute más de un trabajo de activación ad hoc simultáneo por audiencia. |

{style="table-layout:auto"}

### Activación de destinos de personalización de Edge {#edge-destinations-activation}

Las siguientes protecciones se aplican a la activación a través de [destinos de personalización Edge](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [destinos de personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Protección de rendimiento | Puede configurar flujos de datos a 10 destinos de personalización personalizados por zona protegida. |
| Número máximo de atributos asignados a un destino de personalización por zona protegida | 30 | Protección impuesta por el sistema | Se puede asignar un máximo de 30 atributos en un flujo de datos a un destino de personalización por zona protegida. |
| Número máximo de audiencias asignadas a un solo destino de [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50 | Protección de rendimiento | Puede activar un máximo de 50 audiencias en un flujo de activación para un único destino de Adobe Target. |

{style="table-layout:auto"}

### Exportaciones de conjuntos de datos {#dataset-exports}

Las exportaciones de conjuntos de datos se admiten actualmente en un **[[!UICONTROL patrón [Primero completo y luego incremental]**]](/help/destinations/ui/export-datasets.md#scheduling). Las protecciones descritas en esta sección *se aplican a la primera exportación completa* que se produce después de configurar un flujo de trabajo de exportación de conjunto de datos.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Tipos de conjuntos de datos {#dataset-types}

Las protecciones de exportación del conjunto de datos se aplican a dos tipos de conjuntos de datos exportados desde Experience Platform, como se describe a continuación:

**Conjuntos de datos basados en el esquema de eventos de experiencia XDM**
En el caso de los conjuntos de datos basados en el esquema de eventos de experiencia XDM, el esquema del conjunto de datos incluye una columna de nivel superior *timestamp*. Los datos se incorporan de forma exclusiva con datos anexados.

**Conjuntos de datos basados en el esquema de Perfil individual XDM**
En el caso de los conjuntos de datos basados en el esquema Perfil individual de XDM, el esquema del conjunto de datos no incluye una columna de nivel superior *timestamp*. Los datos se incorporan de forma actualizada.

La protección suave siguiente se aplica a todos los conjuntos de datos exportados fuera de Experience Platform. Revise también las protecciones rígidas más abajo, específicas para diferentes tipos de compresión y conjuntos de datos.

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Tamaño de los conjuntos de datos exportados | 5 mil millones de registros | Protección de rendimiento | El límite descrito aquí para las exportaciones de conjuntos de datos es una *protección suave*. Por ejemplo, aunque la interfaz de usuario no le impedirá exportar conjuntos de datos de más de 5000 millones de registros, el comportamiento es impredecible y las exportaciones podrían fallar o tener una latencia de exportación muy larga. |

{style="table-layout:auto"}

#### Protecciones para exportaciones de conjuntos de datos programados

Para exportaciones de conjuntos de datos programadas o recurrentes, las protecciones siguientes son idénticas para los dos formatos del archivo exportado (JSON o parquet) y se agrupan por tipo de conjunto de datos.

>[!WARNING]
>
>Las exportaciones a archivos JSON solo se admiten en modo comprimido.

| Tipo de conjunto de datos | Barrera | Tipo de protección | Descripción |
---------|----------|---------|-------|
| Conjuntos de datos basados en el esquema **XDM Experience Events** | Últimos 365 días de datos | Protección impuesta por el sistema | Se exportan los datos del último año natural. |
| Conjuntos de datos basados en el esquema **XDM Individual Profile** | Diez mil millones de registros en todos los archivos exportados de un flujo de datos | Protección impuesta por el sistema | El recuento de registros del conjunto de datos debe ser inferior a diez mil millones para archivos JSON o parquet comprimidos y un millón para archivos de parquet no comprimidos; de lo contrario, la exportación falla. Reduzca el tamaño del conjunto de datos que está intentando exportar si supera el umbral permitido. |

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

[Destination SDK](/help/destinations/destination-sdk/overview.md) es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que Experience Platform envíe datos de audiencia y perfil a su extremo en función de los datos y los formatos de autenticación que elija. Las siguientes protecciones se aplican a los destinos configurados con Destination SDK.

| Barrera | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Protección de rendimiento | Puede crear un máximo de 5 destinos privados por lotes o de flujo continuo personalizados con Destination SDK. Póngase en contacto con un representante de atención personalizada si necesita crear más de 5 de estos destinos. |
| Directiva de exportación de perfiles para Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 1800 y máximo 3600)</li><li>`maxNumEventsInBatch` (mínimo 1000 y máximo 10 000)</li></ul> | Protección impuesta por el sistema | Cuando uses la opción [agregación configurable](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) para tu destino, ten en cuenta los valores mínimos y máximos que determinan la frecuencia con la que los mensajes HTTP se envían a tu destino basado en API y cuántos perfiles deben incluir los mensajes. |

{style="table-layout:auto"}

### Política de restricción y reintento de destino {#destination-throttling-and-retry-policy}

Detalles sobre los umbrales de restricción o las limitaciones para determinados destinos. Esta sección también proporciona información sobre la directiva de reintentos para destinos.

| Tipo de destino | Descripción |
| --- | --- |
| Destinos empresariales (API HTTP, Amazon Kinesis, Azure EventHubs) | En el 95 por ciento de los casos, Experience Platform intenta ofrecer una latencia de rendimiento de menos de 10 minutos para los mensajes enviados correctamente con una tasa de menos de 10 000 solicitudes por segundo para cada flujo de datos a un destino empresarial. <br>: en caso de solicitudes con errores al destino de empresa, Experience Platform almacena las solicitudes con errores y reintenta enviarlas dos veces al extremo. |

{style="table-layout:auto"}

## Pasos siguientes

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=es#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
