---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2023'
description: Las notas de la versión de febrero de 2023 de Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 22 de febrero de 2023**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Recopilación de datos](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Fuentes](#sources)

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

### Assurance {#assurance}

Adobe Assurance le permite inspeccionar, probar, simular y validar cómo recopila datos o presenta las experiencias en sus aplicaciones móviles.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| API públicas | Las API de Assurance de Adobe ya están disponibles. Las API de Assurance son una colección de API que permiten a los usuarios probar y depurar sus propias aplicaciones web y móviles, cuando se equipan con la extensión de Adobe Assurance con el SDK móvil. Para obtener más información sobre las API de Assurance, lea la [Información general de API de Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Para obtener más información sobre Assurance, lea la [Documentación de Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Funciones nuevas o actualizadas** {#destinations-new-updated-features}

| Función | Descripción |
| ----------- | ----------- |
| [Mejora de la política de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) para integraciones con [destinos basados en archivos (por lotes)](/help/destinations/destination-types.md#file-based) | <p> Cuando los perfiles ya no están cualificados para una directiva de consentimiento, Experience Platform ahora comunica de forma proactiva su salida de directiva a destinos basados en archivos. Esto sigue a la [Versión de febrero de 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la misma funcionalidad para los destinos de streaming. </p> <p> <b>Nota</b>: Esta funcionalidad solo está disponible para los clientes de **[!UICONTROL Escudo de seguridad y privacidad]**, y los de **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentación nueva o actualizada** {#destinations-new-updated-documentation}

| Documentación | Descripción |
| ----------- | ----------- |
| Documentación de funcionamiento de los destinos | <p>Publicamos tres nuevos artículos explicativos sobre cómo funcionan los destinos, basados en preguntas comunes de los usuarios:</p> <p><ul><li>[Configuración de exportación configurable y común en destinos](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamiento de exportación de perfil para diferentes tipos de destino](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Administración de identidades en el flujo de trabajo de activación de destinos](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Obsolescencia de campos mediante la IU | Ahora puede [dejar obsoletos campos de los esquemas después de la ingesta de datos](../../xdm/tutorials/field-deprecation-ui.md). La obsolescencia de los campos XDM permite eliminar campos de la vista de la interfaz de usuario y conservarlos para su uso. Puede volver a mostrar los campos obsoletos si es necesario y los segmentos, consultas o soluciones de flujo descendente que hagan referencia a los campos se ejecutarán de la forma habitual. |

{style="table-layout:auto"}

**Nuevos componentes de XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Perfil de cliente potencial de XDM]](https://github.com/adobe/xdm/pull/1669/files) | La clase de perfil de cliente potencial individual XDM incorpora ID proporcionados por el socio. |

{style="table-layout:auto"}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [!UICONTROL Límites de restricción de frecuencia] | El grupo de campos [!UICONTROL Límites de restricción de frecuencia] [ se ha actualizado para admitir eventos repetidos y personalizados](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo de datos | [!UICONTROL Remitente del reenvío web] | Se han [actualizado las propiedades del remitente del reenvío web actualizado para incluir `xdm:linkName` y `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivamente, son el nombre y la región del elemento HTML seleccionado en la página anterior. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent: detalles de interacción de mensajes] | [El campo [!UICONTROL URL del rastreador] se ha añadido](https://github.com/adobe/xdm/pull/1665/files) al [!UICONTROL Adobe CJM ExperienceEvent]. Este rastreador proporciona la URL seleccionada por el usuario. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent: detalle de interacción de mensajes] | [La propiedad `meta:enum` vacía se ha eliminado](https://github.com/adobe/xdm/pull/1668/files) desde el campo [!UICONTROL Tipo de seguimiento] de la URL. |
| Tipo de datos | [!UICONTROL Información de medios] | [El patrón regex de la propiedad `videoSegment` en el tipo de datos [!UICONTROL Información de medios] se ha eliminado](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de consultas {#query-service}

El servicio de consulta le permite utilizar SQL estándar para consultar datos en el [!DNL Data Lake] de Adobe Experience Platform. Puede unir cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, en Espacio de trabajo de ciencia de datos o para su inserción en el Perfil del cliente en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Habilitar conjuntos de datos para perfiles con SQL | [Utilice ETIQUETAS en consultas CTAS para hacer que un conjunto de datos tenga un &quot;perfil habilitado&quot;](../../query-service/sql/syntax.md#create-table-as-select), o utilice ALTER para actualizar los conjuntos de datos existentes y habilitarlos para el perfil. Puede utilizar esta construcción SQL extendida para proporcionar una compatibilidad perfecta con los atributos derivados para los casos de uso empresariales del Perfil del cliente en tiempo real. Consulte el [documento Flujo SQL fluido para atributos derivados](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) para obtener más información. |
| Monitorización de consultas programadas | Utilice la [pestaña Consultas programadas](../../query-service/ui/monitor-queries.md) para encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. Supervise las consultas para obtener detalles de programación, estado y mensajes/códigos de error en caso de que fallen. |
| Alternancia de la característica de autocompletar | Elimine ciertos comandos de metadatos y mejore los tiempos de procesamiento al [alternar la función de autocompletar del editor de consultas](../../query-service/ui/user-guide.md#auto-complete). Esta función sugiere automáticamente posibles palabras clave SQL y detalles de tabla para la consulta a medida que la escribe. |
| Ejemplos de conjuntos de datos | Especifique una tasa de muestreo en la consulta y [utilice ejemplos de conjuntos de datos para crear una muestra aleatoria uniforme](../../query-service/key-concepts/dataset-samples.md), o cree muestras condicionales basadas en criterios específicos. |

{style="table-layout:auto"}

Para obtener más información sobre los Servicios de consultas, consulte la [Introducción al Servicio de consultas](../../query-service/home.md).


## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP edición B2B, que se creó en Real-time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a públicos específicos con precisión y captarlos en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Habilitar servicio de cuentas relacionadas | La nueva función de alternancia le permite habilitar el servicio de cuentas relacionadas en su cuenta. Para obtener más información, lea la guía de [activación del servicio de cuentas relacionadas](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Para obtener más información sobre Real-Time CDP B2B Edition, lea la [Información general sobre Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Designación del acceso de nivel de suscripción con [!DNL Google PubSub] | Ahora puede definir el acceso a una suscripción a un tema específico al utilizar el origen [!DNL Google PubSub] proporcionando el ID de suscripción al autenticarse. Para obtener más información, lea el [!DNL Google PubSub] tutorial de autenticación [usando la API de Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) o [IU de Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingesta de datos de actividad personalizada de [!DNL Marketo] | Ahora puede obtener datos de actividad personalizada de su instancia [!DNL Marketo] a Experience Platform. Para introducir datos de actividad personalizada, debe configurar grupos de campos de actividades personalizadas en el esquema de actividades B2B y crear un flujo de datos mediante el conjunto de datos de actividades. Una vez completado el flujo de datos, el conjunto de datos introducido contendrá actividades estándar y personalizadas de su instancia [!DNL Marketo]. A continuación, puede utilizar el [Servicio de consultas](../../query-service/home.md) para acceder a sus registros de actividad personalizados en Platform. Para obtener más información, lea la guía de [creación de un flujo de datos para datos de actividad personalizada](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Excluir cuentas no reclamadas de [!DNL Marketo] | Ahora puede configurar si desea excluir o incluir cuentas no reclamadas de la ingesta al crear un flujo de datos para datos de empresas. Para obtener más información, lea la guía sobre la [creación de una conexión de origen y un flujo de datos para  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Para obtener más información acerca de las fuentes, lea la [Información general de fuentes](../../sources/home.md).
