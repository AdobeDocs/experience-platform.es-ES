---
title: Información general sobre Azure Event Hubs Source Connector
description: Obtenga información sobre cómo conectar Azure Event Hubs a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] origen

>[!IMPORTANT]
>
>* El origen [!DNL Azure Event Hubs] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.
>
>* Ahora puede usar el origen [!DNL Azure Event Hubs] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure]. Puede llevar los datos de estos sistemas a Experience Platform.

Las fuentes de almacenamiento en la nube pueden introducir sus propios datos en Experience Platform sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes. Experience Platform le permite traer datos de [!DNL Event Hubs] en tiempo real.

## Escalando con [!DNL Event Hubs]

El factor de escala de su instancia de [!DNL Event Hubs] debe aumentarse si necesita introducir datos de gran volumen, aumentar el paralelismo o aumentar la velocidad de la ingesta en Experience Platform.

### Ingresar datos de mayor volumen

En la actualidad, el volumen máximo de datos que puede traer de su cuenta de [!DNL Event Hubs] a Experience Platform es de 2000 registros por segundo. Para ampliar e introducir datos de mayor volumen, póngase en contacto con su representante de Adobe.

### Aumentar el paralelismo en [!DNL Event Hubs] y Experience Platform

El paralelismo se refiere a la ejecución simultánea de las mismas tareas en varias unidades de procesamiento para aumentar la velocidad y el rendimiento. Puede aumentar el paralelismo en el lado [!DNL Event Hubs] mediante el aumento de la partición o la adquisición de más unidades de procesamiento para la cuenta [!DNL Event Hubs]. Consulte este [[!DNL Event Hubs] documento sobre la escala](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) para obtener más información.

Para aumentar la velocidad de ingesta en Experience Platform, Experience Platform debe aumentar el número de tareas en el conector de origen para leer desde las particiones [!DNL Event Hubs]. Una vez que haya aumentado el paralelismo en el lado [!DNL Event Hubs], póngase en contacto con su representante de Adobe para escalar las tareas de Experience Platform en función de su nueva partición. Actualmente, este proceso no está automatizado.

## Usar una red virtual para conectar a [!DNL Event Hubs] con Experience Platform

Puede configurar una red virtual para conectar [!DNL Event Hubs] a Experience Platform con las medidas del firewall habilitadas. Para configurar una red virtual, vaya a este [[!DNL Event Hubs] documento del conjunto de reglas de red](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) y siga los pasos que se indican a continuación:

* Seleccione **Probarlo** en el panel API de REST;
* Autentique su cuenta de [!DNL Azure] con sus credenciales en el mismo explorador;
* Seleccione el área de nombres [!DNL Event Hubs], el grupo de recursos y la suscripción que desea llevar a Experience Platform y, a continuación, seleccione **EJECUTAR**;
* En el cuerpo JSON que aparece, agregue la siguiente subred de Experience Platform bajo `virtualNetworkRules` dentro de `properties`:


>[!IMPORTANT]
>
>Debe hacer una copia de seguridad del cuerpo de JSON que recibe antes de actualizar `virtualNetworkRules` con la subred de Experience Platform, ya que contiene las reglas de filtrado de IP existentes. De lo contrario, las reglas se eliminarán después de la llamada.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consulte la lista siguiente para ver diferentes regiones de subredes de Experience Platform:

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
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Consulte el siguiente [[!DNL Event Hubs] documento](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) para obtener más información sobre los conjuntos de reglas de red.

## Conectar [!DNL Event Hubs] a Experience Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Event Hubs] a Experience Platform mediante API o la interfaz de usuario:

### Uso de API

* [Crear una conexión de origen de Event Hubs mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Recopilación de datos de flujo continuo mediante la API de Flow Service](../../tutorials/api/collect/streaming.md)

### Uso de la IU

* [Crear una conexión de origen de Event Hubs en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configure un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
