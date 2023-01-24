---
title: Notas de la versión de Adobe Experience Platform, enero de 2023
description: Notas de la versión de enero de 2023 para Adobe Experience Platform.
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de enero de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente en el lado del cliente y enviarlos a Adobe Experience Platform Edge Network, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Nueva pantalla de inicio | La página de inicio de la interfaz de usuario de recopilación de datos se ha actualizado para incluir información de integración y vínculos útiles para optimizar la productividad. Esto incluye:<ol><li>Documentación y flujos de trabajo recomendados para empezar</li><li>Propiedades, reglas y elementos de datos recientes</li><li>Extensiones populares</li><li>Nuevas actualizaciones de extensión con una función de instalación rápida</li></ol> |
| Enviar datos a [!DNL Google Ads] uso del reenvío de eventos | Ahora puede usar la variable [[!DNL Google Ads Enhanced Conversions] Extensión de API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para el reenvío de eventos, combinado con [Secretos de Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar de forma segura datos del lado del servidor a [!DNL Google Ads] en tiempo real. |

{style=&quot;table-layout:auto&quot;}

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Desactivación de valores sugeridos para campos de cadena | Ahora puede [desactivar valores sugeridos individuales para campos de cadena](../../xdm/ui/fields/enum.md) en el [!UICONTROL Esquemas] espacio de trabajo, incluidos los componentes estándar. Esta función solo está disponible para campos con valores sugeridos y no es compatible para restricciones de enumeración. |

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

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Permitir el acceso del usuario a subcarpetas de orígenes de almacenamiento en la nube | Ahora puede definir el acceso a una subcarpeta específica del origen de almacenamiento en la nube al crear una cuenta nueva. Una vez creados, los usuarios solo podrán acceder a los datos de la subcarpeta permitida. Esta función está disponible para las siguientes fuentes de almacenamiento en la nube: [Almacenamiento de Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Almacenamiento en la nube de Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)y [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidad beta de [!DNL SugarCRM] | [!DNL SugarCRM] los orígenes de ya están disponibles en la versión beta. Utilice la variable [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] fuentes para obtener datos de [!DNL SugarCRM] cuenta al Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |
