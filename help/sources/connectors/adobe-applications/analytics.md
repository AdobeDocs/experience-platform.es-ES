---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Analytics;Analytics;Analytics
solution: Experience Platform
title: Conector de origen de Adobe Analytics para datos de grupos de informes
topic-legacy: overview
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 9defe1c3087c2f1284ceedede9d274a51cf97b96
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Conector de origen de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través del conector de origen de Analytics. El conector de origen [!DNL Analytics] transmite los datos recopilados por [!DNL Analytics] a Platform en tiempo real, convirtiendo los datos [!DNL Analytics] con formato SCDS en campos [!DNL Experience Data Model] (XDM) para su consumo por Platform.

Este documento proporciona información general sobre [!DNL Analytics] y describe los casos de uso de los datos [!DNL Analytics].

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer mejor sus clientes, cómo interactúan con sus propiedades web, dónde es eficaz el gasto en marketing digital e identificar áreas de mejora. [!DNL Analytics] gestiona billones de transacciones web al año y el conector de  [!DNL Analytics] origen le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer el contenido  [!DNL Real-time Customer Profile] en cuestión de minutos.

![](./images/analytics-data-experience-platform.png)

En un nivel superior, [!DNL Analytics] recopila datos de varios canales digitales y múltiples centros de datos en todo el mundo. Una vez recopilados los datos, las reglas de Arquitectura de transformación, segmentación e identificación del visitante (VISTA) y las reglas de procesamiento se aplican para dar forma a los datos entrantes. Una vez que los datos sin procesar han pasado por este procesamiento ligero, se consideran listos para el consumo antes de [!DNL Real-time Customer Profile]. En un proceso paralelo al anteriormente mencionado, los mismos datos procesados se incluyen en lotes e incorporados en conjuntos de datos de Platform para su consumo por [!DNL Data Science Workspace], [!DNL Query Service] y otras aplicaciones de descubrimiento de datos.

Consulte la [información general sobre las reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes para que una aplicación se utilice para comunicarse con los servicios en el Experience Platform.

El cumplimiento de los estándares XDM permite incorporar los datos de forma uniforme, facilitando el envío de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [información general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

Cuando se establece una conexión de origen para introducir datos [!DNL Analytics] en el Experience Platform mediante la interfaz de usuario de Platform, los campos de datos se asignan automáticamente y se incorporan a [!DNL Real-time Customer Profile] en cuestión de minutos. Para obtener instrucciones sobre la creación de una conexión de origen con [!DNL Analytics] mediante la interfaz de usuario de Platform, consulte el [Tutorial del conector de origen de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y el Experience Platform, consulte la guía [Adobe Analytics field mapping](./mapping/analytics.md).

## ¿Cuál es la latencia esperada para los datos de Analytics en la plataforma?

La latencia esperada para los datos de Analytics en la plataforma se describe en la siguiente tabla. La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones del consumidor. Por ejemplo, si la implementación de Analytics está configurada con `A4T`, la latencia a la canalización aumentará a 5-10 minutos.

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **no** habilitados) | &lt; 2 minutos |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **está** habilitado) | &lt; 15 minutos |
| Nuevos datos en Data Lake | &lt; 90 minutos |
| Rellenar datos (13 meses de datos o 10 000 millones de eventos, lo que sea menor) | &lt; 4 semanas |

>[!NOTE]
>
>Los datos de relleno de Analytics no se incorporan en [!DNL Profile] y, por lo tanto, no se contabilizan en los perfiles de licencia.

## Identificadores primarios en datos [!DNL Analytics]

Cada visita del conector de origen [!DNL Analytics] contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, el AAID se designa como el principal.
