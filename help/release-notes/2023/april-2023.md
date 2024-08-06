---
title: 'Notas de la versión de Adobe Experience Cloud: abril de 2023'
description: Las notas de la versión de abril de 2023 de Adobe Experience Platform.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 98%

---

# Notas de la versión de Adobe Experience Platform

>[!IMPORTANT]
>
>A partir del 15 de mayo de 2023, el estado `Existing` quedará obsoleto en el mapa de abono del segmento para eliminar la redundancia en el ciclo vital de los miembros del segmento. Después de este cambio, los perfiles clasificados en un segmento se representarán como `Realized` y los perfiles descalificados seguirán representándose como `Exited`. Para obtener más información sobre este cambio, lea la [sección Servicio de segmentación](#segmentation).

**Fecha de publicación: 26 de abril de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Paneles](#dashboards)
- [Preparación de los datos](#data-prep)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Paneles definidos por el usuario | Ahora puede **filtrar datos históricos** desde las perspectivas del widget y utilizar datos recientes o un período de análisis personalizado. Si desea obtener más información, consulte la [guía de paneles definidos por el usuario](../../dashboards/user-defined-dashboards.md#filter-historical-data).<br>Ahora también puede **duplicar los widgets existentes**. Al personalizar un duplicado y editar sus atributos, puede evitar reiniciar desde el principio al crear un widget nuevo y único. Lea la [guía de duplicación de widgets](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones del período de relleno para Adobe Analytics en zonas protegidas que no son de producción | El período de relleno para Adobe Analytics en zonas protegidas que no son de producción se ha reducido a tres meses. El relleno para las zonas protegidas de producción sigue siendo el mismo a los 13 meses. Este cambio solo se aplica a los nuevos flujos y no afecta a los flujos existentes. Para obtener más información, lea la [Información general de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nueva función de asignación para convertir cadenas FPID a ECID | Utilice la función `fpid_to_ecid` para convertir las cadenas FPID en ECID para su uso en las aplicaciones Experience Platform y Experience Cloud. Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea [Información general sobre preparación de datos](../../data-prep/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Ofuscación de direcciones IP para flujos de datos | Ahora puede definir opciones de ofuscación de IP parciales o completas en el nivel de flujo de datos en la variable [IU de configuración de secuencia de datos](../../datastreams/configure.md). <br><br>La configuración de ofuscación de IP en el nivel de flujo de datos tiene prioridad sobre cualquier ofuscación de IP configurada en Adobe Target y Audience Manager. <br><br>Los datos enviados a Adobe Analytics no se ven afectados por la configuración [!UICONTROL Ofuscación de IP] del nivel de conjunto de datos. Actualmente, Adobe Analytics recibe direcciones IP no ofuscadas. Para que Analytics reciba direcciones IP ofuscadas, debe configurar la ofuscación de IP por separado en Adobe Analytics. Este comportamiento se actualizará en futuras versiones.<br><br> Para obtener más información acerca de la ofuscación de IP e instrucciones sobre cómo configurarla, consulte la [documentación de configuración de secuencia de datos](../../datastreams/configure.md#advanced-options). |
| [Anulaciones de configuración de secuencia de datos](../../datastreams/overrides.md) | Ahora puede definir opciones de configuración adicionales para flujos de datos, que puede utilizar para anular configuraciones específicas, como conjuntos de datos de evento, tókenes de propiedades de Target, contenedores de sincronización de ID y grupos de informes de Analytics. <br><br>La anulación de las configuraciones de secuencia de datos es un proceso de dos pasos: <ol><li>En primer lugar, debe definir las anulaciones de configuración de la secuencia de datos en la [página de configuración de secuencia de datos](../../datastreams/configure.md).</li><li>A continuación, debe enviar las anulaciones a Edge Network mediante un comando del SDK web o la [extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) del SDK web.</li></ol> |
| Secreto JWT de OAuth  | El [Secreto JWT de OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) les permite a los clientes utilizar tókenes de Adobe y de servicio de Google para admitir interacciones de servidor a servidor en el reenvío de eventos. |
| Extensión [!DNL Pinterest Conversions API] | La extensión de reenvío de eventos [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=es) permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor que utilizan el [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] conexión](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilice el destino de participación en la cuenta de Marketing Cloud de Salesforce (anteriormente conocido como Pardot) para capturar, rastrear, puntuar y clasificar los posibles clientes. Utilice este destino para casos de uso B2B que impliquen varios departamentos y responsables de la toma de decisiones que requieran ciclos de ventas y decisiones más largos. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Monitorización de flujo de datos para destinos de [!DNL Custom Personalization] y [!DNL Adobe Commerce] | <p> Ahora puede ver las métricas de activación de las conexiones de [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalización](../../destinations/catalog/personalization/custom-personalization.md) y [Personalización con atributos](../../destinations/catalog/personalization/custom-personalization.md). </p> <p>![Imagen de Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas de Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorización de flujos de datos en el espacio de trabajo Destinos](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obtener más información. |
| Nuevo campo **[!UICONTROL Anexar ID de segmento al nombre del segmento]** para los destinos [!DNL Google Ad Manager] y [!DNL Google Ad Manager 360] | <p>Ahora puede hacer que el nombre del segmento en [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) y [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) incluya el ID de segmento de Experience Platform de la siguiente manera: `Segment Name (Segment ID)`.</p><p>![Anexar imagen de ID de segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nuevo campo Anexar ID de segmento a nombre de segmento "){width="100" zoomable="yes"}</p> |
| Rellenos de público programados | <p>Para el destino [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics), la activación de los rellenos de público en el destino está programada para realizarse de 24 a 48 horas después de que un segmento se asigne por primera vez a una conexión de destino. Esta actualización es en respuesta a la directiva de Google de esperar 24 horas hasta la ingesta de datos y mejorará las tasas de coincidencia entre Real-Time CDP y [!DNL Google Display & Video 360].</p> <p>Tenga en cuenta que esta es una configuración back-end aplicable solo a este destino y que no está relacionada con ninguna opción de programación configurable por el cliente en la interfaz de usuario.</p> |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Hemos corregido un problema en las métricas de informes de **Identidades excluidas** para exportaciones de destino basadas en archivos. Los clientes recibían todos los ID exportados de la exportación activada según lo esperado. Sin embargo, la métrica de informes **Identidades excluidas** de la IU mostraba incorrectamente un alto número de identidades excluidas debido a un recuento incorrecto de identidades que nunca se suponía que se exportarían. (PLAT-149774)
- Hemos corregido un problema en el paso **Programación** del flujo de trabajo de activación. En el caso de los destinos que requieren un ID de asignación, los clientes no podían agregar un ID de asignación para los segmentos añadidos a conexiones de destino existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Alternar nombres para mostrar | El Editor de esquemas ahora proporciona un conmutador para cambiar entre los nombres de campo originales y los nombres para mostrar más legibles en lenguaje natural.<br>![El Editor de esquemas con el nombre para mostrar resaltado.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Alternar nombre para mostrar del Editor de esquemas"){width="100" zoomable="yes"}<br>Esta flexibilidad permite mejorar la capacidad de detección de campos y la edición de los esquemas. Los nombres para mostrar de los grupos de campos estándar se generan en el sistema, pero también se pueden personalizar a través de la interfaz de usuario si es necesario. Lea la [documentación de alternancia de nombre para mostrar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle?lang=es) para obtener más información. |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Un nuevo esquema XDM para conjuntos de datos de clasificación de Target que contiene un conjunto de campos de metadatos para clasificar actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Extensión de unión de cuentas del servicio de perfil unificado de Adobe]](https://github.com/adobe/xdm/pull/1696/files) | Se ha añadido un grupo de campos de extensión de cuenta para el Perfil del cliente en tiempo real que permite a los usuarios añadir un abono de segmentos en la unión de cuentas. |
| Esquema | [[!UICONTROL Esquema del sistema de atributos calculados]](https://github.com/adobe/xdm/pull/1696/files) | El grupo de campos Atributos calculados utilizado por el Perfil del cliente en tiempo real se ha actualizado a un esquema global de solo lectura del sistema. |
| Grupo de campos | Múltiple | Se han añadido varios eventos como campos para [[!UICONTROL Esquema de series de tiempo]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalles de fidelización del perfil | [Se ha corregido el título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de “Nombre del programa” a “Fecha de actualización”. |
| Grupo de campos | Múltiple | Varios campos de [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1714/files) se han actualizado para eliminar la jerarquía anidada doble. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

El compilado en Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido del cliente. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Página de inicio de Real-Time CDP mejorada | La [Página de inicio de Real-Time CDP](https://experience.adobe.com) se ha mejorado con un aspecto actualizado y un rendimiento mejorado. La página de inicio ahora reconoce permisos y presenta widgets relevantes para las funciones a las que tiene acceso. Para obtener más información, lea la [Información general del panel de la página de inicio de Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Encuesta de autoidentificación | La encuesta de autoidentificación es un breve cuestionario que se presenta en la página de inicio de la interfaz de usuario de Adobe Experience Platform. Utilice la encuesta de autoidentificación para crear su perfil personal de Experience Platform y recibir directrices adaptadas en función de sus selecciones. Para obtener más información, lea la [Información general sobre la encuesta de autoidentificación](../../landing/self-identification.md). |

Para obtener más información sobre [!DNL Real-Time CDP], consulte la [[!DNL Real-Time CDP] información general](../../rtcdp/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Caducidad de datos de perfil seudónimo | La caducidad de los datos de perfil seudónimo ya está disponible de forma general. Esta versión elimina continuamente los perfiles seudónimos antiguos de la instancia de Experience Platform una vez activadada. Para obtener más información acerca de esta función y los perfiles seudónimos, lea la [Guía de caducidad de datos de perfil seudónimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Mapa de abono de segmento | Como continuación del anuncio anterior, realizado en febrero, el 15 de mayo de 2023, el estado `Existing` quedará obsoleto en el mapa de abono del segmento para eliminar la redundancia en el ciclo vital del abono del segmento. Después de este cambio, los perfiles clasificados en un segmento se representarán como `Realized` y los perfiles descalificados seguirán representándose como `Exited`.<br/><br/> Este cambio podría afectarle si está utilizando [destinos empresariales](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, Azure Event Hubs, API HTTP) y pueden tener procesos descendentes automatizados basados en el estado `Existing`. Si este es su caso, revise las integraciones posteriores. Si está interesado en identificar perfiles recién cualificados más allá de un cierto tiempo, considere la posibilidad de utilizar una combinación del estado `Realized` y el `lastQualificationTime` en el mapa de abono a segmentos. Para obtener más información, póngase en contacto con su representante de Adobe. |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad de la API para filtrar datos de nivel de fila para el origen de CRM de Salesforce. | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para la fuente CRM de Salesforce. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |
| Disponibilidad beta de Shopify Streaming | La [fuente de streaming de Shopify](../../sources/connectors/ecommerce/shopify-streaming.md) ya está disponible en la versión beta. Utilice la fuente de streaming de Shopify para transmitir los datos de su cuenta de socios de Shopify a Experience Platform. |
| Disponibilidad general de la integración de OneTrust | La [Fuente de integración de OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) es ahora GA. Utilice la fuente de integración de OneTrust para llevar los datos de preferencias y consentimiento de su cuenta de integración de OneTrust a Experience Platform. |
| Disponibilidad general de Oracle Service Cloud | La [fuente de nube del servicio de Oracle](../../sources/connectors/customer-success/oracle-service-cloud.md) es ahora GA. Utilice la fuente de nube del servicio de Oracle para llevar los datos de nube del servicio de Oracle a Experience Platform. |

{style="table-layout:auto"}

Para obtener más información acerca de las fuentes, lea la [Información general de fuentes](../../sources/home.md).
