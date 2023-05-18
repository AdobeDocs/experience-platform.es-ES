---
title: Notas de la versión de Adobe Experience Platform, abril de 2023
description: Notas de la versión de abril de 2023 para Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 4%

---

# Notas de la versión de Adobe Experience Platform

>[!IMPORTANT]
>
>A partir del 15 de mayo de 2023, la variable `Existing` se eliminará del mapa de pertenencia a segmentos para eliminar la redundancia en el ciclo de vida de pertenencia a segmentos. Después de este cambio, los perfiles cualificados en un segmento se representarán como `Realized` y los perfiles no calificados se seguirán representando como `Exited`. Para obtener más información sobre este cambio, lea la [Sección Servicio de segmentación](#segmentation).

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

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

**Funciones nuevas o actualizadas** {#dashboards-new-updated-features}

| Función | Descripción |
| --- | --- |
| Tableros definidos por el usuario | Ahora puede **filtrar datos históricos** desde la información del widget, y utilice datos recientes o un período de análisis personalizado. Consulte la [guía de paneles definidos por el usuario](../../dashboards/user-defined-dashboards.md#filter-historical-data) para obtener más información.<br>Ahora también puede **duplicar las utilidades existentes**. Al personalizar un duplicado y editar sus atributos, puede evitar reiniciar desde el principio al crear un nuevo widget único. Lea el [guía de duplicación de utilidades](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) para obtener más información. |

{style="table-layout:auto"}

Para obtener más información sobre los tableros, incluido cómo conceder permisos de acceso y crear utilidades personalizadas, comience por leer [información general sobre los paneles](../../dashboards/home.md).

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Actualizaciones del periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción | El periodo de relleno para Adobe Analytics en entornos limitados que no sean de producción se ha reducido a tres meses. El relleno de los entornos limitados de producción sigue siendo el mismo a los 13 meses. Este cambio solo se aplica a los flujos nuevos y no afecta a los flujos existentes. Para obtener más información, lea la [Información general de Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nueva función de asignación para convertir cadenas FPID en ECID | Utilice la variable `fpid_to_ecid` para convertir cadenas FPID en ECID para su uso en aplicaciones de Experience Platform y Experience Cloud. Para obtener más información, lea la [Guía de funciones de preparación de datos](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obtener más información sobre la preparación de datos, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Confusión de direcciones IP para conjuntos de datos | Ahora puede definir opciones de confusión de IP a nivel de conjunto de datos parciales o completas en la sección [interfaz de configuración del almacén de datos](../../edge/datastreams/configure.md). <br><br>La configuración de confusión de IP a nivel de almacén de datos tiene prioridad sobre cualquier confusión de IP configurada en Adobe Target y Audience Manager. <br><br>Los datos enviados a Adobe Analytics no se ven afectados por el nivel del conjunto de datos [!UICONTROL Confusión de IP] configuración. Actualmente, Adobe Analytics recibe direcciones IP sin confusión. Para que Analytics reciba direcciones IP ofuscadas, debe configurar la confusión de IP por separado en Adobe Analytics. Este comportamiento se actualizará en futuras versiones.<br><br> Para obtener más información sobre la confusión de IP e instrucciones sobre cómo configurarla, consulte la [documentación de configuración de datastream](../../edge/datastreams/configure.md#advanced-options). |
| [Anulaciones de configuración del almacén de datos](../../edge/datastreams/overrides.md) | Ahora puede definir opciones de configuración adicionales para conjuntos de datos, que puede utilizar para anular configuraciones específicas, como conjuntos de datos de evento, tokens de propiedad de Target, contenedores de sincronización de ID y grupos de informes de Analytics. <br><br>La anulación de las configuraciones del conjunto de datos es un proceso de dos pasos: <ol><li>En primer lugar, debe definir las anulaciones de configuración del conjunto de datos en la variable [página de configuración del almacén de datos](../../edge/datastreams/configure.md).</li><li>A continuación, debe enviar las anulaciones a la red perimetral a través de un comando Web SDK o utilizando el SDK web [extensión de etiqueta](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| Secreto JWT de OAuth | La variable [Secreto JWT de OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) permite a los clientes utilizar tokens de Adobe y de servicio de Google para admitir interacciones de servidor a servidor en el reenvío de eventos. |
| [!DNL Pinterest Conversions API] Extensión | La variable [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) la extensión de reenvío de eventos permite aprovechar los datos capturados en Adobe Experience Platform Edge Network y enviarlos a [!DNL Pinterest] en forma de eventos del lado del servidor utilizando la variable [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos** {#new-destinations}

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] connection](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilice el destino Participación de cuenta de Marketing Cloud de Salesforce (anteriormente conocido como Pardot) para capturar, rastrear, puntuar y clasificar posibles clientes. Utilice este destino para casos de uso B2B que involucren múltiples departamentos y responsables de la toma de decisiones que requieren ciclos de decisión y ventas más largos. |

{style="table-layout:auto"}

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Supervisión de flujo de datos para [!DNL Custom Personalization] y [!DNL Adobe Commerce] destinos | <p> Ahora puede ver las métricas de activación para la variable [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md) y [Personalización Personalizada Con Atributos](../../destinations/catalog/personalization/custom-personalization.md) conexiones. </p> <p>![Imagen de Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas de Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorización de flujos de datos en el espacio de trabajo Destinations](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obtener más información. |
| Nuevo **[!UICONTROL Anexar ID de segmento al nombre del segmento]** para la variable [!DNL Google Ad Manager] y [!DNL Google Ad Manager 360] destinos | <p>Ahora puede tener el nombre del segmento en [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) y [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) incluya el ID de segmento de Experience Platform, de esta manera: `Segment Name (Segment ID)`.</p><p>![Anexar imagen de ID de segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nuevo campo Anexar ID de segmento al nombre del segmento "){width="100" zoomable="yes"}</p> |
| Rellenos programados de audiencia | <p>Para la variable [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) de destino, la activación de los rellenos de audiencia en el destino está programada para producirse entre 24 y 48 horas después de que un segmento se asigne por primera vez a una conexión de destino. Esta actualización responde a la política de Google de esperar 24 horas hasta la ingesta de datos y mejorará las tasas de coincidencia entre CDP en tiempo real y [!DNL Google Display & Video 360].</p> <p>Tenga en cuenta que esta es una configuración back-end aplicable solo a este destino y que no está relacionada con ninguna opción de programación configurable por el cliente en la interfaz de usuario.</p> |

{style="table-layout:auto"}

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

- Se ha corregido un problema en la variable **Identidades excluidas** métricas de informes para exportaciones de destino basadas en archivos. Los clientes recibían todos los ID exportados desde la exportación activada según lo esperado. Sin embargo, la variable **Identidades excluidas** la métrica de creación de informes en la interfaz de usuario mostraba incorrectamente un número elevado de identidades excluidas debido a un recuento incorrecto de identidades que no se suponía que nunca se exportarían. (PLAT-149774)
- Se ha corregido un problema en la variable **Programación** del flujo de trabajo de activación. En el caso de los destinos que requieren un ID de asignación, los clientes no podían agregar un ID de asignación para los segmentos añadidos a conexiones de destino existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mostrar nombres, alternador | El Editor de esquemas ahora proporciona un interruptor para cambiar entre los nombres de campo originales y los nombres para mostrar más legibles.<br>![El Editor de esquemas con el nombre para mostrar resaltado.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Alternador de nombre para mostrar del Editor de esquemas"){width="100" zoomable="yes"}<br>Esta flexibilidad permite mejorar la capacidad de detección de campos y la edición de los esquemas. Los nombres para mostrar de los grupos de campos estándar se generan a partir del sistema, pero también se pueden personalizar a través de la interfaz de usuario si es necesario. Lea el [documentación de alternancia de nombre para mostrar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) para obtener más información. |

{style="table-layout:auto"}

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema | [[!UICONTROL Campos de clasificación de Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Un nuevo esquema XDM para conjuntos de datos de clasificación de Target que contiene un conjunto de campos de metadatos para clasificar actividades y experiencias de Target. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Extensión de la unión de cuentas del servicio de perfil unificado de Adobe]](https://github.com/adobe/xdm/pull/1696/files) | Se ha agregado un grupo de campos de extensión de cuenta para el perfil del cliente en tiempo real que permite a los usuarios agregar miembros de segmento en la unión de cuentas. |
| Esquema | [[!UICONTROL Esquema del sistema de atributos calculados]](https://github.com/adobe/xdm/pull/1696/files) | El grupo de campos Atributos calculados utilizado por el perfil de cliente en tiempo real se ha actualizado a un esquema global de solo lectura del sistema. |
| Grupo de campos | Múltiple | Se han añadido varios eventos como campos para [[!UICONTROL Esquema de series temporales]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalles de lealtad del perfil | [Se ha corregido el título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de &quot;Nombre del programa&quot; a &quot;Fecha de actualización&quot;. |
| Grupo de campos | Múltiple | Varios campos de [[!UICONTROL Elemento de decisión]](https://github.com/adobe/xdm/pull/1714/files) se han actualizado para eliminar la jerarquía anidada doble. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Basado en el Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes en todo el recorrido de clientes. [!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos descendentes para ofrecer experiencias personalizadas de cliente personalizadas en todos los canales y dispositivos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Página de inicio de Real-Time CDP mejorada | La variable [Página de inicio de Real-Time CDP](https://experience.adobe.com) se ha mejorado con un aspecto actualizado y un rendimiento mejorado. La página principal ahora reconoce permisos y presentará utilidades relevantes para las funciones a las que tiene acceso. Para obtener más información, lea la [Información general del tablero de la página de inicio de Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Encuesta de autoidentificación | La encuesta de autoidentificación es un breve cuestionario presentado en la página de inicio de la interfaz de usuario de Adobe Experience Platform. Utilice la encuesta de autoidentificación para crear su perfil personal Experience Platform y recibir directrices adaptadas según sus selecciones. Para obtener más información, lea la [información general sobre la encuesta de autoidentificación](../../landing/self-identification.md). |

Para obtener más información, consulte [!DNL Real-Time CDP], consulte la [[!DNL Real-Time CDP] información general](../../rtcdp/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Caducidad de datos de perfil seudónimos | Ya está disponible la caducidad de los datos del perfil seudónimos. Esta versión eliminará continuamente perfiles seudónimos antiguos de la instancia de Experience Platform una vez que se haya activado. Para obtener más información sobre esta función y los perfiles seudónimos, lea la [Guía de caducidad de datos del perfil seudónimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Mapa de pertenencia a segmentos | Como seguimiento al anuncio anterior en febrero, el 15 de mayo de 2023, la `Existing` se eliminará del mapa de pertenencia a segmentos para eliminar la redundancia en el ciclo de vida de pertenencia a segmentos. Después de este cambio, los perfiles cualificados en un segmento se representarán como `Realized` y los perfiles no calificados se seguirán representando como `Exited`.<br/><br/> Este cambio podría afectarle si está utilizando [destinos empresariales](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) y pueden tener procesos descendentes automatizados en su lugar según la variable `Existing` estado. Si este es el caso, revise sus integraciones de flujo descendente. Si le interesa identificar perfiles recién calificados más allá de un cierto tiempo, considere la posibilidad de usar una combinación de `Realized` y `lastQualificationTime` en el mapa de pertenencia a segmentos. Para obtener más información, póngase en contacto con su representante del Adobe. |

{style="table-layout:auto"}

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad de API para filtrar datos de nivel de fila para el origen de Salesforce CRM. | Utilice operadores lógicos y de comparación para filtrar los datos de nivel de fila para el origen de Salesforce CRM. Lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md) para obtener más información. |
| Disponibilidad beta de Shopify Streaming | La variable [Origen de flujo de Shopify](../../sources/connectors/ecommerce/shopify-streaming.md) ya está disponible en versión beta. Utilice la fuente de Shopify Streaming para transmitir los datos de su cuenta de socios de Shopify al Experience Platform. |
| Disponibilidad general de OneTrust Integration | La variable [Origen de integración de OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) es ahora GA. Utilice la fuente de integración de OneTrust para llevar los datos de consentimiento y preferencias de su cuenta de integración de OneTrust al Experience Platform. |
| Disponibilidad general de Oracle Service Cloud | La variable [Origen de nube de servicio de oracle](../../sources/connectors/customer-success/oracle-service-cloud.md) es ahora GA. Utilice el origen de nube de servicio de Oracle para llevar los datos de nube de servicio de Oracle al Experience Platform. |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).