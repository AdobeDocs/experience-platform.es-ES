---
title: Destino del Marketo Engage
description: Marketo Engage es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---


# (Beta) destino del Marketo Engage {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>El destino de Marketo Engage en Adobe Experience Platform está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

## Información general {#overview}

Marketo Engage es la única solución integral de administración de experiencias del cliente (CXM) para marketing, publicidad, análisis y comercio. Permite automatizar y administrar actividades desde la administración de posibles clientes de CRM y la participación de los clientes hasta el marketing basado en cuentas y la atribución de ingresos.

El conector de segmento permite a los especialistas en marketing insertar los segmentos creados en Adobe Experience Platform en Marketo, donde aparecerán como listas estáticas.

## Identidades compatibles {#supported-identities}

| Identidad de Target | Descripción |
|---|---|
| ECID | Un espacio de nombres que representa ECID. Este espacio de nombres también puede ser referenciado por los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte el siguiente documento sobre [ECID](/help/identity-service/ecid.md) para obtener más información. |
| Correo electrónico | Área de nombres que representa una dirección de correo electrónico. Este tipo de área de nombres suele estar asociado a una sola persona y, por lo tanto, se puede utilizar para identificar a esa persona en diferentes canales. |

## Tipo de exportación {#export-type}

Exportación de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino del Marketo Engage.

## Configurar {#set-up}

Las instrucciones sobre cómo configurar el destino [se encuentran aquí](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

## Uso y administración de datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.
