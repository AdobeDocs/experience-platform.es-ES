---
title: Gestión de duplicación de eventos en el Experience Platform
description: Descubra cómo Adobe Experience Platform gestiona la duplicación de eventos
source-git-commit: bc3ae849bd7fd8a9f50ba98528adc43d7282df90
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Gestión de duplicación de eventos en Adobe Experience Platform

Adobe Experience Platform es un sistema muy distribuido diseñado para maximizar la fiabilidad y, al mismo tiempo, ampliarse a volúmenes de datos cada vez mayores.

Para la recopilación de datos en tiempo real, [Eventos de experiencia](../xdm/classes/experienceevent.md) se recopilan mediante la variable [Red perimetral](../web-sdk/home.md#edge-network), desde fuentes del lado del cliente, como [SDK web](../web-sdk/home.md) o [Mobile SDK](https://developer.adobe.com/client-sdks/home/)y se entregan a las capas de procesamiento y almacenamiento del Experience Platform. Estas capas componen soluciones como Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es), y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es).

Para minimizar la pérdida de Experience Event, los SDK del lado del cliente y el servicio de envío interno del Experience Platform esperan una confirmación de que un evento se ha recopilado correctamente.

Si no se recibe esa confirmación, los SDK del lado del cliente o el déclencheur del servicio de entrega de Platform interno vuelven a intentarlo y el evento de experiencia se envía de nuevo.

Se trata de una práctica recomendada para gestionar errores transitorios. El efecto secundario es la posibilidad de introducir eventos duplicados.

Para comprender mejor las prácticas recomendadas para gestionar errores transitorios, consulte este artículo sobre [gestión transitoria de fallos](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Escenarios de duplicación de eventos {#scenarios}

La duplicación de eventos puede producirse en varios escenarios, como, entre otros:

* Problemas relacionados con la red entre los SDK de cliente y [!DNL Edge Network]. Estos problemas pueden deberse a errores del proveedor de servicios de Internet, pérdida de señal móvil u otros errores de red, ya que la conectividad entre el cliente y la red perimetral se realiza a través de la Internet pública.
* Eventos de escalado automático internos del Experience Platform. En ocasiones, los datos pueden reequilibrarse debido a la volatilidad de la infraestructura en la nube.

La capa de recopilación de datos de Adobe Experience Platform está diseñada para admitir el procesamiento de &quot;al menos una vez&quot;. En consecuencia, la duplicación de eventos puede producirse en situaciones limitadas y poco frecuentes.

Para obtener más información sobre el procesamiento de &quot;al menos una vez&quot;, consulte este artículo sobre [garantías de entrega de mensajes](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opciones de deduplicación de eventos {#deduplication}

En el caso de escenarios empresariales sensibles a eventos duplicados, Experience Platform utiliza varios métodos de anulación de duplicación de eventos en sus sistemas de almacenamiento descendente, como los que se describen a continuación.

* El Almacenamiento de perfiles de Real-Time CDP anula los eventos si uno de ellos tiene el mismo `_id` ya existe en el [!DNL Profile Store]. Consulte la documentación sobre [clase XDM ExperienceEvent](../xdm/classes/experienceevent.md) para obtener más información.
* El Customer Journey Analytics permite a los usuarios configurar una métrica para que solo cuente los valores de forma no repetitiva. Para obtener información sobre cómo hacerlo, consulte la documentación de [configuración de componentes de anulación de duplicación de métricas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=es).
* Experience Platform Query Service admite la anulación de duplicación de datos cuando es necesario quitar una fila completa de un cálculo o omitir un conjunto específico de campos porque solo parte de los datos de la fila es información duplicada. Consulte la documentación sobre [anulación de duplicación de datos en Query Service](../query-service/key-concepts/deduplication.md) para obtener más información.

>[!NOTE]
>
>Si se encuentra con problemas de duplicación de eventos fuera de los casos de uso presentados anteriormente, póngase en contacto con su representante de Adobe y proporcione información detallada sobre su caso de uso.