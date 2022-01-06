---
title: Conexión de lista de clientes de pinterest
description: Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 90aa0d16851443255dd4828e9f28330a89a12692
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# [!DNL Pinterest Customer List] connection

## Información general {#overview}

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

>[!IMPORTANT]
>
>Este destino lo creó el equipo de Pinterest. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en https://help.pinterest.com/en/contact.

## Requisitos previos {#prerequisites}

* El usuario tendría que autenticarse con una cuenta de Pinterest que tenga acceso a la cuenta del anunciante a la que desee agregar una audiencia. Puede encontrar más información sobre cómo compartir cuentas de anunciantes [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Concretamente, el usuario necesitaría los niveles de acceso de &quot;audiencia&quot;.
* Puede encontrar más información sobre los formatos de identidad de listas de clientes [here](https://help.pinterest.com/en/business/article/audience-targeting).


## Identidades compatibles {#supported-identities}

La variable [!DNL Pinterest Customer List] destination admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, asigne las identidades deseadas al campo de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Asigne la variable *GAID* área de nombres de identidad de origen al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Asigne la variable *IDFA* área de nombres de identidad de origen al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest. |
| CORREO ELECTRÓNICO | Direcciones de correo electrónico (borrar texto o con hash con el algoritmo SHA256) | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. <br> Asigne la variable *Correo electrónico* o *Email_LC_SHA256* área de nombres de identidad de origen al campo de identidad de destino *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación {#export-type}

**Exportación de segmentos** : exporta todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de la lista de clientes de Pinterest.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL Pinterest Customer List] destino, aquí hay ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.


### Caso de uso n.º 1

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).


### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID del anunciante]**: Su ID de anunciante de Pinterest.

## Activar segmentos en este destino {#activate}

Lectura [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige el control de datos; consulte [Información general sobre la administración de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionales {#additional-resources}

Consulte la [Página del Centro de ayuda de pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obtener más información.
