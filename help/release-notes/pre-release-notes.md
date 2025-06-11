---
title: Notas previas al lanzamiento de Experience Platform
description: Una previsualización de las últimas notas de la versión para Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 42%

---


# Notas previas al lanzamiento de Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento está diseñado como **vista previa** de las notas de la versión del mes actual. Los elementos de la versión están sujetos a cambios y se pueden añadir o eliminar en la versión final.

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: jueves, 18 de junio de 2025**

Nuevas funciones y actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Control de acceso](#access-control)
- [Administración avanzada del ciclo de vida de los datos](#advanced-data-lifecycle-management)
- [Paneles](#dashboards)
- [Gobernanza de datos](#data-governance)
- [Destinos](#destinations)
- [Composición de público federado](#fac)
- [Privacy Service](#privacy-service)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Fuentes](#sources)

## Control de acceso {#access-control}

Experience Platform aprovecha los perfiles de producto de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a usuarios con permisos y zonas protegidas. Los permisos controlan el acceso a una variedad de funciones de Experience Platform, incluido el modelado de datos, la administración de perfiles y la administración de zonas protegidas.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Exportar permiso de datos del panel | Las opciones **[!UICONTROL Descargar CSV]** y **[!UICONTROL Enviar como correo electrónico]** en los paneles ahora requieren el permiso **[!UICONTROL Exportar datos del panel]**. Este permiso garantiza que solo los usuarios autorizados puedan exportar datos de insight tabulados, lo que admite una gobernanza y políticas de control de acceso a datos más estrictas. |

Para obtener más información, consulte la [descripción general del control de acceso](../access-control/home.md).

## Administración avanzada del ciclo de vida de los datos {#advanced-data-lifecycle-management}

Experience Platform proporciona un conjunto de funcionalidades de higiene de datos que le permiten administrar los datos almacenados mediante eliminaciones programáticas de registros de consumidores y conjuntos de datos. Con el espacio de trabajo de Data Lifecycle en la interfaz de usuario o a través de llamadas a la API de Data Hygiene, puede administrar de forma eficaz los almacenes de datos. Utilice estas funciones para asegurarse de que la información se utiliza según lo esperado, se actualiza cuando es necesario corregir datos incorrectos y se elimina cuando las políticas organizativas lo consideran necesario.

**Nueva documentación**

| Nueva documentación | Descripción |
| --- | --- |
| Disponibilidad general de eliminación de registros | Ahora puede eliminar registros individuales basados en campos de identidad mediante la interfaz de usuario o la API. Esta función ayuda a reducir el almacenamiento, aplicar la gobernanza y mejorar la higiene de los datos al permitir eliminaciones de un único conjunto de datos o de todos ellos. Se aplican límites de volumen y requisitos de asignación de derechos. |

Para obtener más información, lea la [información general de la administración avanzada del ciclo de vida de los datos](../hygiene/home.md).

## Paneles {#dashboards}

Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| ------- | ----------- |
| Opción Enviar como exportación de correo electrónico | Ahora puede exportar hasta 10 000 registros desde los paneles del modo Query Pro seleccionando **[!UICONTROL Enviar como correo electrónico]** en el menú **[!UICONTROL Ver más]**. Esta opción envía de forma segura un vínculo de descarga al correo electrónico asociado a Adobe para exportaciones más grandes. |

Para obtener más información sobre los paneles, incluido cómo conceder permisos de acceso y crear widgets personalizados, comience por leer la [información general sobre paneles](../dashboards/home.md).

## Gobernanza de datos {#data-governance}

La gobernanza de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña una función clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de los datos, las políticas de acceso a los datos y el control de acceso de los datos para las acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Configuración de alertas CMK de Azure y Listas de permitidos IP | Ahora puede lista de permitidos la dirección IP estática de Adobe en Azure Key Vault para garantizar un acceso continuo cuando las restricciones de red estén habilitadas. Esto ayuda a evitar interrupciones en los servicios de Platform debido al acceso restringido a las claves. |
| Alertas y resoluciones de configuración de CMK | Experience Platform ahora envía déclencheur cuando los servicios de Adobe pierden el acceso a Azure Key Vault (por ejemplo, debido a entradas de lista de permitidos IP eliminadas o claves deshabilitadas). Una nueva guía le ayuda a comprender cada alerta y a tomar medidas correctivas. |

Para obtener más información, consulte la [Información general sobre la gobernanza de datos](../data-governance/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| --- | --- |
| Segmentos de usuario de Algolia | El destino Segmentos de usuarios de Algolia permite a los profesionales de marketing proporcionar una personalización coherente en todos los sitios, desde la página de inicio hasta la búsqueda. Cree audiencias enriquecidas a partir de varias fuentes de datos y compártalas en varios canales para mejorar las estrategias de segmentación y la personalización de campañas. |

**Funcionalidad nueva o actualizada**

| Función | Descripción |
| --- | --- |
| Información de caducidad de la cuenta de LinkedIn | La información de caducidad de la cuenta para los destinos de LinkedIn ahora está disponible directamente en las vistas [!UICONTROL Examinar] y [!UICONTROL Cuentas]. Anteriormente, esta información solo estaba disponible en la documentación de. Esta mejora proporciona una mejor visibilidad del estado de autenticación de LinkedIn y la administración de credenciales. |
| Disponibilidad y mejora general de Google Customer Match + DV360 | El destino Google Customer Match + DV360 ya está disponible para todos los usuarios de Experience Platform. La documentación ahora incluye instrucciones detalladas para la vinculación de cuentas entre Adobe y las cuentas publicitarias de Google. |
| Compatibilidad con cifrado de destino de zona de aterrizaje de datos (DLZ) | Se ha agregado compatibilidad con cifrado para el destino de zona de aterrizaje de datos. Ahora puede adjuntar claves públicas con formato RSA para agregar cifrado a los archivos exportados. |
| Monitorización de nivel de audiencia para destinos empresariales | La supervisión a nivel de audiencia ya está disponible para los siguientes destinos empresariales: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Para obtener más información, consulte la [Información general sobre destinos](../destinations/home.md).

## Composición de público federado {#fac}

La composición de público federado permite a las empresas componer datos para una mejor aplicación en varios casos de uso. Con este nuevo enfoque, como usuario de Adobe Real-time Customer Data Platform y/o Adobe Journey Optimizer, puede federar conjuntos de datos directamente desde su almacén de datos existente para crear y enriquecer públicos y atributos de Adobe Experience Platform en un solo sistema.

| Nueva función | Descripción |
| ----------- | ----------- |
| Preparación para la HIPAA | La composición de audiencias federada ahora es compatible con HIPAA. Para obtener más información sobre las medidas de seguridad y privacidad de la Composición de audiencias federadas, lea la [información general sobre la seguridad y la privacidad en la Composición de audiencias federadas](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/start/privacy-security). Para obtener más información sobre la conformidad con HIPAA de los productos de Experience Platform en general, lea la [Información general sobre HIPAA y los productos y servicios de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Para obtener más información, lea la documentación de la [Composición de público federado](https://experienceleague.adobe.com/es/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Varias regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de los clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos personales de clientes y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
|--- | ---|
| Compatibilidad con las leyes de privacidad de Tennessee y Minnesota | Privacy Service ahora es compatible con la Ley de Protección de Información de Tennessee (`tipa_tn_usa`) y la Ley de Privacidad de Datos del Consumidor de Minnesota (`mcdpa_mn_usa`). Puede procesar las solicitudes de acceso y eliminación de acuerdo con estas nuevas regulaciones de nivel de estado. Consulte [Resumen de regulaciones](https://experienceleague.adobe.com/es/docs/experience-platform/privacy/regulations/overview) para obtener más detalles. |

Consulte la [información general de Privacy Service](../privacy-service/home.md) para obtener más información sobre el servicio.

## Servicio de consultas {#query-service}

Consulte datos en el lago de datos de Adobe Experience Platform utilizando SQL estándar con el Servicio de consultas. Combine conjuntos de datos sin problemas y genere otros nuevos a partir de los resultados de su consulta para impulsar la creación de informes, habilitar flujos de trabajo de ciencia de datos o facilitar la ingesta en el Perfil del cliente en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Funciones estadísticas avanzadas | **Intersección de bocetos theta**: Nueva función para calcular intersecciones de conjuntos usando bocetos theta para operaciones aproximadas de conteo y definición distintas. **Histogramas KLL**: Funciones de histograma mejoradas que utilizan bocetos KLL (Kth más pequeño, L más grande, elementos grandes) para la estimación cuantil y el análisis de distribución. Estas funciones están disponibles para los clientes de Data Distiller. |
| Biblioteca de plantillas SQL | Ya está disponible una biblioteca completa de plantillas SQL para casos de uso comunes. Esta función acelera el desarrollo de consultas al proporcionar plantillas de prácticas recomendadas para patrones de análisis frecuentes, lo que ayuda a los clientes de Data Distiller a implementar análisis complejos de forma más eficaz. |

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Ejemplo de modelado de RFM | Se ha añadido un ejemplo completo de modelado de actualización, frecuencia y monetario (RFM) para los clientes de Data Distiller. Esto incluye documentación detallada y guías de implementación para la segmentación de clientes y el análisis de valor mediante técnicas de RFM. |

{style="table-layout:auto"}

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Migración de actualizaciones de configuración de objetos | Ahora puede migrar actualizaciones de configuración de objetos iterativas entre entornos limitados después de la replicación inicial. Esta mejora admite flujos de trabajo de desarrollo en los que las configuraciones deben actualizarse y propagarse entre entornos sin volver a crear toda la configuración de la zona protegida. |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../sandboxes/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con el nuevo tipo de autenticación de [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] ahora también admitirá la autenticación de entidad de seguridad de servicio, además de la autenticación de cadena de conexión existente. |

**Actualizaciones importantes en la autenticación**

| Actualización | Descripción |
| --- | --- |
| [!DNL Salesforce] desaprobación de autenticación básica | La autenticación básica para Salesforce CRM y Salesforce Service Cloud dejará de usarse en enero de 2026. Los clientes deben migrar a la autenticación OAuth 2.0 para mantener la conectividad. Este cambio afecta a los conectores de origen y garantiza una seguridad mejorada y el cumplimiento de los estándares de autenticación de Salesforce. |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../sources/home.md).
