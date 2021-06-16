---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 26 de mayo de 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 487d6dbef21459a7ce78cdc70215ad46e06ba892
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 3%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 26 de mayo de 2021**

Nuevas funciones de Adobe Experience Platform:

- [Tableros](#dashboards)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [Perfil del cliente en tiempo real](#profile)
- [Entornos aislados](#sandboxes)
- [Fuentes](#sources)

## Tableros {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver perspectivas importantes sobre los datos de su organización, tal como se capturan durante las instantáneas diarias.

| Función | Descripción |
| --- | --- |
| Perspectivas del perfil | El panel de perfiles proporciona una descripción general diaria de las métricas del Perfil del cliente en tiempo real para cada política de combinación organizativa en Experience Platform. Estas perspectivas de perfil están disponibles para todos los usuarios con la capacidad de acceder y ver los datos de perfil dentro de Platform. |
| Perspectivas de audiencia | El tablero de segmentos proporciona perspectivas relacionadas con la audiencia a todos los usuarios con acceso para ver segmentos dentro de Platform. El tablero proporciona una descripción general diaria de las métricas de audiencia para las audiencias creadas con la interfaz de usuario del Generador de segmentos o importadas desde Adobe Audience Manager. |
| Perspectivas de activación | El panel de destinos está disponible para todos los usuarios con la capacidad de acceder y ver destinos. El tablero proporciona información general diaria sobre las métricas de activación para las activaciones en todos los destinos. |
| Perspectivas específicas del usuario | Cada usuario puede personalizar el aspecto de los tableros, incluida la capacidad de modificar el diseño del tablero añadiendo, eliminando, cambiando el tamaño y reorganizando las utilidades. |
| Creación y administración de utilidades | Los especialistas en marketing pueden acceder a todos los widgets estándar y personalizados en un repositorio centralizado para democratizar la creación y el uso compartido de perspectivas:<br/><ul><li>La pestaña estándar contiene utilidades proporcionadas por Adobe a las que se puede acceder desde el contexto del panel. </li><li>La pestaña personalizada contiene widgets personalizados creados por la organización, incluida una opción para ocultar las utilidades de la vista.</li><li>El flujo de trabajo de creación de utilidades en Profiles and Audience Inghts permite editar, seleccionar, previsualizar y publicar utilidades personalizadas.</li></ul> |
| Perspectivas personalizadas | Los permisos de acceso permiten a los ingenieros de datos y a los especialistas en marketing personalizar los atributos de perfil que están disponibles para la creación de utilidades. |

Para obtener más información sobre los tableros, incluido cómo conceder permisos de acceso y crear utilidades personalizadas, comience leyendo la [información general de los tableros](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

| Función | Descripción |
| ------- | ----------- |
| Advertencias de error leves | Los mensajes de error del Data Prep Mapper serán ahora más indulgentes, ya que proporcionarán advertencias en lugar de errores junto con filas parcialmente transformadas. |
| Nuevas funciones | Funciones agregadas para obtener claves, anexar elementos a una matriz existente, anexar elementos de varias matrices a una matriz existente, usar objetos para crear matrices y usar el nombre del objeto JSON como un literal de cadena. |

Para obtener más información, consulte [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

| Función | Descripción |
| ------- | ----------- |
| Supervisión mejorada (beta) | Se han aumentado las capacidades de supervisión de los destinos, incluida la información para los destinos de lote y de flujo continuo |
| [Exportación de archivos incrementales más rápida (beta)](../../destinations/ui/activate-destinations.md#export-incremental-files) | Se ha agregado la capacidad de exportar archivos incrementales a destinos cada 3, 6, 8 o 12 horas. <br> <br>Esta capacidad está actualmente en fase beta y solo está disponible para un número determinado de clientes. Los clientes que no sean de la versión beta pueden exportar archivos incrementales una vez al día. |
| [Compatibilidad con claves de deduplicación (beta)](../../destinations/ui/activate-destinations.md#deduplication-keys) | Se ha agregado la capacidad de establecer áreas de nombres de identidad o atributos de perfil como claves de deduplicación. Las claves de deduplicación eliminan la posibilidad de tener varios registros del mismo perfil en un archivo de exportación. <br> <br>Esta capacidad está actualmente en fase beta y solo está disponible para un número determinado de clientes. |

Para obtener información más general sobre los destinos, consulte [información general sobre destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) es una especificación de código abierto diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

| Función | Descripción |
| --- | --- |
| Grupos de campos de esquema | El término &quot;mezcla&quot; se ha actualizado a &quot;grupo de campos&quot;. Este cambio se refleja en la interfaz de usuario de Adobe Experience Platform. Además, la API del Registro de esquemas tiene un nuevo extremo [de grupos de campos](../../xdm/api/field-groups.md), mientras que el extremo de mezclas ha quedado obsoleto como punto final heredado. Consulte la [documentación de XDM](../../xdm/home.md) para obtener más información. |

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Informe de superposición de conjunto de datos | El informe de superposición de conjuntos de datos proporciona visibilidad sobre la composición del almacén de perfiles al exponer los conjuntos de datos que contribuyen en mayor medida a la audiencia a la que se puede dirigir. Además de proporcionar perspectivas sobre los datos de perfil, este informe ayuda a los usuarios a realizar acciones para optimizar el uso de licencias, como establecer un límite para la vida útil de ciertos datos. Para obtener más información, siga el tutorial sobre [generación del informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md). |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos [!DNL Profile], lea en primer lugar la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales. Para satisfacer esta necesidad, Experience Platform proporciona entornos limitados que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

| Función | Descripción |
| ------- | ----------- |
| Varios entornos limitados de producción | Ahora puede crear y administrar varios entornos limitados de producción en su organización de IMS y dedicar entornos limitados de producción específicos a distintas líneas de negocios, marcas, proyectos o regiones. Consulte los tutoriales sobre la creación de un entorno limitado de producción [en la interfaz de usuario](../../sandboxes/ui/user-guide.md) o [con la API](../../sandboxes/api/overview.md) para obtener más información. |

### Limitaciones conocidas

- Cada organización de Experience Cloud viene con un simulador para pruebas de producción predeterminado creado previamente. Este simulador para pruebas actúa como destino predeterminado para cada solicitud enviada a Platform desde otra aplicación de Adobe o aplicación que no es de Adobe y que (aún) no es compatible con Sandbox. No se puede restablecer el entorno limitado de producción predeterminado si Adobe Analytics también está utilizando el gráfico de identidad alojado en él para la función [Análisis entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) o si Adobe Audience Manager también está utilizando el gráfico de identidad alojado en él para la función [Destinos basados en personas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) .
- Los entornos limitados de producción que se utilizan para compartir segmentos bidireccionales con Adobe Audience Manager o el servicio principal de audiencia no se pueden restablecer ni eliminar.
- Se pueden eliminar todos los entornos limitados de producción y desarrollo creados por el usuario, excepto el entorno limitado de producción predeterminado.

Para obtener más información sobre los entornos limitados, consulte la [información general de los entornos limitados](../../sandboxes/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con la interfaz de usuario para la ingesta de archivos comprimidos | Ahora puede obtener una vista previa e introducir archivos JSON comprimidos o delimitados mediante fuentes de almacenamiento en la nube en la interfaz de usuario. Para obtener más información, consulte el tutorial sobre la [configuración de un flujo de datos para una conexión de origen de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Azure Synapse Analytics]](../../sources/connectors/databases/synapse-analytics.md)</li><li>[[!DNL Greenplum]](../../sources/connectors/databases/greenplum.md)</li><li>[[!DNL HubSpot]](../../sources/connectors/marketing-automation/hubspot.md)</li><li>[[!DNL ServiceNow]](../../sources/connectors/customer-success/servicenow.md)</li></ul> |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
