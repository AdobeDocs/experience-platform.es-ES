---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform Octubre de 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e2b0048703816dc481eb9486310d86a8f2483af2
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 14 de octubre de 2020**

- [Preparación de datos](#data-prep)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)
- [Tiempo hasta el valor](#time-to-value)

## Preparación de datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Función  de `is_set` | La `is_set` función permite comprobar la presencia de un atributo en los datos de origen. `is_set` puede utilizarse en combinación con `is_empty` para comprobar la presencia del atributo y la presencia del valor dentro del atributo. |
| Función  de `get_values` | La `get_values` función le permite obtener los valores del mapa de entrada para cualquier clave determinada. |

Para obtener más información, lea la descripción general [de](../../data-prep/home.md)la preparación de datos.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Adiciones a la API de previsualización de perfil | La API de previsualización de Perfil (`/previewsamplestatus`) ahora incluye la capacidad de vista de un desglose de los fragmentos de perfil totales en la organización de IMS, así como de vista de la distribución de fragmentos de perfil entre Áreas de nombres de identidad. |
| Actualizaciones de vista de esquema de unión | En la interfaz de usuario del Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad para solucionar problemas y validar que los perfiles estén correctamente configurados, que las identidades estén correctamente vinculadas y que los datos se hayan ingerido correctamente. |

Para obtener más información sobre [!DNL Real-time Customer Profile]tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] datos, lea la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto concreto de perfiles describiendo los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Eliminación del límite de segmentación por flujo continuo | Se ha eliminado el límite de siete días para el período retroactivo. |

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación jerárquica | Durante el proceso de ingestión de datos, puede realizar la previsualización de un archivo de origen jerárquico, como JSON o Parquet. |
| Compatibilidad con autenticación SSH para SFTP | Puede conectar su cuenta SFTP con [!DNL Platform] las claves RSA/DSA Open SSH. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Mejoras en los recursos | Puede habilitar el conjunto de datos para [!DNL Profile] durante el proceso de ingesta de datos. Consulte el tutorial de flujo de trabajo [de flujo de datos de almacenamiento de](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) nube para obtener más información. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.

## Tiempo hasta el valor {#time-to-value}

Adobe Experience Platform permite a los equipos de operaciones de marketing crear una vista de 360 grados de sus clientes sin necesidad de contar con una amplia experiencia en ingeniería de datos. El objetivo es acelerar los equipos y el valor a través de la velocidad de los datos.

&quot;Tiempo de respuesta al valor&quot; va de una persona a otra. Los ingenieros de datos pueden completar tareas de manera eficiente y acelerada con transparencia en la actividad de datos, de modo que antes se disponga de un perfil de clientes robusto y escalable en tiempo real. Los especialistas en marketing pueden utilizar el perfil completo y sólido del cliente para la segmentación y la activación.

### Elementos destacados de las funciones

#### Esquema

Actualiza la facilidad de uso y el flujo de trabajo, y proporciona perspectivas integradas, estandarización y transparencia de los campos clave dentro de las composiciones de esquema. Expone el linaje de datos para la combinación de modelos de datos individuales representados como el &quot;esquema de unión&quot;, proporcionando una perspectiva de la estructura y los ingredientes para el Perfil del cliente en tiempo real.

- Actualización del flujo de trabajo de esquema
   - Utilice métodos abreviados para el tipo más común de esquemas XDM, con la configuración automatizada en el editor de esquemas y la combinación de recomendaciones en función de sus objetivos
   - Aumente la eficacia del flujo de trabajo con selección y previsualización de varias mezclas
   - Proporcionar transparencia en los atributos clave de la composición de esquemas, incluidos la identidad, la relación y los campos obligatorios y obsoletos
- Transparencia de la línea de datos y los atributos clave del Esquema de unión

#### Recopilación e inserción de datos

La asignación automática, la previsualización de asignación y la actualización de uso aportan datos de cualquier plataforma o fuente para su uso en perfil, segmentación posterior y activación. El sistema cuenta con la eficiencia y la inteligencia necesarias para facilitar el uso de este proceso, incluso para personas ajenas a TI.

- Acceso más fácil a las fuentes de datos con la tarjeta de página de catálogo y la actualización del patrón de acciones en línea de la tabla de datos
- Campo/expresión calculada para la ingesta de datos
- Las recomendaciones de asignación de datos aceleran el proceso de ingestión
- Asignación de previsualizaciones y validaciones

#### Configuración de perfil

El visor de perfil compatible con el mercado y la personalización le ayuda a comprender la composición de un perfil para utilizarlo en casos de segmentación, planificación y activación. El flujo de trabajo consolidado hidrata el perfil de forma controlada y eficaz, proporcionando un flujo de trabajo paso a paso para la política de combinación.

- Vista cada perfil individual en un visor de perfil mejorado que muestra un panel con personalización total, lo que permite agrupar los datos de canales cruzados en función de los objetivos comerciales de los especialistas en marketing.
- Edite atributos estándar y personalizados en la utilidad Información básica, según las necesidades comerciales.
- Personalice utilidades con atributos del perfil del cliente en tiempo real mediante el selector de esquemas de unión. El esquema de unión se deriva de los modelos de datos subyacentes utilizados en la ingestión de datos de perfil.


#### Monitoreo

Garantiza la transparencia del flujo de datos y proporciona una perspectiva sobre el estado del tráfico de datos en el sistema desde los conectores de origen, lo que proporciona un mayor autoservicio y una mayor capacidad de acción para solucionar problemas.

- Supervisar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de ejecución, la lista de archivos procesados, los errores y los diagnósticos procesables