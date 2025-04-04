---
title: Gestión de duplicación de eventos en Experience Platform
description: Descubra cómo Adobe Experience Platform gestiona la duplicación de eventos
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Gestión de duplicación de eventos en Adobe Experience Platform

Adobe Experience Platform es un sistema muy distribuido diseñado para maximizar la fiabilidad y, al mismo tiempo, ampliarse a volúmenes de datos cada vez mayores.

Para la recopilación de datos en tiempo real, [los eventos de experiencia](../xdm/classes/experienceevent.md) se recopilan a través de [Edge Network](../web-sdk/home.md#edge-network), de fuentes del lado del cliente, como [Web SDK](../web-sdk/home.md) o [Mobile SDK](https://developer.adobe.com/client-sdks/home/), y se entregan a las capas de procesamiento y almacenamiento de Experience Platform. Estas capas componen soluciones como Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es).

Para minimizar la pérdida de Experience Event, los SDK del lado del cliente y el servicio de entrega interno de Experience Platform esperan una confirmación de que un evento se ha recopilado correctamente.

Si no se recibe esa confirmación, los SDK del lado del cliente o el déclencheur del servicio de entrega interno de Experience Platform lo volverán a intentar y el evento de experiencia se volverá a enviar.

Se trata de una práctica recomendada para gestionar errores transitorios. El efecto secundario es la posibilidad de introducir eventos duplicados.

Para comprender mejor las prácticas recomendadas para administrar errores transitorios, consulte este artículo sobre [administración de errores transitorios](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Escenarios de duplicación de eventos {#scenarios}

La duplicación de eventos puede producirse en varios escenarios, como, entre otros:

* Problemas relacionados con la red entre los SDK de cliente y [!DNL Edge Network]. Estos problemas pueden deberse a errores del proveedor de servicios de Internet, pérdida de la señal móvil u otros errores de red, ya que la conectividad entre el cliente y Edge Network se realiza a través de la Internet pública.
* Eventos internos de escalado automático de Experience Platform. En ocasiones, los datos pueden reequilibrarse debido a la volatilidad de la infraestructura en la nube.

La capa de recopilación de datos de Adobe Experience Platform está diseñada para admitir el procesamiento de &quot;al menos una vez&quot;. En consecuencia, la duplicación de eventos puede producirse en situaciones limitadas y poco frecuentes.

Para obtener más información sobre el procesamiento de &quot;al menos una vez&quot;, consulte este artículo sobre [garantías de entrega de mensajes](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opciones de deduplicación de eventos {#deduplication}

Para los escenarios empresariales sensibles a los eventos duplicados, Experience Platform utiliza varios métodos de deduplicación de eventos en sus sistemas de almacenamiento descendente, como los que se describen a continuación.

* El almacén de perfiles de Real-Time CDP descarta eventos si ya existe un evento con el mismo `_id` en [!DNL Profile store]. Consulte la documentación de [XDM ExperienceEvent class](../xdm/classes/experienceevent.md) para obtener más información.
* Customer Journey Analytics permite a los usuarios configurar una métrica para que solo cuente los valores de forma no repetitiva. Para obtener información sobre cómo hacerlo, consulte la documentación sobre [configuración del componente de anulación de duplicación de métricas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=es).
* Experience Platform Query Service admite la anulación de duplicación de datos cuando es necesario quitar una fila completa de un cálculo o omitir un conjunto específico de campos porque solo parte de los datos de la fila es información duplicada. Consulte la documentación sobre la anulación de duplicación de datos de [en el servicio de consultas](../query-service/key-concepts/deduplication.md) para obtener más información.

>[!NOTE]
>
>Si se encuentra con problemas de duplicación de eventos fuera de los casos de uso presentados anteriormente, póngase en contacto con su representante de Adobe y proporcione información detallada sobre su caso de uso.
