---
keywords: Experience Platform;inicio;temas populares;Conector de datos de Analytics;análisis;Analytics
solution: Experience Platform
title: Conector de origen de Adobe Analytics para datos de grupos de informes
topic: overview
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---


# Conector de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform permite la ingesta de datos de Adobe Analytics a través del conector de datos de Analytics (ADC). ADC transmite datos recopilados por [!DNL Analytics] a [!DNL Platform] en tiempo real, convirtiendo datos con formato SCDS [!DNL Analytics] en campos [!DNL Experience Data Model] (XDM) para su consumo por [!DNL Platform].

Este documento proporciona una visión general de [!DNL Analytics] y describe los casos de uso de los datos [!DNL Analytics].

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer más sobre sus clientes, cómo interactúan con sus propiedades web, ver dónde es eficaz el gasto en mercadotecnia digital e identificar áreas de mejora. [!DNL Analytics] gestiona billones de transacciones web por año y ADC le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer los datos  [!DNL Real-time Customer Profile] en cuestión de minutos.

![](./images/analytics-data-experience-platform.png)

En un nivel alto, [!DNL Analytics] recopila datos de diversos canales digitales y múltiples centros de datos en todo el mundo. Una vez recopilados los datos, las reglas de identificación de Visitante, segmentación y arquitectura de transformación (VISTA) y las reglas de procesamiento se aplican para dar forma a los datos entrantes. Después de que los datos sin procesar hayan pasado por este procesamiento liviano, se considerarán listos para el consumo por [!DNL Real-time Customer Profile]. En un proceso paralelo al anterior, los mismos datos procesados son micro-agrupados e ingeridos en datasets de la Plataforma para su consumo por [!DNL Data Science Workspace], [!DNL Query Service] y otras aplicaciones de descubrimiento de datos.

Consulte [Información general sobre las reglas de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes para una aplicación que se debe utilizar para comunicarse con los servicios en [!DNL Experience Platform].

El cumplimiento de los estándares XDM permite la incorporación uniforme de los datos, facilitando la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [información general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

Cuando se establece una conexión de origen para traer [!DNL Analytics] datos a [!DNL Experience Platform] mediante la interfaz de usuario [!DNL Platform], los campos de datos se asignan automáticamente y se ingestan en [!DNL Real-time Customer Profile] en cuestión de minutos. Para obtener instrucciones sobre cómo crear una conexión de origen con [!DNL Analytics] mediante la interfaz de usuario [!DNL Platform], consulte el [tutorial del conector de datos de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y [!DNL Experience Platform], visite la [guía de asignación de campos de Adobe Analytics](./mapping/analytics.md).

## ¿Cuál es la latencia esperada para los datos de Analytics en la plataforma?

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos en [!DNL Real-time Customer Profile] (A4T **no** habilitado) | &lt; 2 minutos |
| Nuevos datos a [!DNL Real-time Customer Profile] (A4T **está** habilitado) | &lt; 15 minutos |
| Nuevos datos en Data Lake | &lt; 45 minutos |
| Rellenar datos (13 meses de datos o 10 mil millones de eventos, lo que sea menor) | &lt; 4 semanas |

>[!NOTE]
>
>La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones de consumo. Por ejemplo, si la implementación de Analytics está configurada con `A4T`, la latencia a Pipeline aumentará a 5-10 minutos.

## Identificadores principales en datos de Analytics

Cada visita del conector de datos de Analytics contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, el AAID se designa como el principal.