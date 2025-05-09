---
title: 'Notas de la versión de Adobe Experience Platform: octubre de 2020'
description: Las notas de la versión de octubre de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 16%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: jueves, 14 de octubre de 2020**

- [Preparación de los datos](#data-prep)
- [Perfil del cliente en tiempo real](#profile)
- [Servicio de segmentación](#segmentation)
- [Fuentes](#sources)
- [Tiempo hasta el valor](#time-to-value)

## Preparación de los datos {#data-prep}

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Función `is_set` | La función `is_set` le permite comprobar la presencia de un atributo en los datos de origen. `is_set` se puede usar en combinación con `is_empty` para comprobar tanto la presencia del atributo como la presencia del valor dentro del atributo. |
| Función `get_values` | La función `get_values` le permite obtener los valores del mapa de entrada para cualquier clave determinada. |

Para obtener más información, lea [Resumen de la preparación de datos](../../data-prep/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos de clientes dispares en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

| Función | Descripción |
| ------- | ----------- |
| Adiciones a API de previsualización de perfil | La API de vista previa de perfil (`/previewsamplestatus`) ahora incluye la capacidad de ver un desglose del total de fragmentos de perfil en su organización, así como la distribución de fragmentos de perfil en áreas de nombres de identidad. |
| Actualizaciones de vista de esquema de unión | En la interfaz de usuario de Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad de solucionar problemas y validar que los perfiles están correctamente configurados, las identidades están correctamente vinculadas y los datos se han introducido correctamente. |

Para obtener más información sobre [!DNL Real-Time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con datos de [!DNL Profile], lea la [descripción general del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API RESTful que le permiten generar segmentos y audiencias a partir de los datos de [!DNL Real-Time Customer Profile]. Estos segmentos se configuran centralmente y se mantienen en [!DNL Experience Platform], lo que hace que cualquier aplicación de Adobe pueda acceder a ellos fácilmente.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Eliminación del límite de segmentación de streaming | Se ha eliminado el límite de siete días para el período retroactivo. |

Para obtener más información sobre [!DNL Segmentation Service], consulte [Resumen de segmentación](../../segmentation/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con autenticación SSH para SFTP | Puede conectar su cuenta SFTP a [!DNL Experience Platform] mediante claves SSH abiertas RSA/DSA. Consulte la [descripción general de SFTP](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |
| Mejoras de UX | Puede habilitar su conjunto de datos para [!DNL Profile] durante el proceso de ingesta de datos. Consulte el tutorial de [flujo de trabajo de flujo de datos de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).

## Tiempo hasta el valor {#time-to-value}

Adobe Experience Platform permite a los equipos de Operaciones de marketing obtener una vista de 360 grados de sus clientes sin necesidad de tener una amplia experiencia en ingeniería de datos. El objetivo es acelerar los equipos y el valor a través de la velocidad de datos.

&quot;Tiempo de respuesta al valor&quot; se aplica a todas las personas. Los ingenieros de datos pueden completar las tareas de forma eficiente y acelerada con transparencia de actividad de datos, de modo que un perfil de cliente en tiempo real sólido y escalable esté disponible antes. Los especialistas en marketing pueden utilizar el perfil de cliente completo y sólido para la segmentación y la activación.

### Resaltados de funciones

#### Esquema

Actualiza la capacidad de uso y el flujo de trabajo, y proporciona perspectivas, estandarización y transparencia predeterminadas de campos clave dentro de composiciones de esquema. Expone el linaje de datos para la combinación de modelos de datos individuales representados como el &quot;esquema de unión&quot;, lo que proporciona insight en la estructura y los ingredientes del perfil del cliente en tiempo real.

- Actualización del flujo de trabajo del esquema
   - Utilice métodos abreviados para el tipo más común de esquemas XDM, con configuración automatizada en el editor de esquemas y recomendaciones de grupos de campos de esquema en función de sus objetivos
   - Aumente la eficacia del flujo de trabajo con la selección de varios grupos de campos y la capacidad de previsualización
   - Proporcionar transparencia en los atributos clave de la composición del esquema, incluidos la identidad, la relación y los campos obligatorios y obsoletos
- Transparencia de Linaje de datos de esquema de unión y Atributos clave

#### Ingesta y recopilación de datos

La asignación automática, la previsualización de asignación y la actualización de la facilidad de uso traen datos de cualquier plataforma o fuente para su uso en perfiles, segmentación descendente y activación. El sistema tiene la eficiencia y la inteligencia necesarias para facilitar el uso de este proceso, incluso para personas ajenas a la tecnología informática.

- Acceso más fácil a las fuentes de datos con la tarjeta de página del catálogo y la actualización del patrón de acción en línea de la tabla de datos
- Campo/expresión calculado para la ingesta de datos
- Las recomendaciones de asignación de datos aceleran el proceso de ingesta
- Previsualización y validaciones de asignaciones

#### Configuración de perfil

El visualizador de perfiles fácil de personalizar le ayuda a comprender la composición de un perfil para utilizarlo en casos de segmentación, planificación y activación. El flujo de trabajo consolidado hidrata el perfil de forma controlada y eficaz al proporcionar un flujo de trabajo paso a paso para la política de combinación.

- Vea cada perfil individual en un visor de perfiles mejorado que muestra un panel con personalización completa, lo que permite agrupar los datos en canales múltiples en función de los objetivos comerciales del experto en marketing.
- Edite atributos estándar y personalizados en el widget de información básica, según las necesidades de la empresa.
- Personalice widgets con atributos del perfil del cliente en tiempo real, utilizando el selector de esquema de unión. El esquema de unión se deriva de los modelos de datos subyacentes utilizados dentro de la ingesta de datos de perfil.


#### Monitorización

Garantiza la transparencia del flujo de datos y proporciona a insight información sobre el estado del tráfico de datos en el sistema desde los conectores de origen, lo que proporciona un autoservicio más rápido y una capacidad de acción más rápida para solucionar situaciones.

- Supervise todas las ejecuciones de flujo y vea una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y los diagnósticos procesables
