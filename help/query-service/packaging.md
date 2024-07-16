---
title: Empaquetado de servicio de consultas
description: En el siguiente documento se describe el empaquetado de las funciones y los productos disponibles para el servicio de consultas, y se destacan las diferencias entre las consultas ad hoc y por lotes.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 1e18a60478e2755f49d37d4d3bf4bd3ca6dbf23b
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---

# Empaquetado del servicio de consultas

Este documento describe los diferentes tipos de empaquetado y las funciones de ejecución de consultas disponibles en el servicio de consultas.

Adobe Experience Platform Query Service se puede dividir en dos funcionalidades basadas en los patrones de consulta que se pueden ejecutar:

- **Las consultas Ad hoc** son consultas SQL que se usan para explorar conjuntos de datos ingeridos con fines de verificación, validación, experimentación, etc. Estas consultas no escriben datos de nuevo en el lago de datos de Platform.
- **Las consultas por lotes** son consultas SQL utilizadas para realizar el procesamiento posterior a la ingesta de conjuntos de datos ingeridos. Estas consultas limpian, modelan, manipulan y enriquecen los datos, cuyos resultados se escriben de nuevo en el lago de datos de Platform. Estas consultas se pueden programar, administrar y supervisar como trabajos por lotes.

Las funcionalidades del servicio de consulta están empaquetadas con los siguientes productos y complementos:

- **Aplicaciones basadas en la plataforma** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics y Adobe Journey Optimizer): el acceso al servicio de consultas para ejecutar consultas ad hoc se proporciona desde el principio con cada variación y nivel de las aplicaciones basadas en la plataforma.
- **[!DNL Data Distiller]** (paquete de complementos que se puede comprar con Adobe Real-Time CDP, Customer Journey Analytics y Adobe Journey Optimizer): el acceso al servicio de consultas para ejecutar consultas por lotes se proporciona con [!DNL Data Distiller].

## Derechos {#entitlements}

En la tabla siguiente se describen los derechos clave del servicio de consulta en función de cómo se empaquetan:

