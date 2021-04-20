---
keywords: Experience Platform;inicio;temas populares;Analytics Data Connector;Analytics;Analytics
solution: Experience Platform
title: Conector de origen de Adobe Analytics para datos de grupos de informes
topic: overview
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---


# Conector de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform le permite introducir datos de Adobe Analytics mediante el conector de datos de Analytics (ADC). ADC transmite datos recopilados por [!DNL Analytics] a [!DNL Platform] en tiempo real, convirtiendo los datos [!DNL Analytics] con formato SCDS en campos [!DNL Experience Data Model] (XDM) para su consumo por [!DNL Platform].

Este documento proporciona información general sobre [!DNL Analytics] y describe los casos de uso de los datos [!DNL Analytics].

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer mejor sus clientes, cómo interactúan con sus propiedades web, dónde es eficaz el gasto en marketing digital e identificar áreas de mejora. [!DNL Analytics] gestiona billones de transacciones web al año y ADC le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer el  [!DNL Real-time Customer Profile] en cuestión de minutos.

![](./images/analytics-data-experience-platform.png)

En un nivel superior, [!DNL Analytics] recopila datos de varios canales digitales y múltiples centros de datos en todo el mundo. Una vez recopilados los datos, las reglas de Arquitectura de transformación, segmentación e identificación del visitante (VISTA) y las reglas de procesamiento se aplican para dar forma a los datos entrantes. Una vez que los datos sin procesar han pasado por este procesamiento ligero, se consideran listos para el consumo antes de [!DNL Real-time Customer Profile]. En un proceso paralelo al anteriormente mencionado, los mismos datos procesados se incluyen en lotes e incorporados en conjuntos de datos de Platform para su consumo por [!DNL Data Science Workspace], [!DNL Query Service] y otras aplicaciones de descubrimiento de datos.

Consulte [Información general sobre las reglas de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes para que una aplicación se utilice para comunicarse con los servicios en [!DNL Experience Platform].

El cumplimiento de los estándares XDM permite incorporar los datos de forma uniforme, facilitando el envío de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [información general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

Cuando se establece una conexión de origen para introducir datos [!DNL Analytics] en [!DNL Experience Platform] mediante la interfaz de usuario [!DNL Platform], los campos de datos se asignan automáticamente e incorporan a [!DNL Real-time Customer Profile] en cuestión de minutos. Para obtener instrucciones sobre la creación de una conexión de origen con [!DNL Analytics] mediante la interfaz de usuario [!DNL Platform], consulte el [Tutorial del conector de datos de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y [!DNL Experience Platform], visite la [guía de asignación de campos de Adobe Analytics](./mapping/analytics.md).

## ¿Cuál es la latencia esperada para los datos de Analytics en la plataforma?

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **no** habilitados) | &lt; 2 minutos |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **está** habilitado) | &lt; 15 minutos |
| Nuevos datos en Data Lake | &lt; 90 minutos |
| Rellenar datos (13 meses de datos o 10 000 millones de eventos, lo que sea menor) | &lt; 4 semanas |

>[!NOTE]
>
>La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones del consumidor. Por ejemplo, si la implementación de Analytics está configurada con `A4T`, la latencia a la canalización aumentará a 5-10 minutos.

## Identificadores principales en datos de Analytics

Cada visita del conector de datos de Analytics contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, el AAID se designa como el principal.