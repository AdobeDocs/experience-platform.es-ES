---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Analytics;Analytics;Analytics;AAID;
title: Conector de origen de Adobe Analytics para datos de grupos de informes
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d94bbbd34b116f10098624d565c1ae285fc0461e
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 6%

---

# Conector de origen de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través del conector de origen de Analytics. La variable [!DNL Analytics] el conector de origen transmite datos recopilados por [!DNL Analytics] a Platform en tiempo real, convertir con formato SCDS [!DNL Analytics] datos en [!DNL Experience Data Model] (XDM) campos para consumo por plataforma.

Este documento proporciona información general sobre [!DNL Analytics] y describe los casos de uso de [!DNL Analytics] datos.

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer mejor sus clientes, cómo interactúan con sus propiedades web, dónde es eficaz el gasto en marketing digital e identificar áreas de mejora. [!DNL Analytics] gestiona billones de transacciones web por año y la variable [!DNL Analytics] el conector de origen le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer el [!DNL Real-time Customer Profile] en cuestión de minutos.

![](./images/analytics-data-experience-platform.png)

En un nivel superior, [!DNL Analytics] recopila datos de varios canales digitales y varios centros de datos de todo el mundo. Una vez recopilados los datos, las reglas de Arquitectura de transformación, segmentación e identificación del visitante (VISTA) y las reglas de procesamiento se aplican para dar forma a los datos entrantes. Una vez que los datos sin procesar han pasado por este procesamiento liviano, se consideran listos para el consumo de [!DNL Real-time Customer Profile]. En un proceso paralelo al anterior, los mismos datos procesados se agrupan en lotes e incorporan en conjuntos de datos de Platform para su consumo por lotes [!DNL Data Science Workspace], [!DNL Query Service]y otras aplicaciones de detección de datos.

Consulte la [información general sobre las reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación públicamente documentada que proporciona estructuras y definiciones comunes para que una aplicación se utilice para comunicarse con los servicios en el Experience Platform.

El cumplimiento de los estándares XDM permite incorporar los datos de forma uniforme, facilitando el envío de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [Información general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

Cuando se establece una conexión de origen para traer [!DNL Analytics] datos en el Experience Platform mediante la interfaz de usuario de Platform, los campos de datos se asignan automáticamente y se incorporan en [!DNL Real-time Customer Profile] en minutos. Para obtener instrucciones sobre la creación de una conexión de origen con [!DNL Analytics] Con la interfaz de usuario de Platform, consulte la sección [Tutorial del conector de origen de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y Experience Platform, consulte la [Asignación de campos de Adobe Analytics](./mapping/analytics.md) guía.

## ¿Cuál es la latencia esperada para los datos de Analytics en la plataforma?

La latencia esperada para los datos de Analytics en la plataforma se describe en la siguiente tabla. La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones del consumidor. Por ejemplo, si la implementación de Analytics está configurada con `A4T` la latencia a la canalización aumentará a 5-10 minutos.

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **not** enabled) | &lt; 2 minutos |
| Nuevos datos para [!DNL Real-time Customer Profile] (A4T **es** enabled) | &lt; 15 minutos |
| Nuevos datos en Data Lake | &lt; 90 minutos |
| Relleno de menos de 10 mil millones de eventos | &lt; 4 semanas |

Los rellenos de Analytics tienen un valor predeterminado de 13 meses. El límite de 10.000 millones de acontecimientos mencionado en el cuadro anterior es estrictamente con respecto a la latencia esperada.

>[!NOTE]
>
>Los datos de relleno de Analytics no se incorporan en [!DNL Profile] y, por lo tanto, no se contabiliza en los perfiles de licencia.

## Identificadores principales en [!DNL Analytics] data

Cada visita desde la [!DNL Analytics] el conector de origen contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, el AAID se designa como el principal.

La tabla siguiente proporciona más información sobre los campos de identidad de su [!DNL Analytics] datos.

| Campo de identidad | Descripción |
| --- | --- |
| AAID | El AAID es el identificador de dispositivo principal de Adobe Analytics y se garantiza que exista en todos los eventos que se pasan a través del [!DNL Analytics] fuente. A veces, el AAID se denomina *ID de Analytics heredado* o como `s_vi` ID de cookie. A pesar de esto, se crea un AAID incluso si la variable `s_vi` no está presente. El AAID se representa mediante la variable `post_visid_high` y `post_visid_low` columnas de [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=es). En cualquier evento determinado, el campo AAID contiene una sola identidad que puede ser uno de los distintos tipos descritos en la variable [orden de operaciones [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: Dentro de un grupo de informes completo, un AAID puede contener una mezcla de tipos entre eventos. |
| ECID | El ECID (ID de Experience Cloud) es un campo de identificador de dispositivo independiente que se rellena en Adobe Analytics cuando [!DNL Analytics] se implementa mediante el servicio de identidad de Experience Cloud. A veces, el ECID también se denomina MCID (ID de Marketing Cloud). Si existe un ECID en un evento, el AAID puede basarse en ECID en función de si Analytics [período de gracia](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) está configurado. El ECID se representa mediante la variable `mcvisid` en fuentes de datos de Analytics. Para obtener más información sobre ECID, consulte [Información general de ECID](../../../identity-service/ecid.md). Para obtener información sobre cómo funciona ECID con [!DNL Analytics], consulte el documento en [Solicitudes de ID de Experience Cloud y Analytics](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=es). |
| AACUSTOMID | AACUSTOMID es un campo de identificador independiente que se rellena en Adobe Analytics según el uso de la variable `s.VisitorID` en la variable [!DNL Analytics] implementación. AACUSTOMID se representa mediante la variable `cust_visid` en [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Si el AACUSTOMID está presente, el AAID se basará en el AACUSTOMID porque el AACUSTOMID supera todos los demás identificadores definidos por el [orden de operaciones [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Cómo [!DNL Analytics] la fuente trata las identidades

La variable [!DNL Analytics] source pasa estas identidades al Experience Platform en forma XDM como:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Estos campos no están marcados como identidades. En su lugar, las mismas identidades se copian en el `identityMap` como pares clave-valor:

* `{ “key”: “AAID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “ECID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “AACUSTOMID”, “value”: [ { “id”: “<identity>”, “primary”: false } ] }`

En el mapa de identidad, si ECID está presente, se marca como la identidad principal del evento. En este caso, AAID puede basarse en ECID debido al [Período de gracia del servicio de identidad](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). De lo contrario, AAID se marca como la identidad principal del evento. AACUSTOMID nunca se marca como ID principal para el evento. Sin embargo, si AACUSTOMID está presente, AAID se basa en AACUSTOMID debido al orden de operaciones del Experience Cloud.