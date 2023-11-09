---
title: Empaquetado de servicio de consultas
description: En el siguiente documento se describe el empaquetado de las funciones y los productos disponibles para el servicio de consultas, y se destacan las diferencias entre las consultas ad hoc y por lotes.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 2%

---

# Empaquetado del servicio de consultas

Este documento describe los diferentes tipos de empaquetado y las funciones de ejecución de consultas disponibles en el servicio de consultas.

Adobe Experience Platform Query Service se puede dividir en dos funcionalidades basadas en los patrones de consulta que se pueden ejecutar:

- **Consultas ad hoc** son consultas SQL que se utilizan para explorar conjuntos de datos ingeridos para la verificación, validación, experimentación, etc. Estas consultas no escriben datos de nuevo en el lago de datos de Platform.
- **Consultas por lotes** son consultas SQL utilizadas para realizar el procesamiento posterior a la ingesta de conjuntos de datos ingeridos. Estas consultas limpian, modelan, manipulan y enriquecen los datos, cuyos resultados se escriben de nuevo en el lago de datos de Platform. Estas consultas se pueden programar, administrar y supervisar como trabajos por lotes.

Las funcionalidades del servicio de consulta están empaquetadas con los siguientes productos y complementos:

- **Aplicaciones basadas en la plataforma** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics y Adobe Journey Optimizer): El acceso al servicio de consultas para ejecutar consultas ad hoc se proporciona desde el principio con cada variación y nivel de aplicaciones basadas en Platform.
- **[!DNL Data Distiller]** (paquete de complementos que se puede adquirir con Adobe Real-Time CDP, Customer Journey Analytics y Adobe Journey Optimizer): El acceso al servicio de consultas para ejecutar consultas por lotes se proporciona con [!DNL Data Distiller].

## Terminología {#terminology}

En la siguiente sección se proporcionan definiciones de términos clave relacionados con el empaquetado del servicio de consultas:

- **Almacenamiento del lago de datos**: el lago de datos sirve principalmente para los siguientes propósitos:
   - Actúa como zona de ensayo para la incorporación de datos en Experience Platform;
   - Actúa como almacenamiento de datos a largo plazo para todos los datos del Experience Platform;
   - Habilita casos de uso, como análisis de datos y ciencia de datos.
- **Exportación de datos**: La [conjunto de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=es) tipos que puede exportar según la aplicación, el nivel de producto y los complementos adquiridos. Los conjuntos de datos derivados se pueden crear mediante el complemento Query Service Data Distiller y se pueden [exportado desde Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activation-overview.html) a una amplia gama de destinos, incluidos [destinos de almacenamiento en la nube](/help/destinations/ui/export-datasets.md).
- **Consultas aceleradas**: Las consultas aceleradas devuelven resultados basados en datos agregados para reducir el tiempo de espera de los resultados y proporcionar un intercambio de información más interactivo. Las consultas sin estado realizadas en el almacén acelerado solo están disponibles como parte del complemento Data Distiller.
- **Calcular horas**: las horas calculadas son la métrica utilizada para rastrear el análisis y la escritura de datos con consultas por lotes mediante la API del servicio de consultas. Se calcula en horas al año y se mide en todas las zonas protegidas. El número de horas de Compute proporcionadas a su organización se define en el proceso de creación de ámbitos del acuerdo.

## Derechos {#entitlements}

En la tabla siguiente se describen los derechos clave del servicio de consulta en función de cómo se empaquetan:

