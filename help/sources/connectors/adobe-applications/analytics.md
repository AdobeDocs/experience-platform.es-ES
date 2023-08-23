---
title: Conector de origen de Adobe Analytics para datos de grupos de informes
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 59f7b7cd2e7c52b64ee7fdb8e33b3a0116697696
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 7%

---

# Conector de origen de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través del conector de origen de Analytics. El [!DNL Analytics] conector de origen transmite datos recopilados por [!DNL Analytics] a Platform en tiempo real, convertir archivos con formato SCDS [!DNL Analytics] datos en [!DNL Experience Data Model] Campos de (XDM) para el consumo por plataforma.

Este documento proporciona información general sobre [!DNL Analytics] y describe los casos de uso de [!DNL Analytics] datos.

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer más sobre sus clientes, cómo interactúan con sus propiedades web, ver dónde es efectivo su gasto en marketing digital e identificar áreas de mejora. [!DNL Analytics] gestiona billones de transacciones web al año y el [!DNL Analytics] conector de origen permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer el [!DNL Real-Time Customer Profile] en cuestión de minutos.

![Gráfico que ilustra el recorrido de datos de diferentes aplicaciones de Adobe, incluido Adobe Analytics.](./images/analytics-data-experience-platform.png)

En un nivel alto, [!DNL Analytics] recopila datos de varios canales digitales y centros de datos de todo el mundo. Una vez recopilados los datos, se aplican las reglas de Identificación del visitante, Segmentación y Arquitectura de transformación (VISTA) y reglas de procesamiento para dar forma a los datos entrantes. Una vez que los datos en bruto han pasado por este procesamiento ligero, se consideran listos para el consumo por [!DNL Real-Time Customer Profile]. En un proceso paralelo al mencionado, los mismos datos procesados se procesan por microlotes y se incorporan a conjuntos de datos de Platform para su consumo por parte de [!DNL Data Science Workspace], [!DNL Query Service]y otras aplicaciones de descubrimiento de datos.

Consulte la [información general sobre reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=es) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes para que una aplicación se utilice para comunicarse con servicios en Experience Platform.

El cumplimiento de los estándares XDM permite que los datos se incorporen de forma uniforme, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [Información general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

>[!IMPORTANT]
>
>Las transformaciones de la preparación de datos pueden añadir latencia al flujo de datos general. La latencia adicional añadida varía en función de la complejidad de la lógica de transformación.

Cuando se establece una conexión de origen para traer [!DNL Analytics] datos en Experience Platform mediante la interfaz de usuario de Platform, los campos de datos se asignan e incorporan automáticamente en [!DNL Real-Time Customer Profile] en minutos. Para obtener instrucciones sobre cómo crear una conexión de origen con [!DNL Analytics] Con la interfaz de usuario de Platform, consulte [Tutorial del conector de origen de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y Experience Platform, consulte la [Asignación de campos de Adobe Analytics](./mapping/analytics.md) guía.

## ¿Cuál es la latencia esperada para los datos de Analytics en Platform?

La latencia esperada para los datos de Analytics en Platform se describe en la siguiente tabla. La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones de los consumidores. Por ejemplo, si la implementación de Analytics está configurada con `A4T` la latencia a la canalización aumentará a 5-10 minutos.

| Datos de análisis | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos en [!DNL Real-Time Customer Profile] (A4T) **no** enabled) | &lt; 2 minutos |
| Nuevos datos en [!DNL Real-Time Customer Profile] (A4T) **es** enabled) | hasta 30 minutos |
| Nuevos datos en Data Lake | &lt; 90 minutos |
| Relleno de menos de 10 000 millones de eventos | &lt; 4 semanas |

El relleno de Analytics para zonas protegidas de producción tiene un valor predeterminado de 13 meses. Para los datos de Analytics en entornos limitados que no son de producción, el relleno se establece en tres meses. El límite de 10 000 millones de eventos mencionado en el cuadro anterior se aplica estrictamente a la latencia esperada.

