---
title: Conexión de Audiencias personalizadas de twitter
description: Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Twitter Custom Audiences] connection

## Información general {#overview}

Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Antes de configurar el [!DNL Twitter Custom Audiences] , asegúrese de revisar los siguientes requisitos previos de Twitter que necesita cumplir.

1. Su [!DNL Twitter Ads] La cuenta debe ser elegible para publicidad. Nuevo [!DNL Twitter Ads] las cuentas no pueden anunciarse en las dos primeras semanas después de crearse.
2. Su cuenta de usuario de Twitter para la que autorizó el acceso en [!DNL Twitter Audience Manager] debe tener la variable *[!DNL Partner Audience Manager]* permiso habilitado.


## Identidades compatibles {#supported-identities}

[!DNL Twitter Custom Audiences] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| device_id | ID de IDFA/AdID/Android | Adobe Experience Platform admite Google Advertising ID (GAID) y Apple ID para anunciantes (IDFA). Asigne estas áreas de nombres o atributos del esquema de origen según corresponda en la variable [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino. |
| email | Direcciones de correo electrónico del usuario | Asigne a este campo sus direcciones de correo electrónico de texto sin formato y sus direcciones de correo electrónico con hash SHA256. Si el campo de origen contiene atributos sin hash, marque la casilla de verificación **[!UICONTROL Aplicar transformación]** para [!DNL Platform] hash automático de los datos al activarlos. Si crea un hash con las direcciones de correo electrónico de los clientes antes de cargarlas en Adobe Experience Platform, tenga en cuenta que estas identidades deben tener un cifrado hash con SHA256, sin ningún coste adicional. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores utilizados en el destino Audiencias personalizadas de Twitter. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Twitter Custom Audiences] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

### Caso de uso n.º 1

Dirija la campaña a sus seguidores y clientes existentes en Twitter y cree campañas de remarketing relevantes activando las audiencias creadas en Adobe Experience Platform como [!DNL List Custom Audiences] en Twitter.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su [!DNL Twitter Ads] ID de cuenta. Esto se puede encontrar en su [!DNL Twitter Ads] configuración.

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionales {#additional-resources}

Al asignar segmentos de audiencia a Twitter, asegúrese de cumplir los siguientes requisitos de nomenclatura de segmentos:

1. Proporcione nombres de asignación de segmentos legibles en lenguaje natural. Se recomienda utilizar el mismo nombre que se utilizó para los segmentos de Experience Platform.
2. No utilice caracteres especiales (+ &amp; , % : ; @ / = ? $) en nombres de asignación de segmentos y segmentos. Si el nombre del segmento del Experience Platform contiene estos caracteres, elimínelos antes de asignar el segmento a un destino de Twitter.

Más información sobre [!DNL List Custom Audiences] en Twitter se puede encontrar en la [Documentación de twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