| Derecho de servicio de consulta | Empaquetado con aplicaciones basadas en Platform | Empaquetado con [!DNL Data Distiller] |
|---|---|---|
| Patrón de consulta admitido | Solo consultas Ad hoc | Consulta por lotes |
| Caso de uso admitido | <ul><li>Exploración&#x200B;</li><li>Detección de datos&#x200B;</li><li>Validación de datos</li><li>Experimentación</li></ul> | <ul><li>Limpieza</li><li>Forma</li><li>Manipulación</li><li>Enriquecimiento</li></ul> |
| Semántica admitida | <ul><li>SELECCIONAR consultas</li></ul> | <ul><li>Consultas CTAS e ITAS</li></ul> |
| Tiempo máximo de ejecución | 10 minutos | 24 horas |
| Métrica de licencia | **Consulta de concurrencia de usuarios**: <ul><li>1 usuario simultáneo (Real-Time CDP, Adobe Journey Optimizer)&#x200B;</li><li>5 usuarios simultáneos (Customer Journey Analytics)&#x200B;</li></ul> **Concurrencia de consultas**: <ul><li>1 consulta en ejecución simultánea (todas las aplicaciones)&#x200B;</li></ul> **Complemento del paquete de usuarios de consultas ad hoc adicionales** puede adquirirse para aumentar los derechos de consulta ad hoc autorizados de los clientes. <ul><li>+5 usuarios simultáneos adicionales por paquete</li><li>+1 consulta en ejecución simultánea adicional por paquete</li></ul> | **Calcular horas**: <ul><li>Variable (con ámbito basado en los derechos de aplicación del cliente)</li></ul> **Calcular horas** es una medida de la cantidad de tiempo que el motor del servicio de consultas tarda en leer, procesar y escribir datos en el lago de datos cuando se ejecuta una consulta por lotes. |
| Uso acelerado de consultas e informes | No | Sí: las consultas aceleradas simultáneas le permiten leer datos del almacén acelerado y mostrarlos dentro de los paneles. También se proporciona una asignación de derechos dedicada para almacenar modelos de informes y conjuntos de datos en el almacén acelerado. |
| Capacidad de almacenamiento del lago de datos | Sí, el total de derechos de almacenamiento depende de las licencias de las aplicaciones basadas en la plataforma. Por ejemplo, Real-Time CDP, AJO, CJA, etc. | Sí: se proporciona un derecho de almacenamiento adicional para mantener los conjuntos de datos sin procesar y derivados para casos de uso de Data Distiller más allá de una fecha de caducidad de datos de siete días.<br>La capacidad de almacenamiento del lago de datos se mide en terabytes (TB) y depende de la cantidad de horas de Compute que haya comprado. |
| Asignación de exportación de datos | Sí: el derecho total a la exportación depende de las licencias de las aplicaciones basadas en la plataforma. Por ejemplo, Real-Time CDP, AJO, CJA, etc. | Sí: se proporcionan derechos de exportación adicionales para permitir la exportación de conjuntos de datos derivados creados con Data Distiller.<br>Su asignación de exportación de datos anual se mide en terabytes (TB) y depende de la cantidad de horas de Compute que haya comprado. |
| Interfaz de ejecución de consultas | <ul><li>IU del servicio de consultas</li><li>IU de cliente de terceros</li><li>[!DNL PostgresSQL] IU de cliente</li></ul> | <ul><li>IU del servicio de consultas </li><li>IU de cliente de terceros</li><li>[!DNL PostgresSQL] IU de cliente</li><li>API de REST</li></ul> |
| Resultados de consulta devueltos mediante | IU de cliente | Conjunto de datos derivado almacenado en el lago de datos |
| Límite de resultados | <ul><li>IU del servicio de consultas: 100 filas</li><li>Clientes de terceros: 50 000</li><li>[!DNL PostgresSQL] cliente: 50 000</li></ul> | <ul><li>IU del servicio de consultas: el número de filas de salida que se puede [configurado con una configuración de IU](./ui/user-guide.md#result-count) a entre 50 y 500 filas.</li><li>Clientes de terceros (sin límite superior de filas)</li><li>[!DNL PostgresSQL] cliente (sin límite superior de filas)</li><li>API de REST (sin límite superior para filas)</li></ul> |
| Leer capacidad del conjunto de datos | Sí | Sí |
| Escribir capacidad del conjunto de datos | No | Sí |
| Capacidad de programación | No | Sí |
| Monitorización de capacidad | Sí | Sí |
| Capacidad de configuración de alertas de consulta | No | Sí |

{style="table-layout:auto"}

## Control de acceso {#access-control}

El control de acceso del Experience Platform se administra mediante el [Adobe Admin Console](https://adminconsole.adobe.com/) donde los perfiles de producto vinculan a los usuarios con permisos y zonas protegidas. Consulte la [información general de control de acceso](../access-control/home.md) para obtener más información.

Para utilizar el servicio de consulta, las API [!DNL Manage Queries] el permiso debe estar habilitado en Admin Console. Este permiso permite a los usuarios ejecutar consultas ad hoc y por lotes. Instrucciones detalladas para solicitar acceso al perfil del producto [!DNL Manage Queries] Los permisos de se han descrito en [administración de permisos para un perfil de producto](../access-control/ui/permissions.md) y [administración de usuarios para un perfil de producto](../access-control/ui/users.md) documentos.

Después de comprar el [!DNL Data Distiller] complemento, el complemento [!DNL Write Dataset] se debe conceder el permiso. Este permiso permite [!DNL Data Distiller] para ejecutar consultas por lotes.

En la tabla siguiente se describen los efectos del [!DNL Manage Queries] permiso:

| Permiso | Función |
|---|---|
| [!DNL Manage Queries] (sin permiso de escritura de datos) | Proporciona acceso para ejecutar consultas Ad hoc |
| [!DNL Manage Queries] (con permiso de escritura de datos) | Proporciona acceso para ejecutar consultas por lotes |

{style="table-layout:auto"}

## Compatibilidad con zona protegida {#sandbox-support}

Las zonas protegidas son particiones virtuales en una sola instancia de Experience Platform. Cada instancia de Platform admite varios entornos limitados de producción y sin producción, cada uno con su propia biblioteca de recursos de Platform. Los entornos limitados que no son de producción le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre los entornos limitados, consulte [información general sobre zonas protegidas](../sandboxes/home.md). Todos los derechos del servicio de consulta se comparten en todas las zonas protegidas.

## Pasos siguientes

Al leer este documento, debería comprender mejor los diferentes tipos de empaquetado y las capacidades de ejecución de consultas disponibles en el servicio de consultas. Para obtener más información sobre el servicio de consultas, como los casos de uso más conocidos del sector, lea la [documentación de casos de uso](./use-cases/abandoned-browse.md). Para obtener información más general, visite la [Introducción al servicio de consultas](./home.md).
