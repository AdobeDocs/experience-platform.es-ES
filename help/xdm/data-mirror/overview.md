---
keywords: Experience Platform;réplica de datos;esquema relacional;cambiar captura de datos;sincronización de base de datos;clave principal;relaciones
solution: Experience Platform
title: Información general de Data Mirror
description: Descubra cómo Data Mirror permite la ingesta de cambios a nivel de fila desde bases de datos externas a Adobe Experience Platform mediante esquemas relacionales con exclusividad, relaciones y versiones forzadas.
badge: Disponibilidad limitada
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Información general de Data Mirror

>[!AVAILABILITY]
>
>Los esquemas relacionales y de Data Mirror están disponibles para los titulares de licencias de **campañas orquestadas** de Adobe Journey Optimizer. También están disponibles como una **versión limitada** para los usuarios de Customer Journey Analytics, según su licencia y la habilitación de características. Póngase en contacto con su representante de Adobe para obtener acceso.

Data Mirror es una funcionalidad de Adobe Experience Platform que permite la ingesta de cambios a nivel de fila desde bases de datos externas al lago de datos mediante esquemas relacionales. Conserva las relaciones de datos, fuerza la exclusividad y admite el control de versiones sin requerir procesos de extracción, transformación y carga (ETL) en sentido ascendente.

Utilice Data Mirror para sincronizar inserciones, actualizaciones y eliminaciones (datos mutables) de sistemas externos como [!DNL Snowflake], [!DNL Databricks] o [!DNL BigQuery] directamente en Experience Platform. Esto le ayuda a preservar la estructura y la integridad de los datos del modelo de base de datos existente a medida que introduce datos en Platform.

## Capacidades y ventajas

Data Mirror proporciona las siguientes funciones esenciales para la sincronización de bases de datos:

* **Aplicación de clave principal**: garantiza la exclusividad en los conjuntos de datos y evita registros duplicados durante la ingesta.
* **Ingesta de cambios a nivel de fila**: admite cambios de datos granulares, incluidas actualizaciones y eliminaciones con control de precisión.
* **Relaciones de esquema**: habilita las relaciones de clave externa y principal entre conjuntos de datos mediante descriptores.
* **Control de eventos desordenados**: los procesos cambian eventos utilizando descriptores de versión y marca de tiempo, incluso cuando llegan fuera de secuencia.
* **Integración directa con el almacén**: se conecta con almacenes de datos en la nube compatibles para sincronizar los cambios casi en tiempo real.

Utilice Data Mirror para introducir cambios directamente desde los sistemas de origen, aplicar la integridad del esquema y hacer que los datos estén disponibles para los flujos de trabajo de análisis, orquestación de recorrido y conformidad. Data Mirror elimina los procesos complejos de ETL ascendentes y acelera la implementación al permitir la duplicación directa de los modelos de base de datos existentes.

Planifique los requisitos de eliminación e higiene de los datos al implementar esquemas relacionales con Data Mirror. Todas las aplicaciones deben considerar cómo las eliminaciones afectan a los conjuntos de datos relacionados, los flujos de trabajo de conformidad y los procesos descendentes antes de la implementación.

## Requisitos previos {#prerequisites}

Antes de empezar, debe comprender los siguientes componentes de Experience Platform y confirmar que su entorno cumple los requisitos técnicos y estructurales:

