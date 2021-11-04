---
keywords: Experience Platform;inicio;temas populares;centros de eventos de Azure;centros de eventos de azure;centros de eventos;centros de eventos
solution: Experience Platform
title: Descripción general del conector de origen de los centros de eventos de Azure
topic-legacy: overview
description: Obtenga información sobre cómo conectar los centros de eventos de Azure a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: cda9ca9c560b1af2147c00ea4e89dff09b7428ba
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] connector

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform]y [!DNL Azure]. Puede introducir los datos de estos sistemas en Platform.

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a Platform sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . Platform le permite introducir datos de [!DNL Event Hubs] en tiempo real.

## Usar una red virtual para conectarse [!DNL Event Hubs] a Platform

Puede configurar una red virtual para conectarse [!DNL Event Hubs] a Platform mientras tenga habilitadas las medidas del cortafuegos. Para configurar una red virtual, vaya a esta [[!DNL Event Hubs] documento de conjunto de reglas de red](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) y, a continuación, seleccione **Pruébelo** del panel API de REST. A continuación, autentique su [!DNL Azure] cuenta con sus credenciales y, a continuación, seleccione la [!DNL Event Hubs] área de nombres, grupo de recursos y suscripción que desea traer a Platform.

Una vez configurada, actualice la variable **cuerpo de la solicitud** con el JSON que corresponde a su región de red, de la lista siguiente:

>[!TIP]
>
>Debe realizar una copia de seguridad de las reglas de filtrado de IP del cortafuegos existentes, ya que se eliminarán después de esta llamada.

### VA7: América del Norte

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
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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

La siguiente documentación proporciona información sobre cómo conectar [!DNL Event Hubs] a Platform mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de centros de eventos mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Recopilación de datos de flujo continuo mediante la API del servicio de flujo](../../tutorials/api/collect/streaming.md)

### Uso de la interfaz de usuario

- [Creación de una conexión de origen de centros de eventos en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configurar un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
