---
keywords: Dirección IP, intervalo de IP, destinos de lista de permitidos, lista de permitidos, destinos de flujo de lista de permitidos
title: LISTA DE PERMITIDOS de direcciones IP para destinos de flujo continuo
type: Documentation
description: Esta página proporciona rangos de IP que puede agregar a la lista de permitidos para exportar de forma segura datos de Experience Platform a la instancia de extremo de la API HTTP REST, Amazon Kinesis o Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 851565b4c40452d102eff134533c9d44ea19ca76
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# LISTA DE PERMITIDOS de direcciones IP para destinos basados en API de streaming {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. Adobe no notifica nuevos intervalos de IP.

## Información general {#overview}

Los intervalos de IP documentados en esta página se aplican a los siguientes destinos:

* [Destinos empresariales avanzados](../../destination-types.md#advanced-enterprise-destinations): [Destino API HTTP](./http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [Destinos de exportación de audiencias de streaming](../../destination-types.md#streaming-destinations), como [Audiencia en tiempo real Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), integraciones basadas en API con [Salesforce Marketing Cloud](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) y [Oracle Eloqua](/help/destinations/catalog/email-marketing/oracle-eloqua-api.md)
* Destinos públicos o privados creados mediante [Destination SDK](../../destination-sdk/getting-started.md)

El tráfico saliente desde Experience Platform a estos destinos siempre pasa por las direcciones IP enumeradas en esta página.

Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar con seguridad datos de Experience Platform a los destinos enumerados arriba. Esta funcionalidad es especialmente útil si el extremo HTTP se encuentra detrás de un cortafuegos empresarial o si los estándares de seguridad y conformidad de la empresa requieren que una lista de intervalos de IP esté incluida en la lista de permitidos.

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

## Cuándo realizar la lista de permitidos de las direcciones IP en esta página {#when-to-allowlist}

Si la directiva de organización requiere que lista de permitidos direcciones IP para el tráfico entrante, debe agregar los intervalos de IP de las siguientes categorías a la lista de permitidos antes de trabajar con los destinos mencionados anteriormente en esta página:

1. Todas las [direcciones IP globales](#global)
2. Además de las direcciones IP globales, añada las direcciones IP correspondientes a la región en la que está aprovisionado desde la lista situada más abajo en la página. Si no se añade el intervalo de IP específico de su región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar estos destinos de flujo continuo.

## Direcciones IP globales {#global}

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

Además de estas direcciones IP globales, debe lista de permitidos las direcciones IP de la región donde su organización está aprovisionada de la lista siguiente.

## VA7: Clientes de EE. UU. y América {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6: clientes de EE. UU. y América que se ejecutan en AWS {#aws}

El rango de IP siguiente se aplica a los clientes de Experience Platform que se ejecutan en Amazon Web Service (AWS). Consulte la [descripción general de Experience Platform Multi-Cloud](../../../landing/multi-cloud.md) para obtener más información.

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2: Clientes de EMEA {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5: Clientes de APAC {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2: Clientes de Canadá {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9: Clientes de Gran Bretaña {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2: Clientes de India {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`

