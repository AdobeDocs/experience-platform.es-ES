---
keywords: Experience Platform;inicio;temas populares;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Información general sobre el conector de origen de Azure Event Hubs
description: Obtenga información sobre cómo conectar Azure Event Hubs a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] conector

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform], y [!DNL Azure]. Puede llevar los datos de estos sistemas a Platform.

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes. Platform le permite introducir datos de [!DNL Event Hubs] en tiempo real.

## Escala con [!DNL Event Hubs]

El factor de escala de su [!DNL Event Hubs] La instancia de debe aumentarse si necesita introducir datos de alto volumen, aumentar el paralelismo o aumentar la velocidad de la plataforma de ingesta.

### Ingresar datos de mayor volumen

En este momento, el volumen máximo de datos que puede traer de su [!DNL Event Hubs] cuenta a Platform es de 2000 registros por segundo. Para ampliar e ingerir datos de mayor volumen, póngase en contacto con su representante de Adobe.

### Aumentar el paralelismo en [!DNL Event Hubs] y Platform

El paralelismo se refiere a la ejecución simultánea de las mismas tareas en varias unidades de procesamiento para aumentar la velocidad y el rendimiento. Puede aumentar el paralelismo en la [!DNL Event Hubs] al aumentar la partición o al adquirir más unidades de procesamiento para su [!DNL Event Hubs] cuenta. Ver esto [[!DNL Event Hubs] documento sobre escalado](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) para obtener más información.

Para aumentar la velocidad de ingesta en el lado de la plataforma, Platform debe aumentar el número de tareas en el conector de origen para leer desde el [!DNL Event Hubs] particiones. Una vez que haya aumentado el paralelismo en la [!DNL Event Hubs] Póngase en contacto con su representante de Adobe para escalar las tareas de Platform en función de su nueva partición. Actualmente, este proceso no está automatizado.

## Usar una red virtual para conectarse a [!DNL Event Hubs] a Platform

Puede configurar una red virtual para conectarse [!DNL Event Hubs] a Platform mientras tiene las medidas del cortafuegos activadas. Para configurar una red virtual, vaya a [[!DNL Event Hubs] documento de conjunto de reglas de red](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) y siga los pasos que se indican a continuación:

* Seleccionar **Pruébelo.** desde el panel API de REST;
* Autentique su [!DNL Azure] cuenta con sus credenciales en el mismo explorador;
* Seleccione el [!DNL Event Hubs] área de nombres, grupo de recursos y suscripción que desea llevar a Platform y, a continuación, seleccione **EJECUTAR**;
* En el cuerpo JSON que aparece, agregue la siguiente subred de Platform debajo de `virtualNetworkRules` interior `properties`:


>[!IMPORTANT]
>
>Antes de actualizar, debe realizar una copia de seguridad del cuerpo de JSON que recibe `virtualNetworkRules` con la subred de Platform, ya que contiene las reglas de filtrado de IP existentes. De lo contrario, las reglas se eliminarán después de la llamada.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consulte la lista siguiente para ver las diferentes regiones de las subredes de Platform:

### VA7: Norteamérica

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Australia

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Consulte lo siguiente [[!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) para obtener más información sobre los conjuntos de reglas de red.

## Connect [!DNL Event Hubs] a Platform

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Event Hubs] Vaya a Platform mediante las API o la interfaz de usuario de:

### Uso de API

* [Crear una conexión de origen de Event Hubs mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Recopilación de datos de flujo continuo mediante la API de Flow Service](../../tutorials/api/collect/streaming.md)

### Uso de la IU

* [Crear una conexión de origen de Event Hubs en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configure un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
