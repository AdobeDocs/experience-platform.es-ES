---
title: Notas de la versión de Adobe Experience Platform, abril de 2023
description: Notas de la versión de abril de 2023 de Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 4%

---

# Notas de la versión de Adobe Experience Platform

>[!IMPORTANT]
>
>A partir del 15 de mayo de 2023, la `Existing` El estado quedará obsoleto en el mapa de miembros del segmento para eliminar la redundancia en el ciclo vital de los miembros del segmento. Después de este cambio, los perfiles clasificados en un segmento se representarán como `Realized` y los perfiles descalificados seguirán representándose como `Exited`. Para obtener más información sobre este cambio, lea la [Sección Servicio de segmentación](#segmentation).

**Fecha de publicación: 26 de abril de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Tableros](#dashboards)
- [Preparación de datos](#data-prep)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Paneles definidos por el usuario | Ahora puede **filtrar datos históricos** desde las perspectivas del widget y utilice datos recientes o un periodo de análisis personalizado. Consulte la [guía de paneles definidos por el usuario](../../dashboards/user-defined-dashboards.md#filter-historical-data) para obtener más información.<br>Ahora también puede **duplicar los widgets existentes**. Al personalizar un duplicado y editar sus atributos, puede evitar reiniciar desde el principio al crear un widget nuevo y único. Lea el [guía de duplicación de widgets](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer el [información general sobre paneles](../../dashboards/home.md).

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones del período de relleno para Adobe Analytics en zonas protegidas que no son de producción | El período de relleno para Adobe Analytics en zonas protegidas que no son de producción se ha reducido a tres meses. El relleno para las zonas protegidas de producción sigue siendo el mismo a los 13 meses. Este cambio solo se aplica a los nuevos flujos y no afecta a los flujos existentes. Para obtener más información, lea la [Información general de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nueva función de asignación para convertir cadenas FPID a ECID | Utilice el `fpid_to_ecid` para convertir cadenas FPID en ECID para su uso en aplicaciones de Experience Platform y Experience Cloud. Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea la [Resumen de preparación de datos](../../data-prep/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Confusión de direcciones IP para flujos de datos | Ahora puede definir opciones de confusión de IP parciales o completas en el nivel de flujo de datos en la variable [IU de configuración de secuencia de datos](../../edge/datastreams/configure.md). <br><br>La configuración de ofuscación de IP en el nivel de flujo de datos tiene prioridad sobre cualquier ofuscación de IP configurada en Adobe Target y Audience Manager. <br><br>Los datos enviados a Adobe Analytics no se ven afectados por el nivel de conjunto de datos [!UICONTROL Confusión de IP] configuración. Actualmente, Adobe Analytics recibe direcciones IP no ocultadas. Para que Analytics reciba direcciones IP ofuscadas, debe configurar la ofuscación de IP por separado en Adobe Analytics. Este comportamiento se actualizará en futuras versiones.<br><br> Para obtener más información acerca de la confusión de la IP e instrucciones sobre cómo configurarla, consulte la [documentación de configuración de secuencia de datos](../../edge/datastreams/configure.md#advanced-options). |
| [Anulaciones de configuración de secuencia de datos](../../edge/datastreams/overrides.md) | Ahora puede definir opciones de configuración adicionales para flujos de datos, que puede utilizar para anular configuraciones específicas, como conjuntos de datos de evento, tokens de propiedades de Target, contenedores de sincronización de ID y grupos de informes de Analytics. <br><br>Anular las configuraciones de secuencia de datos es un proceso de dos pasos: <ol><li>En primer lugar, debe definir las anulaciones de configuración de la secuencia de datos en la [página configuración de secuencia de datos](../../edge/datastreams/configure.md).</li><li>A continuación, debe enviar las invalidaciones a la red perimetral mediante un comando del SDK web o mediante el SDK web [extensión de etiqueta](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| Secreto JWT de OAuth | El [Secreto JWT de OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) permite a los clientes utilizar tokens de Adobe y servicio de Google para admitir interacciones de servidor a servidor en el reenvío de eventos. |
| [!DNL Pinterest Conversions API] Extensión | El [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) La extensión de reenvío de eventos permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor que utilizan el [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] conexión](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilice el destino de participación en la cuenta de Marketing Cloud de Salesforce (anteriormente conocido como Pardot) para capturar, rastrear, puntuar y clasificar posibles clientes. Utilice este destino para casos de uso B2B que impliquen varios departamentos y responsables de la toma de decisiones que requieran ciclos de ventas y decisión más largos. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Monitorización de flujo de datos para [!DNL Custom Personalization] y [!DNL Adobe Commerce] destinos | <p> Ahora puede ver las métricas de activación de [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md) y el [Personalización personalizada con atributos](../../destinations/catalog/personalization/custom-personalization.md) conexiones. </p> <p>![Imagen de Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas de Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorización de flujos de datos en el espacio de trabajo Destinos](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obtener más información. |
| Nuevo **[!UICONTROL Anexar ID de segmento al nombre del segmento]** para el [!DNL Google Ad Manager] y [!DNL Google Ad Manager 360] destinos | <p>Ahora puede tener el nombre del segmento en [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) y [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) incluya el ID de segmento del Experience Platform de la siguiente manera: `Segment Name (Segment ID)`.</p><p>![Anexar imagen de ID de segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nuevo campo Anexar ID de segmento a nombre de segmento "){width="100" zoomable="yes"}</p> |
| Rellenos de audiencia programados | <p>Para el [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) destino, la activación de los rellenos de audiencia en el destino está programada para realizarse de 24 a 48 horas después de que un segmento se asigne por primera vez a una conexión de destino. Esta actualización es en respuesta a la política de Google de esperar 24 horas hasta la ingesta de datos y mejorará las tasas de coincidencia entre Real-time CDP y [!DNL Google Display & Video 360].</p> <p>Tenga en cuenta que esta es una configuración back-end aplicable solo a este destino y que no está relacionada con ninguna opción de programación configurable por el cliente en la interfaz de usuario.</p> |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Hemos corregido un problema en la **Identidades excluidas** crear informes de métricas para exportaciones de destino basadas en archivos. Los clientes recibían todos los ID exportados de la exportación activada según lo esperado. Sin embargo, la variable **Identidades excluidas** La métrica de informes de la IU de mostraba incorrectamente un alto número de identidades excluidas debido a un recuento incorrecto de identidades que nunca se suponía que se exportarían. (PLAT-149774)
- Hemos corregido un problema en la **Programación** del flujo de trabajo de activación. En el caso de los destinos que requieren un ID de asignación, los clientes no podían agregar un ID de asignación para los segmentos añadidos a conexiones de destino existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Alternar nombres para mostrar | El Editor de esquemas ahora proporciona un conmutador para cambiar entre los nombres de campo originales y los nombres para mostrar más legibles en lenguaje natural.<br>![El Editor de esquemas con el nombre para mostrar resaltado.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Alternar nombre para mostrar del Editor de esquemas"){width="100" zoomable="yes"}<br>Esta flexibilidad permite mejorar la capacidad de detección de campos y la edición de los esquemas. Los nombres para mostrar de los grupos de campos estándar se generan en el sistema, pero también se pueden personalizar a través de la interfaz de usuario si es necesario. Lea el [documentación de alternancia de nombre para mostrar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) para obtener más información. |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Un nuevo esquema XDM para conjuntos de datos de clasificación de Target que contiene un conjunto de campos de metadatos para clasificar actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Extensión de unión de cuentas del servicio de perfiles unificado de Adobe]](https://github.com/adobe/xdm/pull/1696/files) | Se ha añadido un grupo de campos de extensión de cuenta para el Perfil del cliente en tiempo real que permite a los usuarios añadir miembros de segmentos en la unión de cuentas. |
| Esquema | [[!UICONTROL Esquema del sistema de atributos calculados]](https://github.com/adobe/xdm/pull/1696/files) | El grupo de campos Atributos calculados utilizado por el Perfil del cliente en tiempo real se ha actualizado a un esquema global de solo lectura del sistema. |
| Grupo de campos | Múltiple | Se han añadido varios eventos como campos para [[!UICONTROL Esquema de series de tiempo]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalles de fidelización del perfil | [Se ha corregido el título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de &quot;Nombre del programa&quot; a &quot;Fecha de actualización&quot;. |
| Grupo de campos | Múltiple | Varios campos de [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1714/files) se han actualizado para eliminar la jerarquía anidada doble. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Compilado en el Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido de clientes. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Página de inicio de Real-Time CDP mejorada | El [Página de inicio de Real-Time CDP](https://experience.adobe.com) se ha mejorado con un aspecto actualizado y un rendimiento mejorado. La página de inicio ahora reconoce permisos y presenta widgets relevantes para las funciones a las que tiene acceso. Para obtener más información, lea la [Información general del panel de página principal de Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Encuesta de autoidentificación | La encuesta de autoidentificación es un breve cuestionario que se presenta en la página de inicio de la interfaz de usuario de Adobe Experience Platform. Utilice la encuesta de autoidentificación para crear su perfil personal de Experience Platform y recibir directrices adaptadas en función de sus selecciones. Para obtener más información, lea la [información general sobre las encuestas de autoidentificación](../../landing/self-identification.md). |

Para obtener más información sobre [!DNL Real-Time CDP], consulte la [[!DNL Real-Time CDP] descripción general](../../rtcdp/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Caducidad de datos de perfil seudónimos | La caducidad de los datos de perfil seudónimos ya está disponible de forma general. Esta versión eliminará continuamente los perfiles seudónimos antiguos de la instancia de Experience Platform una vez que se haya activado. Para obtener más información acerca de esta función y los perfiles seudónimos, lea la [Pseudónimo Guía de caducidad de datos de perfil](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Asignación de abono de segmento | Como continuación del anuncio anterior, realizado en febrero, el 15 de mayo de 2023, la `Existing` El estado quedará obsoleto en el mapa de miembros del segmento para eliminar la redundancia en el ciclo vital de los miembros del segmento. Después de este cambio, los perfiles clasificados en un segmento se representarán como `Realized` y los perfiles descalificados seguirán representándose como `Exited`.<br/><br/> Este cambio podría afectarle si está utilizando [destinos empresariales](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, API HTTP) y pueden tener procesos descendentes automatizados basados en el `Existing` estado. Si este es el caso, revise sus integraciones posteriores. Si está interesado en identificar perfiles recién cualificados más allá de un cierto tiempo, considere la posibilidad de utilizar una combinación de los siguientes `Realized` estado y el `lastQualificationTime` en el mapa de abono a segmentos. Para obtener más información, póngase en contacto con el representante del Adobe. |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad de la API para filtrar datos de nivel de fila para el origen de CRM de Salesforce. | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para el origen de CRM de Salesforce. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |
| Disponibilidad beta de Shopify Streaming | El [Shopify Streaming source](../../sources/connectors/ecommerce/shopify-streaming.md) ya está disponible en la versión beta. Utilice la fuente Shopify Streaming para transmitir los datos de su cuenta de socios de Shopify al Experience Platform. |
| Disponibilidad general de la integración de OneTrust | El [Origen de integración de OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) es ahora GA. Utilice la fuente de integración de OneTrust para llevar los datos de preferencias y consentimiento de su cuenta de integración de OneTrust al Experience Platform. |
| Disponibilidad general de Oracle Service Cloud | El [Fuente de nube de Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) es ahora GA. Utilice la fuente de nube del servicio de Oracle para llevar los datos de nube del servicio de Oracle a Experience Platform. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).