Al crear un flujo de datos de origen de Analytics en una zona protegida de producción, se crean dos flujos de datos:

* Un flujo de datos que rellena los datos históricos del grupo de informes con un retraso de 13 meses en el lago de datos. Este flujo de datos finaliza cuando se completa el relleno.
* Un flujo de datos que envía datos activos al lago de datos y a [!DNL Real-Time Customer Profile]. Este flujo de datos se ejecuta continuamente.

>[!NOTE]
>
>Los datos de relleno de Analytics no se incorporan en [!DNL Profile] y, por lo tanto, no se contabiliza en los perfiles de licencia.

## Identificadores principales en [!DNL Analytics] datos

Cada visita desde el [!DNL Analytics] El conector de origen contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, entonces el AAID se designa como el principal.

La siguiente tabla proporciona más información sobre los campos de identidad de su [!DNL Analytics] datos.

| Campo de identidad | Descripción |
| --- | --- |
| AAID | AAID es el identificador de dispositivo principal en Adobe Analytics y se garantiza que existe en todos los eventos que se pasan a través de [!DNL Analytics] origen. A veces, AAID se denomina *ID de Analytics heredado* o como el `s_vi` ID de cookie. A pesar de esto, se crea un AAID aunque la variable `s_vi` la cookie no está presente. AAID se representa mediante el `post_visid_high` y `post_visid_low` columnas en [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=es). En cualquier evento determinado, el campo AAID contiene una sola identidad que puede ser de uno de los distintos tipos descritos en la variable [orden de operaciones para [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: Dentro de un grupo de informes completo, un AAID puede contener una combinación de tipos entre eventos. |
| ECID | El ECID (ID de Experience Cloud) es un campo de identificador de dispositivo independiente, que se rellena en Adobe Analytics cuando [!DNL Analytics] se implementa mediante el servicio de ID del Experience Cloud. El ECID a veces también se denomina MCID (ID de Marketing Cloud). Si existe un ECID en un evento, el AAID puede basarse en ECID en función de si Analytics [período de gracia](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) está configurado. El ECID se representa mediante el `mcvisid` en Fuentes de datos de Analytics. Para obtener más información sobre ECID, consulte la [Información general de ECID](../../../identity-service/ecid.md). Para obtener información sobre cómo funciona ECID con [!DNL Analytics], consulte el documento sobre [Solicitudes de ID de Experience Cloud y Analytics](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=es). |
| AACUSTOMID | AACUSTOMID es un campo de identificador independiente que se rellena en Adobe Analytics según el uso del `s.VisitorID` en la variable [!DNL Analytics] implementación. AACUSTOMID se representa mediante el `cust_visid` columna en [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=es). Si el AACUSTOMID está presente, el AAID se basará en el AACUSTOMID porque el AACUSTOMID supera todos los demás identificadores definidos por el [orden de operaciones para [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### ¿Cómo? [!DNL Analytics] la fuente trata las identidades

El [!DNL Analytics] El origen de pasa estas identidades al Experience Platform en forma XDM de la siguiente manera:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Estos campos no están marcados como identidades. En su lugar, se copian las mismas identidades en el de XDM `identityMap` como pares clave-valor:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

En el mapa de identidad, si ECID está presente, se marca como la identidad principal del evento. En este caso, AAID puede basarse en ECID debido a la variable [Período de gracia del servicio de identidad](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). De lo contrario, AAID se marca como la identidad principal del evento. AACUSTOMID nunca se marca como ID principal para el evento. Sin embargo, si AACUSTOMID está presente, AAID se basa en AACUSTOMID debido al orden de operaciones del Experience Cloud.

>[!NOTE]
>
>Puede utilizar la preparación de datos para filtrar las identidades secundarias procedentes de Analytics, como AAID y AACUSTOMID. Si se filtran, estas identidades no se incorporarán en el perfil si están disponibles en los datos entrantes de Analytics. Los datos sin filtrar se seguirán cargando en el lago de datos.
