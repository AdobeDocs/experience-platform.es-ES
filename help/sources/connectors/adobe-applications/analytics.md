---
title: Conector de Adobe Analytics Source para datos de grupos de informes
description: Este documento proporciona información general sobre Analytics y describe los casos de uso de los datos de Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d56a37c5b1c5768b3f6811be9d30d45628fdabca
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Conector de origen de Adobe Analytics para datos de grupos de informes

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través del conector de origen de Analytics. El conector de origen [!DNL Analytics] transmite los datos recopilados por [!DNL Analytics] a Platform en tiempo real, convirtiendo los datos [!DNL Analytics] con formato SCDS en campos [!DNL Experience Data Model] (XDM) para que Platform los consuma.

Este documento proporciona información general sobre [!DNL Analytics] y describe los casos de uso de los datos de [!DNL Analytics].

## Datos de Adobe Analytics y Analytics

[!DNL Analytics] es un potente motor que le ayuda a conocer mejor a sus clientes, cómo interactúan con sus propiedades web, ver dónde es efectivo su gasto en marketing digital e identificar áreas de mejora. [!DNL Analytics] administra billones de transacciones web al año y el conector de origen [!DNL Analytics] le permite aprovechar fácilmente estos datos de comportamiento enriquecidos y enriquecer [!DNL Real-Time Customer Profile] en cuestión de minutos.

![Gráfico que ilustra el recorrido de datos de distintas aplicaciones de Adobe, incluido Adobe Analytics.](./images/analytics-data-experience-platform.png)

En un nivel superior, [!DNL Analytics] recopila datos de varios canales digitales y de varios centros de datos en todo el mundo. Una vez recopilados los datos, se aplican las reglas de Identificación del visitante, Segmentación y Arquitectura de transformación (VISTA) y reglas de procesamiento para dar forma a los datos entrantes. Después de que los datos sin procesar hayan pasado por este procesamiento ligero, [!DNL Real-Time Customer Profile] los considera listos para el consumo. En un proceso paralelo al mencionado anteriormente, los mismos datos procesados se procesan en microlotes y se incorporan a conjuntos de datos de Platform para su consumo por parte de [!DNL Query Service] y otras aplicaciones de detección de datos.

Consulte la [descripción general de las reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=es) para obtener más información sobre las reglas de procesamiento.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes para que una aplicación se utilice para comunicarse con servicios en Experience Platform.

El cumplimiento de los estándares XDM permite que los datos se incorporen de forma uniforme, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM, consulte la [descripción general del sistema XDM](../../../xdm/home.md).

## ¿Cómo se asignan los campos de Adobe Analytics a XDM?

>[!IMPORTANT]
>
>Las transformaciones de la preparación de datos pueden añadir latencia al flujo de datos general. La latencia adicional añadida varía en función de la complejidad de la lógica de transformación.

