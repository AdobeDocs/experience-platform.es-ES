---
title: Notas de la versión de Adobe Experience Platform, enero de 2023
description: Las notas de la versión de enero de 2023 de Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: ht
source-wordcount: '2414'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de enero de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Recopilación de datos](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Servicios de inteligencia artificial y aprendizaje automático {#ai-ml}

Los servicios de inteligencia artificial y aprendizaje automático permiten a los analistas y profesionales de marketing aprovechar el poder de la IA/ML en casos prácticos de experiencias del cliente. Esto permite a los analistas de marketing formular predicciones, sin necesidad de tener conocimientos de ciencia de datos, específicas para las necesidades de una empresa mediante configuraciones empresariales.

### Inteligencia artificial aplicada a la atribución

La inteligencia artificial aplicada a la atribución se utiliza para atribuir créditos a puntos de contacto que llevan a eventos de conversión. Los especialistas en marketing pueden utilizarla para cuantificar el impacto de cada punto de contacto de marketing individual en los recorridos del cliente.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Preparación para la HIPAA | Los clientes de Healthcare Shield ahora pueden recibir, utilizar, mantener o transmitir información médica protegida en la inteligencia artificial aplicada a la atribución y otras aplicaciones basadas en Experience Platform. Healthcare Shield es para clientes de asistencia sanitaria que sean una entidad cubierta o un socio comercial solamente en virtud de la normativa HIPAA. Para obtener más información, lea la documentación sobre la [HIPAA y productos y servicios de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Editar columnas de conjuntos de datos de puntuación adicionales | Ahora puede añadir o quitar columnas de conjuntos de datos de puntuación adicionales (columnas de informes) al editar modelos existentes. Esto amplía la flexibilidad de las puntuaciones de atribución para proporcionarle perspectivas a dimensiones adicionales después de que ya se haya creado un modelo. Consulte la [Guía de la IU de atribución](../../intelligent-services/attribution-ai/user-guide.md) para obtener más información. |

{style="table-layout:auto"}

Consulte la información general sobre los [Servicios AI/ML](../../intelligent-services/attribution-ai/overview.md) para obtener más información.

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente para Real-time Customer Data Platform se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y conversión de perfiles individuales a escala. Esto se obtiene sin necesidad de transformar las necesidades comerciales en un problema de aprendizaje automático, elegir un algoritmo, entrenar o implementar.

**Funciones actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Preparación para la HIPAA | Los clientes de Healthcare Shield ahora pueden recibir, utilizar, mantener o transmitir información médica protegida en la inteligencia artificial aplicada al cliente para Real-time Customer Data Platform y otras aplicaciones basadas en Experience Platform. Healthcare Shield es para clientes de asistencia sanitaria que sean una entidad cubierta o un socio comercial solamente en virtud de la normativa HIPAA. Para obtener más información, consulte la documentación sobre [HIPAA y productos y servicios de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Consulte la información general sobre los [Servicios AI/ML](../../intelligent-services/customer-ai/overview.md) para obtener más información.

## Assurance {#assurance}

Adobe Assurance le permite inspeccionar, probar, simular y validar cómo recopila datos o presenta las experiencias en sus aplicaciones móviles.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Editor de validación | Se han añadido mejoras al editor de validación. Estas mejoras incluyen columnas de validación, nuevas herramientas de creación de código y vistas mejoradas. |

{style="table-layout:auto"}

Para obtener más información sobre Assurance, lea la [Documentación de Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nueva pantalla de inicio | La página de inicio de la IU de recopilación de datos se ha actualizado para incluir información útil de incorporación y vínculos para optimizar la productividad. Esto incluye lo siguiente:<ol><li>Documentación y flujos de trabajo recomendados para empezar</li><li>Propiedades, reglas y elementos de datos recientes</li><li>Extensiones populares</li><li>Nuevas actualizaciones de la extensión con una función de instalación rápida</li></ol> |
| Envío de datos a [!DNL Google Ads] mediante el reenvío de eventos | Ahora puede utilizar la [[!DNL Google Ads Enhanced Conversions] extensión de API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para el reenvío de eventos, combinada con [Secretos de Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar de forma segura datos del lado del servidor a [!DNL Google Ads] en tiempo real. |

{style="table-layout:auto"}

## Destinos (actualizado el 2 de febrero) {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [(Beta) Conexión de audiencias de Adobe Experience Cloud](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilice la conexión [!UICONTROL Audiencias de Adobe Experience Cloud (Beta)] para compartir segmentos desde Experience Platform a varias soluciones de Experience Platform, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo. |
| [Conexión del perfil Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilice el [!DNL Pega Profile Connector] en Adobe Experience Platform para crear una conexión saliente activa con su Almacenamiento de S3 de [!DNL Amazon] para exportar periódicamente datos de perfil a archivos CSV desde Adobe Experience Platform en sus propios contenedores de S3. En [!DNL Pega Customer Decision Hub], puede programar trabajos de datos para importar estos datos de perfil desde el almacenamiento de S3 y actualizar el perfil [!DNL Pega Customer Decision Hub]. |
| [(Beta) La conexión de la UE de CRM de la Oficina de Comercio](../../destinations/catalog/advertising/tradedesk-emails.md) | Con el lanzamiento de EUID (European Unified ID), ahora ve dos destinos [!DNL The Trade Desk - CRM] en el [catálogo de destinos](/help/destinations/catalog/overview.md). <ul><li> Si obtiene datos en la UE, utilice el destino **[!DNL The Trade Desk - CRM (EU)]**.</li><li> Si obtiene datos en las regiones APAC o NAMER, utilice el destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**. </li></ul> |

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Funcionalidad | Descripción |
| ----------- | ----------- |
| Mejora de la política de consentimiento de medios de pago para integraciones con destinos de streaming | Una [mejora de la aplicación de políticas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) en [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations) para casos de uso de activación de medios de pago. Cuando los perfiles ya no están cualificados para una directiva de consentimiento, Experience Platform ahora comunica de forma proactiva su salida de directiva a los destinos de streaming. <br> <b>Nota</b>: Esta funcionalidad solo está disponible para los clientes de **[!UICONTROL Privacy and Security Shield]** y los de **[!UICONTROL Healthcare Shield]**. |
| Nuevas opciones de delimitador para los conectores de destino de almacenamiento en la nube Beta | Tres nuevas opciones de delimitador (dos puntos `:`, coma, punto y coma `;`) ya están disponibles para los nuevos destinos de almacenamiento en la nube beta: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrizaje de datos](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Almacenamiento en la nube de Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Lea más información sobre las [opciones de formato de archivo](/help/destinations/ui/batch-destinations-file-formatting-options.md) para destinos basados en archivos. |
| Nuevo parámetro opcional disponible en configuraciones de [campos de datos del cliente](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) en [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: utilice este parámetro cuando necesite crear un campo de datos de cliente cuyo valor debe ser único en todos los flujos de datos de destino configurados por la organización de un usuario. <br> Por ejemplo, el campo **[!UICONTROL Alias de integración]** en el destino [[!UICONTROL Personalización]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) debe ser único, lo que significa que dos flujos de datos independientes a este destino no pueden tener el mismo valor para este campo. |

**Correcciones y mejoras** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Corrección o mejora</b></td>
        <td><b>Descripción</b></td>
    </tr>
    <tr>
        <td>Comportamiento de exportación actualizado para destinos basados en archivos (PLAT-123316)</td>
        <td>Se ha corregido un problema en el comportamiento de <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=es#mandatory-attributes">atributos obligatorios</a> al exportar archivos de datos a destinos por lotes. <br> Anteriormente, se comprobaba que todos los registros de los archivos de salida contenían lo siguiente: <ol><li>Un valor no nulo de la columna <code>mandatoryField</code> y</li><li>Un valor no nulo en al menos uno de los demás campos no obligatorios.</li></ol> Se ha eliminado la segunda condición. Como resultado, es posible que vea más filas de salida en los archivos de datos exportados, como se muestra en el ejemplo siguiente:<br> <b> Comportamiento de muestra antes de la versión de enero de 2023 </b> <br> Campo obligatorio: <code>emailAddress</code> <br> <b>Datos de entrada para activar</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Salida de activación</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Comportamiento de muestra después de la versión de enero de 2023 </b> <br> <b>Salida de activación</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validación de la IU y la API para asignaciones requeridas y asignaciones duplicadas (PLAT-123316)</td>
        <td>La validación ahora se aplica de la siguiente manera en la IU y la API al <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=es#mapping">asignar campos</a> en el flujo de trabajo activar destinos:<ul><li><b>Asignaciones requeridas</b>: si el desarrollador de destinos ha configurado el destino con las asignaciones necesarias (por ejemplo, el destino <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=es">Google Ad Manager 360</a>), el usuario debe añadir estas asignaciones necesarias al activar datos en el destino. </li><li><b>Duplicar asignaciones</b>: en el paso de asignación del flujo de trabajo de activación, puede añadir valores duplicados en los campos de origen, pero no en los campos de destino. Consulte la tabla siguiente para ver un ejemplo de combinaciones de asignación permitidas y prohibidas. <br><table><thead><tr><th>Permitido/prohibido</th><th>Campo de origen</th><th>Campo de destino</th></tr></thead><tbody><tr><td>Permitido</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>correo electrónico alias2</li></ul></td></tr><tr><td>Prohibido</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Mejoras en el nombre para mostrar del árbol de esquemas | Anteriormente, los nombres de campo se mostraban en la IU, pero ahora, los nombres para mostrar de los campos de esquema en el lienzo de esquema son más fáciles de leer. |

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Conversión]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Una clase para seguir los datos de conversión como las conversiones de divisa. |
| Grupo de campos | [[!UICONTROL Detalles de la tasa de conversión de divisa]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un grupo de campos para la clase de [!UICONTROL Conversión], capturando detalles adicionales relacionados con la conversión de divisa. |
| Grupo de campos | [[!UICONTROL Asignación de resultados de evaluación de directivas de consentimiento con metadatos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Registra detalles del resultado de la evaluación de varias políticas de consentimiento, incluida la información de metadatos sobre entradas y salidas de políticas de consentimiento. |

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Tipo de datos | [[!UICONTROL Información de detalles publicitarios]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | El campo `ID` se cambió de nombre a `name`, y el campo `name` anterior ahora es `friendlyName`. |
| Tipo de datos | [[!UICONTROL Detalles de la propuesta de decisión]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Se ha añadido el campo `selectionStrategy` que captura los detalles de la estrategia de selección. |
| Grupo de campos | [[!UICONTROL Evento de experiencia: interacciones de propuesta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | El grupo de campos ahora es compatible con la clase [!UICONTROL Evento de paso de recorrido]. |
| Tipo de datos | [[!UICONTROL Información de detalles del error]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | El campo `ID` se ha cambiado de nombre a `name`. |
| Tipo de datos | [[!UICONTROL Información de medios]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Se ha revertido un cambio en el patrón a la propiedad del segmento de vídeo. |
| Tipo de datos | [[!UICONTROL Información de detalles de datos de calidad de la experiencia (QoE)]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Se ha eliminado el campo `droppedFrameCount`. |
| Tipo de datos | [[!UICONTROL Información de detalles de sesión]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Se ha cambiado el nombre del campo `isAuthorized` a `authorized` y se ha actualizado su `type` a una cadena cuando anteriormente era un booleano. |
| Tipo de datos | [[!UICONTROL Envío]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Se han añadido varios campos nuevos: `shipDate`, `trackingNumber` y `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidad de AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Se han añadido varios campos nuevos: `journeyNodeID`, `journeyNodeName` y `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiencia del consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | El grupo de campos ahora también es compatible con la clase [!UICONTROL Métricas de resumen]. |
| Grupo de campos | [[!UICONTROL Activadores de producto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | El campo `productTriggers` ahora está anidado en el objeto `weather`. |
| Grupo de campos | [[!UICONTROL Activadores relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | El campo `relativeTriggers` ahora está anidado en el objeto `weather`. |
| Grupo de campos | [[!UICONTROL Activadores graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | El campo `severeTriggers` ahora está anidado en el objeto `weather`. |
| Grupo de campos | [[!UICONTROL Activadores meteorológicos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | El campo `weatherTriggers` ahora está anidado en el objeto `weather`. |
| Grupo de campos | [[!UICONTROL Cuentas empresariales relacionadas de XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | El grupo de campos ahora es estable. |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

**Funciones próximas a quedar en desuso** {#deprecation}

Para eliminar la redundancia en el ciclo vital del abono a segmentos, el estado `Existing` quedó en desuso en el [mapa de abono a segmentos](../../xdm/field-groups/profile/segmentation.md) a finales de marzo de 2023. El anuncio de seguimiento incluirá la fecha exacta de cuando quede en desuso.

Tras la retirada, los perfiles calificados en un segmento se representarán como `Realized` y los perfiles no calificados seguirán representándose como `Exited`. Esto igualará los destinos basados en archivos con los estados de segmentos `Active` y `Expired`.

Este cambio podría afectarle si está utilizando [destinos empresariales](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, API HTTP) y ha automatizado los procesos descendentes en su lugar, en función del estado `Existing`. Revise sus integraciones posteriores si este es el caso para usted. Si está interesado en identificar perfiles recién calificados más allá de un cierto tiempo, considere utilizar una combinación de los estados `Realized` y `lastQualificationTime` en el mapa de abono a segmentos. Para obtener más información, póngase en contacto con su representante de Adobe.

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de perfil, comience por leer la [Información general sobre el perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Importación por lotes de los valores en el Generador de segmentos | El generador de segmentos ahora admite la importación de varios valores, ya sea cargando un archivo CSV o TSV o insertando manualmente valores separados por comas. Encontrará más información en la [Guía del generador de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Caducidad del abono a audiencia externa | De forma predeterminada, los abonos a audiencias externas se conservan durante 30 días. Para conservarlos durante más tiempo, utilice el campo `validUntil` durante la ingesta de datos de audiencia. |
| Caducidad del abono al segmento generado por Platform | Cualquier abono a segmento que esté en el estado `Exited` durante más de 30 días, según el campo `lastQualificationTime` estará sujeto a eliminación. |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Información general sobre segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Permitir al usuario acceso a subcarpetas de orígenes de almacenamiento en la nube | Ahora puede definir el acceso a una subcarpeta específica de su origen de almacenamiento en la nube al crear una cuenta nueva. Una vez creada, los usuarios solo podrán acceder a los datos de la subcarpeta permitida. Esta función está disponible para las siguientes fuentes de almacenamiento en la nube: [Almacenamiento de Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Almacenamiento de Google Cloud](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) y [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidad de versión Beta de [!DNL SugarCRM] | Las fuentes de [!DNL SugarCRM] ya están disponibles en la versión Beta. Utilice las fuentes de [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] para obtener datos de su cuenta de [!DNL SugarCRM] para Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |
