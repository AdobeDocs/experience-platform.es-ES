---
title: Notas de la versión de Adobe Experience Platform, octubre de 2020
description: Notas de la versión de octubre de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 4%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 14 de octubre de 2020**

- [Preparación de datos](#data-prep)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)
- [Tiempo para el valor](#time-to-value)

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Función  de `is_set` | La variable `is_set` permite comprobar la presencia de un atributo en los datos de origen. `is_set` puede utilizarse en combinación con `is_empty` para comprobar la presencia del atributo y la presencia del valor dentro del atributo . |
| Función  de `get_values` | La variable `get_values` permite obtener los valores del mapa de entrada para una clave determinada. |

Para obtener más información, lea la [Resumen de la preparación de datos](../../data-prep/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus diferentes datos de clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Adiciones a la API de vista previa de perfil | La API de vista previa del perfil (`/previewsamplestatus`) ahora incluye la capacidad de ver un desglose del total de fragmentos de perfil en su organización de IMS, así como de ver la distribución de fragmentos de perfil entre áreas de nombres de identidad. |
| Actualizaciones de la vista de esquema de unión | En la interfaz de usuario del Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad de solucionar problemas y validar que los perfiles están correctamente configurados, que las identidades se vinculan correctamente y que los datos se han introducido correctamente. |

Para obtener más información, consulte [!DNL Real-Time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] información, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-Time Customer Profile] datos. Estos segmentos están configurados de forma centralizada y se mantienen en [!DNL Platform], lo que permite que cualquier aplicación de Adobe pueda acceder a ellas fácilmente.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Eliminación del límite de segmentación por transmisión | Se ha eliminado el límite de siete días para el período retroactivo. |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con autenticación SSH para SFTP | Puede conectar su cuenta de SFTP a [!DNL Platform] uso de claves RSA/DSA Open SSH. Consulte la [Información general de SFTP](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |
| Mejoras en la experiencia de usuario | Puede habilitar su conjunto de datos para [!DNL Profile] durante el proceso de ingesta de datos. Consulte la [flujo de trabajo de datos de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) tutorial para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).

## Tiempo para el valor {#time-to-value}

Adobe Experience Platform permite a los equipos de operaciones de marketing crear una vista de 360 grados de sus clientes sin necesidad de una amplia experiencia en ingeniería de datos. El objetivo es acelerar los equipos y el valor a través de la velocidad de los datos.

&quot;Tiempo para el valor&quot; cruza las personalidades. Los ingenieros de datos pueden completar las tareas de forma eficiente y acelerada con transparencia en la actividad de los datos, de modo que antes haya disponible un perfil de cliente robusto y escalable en tiempo real. Los especialistas en marketing pueden utilizar el perfil de cliente completo y sólido para la segmentación y la activación.

### Elementos destacados de las funciones

#### Esquema

Actualiza la facilidad de uso y el flujo de trabajo, y proporciona perspectivas, estandarización y transparencia predeterminadas de los campos clave dentro de las composiciones de esquema. Expone el linaje de datos para la combinación de modelos de datos individuales representados como el &quot;esquema de unión&quot;, lo que proporciona una perspectiva de la estructura y los ingredientes del perfil del cliente en tiempo real.

- Actualización del flujo de trabajo del esquema
   - Utilice accesos directos para el tipo más común de esquemas XDM, con configuración automatizada en el editor de esquemas y recomendaciones de grupos de campos de esquema basadas en sus objetivos
   - Aumente la eficacia del flujo de trabajo con la selección y la capacidad de vista previa de varios grupos de campos
   - Proporcionar transparencia en los atributos clave de la composición del esquema, incluida la identidad, la relación y los campos obligatorios y obsoletos
- Lenguaje de datos del esquema de unión y transparencia de atributos clave

#### Ingesta de datos y recopilación

La asignación automática, la vista previa de asignación y la actualización de uso aportan datos de cualquier plataforma o fuente para su uso en perfiles, segmentación descendente y activación. El sistema tiene la eficiencia y la inteligencia necesarias para facilitar el uso de este proceso, incluso para personas ajenas a TI.

- Acceso más fácil a las fuentes de datos con tarjeta de página de catálogo y actualización de patrón de acción en línea de tabla de datos
- Campo/expresión calculado para la ingesta de datos
- Las recomendaciones de asignación de datos aceleran el proceso de ingesta
- Asignación de vista previa y validaciones

#### Configuración de perfil

El visor de perfiles fácil de usar y personalizado le ayuda a comprender la composición de un perfil para utilizarlo en casos de segmentación, planificación y activación. El flujo de trabajo consolidado hidrata el perfil de forma controlada y eficaz, ya que proporciona un flujo de trabajo paso a paso para la política de combinación.

- Vea cada perfil individual en un visor de perfil mejorado que muestra un panel con personalización completa, lo que permite agrupar los datos entre canales en función de los objetivos comerciales del especialista en marketing.
- Edite los atributos estándar y personalizados en el widget Información básica , según las necesidades del negocio.
- Personalice las utilidades con atributos del perfil del cliente en tiempo real mediante el selector de esquema de unión. El esquema de unión se deriva de los modelos de datos subyacentes utilizados dentro de la incorporación de datos de perfil.


#### Monitoreo

Garantiza la transparencia del flujo de datos y proporciona una perspectiva sobre el estado del tráfico de datos en el sistema desde los conectores de origen, lo que proporciona una mayor autoservicio y una capacidad de acción más rápida para solucionar problemas.

- Supervise todas las ejecuciones de flujo y vea una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y los diagnósticos procesables
