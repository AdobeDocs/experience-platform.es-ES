---
keywords: Destino del centro de eventos de Azure;centro de eventos de azure;azure eventhub
title: Conexión (Beta) !DNL Azure Event Hubs]
description: Cree una conexión saliente en tiempo real a su almacenamiento de !DNL Azure Event Hubs] para transmitir datos desde el Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta) [!DNL Azure Event Hubs] connection

## Información general {#overview}

>[!IMPORTANT]
>
>La variable [!DNL Azure Event Hubs] el destino en Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

[!DNL Azure Event Hubs] es una plataforma de transmisión de grandes datos y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar utilizando cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento/lotes.

Puede crear una conexión saliente en tiempo real con su [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información, consulte [!DNL Azure Event Hubs], consulte la [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] mediante programación, consulte la [Tutorial de la API de destinos de flujo continuo](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Azure Event Hubs] con la interfaz de usuario de Platform, consulte las secciones siguientes.

![AWS Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Azure Event Hubs], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un libro blanco que los califica para un segmento de &quot;alta propensión a convertir&quot;. Asignando el segmento en el que se encuentra el cliente potencial a [!DNL Azure Event Hubs] destino, recibiría este evento en [!DNL Azure Event Hubs]. En este caso, puede utilizar un enfoque propio y describir la lógica empresarial además del evento, ya que considera que funcionará mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de audiencia](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre de clave SAS]** y **[!UICONTROL Clave de SAS]**: Rellene el nombre y la clave de la clave SAS. Obtenga información sobre cómo autenticarse en [!DNL Azure Event Hubs] con claves SAS en la variable [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Área de nombres]**: Rellene su [!DNL Azure Event Hubs] espacio de nombres. Obtenga información sobre [!DNL Azure Event Hubs] áreas de nombres en la variable [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nombre]**: Rellene un nombre para la conexión con [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: Proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes de nivel Premium&quot;, &quot;Hombres interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Proporcione un nombre para la emisión a su [!DNL Azure Event Hubs] destino.

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a [!DNL Azure Event Hubs] en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este cliente potencial son ECID y correo electrónico.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```


>[!MORELIKETHIS]
>
>* [Conéctese a los centros de eventos de Azure y active los datos mediante la API de servicio de flujo](../../api/streaming-destinations.md)
>* [Destino de AWS Kinesis](./amazon-kinesis.md)
>* [Tipos y categorías de destino](../../destination-types.md)

