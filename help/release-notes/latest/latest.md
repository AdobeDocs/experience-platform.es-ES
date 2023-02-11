---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de enero de 2023 para Adobe Experience Platform.
source-git-commit: 6388c72aa0be8f5f91efaaa6a0edd22f3eb99de8
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de enero de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Recopilación de datos](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Servicios de inteligencia artificial/aprendizaje automático {#ai-ml}

Los servicios de inteligencia artificial y aprendizaje automático permiten a los analistas y profesionales de marketing aprovechar el poder de la IA/ML en casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren predicciones, sin necesidad de conocimientos de ciencia de datos, específicas de las necesidades de una empresa mediante configuraciones de nivel de negocio.

### Inteligencia artificial aplicada a la atribución

Attribution AI se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para ayudar a cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Preparación para la HIPAA | Los clientes del Escudo Sanitario ahora pueden recibir, utilizar, mantener o transmitir información sanitaria protegida en Attribution AI y otras aplicaciones basadas en Experience Platform. Healthcare Shield es para clientes sanitarios que son una entidad cubierta o un asociado comercial bajo HIPAA. Para obtener más información, consulte la documentación de [Servicios y productos de HIPAA y Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Editar columnas de conjuntos de datos de puntuación adicionales | Ahora puede agregar o eliminar columnas de conjuntos de datos de puntuación adicionales (columnas de informes) al editar modelos existentes. Esto amplía la flexibilidad de las puntuaciones de atribución para proporcionarle información sobre dimensiones adicionales después de crear un modelo. Consulte la [Guía de Attribution UI](../../intelligent-services/attribution-ai/user-guide.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Consulte la [Servicios AI/ML](../../intelligent-services/attribution-ai/overview.md) información general para obtener más información.

### Customer AI

La Customer AI para Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la pérdida y la conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Preparación para la HIPAA | Los clientes de Healthcare Shield ahora pueden recibir, utilizar, mantener o transmitir información sanitaria protegida en Customer AI para Real-time Customer Data Platform y otras aplicaciones basadas en Experience Platform. Healthcare Shield es para clientes sanitarios que son una entidad cubierta o un asociado comercial bajo HIPAA. Para obtener más información, consulte la documentación de [Servicios y productos de HIPAA y Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style=&quot;table-layout:auto&quot;}

Consulte la [Servicios AI/ML](../../intelligent-services/customer-ai/overview.md) información general para obtener más información.

## Assurance {#assurance}

Adobe Assurance le permite inspeccionar, comprobar, simular y validar cómo recopila datos o sirve experiencias en su aplicación móvil.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Editor de validación | Se han añadido nuevas mejoras al editor de validación. Estas mejoras incluyen columnas de validación, nuevas herramientas de creación de código y vistas mejoradas. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre Assurance, lea la [Documentación de Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nueva pantalla de inicio | La página de inicio de la interfaz de usuario de recopilación de datos se ha actualizado para incluir información de integración y vínculos útiles para optimizar la productividad. Esto incluye:<ol><li>Documentación y flujos de trabajo recomendados para empezar</li><li>Propiedades, reglas y elementos de datos recientes</li><li>Extensiones populares</li><li>Nuevas actualizaciones de extensión con una función de instalación rápida</li></ol> |
| Enviar datos a [!DNL Google Ads] uso del reenvío de eventos | Ahora puede usar la variable [[!DNL Google Ads Enhanced Conversions] Extensión de API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para el reenvío de eventos, combinado con [Secretos de Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar de forma segura datos del lado del servidor a [!DNL Google Ads] en tiempo real. |

{style=&quot;table-layout:auto&quot;}

## Destinos (actualizado el 2 de febrero) {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [(Beta) Conexión de Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilice la variable [!UICONTROL (Beta) Audiencias de Adobe Experience Cloud] conexión para compartir segmentos desde Experience Platform a varias soluciones de Experience Platform, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo. |
| [Pega Conexión de perfil](../../destinations/catalog/personalization/pega-profile.md) | Utilice la variable [!DNL Pega Profile Connector] en Adobe Experience Platform para crear una conexión de salida activa con su [!DNL Amazon] Almacenamiento S3 para exportar periódicamente datos de perfil a archivos CSV desde Adobe Experience Platform a sus propios bloques S3. En [!DNL Pega Customer Decision Hub], puede programar trabajos de datos para importar estos datos de perfil desde el almacenamiento S3 para actualizar el [!DNL Pega Customer Decision Hub] perfil. |
| [(Beta) Conexión de la Oficina de Comercio con CRM UE](../../destinations/catalog/advertising/tradedesk-emails.md) | Con el lanzamiento de EUID (European Unified ID), ahora verá dos [!DNL The Trade Desk - CRM] destinos en la variable [catálogo de destinos](/help/destinations/catalog/overview.md). <ul><li> Si obtiene datos en la UE, utilice el **[!DNL The Trade Desk - CRM (EU)]** destino.</li><li> Si obtiene datos en las regiones de APAC o NAMER, utilice la variable **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destino. </li></ul> |

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Mejora de la política de consentimiento de medios pagados para integraciones con destinos de flujo continuo | Un [mejora de la aplicación de políticas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) en [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations) para casos de uso de activación de medios de pago. Cuando los perfiles ya no están cualificados para una directiva de consentimiento, el Experience Platform ahora comunica de forma proactiva su salida de directiva a los destinos de flujo continuo. <br> <b>Nota</b>: Esta funcionalidad solo está disponible para los clientes de **[!UICONTROL Protección de seguridad y privacidad]** y los de **[!UICONTROL Escudo sanitario]**. |
| Nuevas opciones de delimitador para conectores de destino de almacenamiento de nube beta | Tres nuevas opciones de delimitador (dos puntos) `:`, Tubería, Punto y coma `;`) ya están disponibles para los nuevos destinos de almacenamiento de la nube beta: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Almacenamiento de Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrizaje de datos](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Almacenamiento en la nube de Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Obtenga más información sobre los [opciones de formato de archivo](/help/destinations/ui/batch-destinations-file-formatting-options.md) para destinos basados en archivos. |
| Nuevo parámetro opcional disponible en [campos de datos del cliente](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configuraciones en [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Utilice este parámetro cuando necesite crear un campo de datos de cliente cuyo valor debe ser único en todos los flujos de datos de destino configurados por la organización de un usuario. <br> Por ejemplo, la variable **[!UICONTROL Alias de integración]** en el campo [[!UICONTROL Personalización personalizada]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) el destino debe ser único, lo que significa que dos flujos de datos independientes a este destino no pueden tener el mismo valor para este campo. |

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Corrección o mejora</b></td>
        <td><b>Descripción</b></td>
    </tr>
    <tr>
        <td>Se ha actualizado el comportamiento de exportación a destinos basados en archivos (PLAT-123316)</td>
        <td>Se ha corregido un problema en el comportamiento de <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">atributos obligatorios</a> al exportar archivos de datos a destinos por lotes. <br> Anteriormente, todos los registros de los archivos de salida se verificaban para contener ambos: <ol><li>Un valor no nulo de la variable <code>mandatoryField</code> y</li><li>Un valor no nulo en al menos uno de los demás campos no obligatorios.</li></ol> Se ha eliminado la segunda condición. Como resultado, es posible que vea más filas de salida en los archivos de datos exportados, como se muestra en el ejemplo siguiente:<br> <b> Comportamiento de muestra antes de la versión de enero de 2023 </b> <br> Campo obligatorio: <code>emailAddress</code> <br> <b>Entrada de datos para activar</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Salida de activación</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Comportamiento de muestra después de la versión de enero de 2023 </b> <br> <b>Salida de activación</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validación de la interfaz de usuario y la API para asignaciones obligatorias y asignaciones duplicadas (PLAT-123316)</td>
        <td>La validación ahora se aplica de la siguiente manera en la interfaz de usuario y la API al <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">campos de asignación</a> en el flujo de trabajo activar destinos :<ul><li><b>Asignaciones necesarias</b>: Si el desarrollador de destino ha configurado el destino con las asignaciones necesarias (por ejemplo, la variable <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> ), el usuario debe agregar estas asignaciones necesarias al activar los datos en el destino. </li><li><b>Duplicar asignaciones</b>: En el paso de asignación del flujo de trabajo de activación, puede añadir valores duplicados en los campos de origen, pero no en los campos de destino. Consulte la siguiente tabla para ver un ejemplo de combinaciones de asignación permitidas y prohibidas. <br><table><thead><tr><th>Permitido/prohibido</th><th>Campo de origen</th><th>Campo de destino</th></tr></thead><tbody><tr><td>Permitido</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>alias de correo electrónico 2</li></ul></td></tr><tr><td>Prohibido</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en el nombre para mostrar del árbol de esquemas | Anteriormente, los nombres de campo se mostraban en la interfaz de usuario, pero ahora, los nombres para mostrar de los campos de esquema en el lienzo del esquema son más fáciles de leer. |

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Conversión]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Una clase para rastrear datos de conversión como conversiones de moneda. |
| Grupo de campos | [[!UICONTROL Detalles de tasa de conversión de moneda]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un grupo de campos para la variable [!UICONTROL Conversión] captura de detalles adicionales relacionados con la conversión de moneda. |
| Grupo de campos | [[!UICONTROL Asignación de resultados de evaluación de políticas de consentimiento con metadatos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Captura detalles para el resultado de evaluación de varias políticas de consentimiento, incluida la información de metadatos sobre las entradas de políticas de consentimiento y la existencia de . |

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información sobre los detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | La variable `ID` se ha cambiado el nombre del campo a `name`y el anterior `name` el campo ahora `friendlyName`. |
| Tipo de datos | [[!UICONTROL Detalles de la propuesta de decisión]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Se ha añadido un `selectionStrategy` que captura los detalles de una estrategia de selección. |
| Grupo de campos | [[!UICONTROL Evento de experiencia: interacciones de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | El grupo de campos ahora es compatible con el [!UICONTROL Evento de paso de recorrido] Clase . |
| Tipo de datos | [[!UICONTROL Información de detalles de error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | La variable `ID` se ha cambiado el nombre del campo a `name`. |
| Tipo de datos | [[!UICONTROL Información multimedia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Se ha revertido un cambio de patrón a la propiedad del segmento de vídeo. |
| Tipo de datos | [[!UICONTROL Información de detalles de la solicitud]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Se ha eliminado el `droppedFrameCount` campo . |
| Tipo de datos | [[!UICONTROL Información detallada de la sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se cambió el nombre de la variable `isAuthorized` campo a `authorized`y actualizó su `type` a una cadena cuando anteriormente era booleana. |
| Tipo de datos | [[!UICONTROL Envío]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Se han añadido varios campos nuevos: `shipDate`, `trackingNumber`y `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidad AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Se han añadido varios campos nuevos: `journeyNodeID`, `journeyNodeName`y `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiencia del consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | El grupo de campos ahora también es compatible con el [!UICONTROL Métricas de resumen] Clase . |
| Grupo de campos | [[!UICONTROL Déclencheur del producto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | La variable `productTriggers` ahora está anidado en un `weather` objeto. |
| Grupo de campos | [[!UICONTROL Déclencheur relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | La variable `relativeTriggers` ahora está anidado en un `weather` objeto. |
| Grupo de campos | [[!UICONTROL Déclencheur graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | La variable `severeTriggers` ahora está anidado en un `weather` objeto. |
| Grupo de campos | [[!UICONTROL Déclencheur meteorológicos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | La variable `weatherTriggers` ahora está anidado en un `weather` objeto. |
| Grupo de campos | [[!UICONTROL Cuentas comerciales relacionadas con XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | El grupo de campos ahora es estable. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de los clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Próxima desaprobación** {#deprecation}

Para eliminar la redundancia en el ciclo vital de la pertenencia a los segmentos, la variable `Existing` se desaprobará del [mapa de pertenencia a segmentos](../../xdm/field-groups/profile/segmentation.md) a finales de marzo de 2023. Un anuncio de seguimiento incluirá la fecha exacta de desaprobación.

Tras el desuso, los perfiles cualificados en un segmento se representarán como `Realized` y los perfiles no calificados se seguirán representando como `Exited`. Esto proporciona paridad con los destinos basados en archivos con `Active` y `Expired` estados de segmentos.

Este cambio podría afectarle si está utilizando [destinos empresariales](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) y tienen en su lugar procesos descendentes automatizados basados en el `Existing` estado. Revise sus integraciones descendentes si este es el caso. Si le interesa identificar perfiles recién calificados más allá de un cierto tiempo, considere la posibilidad de usar una combinación de `Realized` y `lastQualificationTime` en el mapa de pertenencia a segmentos. Para obtener más información, póngase en contacto con su representante del Adobe.

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Importación masiva de valores en el Generador de segmentos | El Generador de segmentos ahora admite la importación de varios valores, ya sea cargando un archivo CSV o TSV o insertando manualmente valores separados por comas. Encontrará más información dentro de la variable [Guía del Generador de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Caducidad de pertenencia a una audiencia externa | De forma predeterminada, las suscripciones a audiencias externas se conservan durante 30 días. Para conservarlos durante más tiempo, utilice el `validUntil` durante la ingesta de datos de audiencia. |
| Caducidad de pertenencia a segmentos generada por la plataforma | Cualquier pertenencia a un segmento que se encuentre en la `Exited` durante más de 30 días, según la variable `lastQualificationTime` estará sujeto a eliminación. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Permitir el acceso del usuario a subcarpetas de orígenes de almacenamiento en la nube | Ahora puede definir el acceso a una subcarpeta específica del origen de almacenamiento en la nube al crear una cuenta nueva. Una vez creados, los usuarios solo podrán acceder a los datos de la subcarpeta permitida. Esta función está disponible para las siguientes fuentes de almacenamiento en la nube: [Almacenamiento de Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Almacenamiento en la nube de Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)y [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidad beta de [!DNL SugarCRM] | [!DNL SugarCRM] los orígenes de ya están disponibles en la versión beta. Utilice la variable [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] fuentes para obtener datos de [!DNL SugarCRM] cuenta al Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |