---
title: Destino del Marketo Engage
description: Marketo Engage es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 3e2382cf4b02ea4fd40e3638b52b4719938a2ea2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# destino del Marketo Engage {#beta-marketo-engage-destination}

## Información general {#overview}

Marketo Engage es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.

El destino permite a los especialistas en marketing insertar los segmentos creados en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas.

## Identidades compatibles {#supported-identities}

| Identidad de Target | Descripción |
|---|---|
| ECID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| Correo electrónico | Área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificar a esa persona en diferentes canales. |

## Tipo de exportación {#export-type}

Exportación de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (correo electrónico, ECID) utilizados en el destino del Marketo Engage.

## Configuración del destino y activación de segmentos {#set-up}

Para obtener instrucciones detalladas sobre cómo configurar el destino y activar segmentos, lea [Insertar un segmento de Adobe Experience Platform en una lista estática de Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) en la documentación de Marketo.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->