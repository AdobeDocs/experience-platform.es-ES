---
keywords: Experience Platform;consulta;servicio de consultas;solución de problemas;protecciones;directrices;límite;
title: Protecciones para el servicio de consultas
description: Este documento proporciona información sobre los límites de uso de los datos del servicio de consultas para ayudarle a optimizar el uso de las consultas.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Protecciones para el servicio de consultas

Las protecciones son umbrales que guían el uso de los datos y el sistema, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform.
Este documento proporciona límites de uso predeterminados para los datos del servicio de consulta para ayudarle a optimizar el rendimiento del sistema al consultar datos en relación con sus derechos de licencia.

>[!IMPORTANT]
>
>Compruebe sus derechos de licencia en su pedido de ventas y la [descripción del producto](https://helpx.adobe.com/es/legal/product-descriptions.html?lang=es) correspondiente sobre los límites de uso reales, además de esta página de protecciones.

## Requisitos previos

Antes de continuar con este documento, debe comprender bien las definiciones y capacidades clave del servicio de consulta. Se describen a continuación:

* **Consultas ad hoc**: para ejecutar `SELECT` consultas con el fin de explorar, experimentar y validar datos donde los resultados de las consultas **no se almacenan** en el lago de datos.

* **Consultas por lotes**: para ejecutar `INSERT TABLE AS SELECT` y `CREATE TABLE AS SELECT` consultas para limpiar, dar forma, manipular y enriquecer datos. Los resultados de estas consultas **se almacenan** en el lago de datos. La métrica para medir el consumo de esta funcionalidad es horas de cálculo.

* **Usuarios del servicio de consultas**: Los usuarios del servicio de consultas proporcionados con la licencia actual para Customer Journey Analytics, Adobe Real-Time Customer Data Platform o Adobe Journey Optimizer también se pueden usar con Data Distiller. Los usuarios del servicio de consultas se comparten entre las funciones.

* **Usuarios ad hoc**: Los usuarios ad hoc son los que ejecutan consultas ad hoc.

* **Usuarios por lotes**: Los usuarios por lotes son los que ejecutan las consultas por lotes.

* **API de informes**: una API para realizar llamadas de captura de datos (interna o externamente). Los modelos de datos de creación de informes extendidos se derivan de los modelos de datos de creación de informes nativos de Adobe Experience Platform, como el modelo de datos de paneles de Real-Time CDP.

## Tipos de protección

Existen dos tipos de límites predeterminados en este documento:

| Tipo de protección | Descripción |
|----------|---------|
| **Protección de rendimiento (límite leve)** | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso. Al superar las barreras de rendimiento, puede experimentar una degradación y latencia del rendimiento. Adobe no es responsable de esta degradación del rendimiento. Los clientes que exceden de manera consistente una protección de rendimiento pueden optar por licenciar capacidad adicional para evitar la degradación del rendimiento. |
| **Protecciones impuestas por el sistema (límite estricto)** | La interfaz de usuario o la API de Real-Time CDP aplican las protecciones impuestas por el sistema. Estos son límites que no se pueden superar, ya que la IU y la API le bloquearán el acceso o devolverán un error. |

{style="table-layout:auto"}

>[!NOTE]
>
>Los límites predeterminados descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones.

## Protecciones de rendimiento de la entidad principal

Las siguientes tablas proporcionan los límites de protección recomendados y las descripciones para la ejecución de consultas cuando se utiliza un patrón de consulta en particular.

**Consultas ad hoc**

| Barrera | Límite | Tipo de límite | Descripción |
|---|---|---|---|
| Tiempo máximo de ejecución | 10 minutos | Protección impuesta por el sistema | Define el tiempo máximo de salida para una consulta SQL ad hoc. Si se supera el tiempo límite para devolver un resultado, se genera el código de error 53400. |
| Usuarios del servicio de consultas simultáneas | <ul><li>Como se especifica en la descripción del producto de la aplicación.</li><li>+5 (con cada paquete adicional de complementos para usuarios de Ad Hoc Query adquirido)</li></ul> | Protección impuesta por el sistema | Define la cantidad de usuarios que pueden crear sesiones simultáneamente para una organización en particular. Si se supera el límite de concurrencia, el usuario recibe un error de `Session Limit Reached`. |
| Concurrencia de consulta | <ul><li>Como se especifica en la descripción del producto de la aplicación.</li><li>+1 (con cada paquete adicional de SKU del complemento de consulta ad hoc adquirido)</li></ul> | Protección impuesta por el sistema | Define la cantidad de consultas que se pueden ejecutar simultáneamente para una organización en particular. Si se supera el límite de concurrencia, las consultas se ponen en cola. |
| Conector del cliente y límite de salida de resultados | Conector del cliente<ul><li>IU de consulta (100 filas)</li><li>Cliente de terceros (50 000)</li><li>[!DNL PostgresSQL] cliente (50 000)</li></ul> | Protección impuesta por el sistema | El resultado de una consulta se puede recibir mediante los siguientes medios:<ul><li>IU del servicio de consultas</li><li>Cliente de terceros</li><li>cliente [!DNL PostgresSQL]</li></ul>Nota: Añadir una limitación al recuento de salida puede devolver los resultados más rápido. Por ejemplo, `LIMIT 5`, `LIMIT 10`, etc. |
| Resultados devueltos mediante | IU de cliente | N/A | Define cómo se ponen los resultados a disposición de los usuarios. |

{style="table-layout:auto"}

**Consultas por lotes**

| **Protección** | **Límite** | **Tipo de límite** | **Descripción** |
|---|---|---|---|
| Tiempo máximo de ejecución | 24 horas | Protección impuesta por el sistema | Define el tiempo máximo de ejecución para una consulta SQL por lotes.<br>El tiempo de procesamiento de una consulta depende del volumen de datos que se va a procesar y de la complejidad de la consulta. |
| Usuarios del servicio de consultas simultáneas para lote no programado | <ul><li>Como se especifica en la descripción del producto de la aplicación.</li><li>+5 (con cada paquete adicional de complementos para usuarios de Ad Hoc Query adquirido)</li></ul> | Protección impuesta por el sistema | Para consultas por lotes no programadas (por ejemplo, consultas CTAS/ITAS en modo interactivo), define cuántos usuarios pueden crear sesiones simultáneamente para una organización en particular. Si se supera el límite de concurrencia, el usuario recibe un error de `Session Limit Reached`. |
| Usuarios del servicio de consultas simultáneas para el lote programado | Sin limitación de usuarios | N/A | Las consultas por lotes programadas son trabajos asincrónicos, por lo que no hay limitación de usuario. |
| Horas computacionales para el procesamiento de datos por lotes | Como se especifica en el pedido de ventas de SKU personalizado de Adobe Experience Platform Intelligence Query del cliente | Protección de rendimiento | Define la cantidad de ámbito de tiempo de cálculo por año que se permite a un cliente ejecutar consultas por lotes para analizar, procesar y escribir datos de nuevo en el lago de datos. |
| Concurrencia de consulta | Admitido | N/A | Las consultas por lotes programadas son trabajos asincrónicos, por lo que se admiten consultas simultáneas. |
| Conector del cliente y límite de salida de resultados | Conector del cliente<ul><li>IU de consulta (sin límite superior de filas)</li><li>Cliente de terceros (sin límite superior de filas)</li><li>[!DNL PostgresSQL] cliente (sin límite superior de filas)</li><li>API de REST (sin límite superior para filas)</li></ul> | Protección impuesta por el sistema | El resultado de una consulta puede estar disponible mediante los siguientes métodos:<ul><li>Se puede almacenar como conjuntos de datos derivados</li><li>Se puede insertar en los conjuntos de datos derivados existentes</li></ul>Nota: No hay límite superior para el número de recuento de registros del resultado de la consulta. |
| Resultados devueltos mediante | Conjunto de datos | N/A | Define cómo se ponen los resultados a disposición de los usuarios. |

{style="table-layout:auto"}

## Almacén acelerado de consultas {#query-accelerated-store}

La siguiente tabla proporciona los límites de protección recomendados y la descripción del almacén acelerado de consultas.

| Barrera | Límite | Tipo de límite | Descripción |
|---|---|---|---|
| Concurrencia de consulta | 4 | Protección impuesta por el sistema | Para garantizar que las consultas sobre datos agregados mediante la API de informes (incluidas las consultas que mejoran los modelos de datos, como los modelos de datos de Real-Time CDP) tengan los recursos para ejecutarse de forma eficaz, la API de informes rastrea la utilización de los recursos asignando espacios de concurrencia a cada consulta. El sistema pone las consultas en cola y espera hasta que las ranuras de concurrencia estén disponibles o se puedan servir desde la caché. Hay disponibles un máximo de cuatro ranuras de consulta simultáneas en un momento dado.<br>Si accede a la API de informes a través de una herramienta BI y necesita más concurrencia, se requiere un servidor BI. |

{style="table-layout:auto"}

## Pasos siguientes

Después de leer este documento, debería comprender mejor los límites predeterminados para la ejecución de consultas con los patrones de consulta disponibles.

Consulte la siguiente documentación para obtener más información sobre el servicio de consultas:

* [API del servicio de consultas](./api/getting-started.md)
* [IU del servicio de consultas](./ui/overview.md)

Consulte la siguiente documentación para obtener más información sobre otras protecciones de servicios de Experience Platform, sobre la información de latencia de extremo a extremo y la información de licencias de los documentos de descripción del producto de Real-Time CDP:

* [protecciones de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=es#end-to-end-latency-diagrams) para varios servicios de Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/es/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)