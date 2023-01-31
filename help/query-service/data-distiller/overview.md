---
title: Información general de Data Distiller
description: Resumen de los límites de uso de Data Distiller para los datos del servicio de consulta en relación con su derecho de licencia.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Información general de Data Distiller

Data Distiller es una oferta de paquetes que incluye un subconjunto de las funcionalidades de Adobe Experience Platform. Con Data Distiller, puede realizar la preparación de datos posteriores a la ingesta (como la limpieza, la formación y la manipulación) para perfiles de clientes en tiempo real o casos de uso analítico mediante la ejecución de consultas por lotes en Query Service. El uso de Data Distiller depende de la asignación de derechos para aplicaciones basadas en plataforma.

## Uso de licencias {#license-usage}

La variable  [Panel de uso de licencias de Distiller de datos](./license-usage.md) está disponible una vez que haya comprado horas de cálculo de Data Distiller. El panel de uso de licencias le ayuda a supervisar el consumo de las horas de cálculo correspondientes. Consulte la [Documento de uso de licencia de Distiller de datos](./license-usage.md) para ver información importante sobre el uso de licencias del servicio de consulta de su organización.

## Parámetros de ámbitos {#scoping-parameters}

Los parámetros de ámbito son límites de uso que se relacionan con el alcance de la configuración requerida y que se definen según la capacidad de la licencia. Sin complementos, los parámetros de ámbito de Data Distiller son los siguientes:

* **Horario de cómputo**: Puede utilizar PSQL o la API de servicio de consulta para ejecutar consultas por lotes ejecutadas en cualquier simulador de pruebas (programadas o de otro tipo) para analizar y escribir datos. Esto utiliza las horas calculadas asignadas al año, tal como se determina en el proceso de alcance del contrato de licencia. El total de horas de cómputo se acumula en todos los entornos limitados.
* **Datos ingestados**: Los datos introducidos en Adobe Experience Platform que se pueden consultar mediante Data Distiller están sujetos a las limitaciones descritas en la licencia vigente en ese momento para Adobe Real-time Customer Data Platform, Customer Journey Analytics y/o Adobe Journey Optimizer.
* **Almacenamiento del lago de datos**: El almacenamiento del lago de datos que se proporciona en su licencia entonces actual para Adobe Real-time Customer Data Platform, Customer Journey Analytics y/o Adobe Journey Optimizer también se puede usar con Data Distiller. Data Lake Storage es una función compartida.
* **Usuarios del servicio de consultas**: El número de usuarios del servicio de consulta que se detalla en la licencia actual de Adobe Real-time Customer Data Platform, Customer Journey Analytics o Adobe Journey Optimizer también se puede utilizar con Data Distiller. Los usuarios del servicio de consulta son una función compartida.

## Límites de protección 

Consulte la [Protecciones del servicio de consultas](../guardrails.md) documento relativo a los límites de uso predeterminados para los datos del servicio de consulta en relación con su derecho de licencia.

## Límites estáticos

Un límite estático es el límite de uso relacionado con los límites funcionales de Adobe Experience Platform Activation. [Más información sobre la activación de Adobe Experience Platform](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) se encuentra en los documentos de ayuda de Adobe. A continuación se enumera un resumen de los límites estáticos de Data Distiller. Para obtener información más completa, consulte el documento de protección del servicio de consulta .

* **Consultas por lotes**: Las consultas por lotes programadas agotan el tiempo de espera al cabo de 24 horas.
* **Servicio de consultas**: Puede utilizar el servicio de consultas para los siguientes fines:
   * Para ejecutar consultas SQL para el análisis de datos y la preparación de datos posteriores a la ingesta (limpieza, modelado y manipulación).
   * Para ejecutar consultas SQL con el fin de crear métricas resumidas que aparezcan directamente en una herramienta BI.
   * Para inspeccionar datos rápidamente en Adobe Experience Platform.
   * Para generar perspectivas significativas a partir de los datos.
* **Llamada de API de informes**: Para garantizar que las consultas se ejecuten en datos añadidos mediante la API de informes tengan recursos suficientes para ejecutarse de forma eficaz. Esto incluye consultas que mejoran los modelos de datos existentes, como los que proporciona Real-time Customer Data Platform. La API de informes realiza un seguimiento de la utilización de los recursos asignando espacios de concurrencia a cada consulta. Hay un máximo de 4 llamadas a la API de informes disponibles de forma simultánea. Si accede a la API de informes a través de una herramienta BI y requiere más espacios de concurrencia, se requiere un servidor BI.