Cuando se establece una conexión de origen para llevar datos de [!DNL Analytics] al Experience Platform mediante la interfaz de usuario de Platform, los campos de datos se asignan e incorporan automáticamente en [!DNL Real-Time Customer Profile] en cuestión de minutos. Para obtener instrucciones sobre cómo crear una conexión de origen con [!DNL Analytics] mediante la interfaz de usuario de Platform, consulte el [tutorial del conector de origen de Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obtener información detallada sobre la asignación de campos que se produce entre [!DNL Analytics] y el Experience Platform, consulte la guía [asignación de campos Adobe Analytics](./mapping/analytics.md).

## ¿Cuál es la latencia esperada para los datos de Analytics en Platform?

La latencia esperada para los datos de Analytics en Platform se describe en la siguiente tabla. La latencia variará según la configuración del cliente, los volúmenes de datos y las aplicaciones de los consumidores. Por ejemplo, si la implementación de Analytics está configurada con `A4T`, la latencia a la canalización aumentará a 5-10 minutos.

| Datos de Analytics | Latencia esperada |
| -------------- | ---------------- |
| Nuevos datos en [!DNL Real-Time Customer Profile] (A4T **no habilitado**) | &lt; 2 minutos |
| Nuevos datos para [!DNL Real-Time Customer Profile] (A4T **está** habilitado) | hasta 30 minutos |
| Nuevos datos en Data Lake | &lt; 2,25 horas |
| Nuevos datos para el Customer Journey Analytics sin [vincular](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 horas |
| Nuevos datos para el Customer Journey Analytics con vinculación | &lt; 7 horas |
| Relleno de menos de 10 000 millones de eventos | &lt; 4 semanas |

Para obtener más información acerca de las latencias de Customer Journey Analytics, consulte: [Protecciones de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

El relleno de Analytics para zonas protegidas de producción tiene un valor predeterminado de 13 meses. Para los datos de Analytics en entornos limitados que no son de producción, el relleno se establece en tres meses. El límite de 10 000 millones de eventos mencionado en el cuadro anterior se aplica estrictamente a la latencia esperada.

Al crear un flujo de datos de origen de Analytics en una zona protegida de producción, se crean dos flujos de datos:

* Un flujo de datos que rellena los datos históricos del grupo de informes con un retraso de 13 meses en el lago de datos. Este flujo de datos finaliza cuando se completa el relleno.
* Flujo de flujo de datos que envía datos activos al lago de datos y a [!DNL Real-Time Customer Profile]. Este flujo de datos se ejecuta continuamente.

>[!NOTE]
>
>Los datos de relleno de Analytics no se han ingerido en [!DNL Profile], por lo que no se tienen en cuenta en los perfiles de licencia.

## Identificadores principales en datos de [!DNL Analytics]

Cada visita del conector de origen [!DNL Analytics] contiene un identificador principal que depende de si existe un ECID o un AAID. Si hay un ECID, el ECID se designa como identificador principal. Si hay un AAID, entonces el AAID se designa como el principal.

La siguiente tabla proporciona más información sobre los campos de identidad en los datos de [!DNL Analytics].

| Campo de identidad | Descripción |
| --- | --- |
| AAID | AAID es el identificador de dispositivo principal en Adobe Analytics y se garantiza que existe en todos los eventos que se pasan a través del origen [!DNL Analytics]. A veces, AAID se denomina *ID de Analytics heredado* o ID de cookie `s_vi`. A pesar de esto, se crea un AAID aunque la cookie `s_vi` no esté presente. AAID está representado por las columnas `post_visid_high` y `post_visid_low` en [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). En cualquier evento determinado, el campo AAID contiene una sola identidad que puede ser uno de los distintos tipos descritos en el [orden de operaciones para [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: dentro de un grupo de informes completo, un AAID puede contener una combinación de tipos entre eventos. |
| ECID | El ECID (ID de Experience Cloud) es un campo de identificador de dispositivo independiente, que se rellena en Adobe Analytics cuando [!DNL Analytics] se implementa mediante el servicio de identidad de Experience Cloud. El ECID a veces también se denomina MCID (ID de Marketing Cloud). Si existe un ECID en un evento, el AAID puede basarse en ECID en función de si el [período de gracia](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) de Analytics está configurado. El ECID está representado por `mcvisid` en las fuentes de datos de Analytics. Para obtener más información sobre ECID, consulte la [descripción general de ECID](../../../identity-service/features/ecid.md). Para obtener información sobre cómo funciona ECID con [!DNL Analytics], consulte el documento sobre [Solicitudes de ID de Experience Cloud y Analytics](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | AACUSTOMID es un campo de identificador independiente que se rellena en Adobe Analytics según el uso de la variable `s.VisitorID` en la implementación [!DNL Analytics]. AACUSTOMID se representa mediante la columna `cust_visid` en [[!DNL Analytics] fuentes de datos](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Si el AACUSTOMID está presente, AAID se basará en el AACUSTOMID porque este supera todos los demás identificadores según se definen en el [orden de operaciones para [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Cómo trata el origen [!DNL Analytics] las identidades

El origen [!DNL Analytics] pasa estas identidades al Experience Platform en formato XDM como:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Estos campos no están marcados como identidades. En su lugar, las mismas identidades (si están presentes en el evento) se copian en el XDM `identityMap` como pares clave-valor:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Cuando la identidad o identidades se copian en `identityMap`, `endUserIDs._experience.mcid.namespace.code` también se establece en el mismo evento:

* Si AAID está presente, `endUserIDs._experience.aaid.namespace.code` se establece como &quot;AAID&quot;.
* Si ECID está presente, `endUserIDs._experience.mcid.namespace.code` está establecido en &quot;ECID&quot;.
* Si AACUSTOMID está presente, `endUserIDs._experience.aacustomid.namespace.code` se establece como &quot;AACUSTOMID&quot;.

En el mapa de identidad, si ECID está presente, se marca como la identidad principal del evento. En este caso, AAID puede basarse en ECID debido al [período de gracia del servicio de identidad](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). De lo contrario, AAID se marca como la identidad principal del evento. AACUSTOMID nunca se marca como ID principal para el evento. Sin embargo, si AACUSTOMID está presente, AAID se basa en AACUSTOMID debido al orden de operaciones del Experience Cloud.

>[!NOTE]
>
>Puede utilizar la preparación de datos para filtrar las identidades secundarias procedentes de Analytics, como AAID y AACUSTOMID. Si se filtran, estas identidades no se incorporarán en el perfil si están disponibles en los datos entrantes de Analytics. Los datos sin filtrar se seguirán cargando en el lago de datos.
