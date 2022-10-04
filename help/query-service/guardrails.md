---
keywords: Experience Platform;consulta;servicio de consulta;solución de problemas;protecciones;directrices;límite;
title: Protecciones para el servicio de consulta
description: Este documento proporciona información sobre los límites de uso de los datos del servicio de consulta para ayudarle a optimizar el uso de la consulta.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 8e5df8b3e38197520c6e15f7c6639c62527c086e
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 4%

---

# Protecciones para el servicio de consulta

Las protecciones son umbrales que proporcionan directrices para el uso de los datos y del sistema, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform.

Este documento proporciona límites de uso predeterminados para los datos del servicio de consulta para ayudarle a optimizar el rendimiento del sistema al consultar los datos en relación con sus derechos de licencia.

## Requisitos previos

Antes de continuar con este documento, debe tener una buena comprensión de las dos funcionalidades clave del servicio de consultas que se describen a continuación:

* **Consultas ad hoc**: Para ejecutar `SELECT` consultas para explorar, experimentar y validar datos donde los resultados de las consultas **no se almacenan** en el lago de datos.

* **Consultas por lotes**: Para ejecutar `INSERT TABLE AS SELECT` y `CREATE TABLE AS SELECT` consultas para limpiar, dar forma, manipular y enriquecer datos. Los resultados de estas consultas **se almacenan** en el lago de datos. La métrica para medir el consumo de esta funcionalidad es horas de cálculo.

La siguiente ilustración resume cómo las capacidades del servicio de consulta están actualmente empaquetadas y autorizadas:

![Un diagrama que explica la distribución y el empaquetado de las capacidades del servicio de consulta en relación con la licencia.](./images/guardrails/query-capabilities.png)

## Tipos de límite

Existen dos tipos de límites predeterminados dentro de este documento:

* **Límite leve**: Puede ir más allá de un límite suave, aunque los límites blandos proporcionan una guía recomendada para el rendimiento del sistema.

* **Límite duro**: Un límite estricto proporciona un máximo absoluto.

>[!NOTE]
>
>Los límites predeterminados descritos en este documento se mejoran constantemente. Vuelva regularmente para ver las actualizaciones.

## Protecciones de rendimiento de entidades principales

Las tablas siguientes proporcionan los límites de protección recomendados y las descripciones para la ejecución de consultas cuando se utiliza un patrón de consulta determinado.

**Consultas ad hoc**

| **Seguridad** | **Límite** | **Tipo de límite** | **Descripción** |
|---|---|---|---|
| Tiempo máximo de ejecución | 10 minutos | Grave | Define el tiempo de salida máximo para una consulta SQL ad-hoc. Si se supera el límite de tiempo para devolver un resultado, se genera el código de error 53400. |
| Concurrencia de consulta | <ul><li>Según se especifica en la descripción del producto de la aplicación.</li><li>+1 (con cada paquete adicional de SKU del usuario de consulta ad hoc adicional adquirido)</li></ul> | Grave | Esto define cuántas consultas se pueden ejecutar simultáneamente para una organización en particular. Si se supera el límite de concurrencia, las consultas se ponen en cola. |
| Conector de cliente y límite de salida de resultado | Conector del cliente<ul><li>Interfaz de usuario de consulta (100 filas)</li><li>Cliente de terceros (50 000)</li><li>[!DNL PostgresSQL] cliente (50.000)</li></ul> | Grave | El resultado de una consulta se puede recibir por los siguientes medios:<ul><li>Interfaz de usuario del servicio de consulta</li><li>Cliente de terceros</li><li>[!DNL PostgresSQL] cliente</li></ul>Nota: Añadir una limitación al recuento de salida puede devolver resultados más rápido. Por ejemplo, `LIMIT 5`, `LIMIT 10`, etc. |
| Resultados devueltos mediante | Interfaz de usuario del cliente | N/A | Esto define cómo se ponen los resultados a disposición de los usuarios. |

{style=&quot;table-layout:auto&quot;}

**Consultas por lotes**

| **Seguridad** | **Límite** | **Tipo de límite** | **Descripción** |
|---|---|---|---|
| Tiempo máximo de ejecución | 24 horas | Grave | Define el tiempo de ejecución máximo para una consulta SQL por lotes.<br>El tiempo de procesamiento de una consulta depende del volumen de datos que se procesarán y de la complejidad de la consulta. |
| Concurrencia del usuario | Sin limitación de usuario | N/D | Las consultas por lotes programadas son trabajos asincrónicos, por lo que no hay limitación de usuarios. |
| Horas de cálculo para el procesamiento de datos por lotes | Según se especifica en el pedido de ventas SKU personalizado de consulta de inteligencia de Adobe Experience Platform del cliente | Leve | Esto define la cantidad de tiempo computacional por año que se permite a un cliente ejecutar consultas por lotes para analizar, procesar y escribir datos de nuevo en el lago de datos. |
| Concurrencia de consulta | Admitido | N/D | Las consultas por lotes programadas son trabajos asincrónicos, por lo que se admiten consultas simultáneas. |
| Conector del cliente y límite de salida de resultados | Conector del cliente<ul><li>Interfaz de usuario de consulta (sin límite superior de filas)</li><li>Cliente de terceros (sin límite superior de filas)</li><li>[!DNL PostgresSQL] cliente (sin límite superior de filas)</li><li>API de REST (sin límite superior de filas)</li></ul> | Grave | El resultado de una consulta puede estar disponible mediante los siguientes métodos:<ul><li>Se puede almacenar como conjuntos de datos derivados</li><li>Se puede insertar en los conjuntos de datos derivados existentes</li></ul>Nota: No hay límite superior para el número de recuento de registros del resultado de la consulta. |
| Resultados devueltos mediante | Conjunto de datos | N/D | Esto define cómo se ponen los resultados a disposición de los usuarios. |

{style=&quot;table-layout:auto&quot;}

Para garantizar que cada consulta de un panel de perspectivas de Real-time Customer Data Platform tenga recursos suficientes para ejecutarse de forma eficaz, la API rastrea el uso de los recursos asignando espacios de concurrencia a cada consulta. El sistema puede procesar hasta cuatro consultas simultáneas y, por lo tanto, hay cuatro ranuras de consulta simultáneas disponibles en un momento determinado. Las consultas se ponen en cola en función de las ranuras de concurrencia y después esperan en la cola hasta que haya suficientes ranuras de concurrencia disponibles.

## Pasos siguientes

Después de leer este documento, debe comprender mejor los límites predeterminados para la ejecución de consultas con los patrones de consulta disponibles.

Consulte la siguiente documentación para obtener más información sobre el servicio de consulta:

* [API del servicio de consulta](./api/getting-started.md)
* [Interfaz de usuario del servicio de consulta](./ui/overview.md)
