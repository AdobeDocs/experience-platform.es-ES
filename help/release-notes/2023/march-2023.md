---
title: 'Notas de la versión de Adobe Experience Platform: marzo de 2023'
description: Las notas de la versión de marzo de 2023 de Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '2206'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de marzo de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Paneles definidos por el usuario | Ahora puede **muestrear valores de atributos** antes de añadir un atributo a un widget en el compositor de widgets de paneles definidos por el usuario. Hay algunos valores de muestra de esa columna de atributos disponibles para atributos individuales al crear un widget.<br>Ahora puede **intercambiar los ejes X e Y** en su widget con el botón de intercambiar eje. Esto ahorra tiempo y proporciona una experiencia más ergonómica al añadir atributos a los widgets. También evita la necesidad de volver a buscar ambos atributos desde el panel de atributos.<br> Ahora puede **cambiar la ubicación y el título de la leyenda** dentro de los widgets. Una vez que una leyenda está presente en un widget, puede reubicarla en cualquier lugar alrededor del gráfico y también cambiar el nombre del título de la leyenda, como puede hacer con las etiquetas de eje y el título del widget. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nuevo flujo de trabajo de inicio rápido para la API de Conversiones de Meta (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en “Introducción” desde la pantalla de inicio de la recopilación de datos. El [Flujo de trabajo de inicio rápido para la API de Conversiones de Meta](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=es#quick-start) permite a los clientes recopilar y reenviar rápidamente datos de evento del lado del servidor a Meta para las conversiones de anuncios en solo unos sencillos pasos. |
| Nuevo flujo de trabajo de inicio rápido para el SDK móvil (Beta) | Acceda a los nuevos flujos de trabajo de inicio rápido en “Introducción” desde la pantalla de inicio de la recopilación de datos. El [flujo de trabajo de inicio rápido para el SDK móvil](https://developer.adobe.com/client-sdks/documentation/) le permite implementar rápidamente el SDK móvil y validar eventos móviles básicos en solo unos sencillos pasos. |
| Extensión de reenvío de eventos de [!DNL Braze] | La extensión de reenvío de eventos [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite aprovechar los datos capturados en la red perimetral de Adobe Experience Platform y enviarlos a [!DNL Braze] en forma de eventos del lado del servidor que utilizan las API de seguimiento de usuarios de [!DNL Braze]. |
| Extensión de reenvío de eventos de [!DNL Epsilon] | La extensión [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=es) le permite aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a [!DNL Epsilon] usando la API de evento de [!DNL Epsilon]. |
| Extensión de reenvío de eventos de [!DNL Mixpanel] | La extensión [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=es) permite a los clientes aprovechar el reenvío de eventos para capturar información de eventos en la red perimetral de Adobe Experience Platform y enviarla a Mixpanel mediante la API de seguimiento de eventos. |

{style="table-layout:auto"}

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general del filtrado para datos de Adobe Analytics | Ahora puede emplear las funcionalidades de preparación de datos para aplicar reglas y condiciones con el fin de filtrar los datos de Analytics antes de introducirlos en el perfil del cliente en tiempo real. Para obtener más información, lea la guía de [filtrado de datos de Analytics para la ingesta de perfiles](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuevas funciones para codificar y descodificar cadenas de URL | <ul><li>La función `get_url_encoded` toma una URL como entrada y sustituye o codifica los caracteres especiales con ASCII.</li><li>La función `get_url_decoded` toma una URL como entrada y descodifica los caracteres ASCII en especiales.</li></ul> Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). Para obtener una lista completa de los caracteres reservados y sus caracteres codificados correspondientes, lea la guía sobre [caracteres especiales](../../data-prep/functions.md#special-characters). |

Para obtener más información sobre la preparación de datos, lea [Información general de preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| Disponibilidad general de conexión de [[!DNL Adobe Commerce] ](../../destinations/catalog/personalization/adobe-commerce.md) | El conector de destino de [!DNL Adobe Commerce] (ahora disponible de forma general) le permite seleccionar uno o más públicos de Real-Time CDP para activarlos en su cuenta de [!DNL Adobe Commerce] y ofrecer una experiencia dinámica personalizada a sus compradores. |
| Disponibilidad general de conexión de [[!DNL Snap Inc] ](../../destinations/catalog/advertising/snap-inc.md) | El conector de destino de [!DNL Snap Inc] (ya disponible de forma general) permite a los profesionales del marketing importar segmentos de usuarios creados en Experience Platform a [!DNL Snapchat Ads] y utilizarlos para orientar sus anuncios. |
| [(API) Conexión de Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilice la conexión basada en API a [!DNL Oracle Eloqua] para planificar y ejecutar campañas al tiempo que ofrece una experiencia del cliente personalizada para sus clientes potenciales en [!DNL Oracle Eloqua]. |
| [(Beta) Conexión de  [!DNL Amazon Ads] ](../../destinations/catalog/advertising/amazon-ads.md) | La integración de [!DNL Amazon Ads] con Adobe Experience Platform proporciona una integración llave en mano para productos de [!DNL Amazon Ads], incluido [!DNL Amazon DSP (ADSP)]. Con el destino de [!DNL Amazon Ads] en Adobe Experience Platform, los usuarios pueden definir públicos de anunciante para la segmentación y activación en [!DNL Amazon DSP]. |
| Conexión de [[!DNL Marketo Measure Ultimate] ](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anteriormente Bizible) ofrece a los especialistas en marketing una perspectiva detallada de las medidas de marketing más eficaces para generar ingresos y maximizar el retorno de la inversión para su compañía. El destino habilita los flujos de datos de empresa a empresa (B2B) de Adobe Experience Platform a [!DNL Marketo Measure]. La tarjeta solo está disponible para clientes de [!DNL Marketo Measure Ultimate]. |
| [Conexión de TikTok](../../destinations/catalog/social/tiktok.md) | Cree públicos personalizados en TikTok con sus datos para segmentar con sus campañas de anuncios. |
| [Conexión de Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilice este destino para crear y actualizar identidades dentro de un segmento como contactos dentro de [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Nuevo permiso de control de acceso para destinos: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | El nuevo permiso permite a los usuarios activar segmentos en destinos existentes, sin mostrar el [paso de asignación](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Los usuarios pueden añadir y quitar segmentos en flujos de trabajo de activación, pero no pueden agregar ni quitar atributos o identidades asignados. |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

Estamos publicando una corrección de errores para el cifrado PGP/GPG en destinos basados en archivos para Real-Time CDP. Con este cambio, los destinos basados en archivos existentes que actualmente utilicen cifrado generarán un nombre de archivo con una extensión diferente a la anterior.

- Extensión actual al utilizar cifrado: `filename.csv`
- Extensión futura al utilizar cifrado: `filename.csv.gpg`

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| CSV a recomendación de esquema | Ahora puede cargar los archivos locales para crear esquemas generados por aprendizaje automático que eliminen la necesidad de elaborarlos manualmente. Desde el espacio de trabajo [!UICONTROL Fuentes], cargue un archivo CSV de muestra y los algoritmos de aprendizaje automático de Adobe le sugerirán un esquema basado en los campos del público destinatario. Consulte la [Documentación](../../ingestion/tutorials/map-csv/recommendations.md) para obtener más información.&quot; |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Artículo de oferta]](https://github.com/adobe/xdm/pull/1678/files) | Clase que representa una oferta. |
| Clase | [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1678/files) | Un elemento que puede estar sujeto a decisiones. El resultado de un proceso de toma de decisiones es uno o más elementos de decisión. |
| Clase | [[!UICONTROL Tiempo de espera del servidor de sesión de medios]](https://github.com/adobe/xdm/pull/1676/files) | Indica la cantidad de tiempo en segundos que transcurrió entre la última interacción conocida del usuario y el momento en que se cerró la sesión. |
| Grupo de campos | [[!UICONTROL Atributos calculados de perfil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Esto añade atributos calculados de los servicios internos de Adobe a los datos de clientes entrantes. Los clientes no deben utilizarlo para introducir datos. |
| Tipo de datos | [[!UICONTROL Elemento de devolución]](https://github.com/adobe/xdm/pull/1685/files) | Indica si una devolución está asociada a un pedido y define el tipo de devolución, el importe y la divisa asociada. |
| Tipo de datos | [[!UICONTROL Datos de categoría]](https://github.com/adobe/xdm/pull/1677/files) | Este nuevo tipo de datos representa la categoría de un producto. |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Se ha creado un nuevo esquema XDM para los conjuntos de datos de clasificación de Target. Contiene un conjunto de campos de metadatos que clasifican las actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Detalles del componente de contenido]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` se ha eliminado de [!UICONTROL Detalles del componente de contenido] |
| Grupo de campos | [[!UICONTROL Etiquetas de entidad de AJO]](https://github.com/adobe/xdm/pull/1672/files) | Se han añadido etiquetas de entidad de AJO a [!UICONTROL Campos de entidad de AJO], que corresponden a un recorrido o a una campaña |
| Grupo de campos | (Múltiple) | Se han añadido varios campos para [[!UICONTROL Campos comunes de eventos de pasos de Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Grupo de campos | (Múltiple) | [Se han añadido varios tipos de eventos XDM para [!UICONTROL Creación de informes de medios]](https://github.com/adobe/xdm/pull/1670/files). |
| Grupo de campos | [!UICONTROL Evento de cambio de Workfront] | Se han añadido los grupos de campos `Full Record` y `Accessor Employee Ids`. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/pull/1685/files) | El [!UICONTROL Importe de devolución] se ha añadido para indicar la cantidad reembolsada por el artículo, si la hubiera. |
| Tipo de datos | [[!UICONTROL Pedido ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Lista de devoluciones] se ha añadido a la lista de las devoluciones de este pedido. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos ]](https://github.com/adobe/xdm/pull/1677/files) | Se han añadido categorías de productos a los datos de categoría de este producto. |
| Tipo de datos | [!UICONTROL Información de detalles de sesión] | Se ha añadido el campo de cadena `pev3`que [indica el tipo de flujo de medios utilizado para la creación de informes](https://github.com/adobe/xdm/pull/1676/files). También se ha añadido la propiedad `pccr`, que indica si se ha producido una redirección. |
| Tipo de datos | [!UICONTROL Lista de solicitudes] | Proporciona las [propiedades de la lista de solicitudes](https://github.com/adobe/xdm/pull/1675/files). Incluyen nombre, ID y descripción. |
| Tipo de datos | [!UICONTROL Commerce] | [Se ha actualizado el tipo de datos de Commerce](https://github.com/adobe/xdm/pull/1675/files) para incluir `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` y `requisitionList`. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su inserción en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Control de acceso basado en atributos en el almacén acelerado | Utilice el control de acceso basado en atributos con Data Distiller para definir el control de acceso en todos los conjuntos de datos del almacén acelerado. Controla el acceso a los modelos de datos personalizados creados por los usuarios y almacenados en un almacén acelerado para activar los paneles personalizados. |

{style="table-layout:auto"}

Para obtener más información sobre los servicios de consulta, vea la [Información general del servicio de consulta](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP edición B2B, que se creó en Real-time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a públicos específicos con precisión y captarlos en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Corrección de errores | Para proporcionar una representación más precisa de los perfiles de su sistema, el sistema ya no incluye perfiles internos en el recuento total de perfiles ni en la métrica de públicos direccionables de Real-time Customer Data Platform edición B2B. A partir de hoy, es posible que se produzca un descenso puntual en la métrica de recuento total de perfiles/públicos direccionables. No se han borrado sus datos, se trata simplemente de un cambio en el recuento. Póngase en contacto con su ejecutivo de Adobe si tiene alguna duda |

{style="table-layout:auto"}

Para obtener más información sobre Real-Time CDP edición B2B, lea la [Información general de Real-Time CDP edición B2B](../../rtcdp/overview.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Métricas de perfil | Para ofrecerle una representación más precisa de las métricas de perfil, se combinan las métricas de desglose y pérdida de abonos y ahora se calculan en un periodo de 24 horas. Encontrará más información en la [Guía de la IU de segmentación](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad beta de [!DNL Chatlio] | La fuente [!DNL Chatlio] ya está disponible en versión beta. Use la fuente [!DNL Chatlio] para transmitir sus datos de eventos de [!DNL Chatlio] a Experience Platform. Para obtener más información, lea la Información general de [[!DNL Chatlio] ](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilidad beta de [!DNL Customer.io] | La fuente [!DNL Customer.io] ya está disponible en versión beta. Use la fuente [!DNL Customer.io] para transmitir sus datos de eventos de cliente a Experience Platform. Para obtener más información, lea la Información general de [[!DNL Customer.io] ](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilidad beta de [!DNL Pendo] | La fuente [!DNL Pendo] ya está disponible en versión beta. Use la fuente [!DNL Pendo] para transmitir sus datos de eventos de Product Analytics a Experience Platform. Para obtener más información, lea la Información general de [[!DNL Pendo] ](../../sources/connectors/analytics/pendo-webhook.md). |
| Compatibilidad con flujos de datos en borrador | Ahora puede utilizar la API del servicio de flujo para establecer sus flujos de datos en estado de borrador. Los flujos de datos en borrador se pueden actualizar y publicar posteriormente con nueva información. Para obtener más información, lea la guía de [configuración de los flujos de datos de fuentes como borradores](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Para obtener más información acerca de las fuentes, lea la [Información general de fuentes](../../sources/home.md).
