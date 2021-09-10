---
title: Conexión de Audiencias personalizadas de twitter
description: Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---


# [!DNL Twitter Custom Audiences] connection

## Información general {#overview}

Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Antes de configurar su destino [!DNL Twitter Custom Audiences], asegúrese de revisar los siguientes requisitos previos de Twitter que necesita cumplir.

1. Su cuenta [!DNL Twitter Ads] debe ser elegible para publicidad. Las nuevas cuentas [!DNL Twitter Ads] no pueden anunciarse en las dos primeras semanas después de crearse.
2. La cuenta de usuario de Twitter a la que autorizó el acceso en [!DNL Twitter Audience Manager] debe tener el permiso *[!DNL Partner Audience Manager]* habilitado.


## Identidades compatibles {#supported-identities}

[!DNL Twitter Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| device_id | ID de IDFA/AdID/Android | Adobe Experience Platform admite Google Advertising ID (GAID) y Apple ID para anunciantes (IDFA). Asigne estos espacios de nombres o atributos del esquema de origen según corresponda en el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino. |
| email | Direcciones de correo electrónico del usuario | Asigne a este campo sus direcciones de correo electrónico de texto sin formato y sus direcciones de correo electrónico con hash SHA256. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación. Si crea un hash con las direcciones de correo electrónico de los clientes antes de cargarlas en Adobe Experience Platform, tenga en cuenta que estas identidades deben tener un cifrado hash con SHA256, sin ningún coste adicional. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) con los identificadores utilizados en el destino Audiencias personalizadas de Twitter.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Twitter Custom Audiences], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso n.º 1

Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform como [!DNL List Custom Audiences] en Twitter.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su ID de  [!DNL Twitter Ads] cuenta. Esto se puede encontrar en la configuración de [!DNL Twitter Ads].

## Activar segmentos en este destino {#activate}

Lea [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionales {#additional-resources}

Al asignar segmentos de audiencia a Twitter, asegúrese de cumplir los siguientes requisitos de nomenclatura de segmentos:

1. Proporcione nombres de asignación de segmentos legibles en lenguaje natural. Se recomienda utilizar el mismo nombre que se utilizó para los segmentos de Experience Platform.
2. No utilice caracteres especiales (+ &amp; , % : ; @ / = ? $) en nombres de asignación de segmentos y segmentos. Si el nombre del segmento del Experience Platform contiene estos caracteres, elimínelos antes de asignar el segmento a un destino de Twitter.

Puede encontrar más información sobre [!DNL List Custom Audiences] en Twitter en la [documentación de Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).