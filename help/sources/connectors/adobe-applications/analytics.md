---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de datos de Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Conector de datos de Analytics

Adobe Experience Platform le permite ingestar datos de Adobe Analytics a través del conector de datos de Analytics (ADC). ADC transmite datos recopilados por Adobe Analytics a Platform en tiempo real, convirtiendo datos de Analytics formados por SCDS en campos del Modelo de datos de experiencia (XDM) para su consumo por Platform.

Este documento proporciona información general sobre Adobe Analytics y describe los casos de uso de los datos de Analytics.

## Datos de Adobe Analytics y Analytics

Adobe Analytics es un potente motor para ayudarle a obtener más información sobre sus clientes, cómo interactúan con sus propiedades web, ver dónde es eficaz su inversión en marketing digital e identificar áreas de mejora. Adobe Analytics gestiona billones de transacciones web al año y ADC le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer el Perfil del cliente en tiempo real en cuestión de minutos.

![](./images/analytics-data-experience-platform.png)

En un nivel superior, Adobe Analytics recopila datos de varios canales digitales y de varios centros de datos de todo el mundo. Una vez recopilados los datos, las reglas de identificación de Visitante, segmentación y arquitectura de transformación (VISTA) y las reglas de procesamiento se aplican para dar forma a los datos entrantes. Una vez que los datos sin procesar han pasado por este procesamiento ligero, el Perfil del cliente en tiempo real los considera listos para el consumo. En un proceso paralelo al anterior, los mismos datos procesados se procesan mediante microlotes y se ingieren en conjuntos de datos de Platform para su consumo por el Área de trabajo de ciencia de datos, el Servicio de Consulta y otras aplicaciones de descubrimiento de datos.

Consulte Introducción a las reglas [de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación públicamente documentada que proporciona estructuras y definiciones comunes para una aplicación que se utiliza para comunicarse con los servicios en Adobe Experience Platform.

El cumplimiento de los estándares XDM permite la incorporación uniforme de los datos, facilitando la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la descripción general [del sistema](../../../xdm/home.md)XDM.

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

Cuando se establece una conexión de origen para llevar datos de Analytics al Experience Platform mediante la interfaz de usuario de Platform, los campos de datos se asignan automáticamente y se ingestan en el Perfil del cliente en tiempo real en cuestión de minutos. Para obtener instrucciones sobre cómo crear una conexión de origen con Adobe Analytics mediante la interfaz de usuario de Platform, consulte el tutorial [del conector de datos de](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Para obtener información detallada sobre la asignación de campos que se produce entre Analytics y Experience Platform, visite la guía de asignación [de campos Analytics de](./mapping/analytics.md) Adobe.

## ¿Cuál es la latencia esperada para Analytics Data en Platform?

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos para el Perfil del cliente en tiempo real (A4T **no** está habilitado) | &lt; 2 minutos |
| Nuevos datos para el Perfil del cliente en tiempo real (A4T **está** habilitado) | &lt; 15 minutos |
| Nuevos datos en Data Lake | &lt; 45 minutos |
| Rellenar datos (13 meses de datos o 10 mil millones de eventos, lo que sea menor) | &lt; 4 semanas |

>[!NOTE]
>
>La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones de consumo. Por ejemplo, si la implementación de Analytics está configurada con `A4T` la latencia de Pipeline aumentará a 5-10 minutos.