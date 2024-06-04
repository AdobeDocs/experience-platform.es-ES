---
title: Protecciones de Real-Time CDP
description: Obtenga información acerca de las protecciones de datos en los distintos servicios y áreas de Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# Protecciones de Real-Time CDP

Las protecciones son umbrales que proporcionan directrices para el uso de datos y sistemas, la optimización del rendimiento y la prevención de errores o resultados inesperados en Real-Time CDP. Las protecciones pueden hacer referencia al uso o consumo de datos y al procesamiento en relación con los derechos de licencia.

>[!IMPORTANT]
>
>Compruebe los derechos de licencia en su pedido de ventas y en los correspondientes [Descripción del producto](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) sobre los límites de uso reales además de esta página de protecciones.

Comience aquí y siga los vínculos a continuación para comprender todas las protecciones en los distintos servicios y áreas de Real-Time CDP:

* [Protecciones para la ingesta de datos](/help/ingestion/guardrails.md)
* [Protecciones para el [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Protecciones para [!DNL Real-Time Customer Profile] datos y segmentación](/help/profile/guardrails.md)
* [Protecciones para [!DNL Identity Service] datos](/help/identity-service/guardrails.md)
* [Protecciones para [!DNL Query Service]](/help/query-service/guardrails.md)
* [Protecciones para la activación de datos mediante destinos](/help/destinations/guardrails.md)
* [Protecciones para Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Además, visite [los modelos de experiencia digital](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) para obtener más información, como [diagramas de latencia de extremo a extremo](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para varios servicios de Experience Platform.

## Tipos de protección {#guardrail-types}

Tenga en cuenta que los dos tipos de protecciones en todas las áreas y servicios de Real-Time CDP son:

| Tipo de protección | Descripción |
|----------|---------|
| **Protección de rendimiento (límite suave)** | Las protecciones de rendimiento son límites de uso relacionados con el ámbito de los casos de uso. Al superar las barreras de rendimiento, puede experimentar una degradación y latencia del rendimiento. El Adobe no es responsable de esta degradación del rendimiento. Los clientes que exceden de manera consistente una protección de rendimiento pueden optar por licenciar capacidad adicional para evitar la degradación del rendimiento. |
| **Protecciones reforzadas por el sistema (límite estricto)** | La interfaz de usuario o la API de Real-Time CDP aplican las protecciones impuestas por el sistema. Estos son límites que no se pueden superar, ya que la IU y la API le bloquearán el acceso o devolverán un error. |

{style="table-layout:auto"}

## Información sobre licencias y derechos de Real-Time CDP {#product-descriptions}

Además, consulte los vínculos de la descripción del producto a continuación para obtener información sobre las licencias y las autorizaciones en función de la edición y el nivel de Real-Time CDP que haya adquirido:

* [Todas las descripciones de productos de Adobe](https://helpx.adobe.com/legal/product-descriptions.html?lang=es)
* [Real-time Customer Data Platform (edición B2C - paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (edición B2P - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (edición B2B - Paquetes Prime y Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Protecciones para otras aplicaciones de Experience Platform  {#guardrails-other-aep-apps}

Existen protecciones similares para otras aplicaciones de Experience Platform. Visite los siguientes enlaces para obtener más información:

* [protecciones de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [protecciones de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## Pasos siguientes

Después de comprender las protecciones que se aplican a varias áreas y servicios de Real-Time CDP, puede seguir junto con una [ejemplo de uso de una implementación de Real-Time CDP](/help/rtcdp/get-started.md).
