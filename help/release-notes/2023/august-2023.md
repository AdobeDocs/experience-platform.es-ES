---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión de agosto de 2023 de Adobe Experience Platform.
source-git-commit: a699f66fd48f463cc69ea0f214f487cce360615e
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 32%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 23 de agosto de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Control de acceso basado en atributos](#abac)
- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Ingesta de datos](#data-ingestion)
- [Preparación de datos](#data-prep)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Real-Time Customer Data Platform {#rtcdp}

El compilado en Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a través del recorrido del cliente.

[!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Guía del caso de uso de renovación de participación inteligente | El [Reparticipación inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) la guía del caso de uso proporciona detalles sobre cómo volver a atraer a los clientes que han abandonado una conversión antes de completarla de una manera inteligente y responsable. Esta guía utiliza los siguientes recorridos de ejemplo para volver a atraer a los clientes: <ul><li>Recorrido de renovación de la participación: Segmentación de clientes que han abandonado la navegación por productos.</li><li>Recorrido de carro de compras abandonado: segmenta a los clientes que han colocado productos en el carro de compras, pero que aún no han completado la compra.</li><li>Recorrido de confirmación de pedido: enfoque en las compras de productos</li></ul> Utilice el vínculo de opciones de comentarios detallado en la parte inferior de la [Guía del caso de uso de renovación de participación inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) para proporcionar comentarios. |
| Perfiles de clientes potenciales | Ejecute marketing de canal superior en Real-Time CDP, con perfiles de clientes potenciales de origen socio e ID de socios para llegar a nuevos clientes y enriquecer los datos de origen: <ul><li>Adquisición y direccionamiento de clientes: aproveche los identificadores sin cookies y la PII con hash de los socios de datos que elija para llegar a nuevos clientes netos y reducir la dependencia de cookies de terceros.</li><li>Marketing por canal completo en un solo sistema: segmentación de autoservicio, depuración de audiencias y activación nativa para clientes potenciales y conocidos en un solo sistema.</li><li>Base de confianza: gobierne los datos y perfiles de los socios con uso de datos patentado, etiquetado, controles de acceso y mucho más para comercializar de forma responsable. Lea las siguientes guías de casos de uso para obtener más información: Las guías de casos de uso de prospección ya están disponibles. Lea las guías de casos de uso de prospección para aprender a atraer y adquirir nuevos clientes a través de casos de uso de prospección:<ul><li>[Prospección](../../rtcdp/partner-data/prospecting.md)</li><li>[Personalización in situ](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Suplemento de perfiles de origen](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Activar audiencias de clientes potenciales](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de Real-Time CDP](../../rtcdp/overview.md).

## Control de acceso basado en atributos {#abac}

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad una mayor flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a funciones de usuario. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Platform específicos de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y otro tipo personalizado de datos en todos los flujos de trabajo y recursos de la plataforma. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Configuración de zona protegida de directiva de permisos | El nuevo [configuración de zona protegida de directivas de permisos](../../access-control/abac/ui/policies.md) Esta función le permite aplicar una directiva de control de acceso basada en atributos en todos los entornos limitados o en un número determinado de ellos, según sus necesidades y requisitos. |

{style="table-layout:auto"}

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general sobre el control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo de control de acceso basado en atributos, lea la [guía completa de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Caso de uso de análisis de consentimiento y seguimiento | Obtenga información sobre cómo crear un tablero de consentimiento para varios casos de uso de marketing para datos de Real-Time CDP con [documento de análisis de consentimiento y seguimiento](../../dashboards/insights-use-cases/consent-analysis.md). Detalla cómo crear una audiencia con los atributos adecuados para sus necesidades comerciales y luego consumir las perspectivas mediante el uso de widgets preconfigurados en la interfaz de usuario de Adobe Experience Platform. También proporciona instrucciones sobre cómo crear su propio widget personalizado con la función de paneles definida por el usuario. El documento cubre las tendencias de consentimiento y los casos de uso de superposición de consentimiento. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Reenvío de eventos y etiquetas | [Etiquetas de Experience Platform (China)](/help/tags/ui/publishing/premium-cdn.md) | La nueva función Etiquetas de Experience Platform (China) mejora la fiabilidad y latencia del sitio web, lo que conduce a tiempos de respuesta más rápidos para los clientes que implementan etiquetas en sitios web en China. Los clientes ahora pueden utilizar el código JavaScript en la biblioteca de etiquetas al implementar sitios web en China. Esta función también se ha agregado al Protocolo de aprovisionamiento unificado (UPP), lo que permite automatizar la implementación de productos tras la compra. |

{style="table-layout:auto"}

Para obtener más información, lea la [información general sobre colecciones de datos](../../tags/home.md).

## Ingesta de datos {#data-ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Puede hacerlo mediante las API por lotes o de streaming, utilizando fuentes creadas por Adobe, socios de integración de datos o la IU de Adobe Experience Platform.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en los flujos de trabajo de ingesta de datos | Ahora se rechazarán las filas de datos que contengan valores mayores que el tipo de datos especificado (por ejemplo, datos largos pasados como un tipo de datos entero) y se presentarán mensajes de error. Anteriormente, estas filas se rechazaban sin previo aviso. |

Para obtener más información, lea la [información general sobre ingesta de datos](../../ingestion/home.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el filtrado de identidades secundarias | Ahora puede utilizar la preparación de datos para filtrar las identidades procedentes de Adobe Analytics, como AAID y AACUSTOMID. Si se filtran, estas identidades no se incorporan en el Perfil del cliente en tiempo real. Los datos sin filtrar se seguirán introduciendo en el lago de datos. |
| Compatibilidad con nuevos `correlationID` campo para Adobe Analytics | El `_experience.decisioning.propositions.scopeDetails.correlationID` El campo ahora está disponible en el esquema del conector de origen de Adobe Analytics. Este campo se utiliza para clasificaciones de A4T y se rellenará a partir de septiembre de 2023. |

{style="table-layout:auto"}

Para obtener más información, lea la [Resumen de preparación de datos](../../data-prep/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Perfil de cliente potencial de XDM]](https://github.com/adobe/xdm/pull/1758/files) | Utilice esta clase para incorporar perfiles de clientes potenciales procedentes de los casos de uso de adquisición de clientes principales de los proveedores de datos. |

Para obtener más información, lea la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en los límites del gráfico de identidad | A finales de septiembre, el gráfico de identidad cambiará a 50 identidades por gráfico y se ingestará la última identidad. Como consecuencia, la identidad más antigua se eliminará en función de la marca de tiempo de ingesta y el tipo de identidad, y los tipos de identidad de cookies se eliminarán primero. Actualmente, los gráficos de identidad tienen un límite de 150 identidades por gráfico y, una vez alcanzado este límite, los gráficos ya no se actualizan. Póngase en contacto con el representante de cuentas para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobes procesará manualmente estas solicitudes. Para obtener más información, lea la [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md). |

Para obtener más información, lea la [Introducción al servicio de identidad](../../identity-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar datos almacenados en [!DNL Experience Platform] que se relaciona con personas (como clientes, clientes potenciales, usuarios u organizaciones) en audiencias. Puede crear audiencias a través de definiciones de segmentos u otras fuentes a partir de sus [!DNL Real-Time Customer Profile] datos. Estas audiencias se configuran de forma centralizada y se mantienen en [!DNL Platform]y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Audiencias de similitud (disponibilidad limitada) | Las audiencias de similitud proporcionan una perspectiva inteligente de cada una de sus audiencias, aprovechando las perspectivas basadas en el aprendizaje automático para identificar y dirigirse a clientes de alto valor con sus campañas de marketing. Con las audiencias de similitud, puede crear audiencias ampliadas dirigidas a clientes similares a sus audiencias de alto rendimiento o a clientes de destino similares a audiencias convertidas anteriormente. Para obtener más información sobre audiencias de similitud, lea la [Resumen de audiencias de similitud](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de [!DNL SugarCRM] | [!DNL SugarCRM] ya están disponibles las fuentes de. Utilice las fuentes de [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] para obtener datos de su cuenta de [!DNL SugarCRM] para Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |
| Compatibilidad con la ingesta bajo demanda para flujos de datos de origen en la IU | Ahora puede crear ejecuciones de flujo bajo demanda para un flujo de datos de fuentes existente en la interfaz de usuario. Para obtener más información, lea la guía de [creación de una ejecución de flujo bajo demanda para orígenes que utilicen la interfaz de usuario](../../sources/tutorials/ui/on-demand-ingestion.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [información general de orígenes](../../sources/home.md).
