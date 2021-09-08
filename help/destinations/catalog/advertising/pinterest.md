---
title: Conexión de lista de clientes de pinterest
description: Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# [!DNL Pinterest Customer List] connection

## Información general {#overview}

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

>[!IMPORTANT]
>
>Este destino lo creó el equipo de Pinterest. Para cualquier consulta o solicitud de actualización, póngase en contacto con ellos directamente en https://help.pinterest.com/en/contact.

## Requisitos previos {#prerequisites}

* El usuario tendría que autenticarse con una cuenta de Pinterest que tenga acceso a la cuenta del anunciante a la que desee agregar una audiencia. Los detalles sobre cómo compartir cuentas de anunciantes se pueden encontrar [aquí](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Concretamente, el usuario necesitaría los niveles de acceso de &quot;audiencia&quot;.
* Los detalles sobre los formatos de identidad de lista de clientes se pueden encontrar [aquí](https://help.pinterest.com/en/business/article/audience-targeting).


## Identidades compatibles {#supported-identities}

El destino [!DNL Pinterest Customer List] admite la activación de identidades descritas en la siguiente tabla. Obtenga más información sobre [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

En el [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flujo de trabajo de activación de destino, asigne las identidades deseadas al campo de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Asigne el espacio de nombres de la identidad de origen *GAID* al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Asigne el espacio de nombres de la identidad de origen *IDFA* al campo de identidad de destino *pinterest_audience*. Las identidades se distinguen y se resuelven tras la incorporación de datos a Pinterest. |
| CORREO ELECTRÓNICO | Direcciones de correo electrónico (borrar texto o con hash con el algoritmo SHA256) | Adobe Experience Platform admite las direcciones de correo electrónico con texto sin formato y con hash SHA 256. <br> Asigne el área de nombres de identidad de origen  ** Correo electrónico  *LC_SHA256* al campo de identidad de destino  *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en el destino de Lista de clientes de Pinterest.

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Pinterest Customer List], estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.


### Caso de uso n.º 1

Cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).



### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su ID de cuenta de anuncio de Pinterest.

## Activar segmentos en este destino {#activate}

Lea [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Uso y gobernanza de los datos {#data-usage-governance}

Todos los destinos [!DNL Adobe Experience Platform] cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, consulte la [Información general sobre el control de datos](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionales {#additional-resources}

Consulte la [página del Centro de ayuda de Pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obtener más información.
