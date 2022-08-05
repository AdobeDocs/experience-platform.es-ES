---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c4cd691eeae9e27dd7616dc19672dc5d08b8cec7
workflow-type: tm+mt
source-wordcount: '2327'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de julio de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Tableros](#dashboards)
- [Recopilación de datos](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Real-time Customer Data Platform edición B2B](#b2b)
- [Perfil del cliente en tiempo real](#profile)
- [Fuentes](#sources)

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios [!DNL dashboards] a través de la cual puede ver información importante sobre los datos de su organización, tal como se captura durante las instantáneas diarias.

### Tableros de perfiles de cuenta

El tablero Perfiles de la cuenta muestra una instantánea de la información de cuenta unificada de las múltiples fuentes en los canales de marketing y los diversos sistemas que su organización utiliza actualmente para almacenar información de cuentas de clientes.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Total de cuentas por widget de sector | Este widget muestra el número total de cuentas en una única métrica y utiliza un gráfico circular para ilustrar los tamaños proporcionales de los recuentos para las industrias que conforman el número total. |
| Widget de perfiles de cuenta agregados | Esta utilidad utiliza un gráfico de barras con códigos de color para ilustrar el recuento de perfiles agregados a una cuenta durante un período de tiempo determinado y la proporción de diferentes industrias que constituyen estos perfiles añadidos. |

{style=&quot;table-layout:auto&quot;}

Consulte la [Resumen de CDP en tiempo real, B2B Edition](../../rtcdp/b2b-overview.md) para obtener más información sobre las funciones B2B disponibles, o [tutorial completo](../../rtcdp/b2b-tutorial.md) Para obtener más información sobre cómo se crean los perfiles de cuenta como parte del flujo de trabajo B2B.

Para obtener más información sobre los widgets disponibles para visualizar las métricas relacionadas con el perfil de la cuenta, consulte la [documentación de los widgets de perfiles de cuenta](../../dashboards/guides/account-profiles.md#standard-widgets).

### Tableros de perfil

El panel Perfiles muestra una instantánea de los datos de atributo (registro) que su organización tiene en el Experience Platform Almacenamiento de perfiles .

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Widget de audiencias asignadas | Esta utilidad muestra el número total de audiencias asignadas que se pueden activar en el destino seleccionado en la lista desplegable del panel Perfiles . |

Para obtener más información sobre el panel Perfiles, consulte la [Información general sobre los paneles de perfiles](../../dashboards/guides/profiles.md).

### Tableros de destinos

El panel Destinos muestra una instantánea de los destinos que su organización ha habilitado en el Experience Platform.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| utilidad Audiencias | Esta utilidad proporciona el número total de segmentos que están listos para activarse, según la política de combinación elegida aplicada a los datos de perfil. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el panel Destinos, consulte la [información general del panel Destinations](../../dashboards/guides/destinations.md).

## Recopilación de datos {#collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Administración de permisos mediante Adobe Admin Console | El acceso a las funciones de recopilación de datos ahora se administra mediante Adobe Admin Console en la tarjeta de recopilación de datos de Adobe Experience Platform. Consulte la guía de [permisos de recopilación de datos](../../collection/permissions.md) para obtener más información.<br><br>Los permisos para los conjuntos de datos ahora se administran a través del Admin Console en la tarjeta de Adobe Experience Platform, lo que mejora la seguridad con respecto al método anterior de configurar estos permisos manualmente para cada usuario. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información, consulte la [información general sobre recopilación de datos](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations es ahora más inteligente y rápido. Las nuevas comprobaciones de validación reducen considerablemente los errores de asignación más comunes, lo que reduce aún más el tiempo de respuesta al valor. |
| Compatibilidad jerárquica con problemas de transmisión | Ahora puede utilizar funciones `upsert_array_append` y `upsert_array_replace` para actualizar matrices y objetos al transmitir actualizaciones a Perfil. Consulte la [[!DNL Data Prep] guía de funciones de asignación](../../data-prep/functions.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ----------- | ----------- |
| [Exportar archivo ahora (Beta)](../../destinations/ui/export-file-now.md) | Exporte un archivo completo sin interrumpir la programación de exportación actual de un segmento previamente programado. Esta exportación se produce además de exportaciones programadas anteriormente y no cambia la frecuencia de exportación del segmento. <br> La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform. <br> <br>Póngase en contacto con su representante de Adobe para obtener acceso a esta funcionalidad. |

{style=&quot;table-layout:auto&quot;}

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [Marketo V2](../../destinations/catalog/adobe/marketo-engage.md) | La actualización de destino del Marketo Engage le permite agilizar el proceso de creación de listas estáticas con automatización y permitir a los usuarios introducir campos adicionales en sus posibles clientes. Consulte más información sobre las mejoras de Marketo V2 a continuación: <br><ul><li>En el **[!UICONTROL Programar segmento]** paso del flujo de trabajo de activación, en Marketo V1, debe añadir manualmente un **ID de asignación** para exportar datos correctamente a Marketo. Este paso manual ya no es necesario en Marketo V2.</li><li>En el **[!UICONTROL Asignación]** del flujo de trabajo de activación, en Marketo V1, solo se han podido asignar campos XDM a tres campos de destino en Marketo: `firstName`, `lastName`y `companyName`. Con la versión Marketo V2, ahora puede asignar campos XDM a muchos más campos en Marketo. Para obtener más información, lea [atributos admitidos en Marketo V2](../../destinations/catalog/adobe/marketo-engage.md#supported-attributes).  </li></ul> |
| [Centro de decisión de clientes Pega](../../destinations/catalog/personalization/pega.md) | Utilice los atributos de perfil y la información de pertenencia a segmentos de Adobe Experience Platform en Pega Customer decisions Hub como predictores en modelos adaptables y ayude a ofrecer la mejor opción de acción |
| [(API) Marketing Cloud de Salesforce](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) | Este destino permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform en anuncios de Snapchat y utilizarlos para dirigir sus anuncios. |
| [Salesforce CRM](../../destinations/catalog/crm/salesforce.md) | Actualizar la información de contacto en el Marketing Cloud de Salesforce con información de perfil y segmento en el Experience Platform |
| [(Beta) [!DNL Snap Inc.]](../../destinations/catalog/advertising/snap-inc.md) | Este destino permite a los especialistas en marketing importar segmentos de usuario creados en Experience Platform en anuncios de Snapchat y utilizarlos para dirigir sus anuncios. <br><br>Este destino está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios. |
| [(Beta) El [!DNL Trade Desk] - Conexión CRM](../../destinations/catalog/advertising/tradedesk-emails.md) | Uso [!DNL The Trade Desk] Destino de CRM para activar perfiles en su [!DNL Trade Desk] cuenta para la segmentación y supresión de audiencias en función de los datos CRM. <br><br>Este destino está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios. |

{style=&quot;table-layout:auto&quot;}

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Modelo de datos del sector sanitario | Se ha introducido un modelo de datos de atención médica estándar para apoyar cinco casos de uso comunes de la industria relacionados con el aumento de la adquisición digital, la mejora de la inscripción en los programas y la promoción de la información sobre medicamentos. Consulte la descripción general de la [modelo de datos de asistencia sanitaria](../../xdm/schema/industries/healthcare.md) para obtener más información sobre estos casos de uso y los componentes XDM estándar que los admiten.<br><br>Se ha añadido un nuevo filtro de sector a la variable [!UICONTROL Esquemas] IU para ayudarle a examinar los componentes relacionados con el cuidado de la salud al crear esquemas personalizados. |

{style=&quot;table-layout:auto&quot;}

**Nuevos componentes XDM**

>[!WARNING]
>
>Los nuevos componentes XDM enumerados en la siguiente tabla son experimentales y están actualmente en prueba. Se espera que estos componentes se actualicen con cambios de ruptura (si es necesario) antes de que se estabilicen. Planifique sus esfuerzos de desarrollo en consecuencia.

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Tiempo]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Una clase basada en registros que se utiliza para capturar datos meteorológicos. |
| Grupo de campos | [[!UICONTROL Tiempo actual]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] clases, utilizadas para capturar las condiciones climáticas actuales de un código postal. |
| Grupo de campos | [[!UICONTROL Tiempo previsto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] , que se utiliza para capturar las condiciones meteorológicas previstas para un código postal. |
| Grupo de campos | [[!UICONTROL Déclencheur del producto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] , que se utiliza para capturar déclencheur específicos de productos que aprovechan las condiciones meteorológicas conocidas para impulsar el comportamiento de los consumidores. |
| Grupo de campos | [[!UICONTROL Déclencheur relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] , que se utiliza para capturar déclencheur relativos que aprovechan las condiciones meteorológicas conocidas para impulsar el comportamiento de los consumidores. |
| Grupo de campos | [[!UICONTROL Déclencheur graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] , que se utiliza para capturar déclencheur que aprovechan las condiciones climáticas severas conocidas por impulsar el comportamiento de los consumidores. |
| Grupo de campos | [[!UICONTROL Déclencheur meteorológicos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/weather-triggers.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] y [!UICONTROL Tiempo] , que se utiliza para capturar déclencheur generales que aprovechan las condiciones meteorológicas conocidas para impulsar el comportamiento de los consumidores. |
| Grupo de campos | [[!UICONTROL Detalles de interacción de MediaCollection]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-collection.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] que captura detalles sobre una interacción multimedia. |
| Grupo de campos | [[!UICONTROL Detalles de interacción de informes de medios]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-reporting.schema.json) | Un grupo de campos para la variable [!UICONTROL XDM ExperienceEvent] que captura detalles sobre una interacción con los informes de contenidos. |
| Tipo de datos | [[!UICONTROL Información sobre los detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Captura detalles sobre un recurso publicitario. |
| Tipo de datos | [[!UICONTROL Información sobre los detalles de la Pod de publicidad]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json) | Captura detalles sobre un pod publicitario, que es una secuencia de varios anuncios reproducidos uno tras otro dentro de una sola pausa publicitaria. |
| Tipo de datos | [[!UICONTROL Información detallada del capítulo]](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) | Captura detalles sobre un capítulo o segmento de un fragmento de contenido de vídeo. |
| Tipo de datos | [[!UICONTROL Información de detalles de error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Captura detalles sobre un error de reproducción de vídeo. |
| Tipo de datos | [[!UICONTROL Información detallada del evento del reproductor]](https://github.com/adobe/xdm/blob/master/components/datatypes/playereventdetails.schema.json) | Captura detalles relacionados con eventos sobre un reproductor de vídeo, incluida la posición del cursor de reproducción y el ID de sesión. |
| Tipo de datos | [[!UICONTROL Información de datos del estado del reproductor]](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) | Captura detalles relacionados con el estado sobre un reproductor de vídeo. |
| Tipo de datos | [[!UICONTROL Información de detalles de la solicitud]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Captura los detalles de calidad de experiencia (QoE) sobre un evento de reproducción de vídeo. |
| Tipo de datos | [[!UICONTROL Información detallada de la sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Captura los detalles de la sesión sobre un evento de reproducción de vídeo. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Real-time Customer Data Platform edición B2B {#b2b}

El CDP B2B Edition en tiempo real, que se basa en Real-time Customer Data Platform (CDP en tiempo real), está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Confrontación de posibles clientes con cuentas | La coincidencia de posibles clientes con cuentas le permite unir perfiles de personas conocidas con perfiles de cuenta. A continuación, puede segmentar y segmentar los datos en un contexto B2B, como cuentas u oportunidades. Los trabajos de ejecución diaria utilizan factores determinísticos y probabilísticos para hacer coincidir los perfiles de persona que no están asociados a ninguna cuenta con una cuenta que coincida mejor. A continuación, puede decidir si desea incluir estas coincidencias en sus definiciones de segmento |

Para obtener más información, consulte el documento sobre [conllevar concordancia de cuentas](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

Para obtener una guía sobre cómo monitorizar el enriquecimiento de perfiles, consulte el documento sobre [supervisión del enriquecimiento de perfiles en la interfaz de usuario](../../dataflows/ui/b2b/monitor-profile-enrichment.md).

Para obtener instrucciones sobre cómo configurar la coincidencia de posibles clientes con cuentas, consulte la [Guía de la interfaz de usuario del perfil de la cuenta](../../rtcdp/account/../accounts/account-profile-ui-guide.md?lang=en#configure-lead-to-account-matching).

Para obtener más información sobre CDP B2B Edition en tiempo real, consulte la [Resumen de CDP B2B en tiempo real](../../rtcdp/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Limpieza de atributos perimetrales de perfil huérfanos (versión limitada) | Si su organización tiene acceso a esta función, el servicio de perfil ahora elimina diariamente los atributos perimetrales sobrantes de la región de actividad del usuario para proporcionar una representación más precisa de sus perfiles en su sistema. Esta limpieza se produce después de que se eliminan todos los fragmentos de perfil de un perfil determinado y debe afectar a los perfiles que se combinan desde conjuntos de datos en los que `com_adobe_aep_profile_region_dataset` se marca como verdadero. Esto puede mostrar una caída en la métrica &quot;Audiencia direccionable&quot; en el panel de uso de licencias y mostrar una caída en la métrica &quot;Recuento de perfiles&quot; en el panel de perfiles, ya que estas métricas incluían fragmentos de atributos perimetrales restantes antes de esta versión. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Disponibilidad general del [!DNL Azure Data Explorer] source | Utilice el origen de la Data Explorer de Azure para obtener datos de su [!DNL Azure] instancia a Experience Platform. Consulte la [[!DNL Azure Data Explorer] información general de la fuente](../../sources/connectors/databases/data-explorer.md) para obtener más información. |
| Disponibilidad general [!DNL Generic OData] source | Utilice la variable [!DNL Generic OData] fuente para traer recursos de sistemas compatibles con el protocolo de datos abiertos al Experience Platform. Consulte la [[!DNL Generic OData] información general de la fuente](../../sources/connectors/protocols/odata.md) para obtener más información. |
| Compatibilidad con la detección automática de propiedades de archivos de origen para [!DNL Data Landing Zone] en la interfaz de usuario de Experience Platform | La variable [!DNL Data Landing Zone] el origen ahora admite la detección automática de propiedades de archivo al utilizar la interfaz de usuario del Experience Platform. Consulte la documentación sobre [crear un [!DNL Data Landing Zone] conexión de origen](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
