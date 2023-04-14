---
keywords: Experience Platform;activación;solución de problemas;protecciones;guías;límite
title: Protecciones predeterminadas para los datos de activación
solution: Experience Platform
product: experience platform
type: Documentation
description: Obtenga más información sobre el uso predeterminado y los límites de velocidad de activación de datos.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 1132c5166f1271f1b8eb0c618b83d028b413b991
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 3%

---

# Protecciones para los datos de activación

Esta página proporciona uso predeterminado y límites de velocidad con respecto al comportamiento de activación. Al revisar las siguientes barreras, se da por hecho que se ha [conectado a destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La mayoría de los clientes no superan estos límites predeterminados. Si desea obtener más información sobre los límites personalizados, póngase en contacto con su representante de atención al cliente.
>* Los límites descritos en este documento se están mejorando constantemente. Vuelva regularmente para ver las actualizaciones.
>* Según las limitaciones individuales de los flujos descendentes, algunos destinos pueden tener protecciones más estrictas que las documentadas en esta página. Asegúrese de comprobar también la variable [catálogo](/help/destinations/catalog/overview.md) del destino al que está conectando y activando los datos.


## Tipos de límite {#limit-types}

Existen dos tipos de límites predeterminados dentro de este documento:

* **Límite leve:** Es posible ir más allá de un límite suave, aunque los límites blandos proporcionan una guía recomendada para el rendimiento del sistema.
* **Límite grave:** Un límite estricto proporciona un máximo absoluto. La interfaz de usuario o la API del Experience Platform no le permiten superar este límite, o se devuelve un error si supera este límite.


## Límites de activación {#activation-limits}

Las siguientes protecciones proporcionan límites recomendados al activar los datos del perfil del cliente en tiempo real en los destinos.

### Protecciones generales de activación {#general-activation-guardrails}

Las barreras que se indican a continuación se aplican generalmente a la activación mediante [todos los tipos de destino](/help/destinations/destination-types.md#destination-types).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de segmentos en un único destino | 250 | Leve | La recomendación es asignar un máximo de 250 segmentos a un único destino en un flujo de datos. <br><br> Si necesita activar más de 250 segmentos en un destino, puede: <ul><li> Desasigne segmentos que ya no desee activar, o</li><li>Cree un nuevo flujo de datos al destino deseado y asigne segmentos a este nuevo flujo de datos.</li></ul> <br> Tenga en cuenta que en el caso de algunos destinos, puede estar limitado a menos de 250 segmentos asignados al destino. Estos destinos se señalan más adelante en la página, en sus secciones correspondientes. |
| Número máximo de destinos | 100 | Leve | La recomendación es crear un máximo de 100 destinos a los que se pueda conectar y activar datos *por simulador de pruebas*. [Destinos de personalización de Edge (personalización personalizada)](#edge-destinations-activation) puede constituir un máximo de 10 de los 100 destinos recomendados. |
| Número máximo de atributos asignados a un destino | 50 | Leve | En el caso de varios destinos y tipos de destino, puede seleccionar atributos de perfil e identidades para asignarlos y exportarlos. Para obtener un rendimiento óptimo, se debe asignar un máximo de 50 atributos en un flujo de datos a un destino. |
| Tipo de datos activados en los destinos | Datos de perfil, incluidas identidades y mapa de identidad | Grave | Actualmente, solo es posible exportar *atributos de registro de perfil* a destinos. Los atributos XDM que describen datos de evento no se pueden exportar en este momento. |
| Tipo de datos activados en los destinos : compatibilidad con los atributos de matriz y asignación | No disponible | Grave | En este momento, es **not** posible para exportar *atributos de matriz o asignación* a destinos. La excepción a esta regla es la [mapa de identidad](/help/xdm/field-groups/profile/identitymap.md), que se exporta en activaciones de flujo continuo y basadas en archivos. |

{style="table-layout:auto"}

### Activación por transmisión {#streaming-activation}

Las protecciones siguientes se aplican a la activación mediante [destinos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número de activaciones (mensajes HTTP con exportaciones de perfil) por segundo | N/A | - | Actualmente no hay límite en el número de mensajes por segundo enviados desde el Experience Platform a los extremos de API de los destinos de socio. <br> Cualquier límite o latencia viene determinada por el punto final donde el Experience Platform está enviando datos. Asegúrese de comprobar también la variable [catálogo](/help/destinations/catalog/overview.md) del destino al que está conectando y activando los datos. |

{style="table-layout:auto"}

### Activación por lotes (basada en archivos) {#batch-file-based-activation}

Las protecciones siguientes se aplican a la activación mediante [destinos por lotes (basados en archivos)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Frecuencia de activación | Una exportación completa diaria o exportaciones incrementales más frecuentes cada 3, 6, 8 o 12 horas. | Grave | Lea el [exportar archivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) y [exportar archivos incrementales](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) secciones de documentación para obtener más información sobre los incrementos de frecuencia de las exportaciones por lotes. |
| Número máximo de segmentos que se pueden exportar en una hora determinada | 100 | Leve | La recomendación es agregar un máximo de 100 segmentos a flujos de datos de destino de lotes. |
| Número máximo de filas (registros) por archivo para activar | 5 millones | Grave | Adobe Experience Platform divide automáticamente los archivos exportados en 5 millones de registros (filas) por archivo. Cada fila representa un perfil. Los nombres de archivos divididos se añaden con un número que indica que el archivo forma parte de una exportación más grande, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obtener más información, lea la [sección de programación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) del tutorial activación de destinos de lote . |

{style="table-layout:auto"}

### Activación ad hoc {#ad-hoc-activation}

Las barreras que se indican a continuación se aplican a la variable [activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md) método.

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Segmentos activados por trabajo de activación ad hoc | 80 | Grave | Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 segmentos. Si se intentan activar más de 80 segmentos por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones. |
| Trabajos de activación ad hoc simultáneos por segmento | 1 | Grave | No ejecute más de un trabajo de activación ad hoc simultáneo por segmento. |

{style="table-layout:auto"}

### Activación de destinos de personalización de Edge {#edge-destinations-activation}

Las protecciones siguientes se aplican a la activación mediante [destinos de personalización Edge](/help/destinations/destination-types.md#streaming-profile-export).

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [Personalización personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos | 10 | Leve | Puede configurar flujos de datos en 10 destinos de personalización personalizados por simulador de pruebas. |
| Número máximo de atributos asignados a un destino de personalización por simulador de pruebas | 30 | Grave | Se puede asignar un máximo de 30 atributos en un flujo de datos a un destino de personalización, por simulador de pruebas. |
| Número máximo de segmentos asignados a un único [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destino | 50 | Leve | Puede activar un máximo de 50 segmentos en un flujo de activación a un único destino de Adobe Target. |

{style="table-layout:auto"}

### protecciones del Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) es un conjunto de API de configuración que le permiten configurar patrones de integración de destino para que el Experience Platform entregue datos de audiencia y perfil a su punto final, en función de los formatos de autenticación y datos que elija. Las protecciones siguientes se aplican a los destinos que configure con el Destination SDK .

| Seguridad | Límite | Tipo de límite | Descripción |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Leve | Puede crear un máximo de 5 destinos de flujo continuo o por lotes personalizados y privados mediante Destination SDK. Póngase en contacto con un representante de atención personalizada si necesita crear más de 5 de estos destinos. |
| Política de exportación de perfiles para el Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 1 800 y máximo 3 600)</li><li>`maxNumEventsInBatch` (mínimo 1 000, máximo 10 000)</li></ul> | Grave | Al usar la variable [agregación configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) para el destino, tenga en cuenta los valores mínimo y máximo que determinan la frecuencia con la que se envían los mensajes HTTP a su destino basado en API y cuántos perfiles deben incluir los mensajes. |

{style="table-layout:auto"}

### Restricción de destino y directiva de reintentos {#destination-throttling-and-retry-policy}

Detalles sobre umbrales o limitaciones de regulación para destinos determinados. Esta sección también proporciona información sobre la directiva de reintentos para los destinos.

| Tipo de destino | Descripción |
| --- | --- |
| Destinos empresariales (API HTTP, Amazon Kinesis, Azure EventHubs) | En el 95 % de las veces, el Experience Platform intenta ofrecer una latencia de rendimiento inferior a 10 minutos para los mensajes enviados correctamente con una tasa inferior a 10 000 solicitudes por segundo para cada flujo de datos a un destino empresarial. <br> En caso de que falle la solicitud al destino empresarial, el Experience Platform almacena las solicitudes y los reintentos fallidos dos dos veces para enviar las solicitudes al extremo. |

{style="table-layout:auto"}

## Seguridad para otros servicios de Experience Platform {#guardrails-other-services}

Ver información de protecciones para otros servicios de Experience Platform:

* Seguridad para [ingesta de datos](/help/ingestion/guardrails.md)
* Seguridad para [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Seguridad para [[!DNL Real-Time Customer Profile] data](/help/profile/guardrails.md)
* Seguridad para [[!DNL Query Service] data](/help/query-service/guardrails.md)