| Derecho de servicio de consulta | Empaquetado con aplicaciones basadas en Platform | Empaquetado con [!DNL Data Distiller] |
|---|---|---|
| Patrón de consulta admitido | Solo consultas Ad hoc | Consulta por lotes |
| Caso de uso admitido | <ul><li>Exploración&#x200B;</li><li>Detección de datos&#x200B;</li><li>Validación de datos</li><li>Experimentación</li></ul> | <ul><li>Limpieza</li><li>Forma</li><li>Manipulación</li><li>Enriquecimiento</li></ul> |
| Semántica admitida | <ul><li>SELECCIONAR consultas</li></ul> | <ul><li>Consultas CTAS e ITAS</li></ul> |
| Tiempo máximo de ejecución | 10 minutos | 24 horas |
| Métrica de licencia | **Concurrencia de usuario de consulta**: <ul><li>1 usuario simultáneo (Real-Time CDP, Adobe Journey Optimizer)&#x200B;</li><li>5 usuarios simultáneos (Customer Journey Analytics)&#x200B;</li></ul> **Concurrencia de consulta**: <ul><li>1 consulta en ejecución simultánea (todas las aplicaciones)&#x200B;</li></ul> **Se puede comprar un complemento adicional del paquete de usuarios de consultas ad hoc** para aumentar sus derechos de consulta ad hoc autorizados. <ul><li>+5 usuarios simultáneos adicionales por paquete</li><li>+1 consulta en ejecución simultánea adicional por paquete</li></ul> | **Calcular horas**: <ul><li>Variable (con ámbito basado en sus derechos de aplicación)</li></ul> **Calcular horas** es una medida del tiempo que tarda el motor del servicio de consultas en leer, procesar y escribir datos en el lago de datos cuando se ejecuta una consulta por lotes. <br>Con el SKU de Data Distiller, también obtiene la concurrencia de un usuario y una consulta adicionales, que pueden utilizarse para ejecutar consultas Ad hoc.  El SKU de Data Distiller incluye:<br><ul><li>+5 usuarios simultáneos adicionales</li><li>+1 consulta adicional en ejecución simultánea</li></ul> |
| Uso acelerado de consultas e informes | No | Sí: las consultas aceleradas simultáneas le permiten leer datos del almacén acelerado y mostrarlos dentro de los paneles. También se proporciona una asignación de derechos dedicada para almacenar modelos de informes y conjuntos de datos en el almacén acelerado. |
| Capacidad de almacenamiento del lago de datos | El derecho total de almacenamiento depende de las licencias de las aplicaciones basadas en la plataforma. Por ejemplo, Real-Time CDP, AJO, CJA, etc. | Sí: se proporciona un derecho de almacenamiento adicional para mantener los conjuntos de datos sin procesar y derivados para casos de uso de Data Distiller más allá de una fecha de caducidad de datos de siete días.<br>La capacidad de almacenamiento de su lago de datos se mide en terabytes (TB) y depende de la cantidad de horas de Compute que haya comprado. Consulte la descripción del producto para obtener más detalles. |
| Asignación de exportación de datos | El derecho total a la exportación depende de las licencias de las aplicaciones basadas en la plataforma. Por ejemplo, Real-Time CDP, AJO, CJA, etc. | Sí: se proporciona un derecho de exportación adicional para permitir la exportación de conjuntos de datos derivados creados con Data Distiller.<br>Su asignación de exportación de datos anual se mide en terabytes (TB) y depende de la cantidad de horas de Compute que haya comprado. Consulte la descripción del producto para obtener más información. |
| Interfaz de ejecución de consultas | <ul><li>IU del servicio de consultas</li><li>IU de cliente de terceros</li><li>IU de cliente [!DNL PostgresSQL]</li></ul> | <ul><li>IU del servicio de consultas </li><li>IU de cliente de terceros</li><li>IU de cliente [!DNL PostgresSQL]</li><li>API de REST</li></ul> |
| Resultados de consulta devueltos mediante | IU de cliente | Conjunto de datos derivado almacenado en el lago de datos |
| Límite de resultados | <ul><li>IU del servicio de consultas: el número de filas de salida se puede [configurar con una configuración de IU](./ui/user-guide.md#result-count) entre 50 y 500 filas.</li><li>Clientes de terceros: 50 000</li><li>[!DNL PostgresSQL] cliente: 50 000</li></ul> | Las consultas CTAS e ITAS solo generan mensajes de éxito, ya que el resultado de la consulta se almacena en conjuntos de datos derivados. |
| Leer capacidad del conjunto de datos | Sí | Sí |
| Escribir capacidad del conjunto de datos | No | Sí |
| Capacidad de programación | No | Sí |
| Monitorización de capacidad | Sí | Sí |
| Capacidad de configuración de alertas de consulta | No | Sí |

{style="table-layout:auto"}

## Control de acceso {#access-control}

El control de acceso para el Experience Platform se administra a través de [Adobe Admin Console](https://adminconsole.adobe.com/), donde los perfiles de producto vinculan a los usuarios con permisos y zonas protegidas. Consulte la [descripción general del control de acceso](../access-control/home.md) para obtener más información.

Consulte los documentos [Administrar permisos para un perfil de producto](../access-control/ui/permissions.md) y [Administrar usuarios para un perfil de producto](../access-control/ui/users.md) para obtener instrucciones detalladas sobre cómo solicitar acceso a los permisos del perfil de producto

### Permisos relevantes del servicio de consultas {#query-service-permissions}

Para usar el servicio de consultas, el permiso **[!DNL Manage Queries]** debe estar habilitado en el Admin Console. Este permiso permite a los usuarios ejecutar consultas ad hoc y por lotes.

En la tabla siguiente se describen los efectos del permiso [!DNL Manage Queries]:

| Permiso | Función |
|---|---|
| [!DNL Manage Queries] (sin permiso de escritura de datos) | Proporciona acceso para ejecutar consultas Ad hoc |
| [!DNL Manage Queries] (con permiso de escritura de datos) | Proporciona acceso para ejecutar consultas por lotes |

{style="table-layout:auto"}

### Permisos relevantes de Perspectivas personalizables {#customizable-insights-permissions}

Para crear Data Distiller [Perspectivas personalizables](./data-distiller/customizable-insights/overview.md) en los paneles, los siguientes permisos **deben** estar habilitados en el Admin Console.

| Permiso | Función |
|---|---|
| [!DNL View Custom Dashboard] | Proporciona acceso de visualización a los paneles definidos por el usuario |
| [!DNL Manage Custom Dashboard] | Proporciona acceso de administración para los paneles definidos por el usuario |

{style="table-layout:auto"}

## Compatibilidad con zona protegida {#sandbox-support}

Las zonas protegidas son particiones virtuales en una sola instancia de Experience Platform. Cada instancia de Platform admite varios entornos limitados de producción y sin producción, cada uno con su propia biblioteca de recursos de Platform. Los entornos limitados que no son de producción le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre las zonas protegidas, consulte la [descripción general de las zonas protegidas](../sandboxes/home.md). Todos los derechos del servicio de consulta se comparten en todas las zonas protegidas.

## Pasos siguientes

Al leer este documento, debería comprender mejor los diferentes tipos de empaquetado y las capacidades de ejecución de consultas disponibles en el servicio de consultas. Para obtener más información sobre el servicio de consultas, como los casos de uso conocidos del sector, lea la [documentación del caso de uso](./use-cases/abandoned-browse.md). Para obtener más información general, visite [Introducción al servicio de consultas](./home.md).

