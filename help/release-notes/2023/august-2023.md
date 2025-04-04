---
title: Notas de la versión de Adobe Experience Platform, agosto de 2023
description: Las notas de la versión de agosto de 2023 de Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 40%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: jueves, 23 de agosto de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Control de acceso basado en atributos](#abac)
- [Paneles](#dashboards)
- [Recopilación de datos](#data-collection)
- [Ingesta de datos](#data-ingestion)
- [Preparación de los datos](#data-prep)
- [Destinos](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de identidad](#identity-service)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Real-Time Customer Data Platform ([!DNL Real-Time CDP]), que se creó en Experience Platform, ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a lo largo del recorrido del cliente.

[!DNL Real-Time CDP] combina varias fuentes de datos empresariales para crear perfiles de clientes en tiempo real. Los segmentos creados a partir de estos perfiles se pueden enviar a destinos de flujo descendente para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Guía del caso de uso de renovación de participación inteligente | La guía del caso de uso de [Reparticipación inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) proporciona detalles sobre cómo volver a atraer a los clientes que han abandonado una conversión antes de completarla de una manera inteligente y responsable. Esta guía utiliza los siguientes recorridos de ejemplo para volver a atraer a los clientes: <ul><li>Recorrido de renovación de la participación: Segmentación de clientes que han abandonado la navegación por productos.</li><li>Recorrido de carro de compras abandonado: segmenta a los clientes que han colocado productos en el carro de compras, pero que aún no han completado la compra.</li><li>Recorrido de confirmación de pedido: enfoque en las compras de productos</li></ul> Use el vínculo de opciones de comentarios detallados que aparece en la parte inferior de la [guía del caso de uso de la participación inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) para proporcionar comentarios. |
| Asistencia de datos de socios | Ejecute marketing de canal superior en Real-Time CDP, con perfiles de clientes potenciales de origen socio e ID de socios para llegar a nuevos clientes y enriquecer los datos de origen: <ul><li>Adquisición y direccionamiento de clientes: aproveche los identificadores sin cookies y la PII con hash de los socios de datos que elija para llegar a nuevos clientes netos y reducir la dependencia de cookies de terceros.</li><li>Marketing por canal completo en un solo sistema: segmentación de autoservicio, depuración de audiencias y activación nativa para clientes potenciales y conocidos en un solo sistema.</li><li>Base de confianza: gobierne los datos y perfiles de los socios con uso de datos patentado, etiquetado, controles de acceso y mucho más para comercializar de forma responsable. Lea las siguientes guías de casos de uso para obtener más información: Las guías de casos de uso de prospección ya están disponibles. Lea las guías de casos de uso de prospección para aprender a atraer y adquirir nuevos clientes a través de casos de uso de prospección:<ul><li>[Prospección](../../rtcdp/partner-data/prospecting.md)</li><li>[Personalización en el sitio](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Perfiles de origen complementarios](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Activar audiencias de clientes potenciales](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de Real-Time CDP](../../rtcdp/overview.md).

## Control de acceso basado en atributos {#abac}

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad una mayor flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a funciones de usuario. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Experience Platform específicos de su organización.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD), la información de identificación personal (PII) y otros tipos personalizados de datos en todos los flujos de trabajo y recursos de Experience Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Configuración de zona protegida de directiva de permisos | La nueva característica [configuración de espacio aislado para directivas de permisos](../../access-control/abac/ui/policies.md) le permite aplicar una directiva de control de acceso basada en atributos en todos los espacios aislados o en un número determinado de ellos, según sus necesidades y requisitos. |

{style="table-layout:auto"}

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general del control de acceso basado en atributos](../../access-control/abac/overview.md). Para obtener una guía completa sobre el flujo de trabajo de control de acceso basado en atributos, lea la [guía completa de control de acceso basado en atributos](../../access-control/abac/end-to-end-guide.md).

## Paneles {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Caso de uso de análisis de consentimiento y seguimiento | Aprenda a crear un tablero de consentimiento para varios casos de uso de marketing para datos de Real-Time CDP con el [documento de análisis y seguimiento de consentimiento](../../dashboards/insights-use-cases/consent-analysis.md). Detalla cómo crear una audiencia con los atributos adecuados para sus necesidades comerciales y luego consumir las perspectivas mediante el uso de widgets preconfigurados en la interfaz de usuario de Adobe Experience Platform. También proporciona instrucciones sobre cómo crear su propio widget personalizado con la función de paneles definida por el usuario. El documento cubre las tendencias de consentimiento y los casos de uso de superposición de consentimiento. |

{style="table-layout:auto"}

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../../dashboards/home.md).

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Tipo | Función | Descripción |
| --- | --- | --- |
| Reenvío de eventos y etiquetas | [Etiquetas de Experience Platform (China)](/help/tags/ui/publishing/premium-cdn.md) | La nueva función Etiquetas de Experience Platform (China) mejora la fiabilidad y la latencia del sitio web, lo que conduce a tiempos de respuesta más rápidos para los clientes que implementan etiquetas en sitios web en China. Los clientes ahora pueden utilizar el código de JavaScript en la biblioteca de etiquetas al implementar sitios web en China. Esta función también se ha agregado al Protocolo de aprovisionamiento unificado (UPP), lo que permite automatizar la implementación de productos tras la compra. |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general de las colecciones de datos](../../tags/home.md).

## Ingesta de datos {#data-ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Puede hacerlo mediante las API por lotes o de streaming, utilizando fuentes creadas por Adobe, socios de integración de datos o la IU de Adobe Experience Platform.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en los flujos de trabajo de ingesta de datos | Ahora se rechazarán las filas de datos que contengan valores mayores que el tipo de datos especificado (por ejemplo, datos largos pasados como un tipo de datos entero) y se presentarán mensajes de error. Anteriormente, estas filas se rechazaban sin previo aviso. |

Para obtener más información, lea la [descripción general de la ingesta de datos](../../ingestion/home.md).

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el filtrado de identidades secundarias | Ahora puede utilizar la preparación de datos para filtrar las identidades procedentes de Adobe Analytics, como AAID y AACUSTOMID. Si se filtran, estas identidades no se incorporan en el Perfil del cliente en tiempo real. Los datos sin filtrar se seguirán introduciendo en el lago de datos. |

{style="table-layout:auto"}

Para obtener más información, lea [Resumen de la preparación de datos](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

- Ahora puede [activar audiencias de clientes potenciales](../../destinations/ui/activate-prospect-audiences.md) en destinos de almacenamiento en la nube.
- La [protección de activación general](../../destinations/guardrails.md#general-activation-guardrails) de un máximo de 100 destinos por zona protegida se ha actualizado para establecer un _límite estricto_.

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Perfil de cliente potencial de XDM]](https://github.com/adobe/xdm/pull/1758/files) | Utilice esta clase para incorporar perfiles de clientes potenciales procedentes de los casos de uso de adquisición de clientes principales de los proveedores de datos. Consulte la documentación de [[!UICONTROL Perfil de cliente potencial individual de XDM]](../../xdm/classes/prospect.md) para ver ejemplos y obtener más información. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Actualizar descripción |
| --- | --- | --- |
| Extensión ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Datos de contexto]](https://github.com/adobe/xdm/pull/1761/files) | Se agregó el objeto de asignación [!UICONTROL Datos de contexto] a [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] para proporcionar datos de contexto para Adobe Analytics. |
| Grupo de campo | Múltiples | Se agregaron varios campos a [[!UICONTROL Detalles del segmento de evento enriquecido]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Para obtener más información, lea la [descripción general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity-service}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Cambios en los límites del gráfico de identidad | A finales de septiembre, el gráfico de identidad cambiará a 50 identidades por gráfico y se ingestará la última identidad. Como consecuencia, la identidad más antigua se eliminará en función de la marca de tiempo de ingesta y el tipo de identidad, y los tipos de identidad de cookies se eliminarán primero. Actualmente, los gráficos de identidad tienen un límite de 150 identidades por gráfico y, una vez alcanzado este límite, los gráficos ya no se actualizan. Póngase en contacto con el representante de cuentas para solicitar un cambio en el tipo de identidad si la zona protegida de producción contiene lo siguiente: <ul><li>un área de nombres personalizada donde los identificadores de persona (como los ID de CRM) están configurados como tipo de identidad de cookie/dispositivo.</li><li>un área de nombres personalizada donde los identificadores de cookies/dispositivos están configurados como tipo de identidad entre dispositivos.</li></ul> El personal de ingeniería de Adobe procesará manualmente estas solicitudes. Para obtener más información, lea las [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md). |

Para obtener más información, lea la [descripción general del servicio de identidad](../../identity-service/home.md).

## Servicio de segmentación {#segmentation}

[!DNL Segmentation Service] le permite segmentar los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en públicos. Puede crear públicos a través de definiciones de segmentos u otras fuentes a partir de sus datos de [!DNL Real-Time Customer Profile]. Estos públicos se configuran de forma centralizada y se mantienen en [!DNL Experience Platform] y son fácilmente accesibles desde cualquier solución de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Audiencias de similitud (disponibilidad limitada) | Las audiencias de similitud proporcionan una perspectiva inteligente de cada una de sus audiencias, aprovechando las perspectivas basadas en el aprendizaje automático para identificar y dirigirse a clientes de alto valor con sus campañas de marketing. Con las audiencias de similitud, puede crear audiencias ampliadas dirigidas a clientes similares a sus audiencias de alto rendimiento o a clientes de destino similares a audiencias convertidas anteriormente. Para obtener más información sobre audiencias de similitud, lea la [Información general sobre audiencias de similitud](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

Para obtener más información, lea [Resumen de segmentación](../../segmentation/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Disponibilidad general de [!DNL SugarCRM] | Ya están disponibles [!DNL SugarCRM] orígenes. Utilice las fuentes de [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] para obtener datos de su cuenta de [!DNL SugarCRM] para Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |
| Compatibilidad con la ingesta bajo demanda para flujos de datos de origen en la IU | Ahora puede crear ejecuciones de flujo bajo demanda para un flujo de datos de fuentes existente en la interfaz de usuario. Para obtener más información, lea la guía sobre [creación de una ejecución de flujo bajo demanda para orígenes que usan la interfaz de usuario](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Compatibilidad con el nuevo campo `correlationID` para Adobe Analytics | El campo de `_experience.decisioning.propositions.scopeDetails.correlationID` ahora está disponible en el esquema del conector de origen de Adobe Analytics. Este campo se utiliza para clasificaciones de A4T y se rellenará a partir de septiembre de 2023. |

{style="table-layout:auto"}

Para obtener más información, lea [información general de orígenes](../../sources/home.md).
