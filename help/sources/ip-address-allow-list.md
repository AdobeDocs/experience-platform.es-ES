---
description: Obtenga información acerca de las direcciones IP que debe agregar a la lista de permitidos para utilizar correctamente las fuentes de Adobe Experience Platform.
title: LISTA DE PERMITIDOS de direcciones IP para orígenes
exl-id: 40093c80-dbdb-4dc1-97bb-81a8200b731f
source-git-commit: e2403b235b4cfee37761ebd683a1fb8662061406
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# LISTA DE PERMITIDOS de direcciones IP

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP de origen adecuado, puede permitir que el tráfico fluya para el servicio de transferencia de datos. Las siguientes direcciones IP deben agregarse a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes.

## LISTA DE PERMITIDOS de direcciones IP para orígenes que se conectan a Experience Platform en [!DNL Azure] {#azure}

### Orígenes de lotes en Experience Platform en [!DNL Azure] {#batch}

Debe agregar las siguientes direcciones IP a la lista de permitidos para permitir que el tráfico fluya para el servicio de transferencia de datos para los orígenes de lotes.

>[!BEGINTABS]

>[!TAB VA7: América del Norte]

#### VA7: Norteamérica

- `20.42.2.0/23`
- `20.42.4.0/26`
- `20.42.64.0/28`
- `20.49.111.0/29`
- `40.71.14.32/28`
- `40.78.229.96/28`
- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`
- `20.98.198.224/29`
- `20.119.28.57/32`
- `20.232.89.104/29`
- `20.98.195.172/32`
- `172.210.218.144/28`
- `48.211.4.136/29`
- `48.211.4.144/28`
- `48.211.4.160/29`
- `40.84.85.144/28`
- `40.84.85.192/28`

>[!TAB NLD2: Europa]

#### NLD2: Europa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

>[!TAB AUS5: Australia]

#### AUS5: Australia

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `20.53.45.0/24`
- `20.53.46.0/26`
- `40.79.163.80/28`
- `40.79.171.160/28`
- `20.213.194.144/29`
- `20.227.120.32/27`

>[!TAB CAN2: Canadá]

#### CAN2: Canadá

- `13.71.175.80/28`
- `20.38.147.224/28`
- `20.48.201.0/26`
- `20.116.47.72/29`
- `52.228.80.128/25`
- `52.228.81.0/26`
- `52.228.86.144/29`
- `52.246.155.224/28`

>[!TAB IND2: India]

#### IND2: India

- `20.43.121.48/28`
- `20.192.42.0/24`
- `20.192.43.0/26`
- `20.192.102.80/28`
- `20.204.193.112/29`
- `40.80.51.160/28`
- `52.140.104.128/25`
- `52.140.105.0/26`
- `52.140.108.208/29`

>[!ENDTABS]

### Transmitiendo orígenes en Experience Platform en [!DNL Azure] {#streaming}

Debe agregar las siguientes direcciones IP a su lista de permitidos para permitir que el tráfico fluya para el servicio de transferencia de datos para orígenes de transmisión por secuencias como [[!DNL Amazon Kinesis]](./connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hub]](./connectors/cloud-storage/eventhub.md), [[!DNL Google PubSub]](./connectors/cloud-storage/google-pubsub.md) y [[!DNL Snowflake Streaming]](./connectors/databases/snowflake-streaming.md).

>[!BEGINTABS]

>[!TAB VA7: América del Norte]

#### VA7: Norteamérica

- `52.254.106.240/28`
- `52.254.107.144/28`
- `20.22.83.112`
- `20.186.185.181`
- `52.254.106.208/28`
- `52.254.106.192/28`
- `52.254.106.144/28`
- `20.14.241.153`
- `52.254.107.32/28`
- `52.254.107.128/28`
- `52.254.107.64/28`
- `52.254.106.224/28`
- `52.254.106.176/28`
- `52.254.107.0/28`
- `52.254.107.16/28`
- `20.186.185.239`
- `52.254.105.192/28`
- `40.70.154.136/29`
- `52.254.106.160/28`
- `52.254.106.0/28`
- `52.254.107.80/28`
- `20.186.185.227`

>[!TAB NLD2: Europa]

#### NLD2: Europa

- `51.138.17.0/28`
- `51.138.16.176/28`
- `51.138.17.96/28`
- `51.138.16.160/28`
- `20.31.145.248`
- `51.138.16.128/28`
- `51.138.12.160/28`
- `51.138.16.240/28`
- `51.138.17.32/28`
- `51.138.16.224/28`
- `51.138.16.208/28`
- `51.138.12.11`
- `51.138.16.144/28`
- `51.138.17.64/28`
- `51.138.17.48/28`
- `51.138.17.112/28`
- `51.138.17.16/28`
- `51.138.17.80/28`
- `51.138.12.94`
- `20.126.189.248`
- `51.138.16.192/28`
- `51.138.12.100`

>[!TAB AUS5: Australia]

#### AUS5: Australia

- `20.40.188.194`
- `20.53.206.128`
- `20.43.105.0/28`
- `20.43.104.96/28`
- `20.40.191.96/28`
- `20.43.105.32/28`
- `20.40.191.240/28`
- `20.43.104.128/28`
- `20.43.104.0/28`
- `20.43.104.16/28`
- `20.43.105.48/28`
- `20.43.104.144/28`
- `20.40.188.227`
- `20.43.104.160/28`
- `20.43.104.64/28`
- `20.43.104.112/28`
- `20.43.104.80/28`
- `20.43.104.32/28`
- `20.43.105.16/28`
- `20.40.191.224/28`
- `20.43.104.192/28`
- `20.40.188.166`
- `20.43.104.176/28`
- `20.227.35.177`
- `20.43.104.48/28`

>[!TAB CAN2: Canadá]

#### CAN2: Canadá

- `20.200.70.240/28`
- `20.200.94.116`
- `20.200.71.48/28`
- `20.200.70.224/28`
- `20.104.46.64/28`
- `20.200.71.128/28`
- `20.200.71.0/28`
- `20.200.71.176/28`
- `20.200.71.16/28`
- `20.104.46.80/28`
- `20.200.71.112/28`
- `20.116.147.168`
- `20.200.93.180`
- `20.200.71.80/28`
- `20.116.145.94`
- `20.200.71.160/28`
- `20.200.94.83`
- `20.200.71.96/28`
- `20.104.46.160/28`
- `20.200.71.64/28`
- `20.200.71.32/28`
- `20.104.46.128/28`
- `20.200.70.208/28`
- `20.200.70.192/28`
- `20.200.71.144/28`

>[!TAB GBR9: Reino Unido]

#### GBR9: Reino Unido

- `20.254.2.128/28`
- `20.26.131.71`
- `20.108.202.84`
- `20.254.4.16/28`
- `20.254.4.96/28`
- `20.254.2.32/28`
- `20.26.64.240/28`
- `20.254.4.64/28`
- `20.254.3.48/28`
- `20.254.4.32/28`
- `20.254.3.240/28`
- `20.108.119.100`
- `20.254.3.192/28`
- `20.254.3.176/28`
- `20.254.1.128/28`
- `20.254.3.144/28`
- `20.26.130.226`
- `20.26.65.0/28`
- `20.254.4.0/28`
- `20.254.3.112/28`
- `20.26.64.208/28`
- `20.254.2.208/28`
- `20.254.3.32/28`
- `20.26.128.247`
- `20.26.64.112/28`

>[!TAB IND2: India]

#### IND2: India

- `4.224.74.0/28`
- `20.244.79.80/28`
- `20.244.79.128/28`
- `4.188.4.154`
- `4.213.223.207`
- `20.244.77.16/28`
- `4.224.74.80/28`
- `4.224.74.64/28`
- `4.224.74.96/28`
- `4.188.4.99`
- `20.244.79.0/28`
- `20.244.79.224/28`
- `20.244.77.208/28`
- `4.188.4.11`
- `20.244.79.208/28`
- `20.244.78.0/28`
- `20.244.79.144/28`
- `20.244.74.112/28`
- `20.244.79.192/28`
- `20.244.79.48/28`
- `20.244.79.16/28`
- `20.244.78.208/28`
- `4.213.40.145`
- `4.188.4.167`
- `20.244.77.160/28`
- `20.244.77.0/28`
- `4.188.4.138`

>[!ENDTABS]

## Direcciones IP a la lista de permitidos para la conexión de orígenes a Experience Platform en [!DNL Amazon Web Services] (AWS) {#aws}

Debe agregar la siguiente dirección IP a la lista de permitidos para conectar el origen a Experience Cloud en AWS:.

### VA6

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`