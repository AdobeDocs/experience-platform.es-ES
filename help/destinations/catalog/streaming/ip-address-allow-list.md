---
keywords: Dirección IP, rango de IP, destinos de lista de permitidos, lista de permitidos, destinos de flujo de lista de permitidos
title: LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo
type: Documentation
description: Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar de forma segura los datos del Experience Platform a su extremo de API HTTP REST, Amazon Kinesis o Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 4d71e246c8ce92cbdae4d248568cf32ab44ac82a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe recomienda marcar esta página y volver a visitarla cada tres meses para buscar las últimas direcciones IP. Adobe no proporciona notificaciones de nuevos rangos de IP.
> * La lista de IP documentadas aquí *no* se aplican a cualquier destino que genere con [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## Información general {#overview}

Los intervalos de IP documentados aquí se aplican a los siguientes destinos:

* [Destino de la API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

El tráfico saliente desde el Experience Platform a estos destinos siempre pasa por las direcciones IP enumeradas en esta página.

Esta página proporciona rangos de IP que puede agregar a la lista de permitidos para exportar de forma segura los datos del Experience Platform al extremo HTTP. [!DNL Amazon Kinesis]o [!DNL Azure Event Hubs] instancia. Esta funcionalidad es especialmente útil si el extremo HTTP se encuentra detrás de un firewall empresarial o si los estándares de seguridad y cumplimiento de la empresa requieren que se incluida en la lista de permitidos una lista de intervalos de IP.

Puede definir los controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

Adobe recomienda agregar los siguientes rangos de IP a una lista de permitidos antes de trabajar con los destinos mencionados anteriormente en esta página. Si no se añade el intervalo IP específico de la región a la lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar estos destinos de flujo continuo.

## VA7: Clientes de EE. UU. y América {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2: Clientes de EMEA {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: Clientes de APAC {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`