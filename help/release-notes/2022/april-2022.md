---
title: Notas de la versión de Adobe Experience Platform, abril de 2022
description: Notas de la versión de abril de 2022 para Adobe Experience Platform.
source-git-commit: d09eb2e71a5ebce31aeaf8560c20f0c8595f5d19
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 27 de abril de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Flujos de datos](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Real-time Customer Data Platform edición B2B](#B2B)
- [Fuentes](#sources)

## Flujos de datos {#dataflows}

En Platform, los datos se incorporan de muchas fuentes diferentes, se analizan dentro del sistema y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia con flujos de datos.

Los flujos de datos son una representación de trabajos que mueven datos a través de Platform. Estos flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, donde el servicio de identidad y el perfil del cliente en tiempo real los utilizan antes de activarse finalmente en los destinos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Panel de segmentos | Ahora puede utilizar el panel de monitorización para monitorizar los flujos de datos de los segmentos. Para obtener más información, consulte la guía de [monitorización de segmentos en la interfaz de usuario](../../dataflows/ui/monitor-segments.md) |

Para obtener información más general sobre flujos de datos, consulte la [información general sobre flujos de datos](../../dataflows/home.md). Para obtener más información sobre la segmentación, consulte [información general sobre segmentación](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con orígenes Adobe Analytics | El origen de Adobe Analytics ahora admite las funciones de preparación de datos, que le permiten asignar los datos del grupo de informes de Analytics a un esquema XDM de destino al crear un flujo de datos. Consulte el tutorial en [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad con la importación de reglas de asignación existentes | Ahora puede importar reglas de asignación de un flujo de datos existente para acelerar las configuraciones del flujo de datos y limitar los errores. Consulte el tutorial en [importación de reglas de asignación existentes](../../data-prep/ui/mapping.md) para obtener más información. |

Para obtener más información, consulte [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Adición o eliminación de campos estándar individuales para un esquema | La interfaz de usuario del Editor de esquemas ahora le permite añadir partes de grupos de campos estándar a sus esquemas, lo que proporciona más flexibilidad para los campos que elija incluir sin necesidad de crear recursos personalizados desde cero.<br><br>Ahora también puede definir campos personalizados específicos directamente dentro de la estructura de esquema y asignarlos a un grupo de campos personalizados nuevo o existente sin necesidad de crear o editar el grupo de campos de antemano.<br><br>Consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../xdm/ui/resources/schemas.md) para obtener más información sobre estos nuevos flujos de trabajo. |

{style=&quot;table-layout:auto&quot;}

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Solicitud de operación de higiene de datos]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Captura los detalles de una solicitud de limpieza de datos para eliminar o modificar registros en un conjunto de datos o simulador de pruebas especificado. |
| Descriptor | [[!UICONTROL Descriptor de granularidad de series temporales]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica la granularidad de los datos de resumen y series temporales. Cuando se aplica a un esquema, el esquema `timestamp` es la primera marca de tiempo de un periodo de esta granularidad. |
| Clase | [[!UICONTROL Métricas de resumen de XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Proporciona métricas resumidas previamente con dimensiones de agrupación, como los resultados de un SQL SELECT con un GROUP BY. |
| Grupo de campos | [[!UICONTROL Mapa de resultados de evaluación de políticas de consentimiento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura el resultado de la evaluación de la directiva de consentimiento para un individuo. |
| Grupo de campos | [[!UICONTROL Búsqueda del sitio]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura la información relacionada con la búsqueda del sitio, como la consulta de búsqueda, el filtrado y el pedido. |
| Grupo de campos | [[!UICONTROL Combinar posibles clientes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Captura los detalles de un evento en el que se combinan dos o más posibles clientes. |
| Grupo de campos | [[!UICONTROL Correo electrónico enviado]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Captura los detalles de un evento en el que se envía un correo electrónico a un destinatario. |
| Grupo de campos | [[!UICONTROL Definición de campos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Captura valores calculados mediante el proceso de vinculación de identidad para un evento. |
| Grupo de campos | [[!UICONTROL Detalle del destinatario secundario para auditoría]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Grupo de campos de Adobe Journey Optimizer que captura un detalle de destinatario secundario para una auditoría. |
| Grupo de campos | [[!UICONTROL Detalles de relación de persona de cuenta comercial XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalles relacionados con una relación entre cuenta y persona. |
| Grupo de campos | [[!UICONTROL Detalles de la persona de la cuenta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalles relacionados con una relación entre cuenta y persona. |
| Tipo de datos | [[!UICONTROL Carro de compras]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Captura información sobre un carro de compras de comercio electrónico. |
| Tipo de datos | [[!UICONTROL Envío]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Captura la información de envío de uno o más productos. |
| Tipo de datos | [[!UICONTROL Búsqueda del sitio]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura información sobre la actividad de búsqueda de sitios. |
| Extensión (Workfront) | [[!UICONTROL Atributos de tarea operativa]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captura detalles relacionados con una tarea operativa. |
| Extensión (Workfront) | [[!UICONTROL Atributos del Portfolio de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Captura detalles relacionados con un portafolio de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Atributos del programa de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Captura detalles relacionados con un programa de trabajo. |
| Extensión (Workfront) | [[!UICONTROL Atributos del proyecto de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Captura detalles relacionados con un proyecto de trabajo. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Destinos ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nuevos valores de enumeración para `destinationCategory`. |
| Descriptor | [[!UICONTROL Descriptor de nombres descriptivos]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Se agregó compatibilidad para eliminar los valores sugeridos (`meta:enum`) que no son necesarios en los campos estándar. |
| Grupo de campos | [[!UICONTROL Proceso de inicio de sesión del usuario]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` se ha añadido. |
| Tipo de datos | [[!UICONTROL Comercio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Se han agregado varios campos relacionados con el carro de compras. |
| Tipo de datos | [[!UICONTROL Elemento de lista de productos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Se han añadido nuevos campos para las opciones seleccionadas y la cantidad de descuento. |
| Extensión (servicios inteligentes) | [[!UICONTROL Optimización del tiempo de envío de JourneyAI de servicios inteligentes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimizar el formato de almacenamiento para puntuaciones de tiempo de envío. |
| Extensión (Workfront) | [[!UICONTROL Evento de cambio de Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Varios campos se han sustituido por un `workfront:customData` para campos de formulario personalizados. |
| Extensión (Workfront) | [[!UICONTROL Atributos de tarea de trabajo]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Se han añadido varios campos. |
| Extensión (Workfront) | [[!UICONTROL Objeto Work]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nuevos campos para el tipo de objeto principal y campos de formulario personalizados. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

### Real-time Customer Data Platform edición B2B {#B2B}

El CDP B2B Edition en tiempo real, que se basa en Real-time Customer Data Platform (CDP en tiempo real), está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con `isDeleted` funcionalidad | Todo [!DNL Marketo] conjuntos de datos excepto `Activities` ahora admita el `isDeleted` asignación. La nueva asignación se agrega automáticamente a los flujos de datos B2B existentes. Puede usar la variable `isDeleted` asignación para filtrar los registros que se han eliminado para que sus datos en la [!DNL Data Lake] es coherente con los datos de origen. Consulte la [[!DNL Marketo] guía de campos de asignación](../../sources/connectors/adobe-applications/mapping/marketo.md) para obtener más información sobre `isDeleted`. |

Para obtener más información sobre Real-time Customer Data Platform B2B Edition, consulte la [Información general de B2B](../../rtcdp/b2b-overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con [!DNL OneTrust Integration] | Ahora puede usar la variable [!DNL OneTrust Integration] fuente para introducir datos de consentimiento y preferencias de su [!DNL OneTrust] a Platform. Consulte la documentación sobre [crear un [!DNL OneTrust Integration] conexión de origen](../../sources/connectors/consent-and-preferences/onetrust.md) para obtener más información. |
| Compatibilidad con [!DNL Square] | Ahora puede usar la variable [!DNL Square] fuente para introducir datos de pagos de su [!DNL Square] a Platform. |
| Compatibilidad con la eliminación de flujos de datos de Atributos del cliente | Ahora puede eliminar flujos de datos creados con el conector de origen de Atributos del cliente. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
