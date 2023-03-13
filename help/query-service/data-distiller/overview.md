---
title: Información general de Data Distiller
description: Resumen de los límites de uso de Data Distiller para los datos del servicio de consultas en relación con sus derechos de licencia.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Resumen de Data Distiller

Data Distiller es un paquete de ofertas que incluye un subconjunto de las funcionalidades de Adobe Experience Platform. Con Data Distiller puede realizar la preparación de datos posterior a la ingesta (como limpieza, forma y manipulación) para casos de uso analítico o de perfil del cliente en tiempo real ejecutando consultas por lotes en Query Service. El uso de Data Distiller depende de los derechos que tenga para las aplicaciones basadas en Platform.

## Uso de licencias {#license-usage}

El  [Tablero de uso de licencias de Data Distiller](./license-usage.md) está disponible una vez que haya adquirido las horas calculadas de Data Distiller. El tablero de uso de licencias le ayuda a monitorizar el consumo de horas de cálculo autorizadas. Consulte la [Documento de uso de licencia de Data Distiller](./license-usage.md) para ver información importante sobre el uso de licencias del servicio de consultas de su organización.

## Parámetros de ámbito {#scoping-parameters}

Los parámetros de ámbito son límites de uso relacionados con el ámbito de la configuración necesaria y definidos por la capacidad de la licencia. Sin complementos, los parámetros de ámbito de Data Distiller son los siguientes:

* **Calcular horas**: Puede utilizar PSQL o la API del servicio de consultas para ejecutar consultas por lotes ejecutadas en cualquier zona protegida (programadas o de otro tipo) para analizar y escribir datos. Utiliza las horas de cálculo asignadas al año según se determine en el proceso de definición de ámbitos del acuerdo de licencia. El total de horas calculadas se acumula en todas las zonas protegidas.
* **Datos ingeridos**: los datos introducidos en Adobe Experience Platform que se pueden consultar mediante Data Distiller están sujetos a las limitaciones descritas en la licencia actual para Adobe Real-time Customer Data Platform, Customer Journey Analytics o Adobe Journey Optimizer.
* **Almacenamiento de Data Lake**: El almacenamiento del lago de datos proporcionado en la licencia actual para Adobe Real-time Customer Data Platform, Customer Journey Analytics o Adobe Journey Optimizer también se puede utilizar con Data Distiller. El almacenamiento de Data Lake es una característica compartida.
* **Usuarios del servicio de consultas**: el número de usuarios del servicio de consultas detallado en la licencia actual para Adobe Real-time Customer Data Platform, Customer Journey Analytics o Adobe Journey Optimizer también se puede utilizar con Data Distiller. Usuarios del servicio de consultas es una función compartida.

## Mecanismos de protección

Consulte la [Protecciones del servicio de consultas](../guardrails.md) documento con respecto a los límites de uso predeterminados para los datos del servicio de consulta en relación con sus derechos de licencia.

## Límites estáticos

Un límite estático es el límite de uso que se relaciona con los límites funcionales de Adobe Experience Platform Activation. [Más información sobre Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) se encuentra en los documentos de ayuda de Adobe. A continuación se enumera un resumen de los límites estáticos de Data Distiller. Para obtener información más completa, consulte el documento de la protección del servicio de consultas.

* **Consultas por lotes**: las consultas por lotes programadas agotan el tiempo de espera después de 24 horas.
* **Servicio de consultas**: puede utilizar el servicio de consultas para los siguientes fines:
   * Para ejecutar consultas SQL para el análisis de datos y la preparación de datos posterior a la ingesta (limpieza, forma y manipulación).
   * Ejecutar consultas SQL para crear métricas de resumen que aparezcan directamente en una herramienta de BI.
   * Para inspeccionar rápidamente los datos de Adobe Experience Platform.
   * Para generar perspectivas significativas a partir de sus datos.
* **Llamada de API de informes**: Para garantizar que las consultas que se ejecutan en datos agregados mediante la API de informes tengan recursos suficientes para ejecutarse de forma eficaz. Esto incluye consultas que mejoran los modelos de datos existentes, como los que proporciona Real-time Customer Data Platform. La API de informes rastrea la utilización de los recursos asignando espacios de concurrencia a cada consulta. Hay disponibles simultáneamente un máximo de 4 llamadas a la API de creación de informes. Si accede a la API de informes a través de una herramienta de BI y necesita más ranuras de concurrencia, se requiere un servidor de BI.


