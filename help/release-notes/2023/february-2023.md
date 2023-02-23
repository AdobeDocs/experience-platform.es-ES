---
title: Notas de la versión de Adobe Experience Platform, febrero de 2023
description: Notas de la versión de febrero de 2023 para Adobe Experience Platform.
source-git-commit: 66ca8d3972045cffe4a1614f638546f4e7838680
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 22 de febrero de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Modelo de datos de experiencia (XDM)](#xdm)
- [Servicio de consultas](#query-service)
- [Real-Time Customer Data Platform edición B2B](#b2b)
- [Fuentes](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Funciones nuevas o actualizadas** {#destinations-new-updated-features}

| Función | Descripción |
| ----------- | ----------- |
| [Mejora de la política de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) para integraciones con [destinos basados en archivos (por lotes)](/help/destinations/destination-types.md#file-based) | <p> Cuando los perfiles ya no están cualificados para una directiva de consentimiento, el Experience Platform ahora comunica de forma proactiva su salida de directiva a destinos basados en archivos. Esto sigue a la [versión de febrero de 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la misma funcionalidad para los destinos de flujo continuo. </p> <p> <b>Nota</b>: Esta funcionalidad solo está disponible para los clientes de **[!UICONTROL Protección de seguridad y privacidad]** y los de **[!UICONTROL Escudo sanitario]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentación nueva o actualizada** {#destinations-new-updated-documentation}

| Documentación | Descripción |
| ----------- | ----------- |
| Cómo funcionan los destinos en la documentación | <p>Publicamos tres nuevos artículos explicativos sobre cómo funcionan los destinos, basados en preguntas comunes de los usuarios:</p> <p><ul><li>[Configuración de exportación configurable y común en destinos](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportamiento de exportación de perfil para diferentes tipos de destino](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestión de identidades en el flujo de trabajo de activación de destinos](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se introducen en Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Funciones actualizadas**
&#x200B; | Función | Descripción | | — | — | | Desaprobación de campos a través de la interfaz de usuario | Ahora puede [eliminar campos de los esquemas después de ingerir datos](../../xdm/tutorials/field-deprecation-ui.md). La desaprobación de campos XDM le permite eliminar campos de la vista de IU al conservarlos para su uso. Puede volver a mostrar los campos obsoletos si es necesario, y cualquier segmento, consulta o solución descendente que haga referencia a los campos se ejecutará de la forma habitual. |

{style=&quot;table-layout:auto&quot;}

**Nuevos componentes XDM**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Clase | [[!UICONTROL Perfil de cliente potencial individual XDM]](https://github.com/adobe/xdm/pull/1669/files) | La clase XDM Individual Prospect Profile incorpora ID proporcionados por el socio. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM actualizados**

| Tipo de componente | Nombre | Descripción |
| --- | --- | --- |
| Grupo de campos | [!UICONTROL Restricciones de restricción de frecuencia] | La variable [!UICONTROL Restricciones de restricción de frecuencia] el grupo de campos se ha [actualizado para admitir eventos repetidos y personalizados](https://github.com/adobe/xdm/pull/1641/files). |
| Tipo de datos | [!UICONTROL Referente web] | Se han realizado las propiedades de referente web [actualizado para incluir `xdm:linkName` y `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivamente, son el nombre y la región del elemento HTML que se seleccionó en la página anterior. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent: Detalles de la interacción de mensajes] | [La variable [!UICONTROL URL de seguimiento] se agregó el campo](https://github.com/adobe/xdm/pull/1665/files) a [!UICONTROL Adobe CJM ExperienceEvent]. Este rastreador proporciona la URL seleccionada por el usuario. |
| Grupo de campos | [!UICONTROL Adobe CJM ExperienceEvent: Detalles de interacción de mensajes] | [El vacío `meta:enum` se quitó la propiedad](https://github.com/adobe/xdm/pull/1668/files) desde la dirección URL [!UICONTROL Tipo de seguimiento] campo . |
| Tipo de datos | [!UICONTROL Información multimedia] | [El patrón regex de la variable `videoSegment` propiedad en [!UICONTROL Información multimedia] el tipo de datos se ha eliminado](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre XDM en Platform, lea la [Información general del sistema XDM](../../xdm/home.md)&#x200B;

## Servicio de consultas {#query-service}

El servicio de consultas permite utilizar SQL estándar para consultar datos en Adobe Experience Platform [!DNL Data Lake]. Puede unirse a cualquier conjunto de datos de un lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en informes, Data Science Workspace o para su incorporación al Perfil del cliente en tiempo real.

**Funciones actualizadas**
&#x200B; | Función | Descripción | | — | — | | Habilitar conjuntos de datos para perfil con SQL | Utilice LABEL en consultas CTAS para hacer un conjunto de datos &quot;perfil habilitado&quot;, o utilice ALTER para actualizar los conjuntos de datos existentes para habilitarlos para el perfil. | | Monitorización de consultas programadas | Utilice la pestaña Consultas programadas para encontrar información importante sobre las ejecuciones de consultas y suscribirse a alertas. Supervise las consultas para ver los detalles de la programación, el estado y los mensajes/códigos de error en caso de que se produzcan errores.  | | Alternar la función de autocompletar | Elimine ciertos comandos de metadatos y mejore los tiempos de procesamiento alternando la función de autocompletar del Editor de consultas. Esta función sugiere automáticamente posibles palabras clave SQL y detalles de tabla para la consulta a medida que la escribe. | | Ejemplos de conjuntos de datos | Especifique una tasa de muestreo en la consulta y use muestras de conjuntos de datos para crear una muestra aleatoria uniforme o crear muestras condicionales basadas en criterios específicos. |

{style=&quot;table-layout:auto&quot;} &#x200B; Para obtener más información sobre los servicios de consulta, consulte la [Información general del servicio de consultas](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time Customer Data Platform edición B2B {#b2b}

Basado en Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Habilitar el servicio de cuentas relacionadas | La nueva función de alternancia le permite habilitar el servicio de cuentas relacionado en su cuenta. Para obtener más información, consulte la guía de [activación del servicio de cuentas relacionado](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre Real-Time CDP B2B Edition, lea la [Información general de Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Designe el acceso de nivel de suscripción con [!DNL Google PubSub] | Ahora puede definir el acceso a una suscripción a un tema específico al usar la variable [!DNL Google PubSub] al proporcionar el ID de suscripción al autenticarse. Para obtener más información, lea la [!DNL Google PubSub] tutorial de autenticación [uso de la API de servicio de flujo](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) o [Interfaz de usuario de Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingesta datos de actividad personalizados de [!DNL Marketo] | Ahora puede traer datos de actividad personalizados de su [!DNL Marketo] instancia a Experience Platform. Para introducir datos de actividad personalizados, debe configurar grupos de campos de actividades personalizados en el esquema de actividades B2B y crear un flujo de datos mediante el conjunto de datos de actividades. Una vez completado el flujo de datos, el conjunto de datos ingestado contendrá actividades estándar y personalizadas de su [!DNL Marketo] instancia. A continuación, puede usar [Servicio de consultas](../../query-service/home.md) para acceder a los registros de actividad personalizados en Platform. Para obtener más información, consulte la guía de [creación de un flujo de datos para datos de actividad personalizados](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Excluir cuentas no reclamadas de [!DNL Marketo] | Ahora puede configurar si desea excluir o incluir cuentas no reclamadas de la ingesta al crear un flujo de datos para datos de empresas. Para obtener más información, consulte la guía de [crear una conexión de origen y un flujo de datos para [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, lea la [información general sobre fuentes](../../sources/home.md).