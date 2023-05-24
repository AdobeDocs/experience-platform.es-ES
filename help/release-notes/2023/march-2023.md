---
title: Notas de la versión de Adobe Experience Platform de marzo de 2023
description: Notas de la versión de marzo de 2023 de Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 4%

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

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Paneles definidos por el usuario | Ahora puede **valores de atributo de muestra** antes de agregar un atributo a un widget en el compositor de widgets de paneles definidos por el usuario. Hay algunos valores de muestra de esa columna de atributos disponibles para atributos individuales al crear un widget.<br>Ahora puede **intercambiar los ejes X e Y** en el widget con el botón intercambiar eje. Esto ahorra tiempo y proporciona una experiencia más ergonómica al añadir atributos a los widgets. Esto evita la necesidad de volver a encontrar ambos atributos desde el panel de atributos.<br> Ahora puede **cambiar la ubicación y el título del pie de ilustración** dentro de los widgets. Una vez que una leyenda está presente en un widget, puede reubicarla en cualquier lugar alrededor del gráfico y también cambiar el nombre del título de la leyenda, como puede hacer con las etiquetas de eje y el título del widget. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer el [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo flujo de trabajo de inicio rápido para la API de metaconversiones (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. El [Flujo de trabajo de inicio rápido para la API de conversiones meta](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permite a los clientes recopilar y reenviar rápidamente datos de evento del lado del servidor a Meta para las conversiones de anuncios en solo unos sencillos pasos. |
| Nuevo flujo de trabajo de inicio rápido para el SDK móvil (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en &quot;Introducción&quot; desde la pantalla de inicio de la recopilación de datos. El [flujo de trabajo de inicio rápido para Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) le permite implementar rápidamente el SDK de Mobile y validar eventos móviles básicos en solo unos sencillos pasos. |
| [!DNL Braze] extensión de reenvío de eventos | El [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) La extensión de reenvío de eventos permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor que utilizan el [!DNL Braze] API de seguimiento de usuario. |
| [!DNL Epsilon] extensión de reenvío de eventos | El [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) La extensión de le permite aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a [!DNL Epsilon] uso del [!DNL Epsilon] API de evento. |
| [!DNL Mixpanel] extensión de reenvío de eventos | El [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Esta extensión permite a los clientes aprovechar el reenvío de eventos para capturar información de eventos en Adobe Experience Platform Edge Network y enviarla a Mixpanel mediante la API de seguimiento de eventos. |

{style="table-layout:auto"}

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general del filtrado para datos de Adobe Analytics | Ahora puede utilizar las funcionalidades de preparación de datos para aplicar reglas y condiciones para filtrar los datos de Analytics antes de introducirlos en el perfil del cliente en tiempo real. Para obtener más información, lea la guía de [filtrado de datos de Analytics para la ingesta de perfiles](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuevas funciones para codificar y descodificar cadenas de URL | <ul><li>El `get_url_encoded` toma una URL como entrada y reemplaza o codifica caracteres especiales con caracteres ASCII.</li><li>El `get_url_decoded` toma una URL como entrada y descodifica los caracteres ASCII en caracteres especiales.</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). Para obtener una lista completa de los caracteres reservados y sus caracteres codificados correspondientes, lea la guía sobre [caracteres especiales](../../data-prep/functions.md#special-characters). |

Para obtener más información sobre la preparación de datos, lea la [Resumen de preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] conexión GA](../../destinations/catalog/personalization/adobe-commerce.md) | El [!DNL Adobe Commerce] destination connector (ahora disponible de forma general) permite seleccionar una o varias audiencias de Real-Time CDP para activarlas en la [!DNL Adobe Commerce] para ofrecer una experiencia dinámica y personalizada a sus compradores. |
| [[!DNL Snap Inc] conexión GA](../../destinations/catalog/advertising/snap-inc.md) | El [!DNL Snap Inc] destination connector (ahora disponible de forma general) permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform en [!DNL Snapchat Ads] y utilizarlos para segmentar sus anuncios. |
| [(API) Conexión de Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilice la conexión basada en API para lo siguiente [!DNL Oracle Eloqua] para planificar y ejecutar campañas al tiempo que ofrecen una experiencia del cliente personalizada para sus posibles clientes en [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] conexión](../../destinations/catalog/advertising/amazon-ads.md) | El [!DNL Amazon Ads] La integración de con Adobe Experience Platform proporciona una integración llave en mano de [!DNL Amazon Ads] productos, incluido el [!DNL Amazon DSP (ADSP)]. Uso del [!DNL Amazon Ads] destino en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para la segmentación y activación en [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] conexión](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) ofrece a los especialistas en marketing una perspectiva detallada de las medidas de marketing más eficaces para generar ingresos y maximizar el retorno de la inversión para su compañía. El destino habilita los flujos de datos de empresa a empresa (B2B) de Adobe Experience Platform a [!DNL Marketo Measure]. La tarjeta solo está disponible para [!DNL Marketo Measure Ultimate] clientes. |
| [Conexión de TikTok](../../destinations/catalog/social/tiktok.md) | Cree audiencias personalizadas en TikTok con sus datos para segmentar con sus campañas publicitarias. |
| [Conexión de Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilice este destino para crear y actualizar identidades dentro de un segmento como contactos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Nuevo permiso de control de acceso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | El nuevo permiso permite a los usuarios activar segmentos en destinos existentes, sin mostrar el [paso de asignación](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden agregar y eliminar segmentos en flujos de trabajo de activación, pero no pueden agregar ni eliminar atributos o identidades asignados. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Estamos publicando una corrección de errores para el cifrado PGP/GPG en destinos basados en archivos para Real-Time CDP. Con este cambio, los destinos basados en archivos existentes que utilicen cifrado generarán un nombre de archivo con una extensión diferente a la anterior.

- Extensión actual al utilizar el cifrado: `filename.csv`
- Extensión futura al utilizar el cifrado: `filename.csv.gpg`

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| CSV para recomendación de esquema | Ahora puede cargar los archivos locales para crear esquemas generados por el aprendizaje automático que eliminen la necesidad de crear manualmente un esquema. Desde el [!UICONTROL Fuentes] workspace, cargue un archivo CSV de muestra y los algoritmos de aprendizaje automático de Adobe le sugerirán un esquema en función de los campos de destino. Consulte la [Documentación](../../ingestion/tutorials/map-csv/recommendations.md) para obtener más información.&quot; |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Artículo de oferta]](https://github.com/adobe/xdm/pull/1678/files) | Clase que representa una oferta. |
| Clase | [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1678/files) | Un elemento que puede estar sujeto a decisiones. El resultado de un proceso de toma de decisiones es uno o más elementos de decisión. |
| Clase | [[!UICONTROL Tiempo de espera del servidor de sesión multimedia]](https://github.com/adobe/xdm/pull/1676/files) | Indica la cantidad de tiempo en segundos que transcurrió entre la última interacción conocida del usuario y el momento en que se cerró la sesión. |
| Grupo de campos | [[!UICONTROL Atributos calculados de perfil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Esto agrega atributos calculados de los servicios internos de Adobe a los datos de clientes entrantes. Los clientes no deben utilizarlo para introducir datos. |
| Tipo de datos | [[!UICONTROL Elemento de reembolso]](https://github.com/adobe/xdm/pull/1685/files) | Indica si una devolución está asociada a un pedido y define el tipo de devolución, el importe y la divisa asociada. |
| Tipo de datos | [[!UICONTROL Datos de categoría]](https://github.com/adobe/xdm/pull/1677/files) | Este nuevo tipo de datos representa la categoría de un producto. |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Se ha creado un nuevo esquema XDM para los conjuntos de datos de clasificación de Target. Contiene un conjunto de campos de metadatos que clasifican las actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalles del componente de contenido]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` se ha eliminado de [!UICONTROL Detalles del componente de contenido] |
| Grupo de campos | [[!UICONTROL Etiquetas de entidad AJO]](https://github.com/adobe/xdm/pull/1672/files) | Se han añadido etiquetas de entidad AJO a [!UICONTROL Campos de entidad de AJO], que corresponden a un Recorrido o a una campaña |
| Grupo de campos | (Múltiple) | Se han añadido varios campos para [[!UICONTROL Campos comunes de eventos de pasos de Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Múltiple) | [Se han añadido varios tipos de eventos XDM para [!UICONTROL Informes de contenidos]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento de cambio de Workfront] | El `Full Record` y `Accessor Employee Ids` se agregaron grupos de campos. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/pull/1685/files) | El [!UICONTROL Importe de reembolso] se añadió para indicar la cantidad reembolsada por el artículo, si la hubiera. |
| Tipo de datos | [[!UICONTROL Pedido ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Lista de reembolsos] se ha añadido a la lista de reembolsos de este pedido. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos ]](https://github.com/adobe/xdm/pull/1677/files) | Se han añadido categorías de productos a los datos de categoría de este producto. |
| Tipo de datos | [!UICONTROL Información de detalles de sesión] | Se ha añadido la `pev3` campo de cadena que [indica el tipo de flujo de medios utilizado para los informes](https://github.com/adobe/xdm/pull/1676/files). También se ha añadido la variable `pccr` indica si se ha producido una redirección. |
| Tipo de datos | [!UICONTROL Lista de solicitudes] | Proporciona el [propiedades de lista de solicitudes](https://github.com/adobe/xdm/pull/1675/files). Incluyen nombre, ID y descripción. |
| Tipo de datos | [!UICONTROL Commerce] | El [Se ha actualizado el tipo de datos de Commerce](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, y `requisitionList`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

Query Service permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unir cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Data Science Workspace o para su inserción en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Control de acceso basado en atributos en el almacén acelerado | Utilice el control de acceso basado en atributos con Data Distiller para definir el control de acceso en todos los conjuntos de datos del almacén acelerado. Controla el acceso a los modelos de datos personalizados creados por los usuarios y almacenados en un almacén acelerado para activar los paneles personalizados. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, consulte [Introducción al servicio de consultas](../../query-service/home.md).

## Real-Time Customer Data Platform edición B2B {#b2b}

Real-Time CDP B2B Edition, que se creó en Real-time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a audiencias específicas con precisión y captar esas audiencias en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Corrección de errores | Para proporcionar una representación más precisa de los perfiles de su sistema, el sistema ya no incluye perfiles internos en el recuento total de perfiles ni en la métrica de audiencias direccionables de Real-time Customer Data Platform B2B Edition. A partir de hoy, es posible que vea una caída única en el recuento total de perfiles/métrica de audiencias a las que se puede dirigir. No se han borrado sus datos, se trata simplemente de un cambio en el recuento. Póngase en contacto con su ejecutivo de Adobe si tiene alguna duda |

{style="table-layout:auto"}

Para obtener más información sobre Real-Time CDP B2B Edition, lea la [Información general sobre Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Métricas de perfil | Para ofrecerle una representación más precisa de las métricas de perfil, se combinan las métricas de desglose y pérdida de miembros y ahora se calculan en un periodo de 24 horas. Encontrará más información en la [Guía de IU de segmentación](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad beta de [!DNL Chatlio] | El [!DNL Chatlio] El origen de ya está disponible en la versión beta. Utilice el [!DNL Chatlio] fuente para transmitir su [!DNL Chatlio] datos de eventos al Experience Platform. Para obtener más información, lea la [[!DNL Chatlio] descripción general](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidad beta de [!DNL Customer.io] | El [!DNL Customer.io] El origen de ya está disponible en la versión beta. Utilice el [!DNL Customer.io] origen para transmitir los datos de eventos del cliente a Experience Platform. Para obtener más información, lea la [[!DNL Customer.io] descripción general](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidad beta de [!DNL Pendo] | El [!DNL Pendo] El origen de ya está disponible en la versión beta. Utilice el [!DNL Pendo] fuente para transmitir los datos de análisis de productos al Experience Platform. Para obtener más información, lea la [[!DNL Pendo] descripción general](../../sources/connectors/analytics/pendo-webhook.md). |
| Compatibilidad con flujos de datos de borrador | Ahora puede utilizar la API de Flow Service para establecer los flujos de datos en un estado de borrador. Los flujos de datos borrador se pueden actualizar y publicar posteriormente con nueva información. Para obtener más información, lea la guía de [configuración de los flujos de datos de origen como borradores](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