* [Crear esquemas en la interfaz de usuario de Experience Platform](../ui/resources/schemas.md) o [API](../api/schemas.md)
* [Configurar conexiones de origen en la nube](../../sources/home.md#cloud-storage)
* [Aplicar cambiar conceptos de captura de datos](../../sources/tutorials/api/change-data-capture.md) (actualizaciones y eliminaciones)
* Distinguir entre [esquemas estándar](../schema/composition.md) y [esquemas relacionales](../schema/relational.md)
* [Definir relaciones estructurales con descriptores](../api/descriptors.md)

### Requisitos de implementación

La instancia de Platform y los datos de origen deben cumplir con requisitos específicos para que Data Mirror funcione correctamente. Data Mirror requiere **esquemas relacionales**, que son estructuras de datos flexibles con restricciones forzadas.

Incluya una **clave principal y un descriptor de versión** en todos los esquemas. Si está trabajando con un esquema de serie temporal, también se requiere un **descriptor de marca de tiempo**.

La base de datos externa debe admitir la captura de datos modificados o proporcionar metadatos que identifiquen las inserciones, actualizaciones y eliminaciones. Los datos de Source deben incluir **identificadores únicos**, ya sea un solo campo o una clave principal compuesta e **información de la versión** para que el sistema pueda aplicar las actualizaciones en el orden correcto.

Para detectar eliminaciones, agregue una columna `_change_request_type` que especifique si cada registro es una actualización o una eliminación.

## Implementación de Data Mirror {#implementation-workflow}

A diferencia de los enfoques de ingesta estándar, Data Mirror conserva la estructura del modelo de base de datos dentro del lago de datos de Experience Platform. Esta coherencia de la estructura de datos elimina la necesidad de preprocesamiento externo. A continuación se muestra un flujo de trabajo de implementación de alto nivel de Data Mirror. Elija el método de implementación en función del flujo de trabajo y el sistema de origen de su equipo.

### Definición de la estructura de esquema

Cree [esquemas relacionales](../schema/relational.md) con los descriptores necesarios (metadatos que definen el comportamiento y las restricciones del esquema). Elija un método que se ajuste al flujo de trabajo de su equipo, ya sea a través de la interfaz de usuario o directamente a través de la API.

* **Enfoque de interfaz de usuario**: [Crear esquemas relacionales en el Editor de esquemas](../ui/resources/schemas.md#create-relational-schema)
* **Enfoque de API**: [Crear esquemas a través de la API del Registro de esquemas](../api/schemas.md#create-relational-schema)

### Asignación de relaciones y definición de administración de datos

Defina conexiones entre conjuntos de datos mediante descriptores de relación. Administre relaciones y mantenga la calidad de los datos en todos los conjuntos de datos. Estas tareas garantizan uniones coherentes y admiten el cumplimiento de los requisitos de higiene de los datos.

* **Relaciones de esquema**: [Defina relaciones entre conjuntos de datos mediante descriptores](../api/descriptors.md)
* **Higiene de registros**: [Administrar eliminaciones de registros de precisión para conjuntos de datos basados en esquemas relacionales](../../hygiene/ui/record-delete.md#relational-record-delete)

### Configuración de la conexión de origen

Seleccione un método de ingesta basado en el sistema de origen y el caso de uso. Cada opción admite diferentes niveles de automatización, transformación y escalabilidad.

* [**Configurar conexiones de origen en la nube**](../../sources/home.md#cloud-storage)
* **Ingesta de SQL**: use Data Distiller para escribir en conjuntos de datos relacionales
* [**Carga de archivos**](../ui/resources/schemas.md#upload-ddl-file): Cargue archivos manualmente para la ingesta por lotes o única

### Habilitar la ingesta de captura de datos modificados

Configure las conexiones de captura de datos modificados con los almacenes de datos en la nube admitidos. Introduzca cambios de nivel de fila manteniendo la exclusividad y aplicando actualizaciones en el orden correcto.

* **Cambiar captura de datos**: [Habilitar la captura de datos modificados en las conexiones de origen](../../sources/tutorials/api/change-data-capture.md)

## Casos de uso comunes {#use-cases}

Revise los casos de uso comunes que se enumeran a continuación, en los que Data Mirror admite la sincronización de datos precisa y la preservación de relaciones. Cada escenario muestra cómo Data Mirror admite las necesidades comerciales comunes en análisis, orquestación y conformidad.

### Modelado de datos relacionales

Use [esquemas relacionales](../schema/relational.md) en Data Mirror para representar entidades, insertar procesos, actualizar y eliminar en el nivel de fila y mantener las relaciones de clave principal y externa que existen en los orígenes de datos. Este enfoque incorpora los principios de modelado de datos relacionales a Experience Platform y garantiza la coherencia estructural en todos los conjuntos de datos.

### Sincronización de almacén a lago

Datos de evento espejo, registros de interacción de clientes, eventos de campaña y datos auxiliares de los almacenes de datos de nube admitidos en Experience Platform. Esto admite la idoneidad de la campaña, la precisión de la segmentación y la secuencia de mensajes. Journey Optimizer y Real-Time CDP B2B confían en esto para la lógica de orquestación casi en tiempo real.

### Integración de Customer Journey Analytics

Sincronice eventos de series de tiempo como clics web, vistas de productos, compras y admita interacciones de sistemas como centros de llamadas o registros de chat. Un historial de cambios completo admite un análisis de tendencias y una segmentación de comportamiento precisos. Experience Platform Data Mirror para Customer Journey Analytics utiliza esto para reflejar las actualizaciones y eliminaciones de los sistemas de origen.

### Modelado de relaciones B2B

Conservar relaciones como jerarquías de cuenta a contacto, suscripción a cuenta o contacto a región. Estos admiten la segmentación, la puntuación de posibles clientes, el seguimiento de oportunidades y la coordinación multicanal. A diferencia de la ingesta estándar que aplana las relaciones, Data Mirror las mantiene de forma nativa mediante descriptores para un modelado más preciso.

### Administración de suscripciones

Rastree eventos como renovaciones, cancelaciones, actualizaciones, rebajas de categoría y cambios de plan con un historial completo de versiones. Esto admite campañas de retención, predicción de pérdidas y segmentación basada en el ciclo vital. El historial completo permite obtener perspectivas de comportamiento y una segmentación precisa.

### Operaciones de higiene de datos

Utilice la captura de datos de cambio para permitir eliminaciones precisas a nivel de registro para flujos de trabajo de cumplimiento (por ejemplo, industrias reguladas) y limpieza. Data Mirror aplica las eliminaciones con precisión mientras preserva los datos relacionados en todos los conjuntos de datos conectados.

## Consideraciones importantes {#considerations}

Revise estas consideraciones clave para asegurarse de que la implementación se alinea con los comportamientos de esquema, los métodos de ingesta y los patrones de relación admitidos. Una planificación adecuada ayuda a evitar problemas de integración y garantiza un modelado de datos preciso.

### Requisitos de higiene y eliminación de datos

Todas las aplicaciones que utilizan esquemas relacionales y Data Mirror deben comprender las implicaciones de la eliminación de datos. Los esquemas relacionales permiten eliminaciones precisas a nivel de registro que pueden afectar a los datos relacionados en todos los conjuntos de datos conectados. Estas funciones de eliminación afectan a la integridad de los datos, el cumplimiento normativo y el comportamiento de las aplicaciones posteriores independientemente de su caso de uso específico. Revise los [requisitos de higiene de datos para conjuntos de datos basados en esquemas relacionales](../../hygiene/ui/record-delete.md#relational-record-delete) y planifique escenarios de eliminación antes de la implementación.

### Selección del comportamiento del esquema

Los esquemas relacionales tienen el valor predeterminado **comportamiento de registro**, que captura el estado de la entidad (clientes, cuentas, etc.). Si necesita **comportamiento de la serie temporal** para el seguimiento de eventos, debe configurarlo explícitamente.

### Comparación del método de ingesta

Utilice esta tabla de comparación para elegir el mejor método de ingesta para sus necesidades de datos, ya sea que requiera sincronización en tiempo real, transformación basada en SQL o cargas manuales de archivos.

| Método de ingesta | Caso de uso |
| ----------------------- | -------------------------------------------------------------- |
| **Cambiar captura de datos** | Sincronización en tiempo real desde almacenes en la nube compatibles |
| **Distiller de datos** | Flujos de trabajo de ingesta y transformación basados en SQL |
| **Carga de archivo** | Ingesta por lotes/manual cuando la integración de origen no está disponible |

### Limitaciones de relaciones

Data Mirror admite relaciones **uno a uno** y **varios a uno** mediante descriptores. Las relaciones **varios a varios** requieren un modelado adicional y no se admiten directamente.

## Próximos pasos

Después de revisar esta descripción general, debería poder determinar si Data Mirror se ajusta a su caso de uso y comprender los requisitos para la implementación. Para empezar:

1. **Los arquitectos de datos** deben evaluar su modelo de datos para asegurarse de que admite claves principales, versiones y capacidades de seguimiento de cambios.
2. **Las partes interesadas empresariales** deben confirmar que su licencia incluye compatibilidad con esquemas relacionales y las ediciones de Experience Platform requeridas.
3. **Los diseñadores de esquemas** deben planificar la estructura de esquemas para identificar los descriptores, las relaciones de campo y las necesidades de control de datos que se requieran.
4. **Los equipos de implementación** deben elegir un método de ingesta basado en sus sistemas de origen, requisitos en tiempo real y flujos de trabajo operativos.

Para obtener detalles de implementación, consulte la [documentación de esquemas relacionales](../schema/relational.md).
