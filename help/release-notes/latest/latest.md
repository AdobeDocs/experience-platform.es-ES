---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de marzo de 2023 para Adobe Experience Platform.
source-git-commit: 5b8dd4b295f9363fd7e848070b1ec21ff519c524
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de marzo de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Tableros](#dashboards)
- [Recopilación de datos](#data-collection)
- [Preparación de datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time Customer Data Platform edición B2B](#b2b)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Tableros definidos por el usuario | Ahora puede **valores de atributo de muestra** antes de agregar un atributo a un widget en el compositor de widgets de tableros definido por el usuario. Algunos valores de muestra de esa columna de atributos están disponibles para atributos individuales al crear un widget.<br>Ahora puede **intercambiar los ejes X e Y** en el widget con el botón de eje de intercambio. Esto ahorra tiempo y proporciona una experiencia más ergonómica al agregar atributos a las utilidades. Esto guarda la necesidad de volver a encontrar ambos atributos en el panel de atributos.<br>Ahora puede **cambiar la ubicación y el título de la leyenda** en sus widgets. Una vez que una leyenda está presente en un widget, puede reubicarla en cualquier lugar alrededor del gráfico y también cambiar el nombre del título de la leyenda, como puede hacerse con las etiquetas de eje y el título del widget. |

{style="table-layout:auto"}

Para obtener más información sobre los tableros, incluido cómo conceder permisos de acceso y crear utilidades personalizadas, comience por leer [información general sobre los paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo flujo de trabajo de inicio rápido para la API de Meta Conversions (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. La variable [flujo de trabajo de inicio rápido para la API de Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite a los clientes recopilar y reenviar rápidamente datos de eventos, del lado del servidor a Meta para conversiones de anuncios en solo unos pasos sencillos. |
| Nuevo flujo de trabajo de inicio rápido para el SDK de Mobile (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. La variable [flujo de trabajo de inicio rápido para el SDK de Mobile](https://developer.adobe.com/client-sdks/documentation/) le permite implementar rápidamente el SDK móvil y validar eventos móviles básicos en solo unos pasos sencillos. |
| [!DNL Braze] extensión de reenvío de eventos | La variable [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) la extensión de reenvío de eventos permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor utilizando la variable [!DNL Braze] API de seguimiento de usuarios. |
| [!DNL Epsilon] extensión de reenvío de eventos | La variable [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) permite aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a [!DNL Epsilon] usando la variable [!DNL Epsilon] API de evento. |
| [!DNL Mixpanel] extensión de reenvío de eventos | La variable [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) permite a los clientes aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a Mixpanel mediante la API de seguimiento de eventos. |

{style="table-layout:auto"}

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general del filtrado para los datos de Adobe Analytics | Ahora puede utilizar las funcionalidades de preparación de datos para aplicar reglas y condiciones para filtrar los datos de Analytics antes de ingerirlos en el perfil del cliente en tiempo real. Para obtener más información, consulte la guía de [filtrado de datos de Analytics para la ingesta de perfiles](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuevas funciones para codificar y descodificar cadenas URL | <ul><li>La variable `get_url_encoded` toma una URL como entrada y reemplaza o codifica caracteres especiales con caracteres ASCII.</li><li>La variable `get_url_decoded` toma una URL como entrada y descodifica los caracteres ASCII en caracteres especiales.</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). Para obtener una lista completa de los caracteres reservados y sus correspondientes caracteres codificados, lea la guía de [caracteres especiales](../../data-prep/functions.md#special-characters). |

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexión GA](../../destinations/catalog/personalization/adobe-commerce.md) | La variable [!DNL Adobe Commerce] el conector de destino (ahora disponible de forma general) le permite seleccionar una o varias audiencias de Real-Time CDP para activarlas en su [!DNL Adobe Commerce] para ofrecer una experiencia personalizada dinámica para sus compradores. |
| [[!DNL Snap Inc] conexión GA](../../destinations/catalog/advertising/snap-inc.md) | La variable [!DNL Snap Inc] conector de destino (ahora disponible de forma general) permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform a [!DNL Snapchat Ads] y úselo para dirigir sus anuncios. |
| [Conexión (API) Eloqua de Oracle](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilice la conexión basada en API para [!DNL Oracle Eloqua] para planificar y ejecutar campañas al tiempo que ofrece una experiencia de cliente personalizada para sus clientes potenciales en [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | La variable [!DNL Amazon Ads] la integración con Adobe Experience Platform proporciona integración llave en mano a [!DNL Amazon Ads] los productos, incluido el [!DNL Amazon DSP (ADSP)]. Al usar la variable [!DNL Amazon Ads] destino en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para el direccionamiento y la activación en el [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] connection](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) proporciona a los especialistas en marketing una perspectiva de cuáles son los esfuerzos de marketing más efectivos para generar ingresos y maximizar el retorno de la inversión para su empresa. El destino permite los flujos de datos de empresa a empresa (B2B) de Adobe Experience Platform a [!DNL Marketo Measure]. La tarjeta solo está disponible para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexión TikTok](../../destinations/catalog/social/tiktok.md) | Cree audiencias personalizadas en TikTok con sus datos para segmentar con sus campañas de publicidad. |
| [Conexión de Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilice este destino para crear y actualizar identidades dentro de un segmento como contactos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Nuevo permiso de control de acceso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | El nuevo permiso permite a los usuarios activar segmentos en destinos existentes, sin mostrar la variable [paso de asignación](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden agregar y eliminar segmentos en flujos de trabajo de activación, pero no pueden agregar ni eliminar atributos o identidades asignados. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Estamos publicando una corrección de errores para el cifrado PGP/GPG en destinos basados en archivos para CDP en tiempo real. Con este cambio, los destinos basados en archivos existentes que actualmente utilizan cifrado generarán un nombre de archivo con una extensión diferente a la anterior.

- Extensión actual al utilizar cifrado: `filename.csv`
- Extensión futura al utilizar el cifrado: `filename.csv.gpg`

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| CSV a recomendación de esquema | Ahora puede cargar los archivos locales para crear esquemas generados por el aprendizaje automático que eliminen la necesidad de crear manualmente un esquema. En el [!UICONTROL Fuentes] espacio de trabajo, cargue un archivo CSV de muestra y los algoritmos de aprendizaje automático de Adobe le sugerirán un esquema basado en los campos de destino. Consulte la [Documentación](../../ingestion/tutorials/map-csv/recommendations.md) para obtener más información.&quot; |

{style="table-layout:auto"}

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Elemento de oferta]](https://github.com/adobe/xdm/pull/1678/files) | Clase que representa una oferta. |
| Clase | [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1678/files) | Elemento que puede ser objeto de una decisión. El resultado de un proceso de toma de decisiones es uno o más elementos de decisión. |
| Clase | [[!UICONTROL Tiempo de espera del servidor de sesión de medios]](https://github.com/adobe/xdm/pull/1676/files) | Esto indica la cantidad de tiempo, en segundos, que transcurrió entre la última interacción conocida del usuario y el momento en que se cerró la sesión. |
| Grupo de campos | [[!UICONTROL Atributos calculados de perfil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Esto agrega atributos calculados de los servicios internos de Adobe a los datos de clientes entrantes. Los clientes no deben usar esto para ingerir datos. |
| Tipo de datos | [[!UICONTROL Artículo de reembolso]](https://github.com/adobe/xdm/pull/1685/files) | Indica si un reembolso está asociado a un pedido y define el tipo de reembolso, el importe y la moneda asociada. |
| Tipo de datos | [[!UICONTROL Datos de categoría]](https://github.com/adobe/xdm/pull/1677/files) | Este nuevo tipo de datos representa la categoría de un producto. |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Se creó un nuevo esquema XDM para conjuntos de datos de clasificación de Target. Contiene un conjunto de campos de metadatos que clasifican las actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalles de los componentes de contenido]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` se ha eliminado de [!UICONTROL Detalles de los componentes de contenido] |
| Grupo de campos | [[!UICONTROL Etiquetas de entidades AJO]](https://github.com/adobe/xdm/pull/1672/files) | Se han añadido etiquetas de entidad AJO a [!UICONTROL Campos de entidad AJO], que corresponden a un Recorrido o a una campaña |
| Grupo de campos | (Múltiple) | Se han añadido varios campos para [[!UICONTROL Campos comunes de eventos de los pasos del Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Múltiple) | [Se han agregado varios tipos de eventos XDM para [!UICONTROL Informes de contenidos]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento de cambio de Workfront] | La variable `Full Record` y `Accessor Employee Ids` se agregaron grupos de campos. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/pull/1685/files) | La variable [!UICONTROL Importe de reembolso] se agregó para indicar la cantidad reembolsada por el artículo, si la hubiera. |
| Tipo de datos | [[!UICONTROL Pedido ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Lista de reembolsos] se agregó a la lista de reembolsos para este pedido. |
| Tipo de datos | [[!UICONTROL Elemento Lista de productos ]](https://github.com/adobe/xdm/pull/1677/files) | Se han añadido categorías de productos a la lista de datos de categoría de este producto. |
| Tipo de datos | [!UICONTROL Información detallada de la sesión] | Se ha añadido la variable `pev3` campo de cadena que [indica el tipo de flujo de medios que se usa para los informes](https://github.com/adobe/xdm/pull/1676/files). También se ha añadido la variable `pccr` indica si se ha producido una redirección. |
| Tipo de datos | [!UICONTROL Lista de solicitudes] | Proporciona la variable [propiedades de la lista de solicitudes](https://github.com/adobe/xdm/pull/1675/files). Incluyen nombre, ID y descripción. |
| Tipo de datos | [!UICONTROL Commerce] | La variable [Se ha actualizado el tipo de datos de comercio](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`y `requisitionList`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos de un lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en informes, Data Science Workspace o para su incorporación al Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Control de acceso basado en atributos en el almacén acelerado | Utilice el control de acceso basado en atributos con Data Distiller para definir el control de acceso en todos los conjuntos de datos del almacén acelerado. Esto controla el acceso a los modelos de datos personalizados creados por los usuarios y almacenados en un almacén acelerado para activar los paneles personalizados. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md).

## Real-Time Customer Data Platform edición B2B {#b2b}

Basado en Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Corrección de errores | Para proporcionar una representación más precisa de los perfiles en su sistema, el sistema ya no incluye perfiles internos en el recuento total de perfiles ni la métrica de audiencias a las que se puede dirigir para Real-time Customer Data Platform B2B Edition. A partir de hoy, es posible que vea una caída única en la métrica total de recuento de perfiles/audiencia a la que se puede dirigir. No se ha borrado ningún dato, esto es simplemente un cambio en el recuento. Póngase en contacto con su ejecutivo de Adobe por cualquier motivo que pueda tener |

{style="table-layout:auto"}

Para obtener más información sobre Real-Time CDP B2B Edition, lea la [Información general de Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Métricas de perfil | Para proporcionar una representación más precisa de las métricas de perfil, el desglose de miembros y las métricas de pérdida se están combinando y ahora se calculan en un período de 24 horas. Encontrará más información en la [Guía de la interfaz de usuario de segmentación](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad beta de [!DNL Chatlio] | La variable [!DNL Chatlio] el origen ya está disponible en versión beta. Utilice la variable [!DNL Chatlio] fuente para transmitir su [!DNL Chatlio] datos de eventos a Experience Platform. Para obtener más información, lea la [[!DNL Chatlio] información general](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidad beta de [!DNL Customer.io] | La variable [!DNL Customer.io] el origen ya está disponible en versión beta. Utilice la variable [!DNL Customer.io] fuente para transmitir los datos de eventos del cliente al Experience Platform. Para obtener más información, lea la [[!DNL Customer.io] información general](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidad beta de [!DNL Pendo] | La variable [!DNL Pendo] el origen ya está disponible en versión beta. Utilice la variable [!DNL Pendo] para transmitir los datos de análisis de productos al Experience Platform. Para obtener más información, lea la [[!DNL Pendo] información general](../../sources/connectors/analytics/pendo-webhook.md). |
| Compatibilidad con flujos de datos de borrador | Ahora puede utilizar la API de servicio de flujo para establecer los flujos de datos en un estado de borrador. Los flujos de datos borrados se pueden actualizar y publicar posteriormente con nueva información. Para obtener más información, consulte la guía de [definición de los flujos de datos de origen como borradores](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).
