---
keywords: Destino del centro de eventos de Azure;centro de eventos de azure;azure eventhub
title: (Beta) Conexión de los centros de eventos de Azure
description: Cree una conexión saliente en tiempo real con el almacenamiento de los centros de eventos de Azure para transmitir datos desde el Experience Platform.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# (Beta) Conexión [!DNL Azure Event Hubs]

## Información general {#overview}

>[!IMPORTANT]
>
>El destino [!DNL Azure Event Hubs] en Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

[!DNL Azure Event Hubs] es una plataforma de transmisión de grandes datos y un servicio de ingesta de eventos. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un centro de eventos se pueden transformar y almacenar utilizando cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento/lotes.

Puede crear una conexión saliente en tiempo real con su almacenamiento [!DNL Azure Event Hubs] para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Azure Event Hubs], consulte la [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] mediante programación, consulte el [tutorial de API de destinos de transmisión](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Azure Event Hubs] mediante la interfaz de usuario de Platform, consulte las secciones a continuación.

![AWS Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casos de uso {#use-cases}

Al utilizar destinos de flujo continuo como [!DNL Azure Event Hubs], puede alimentar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados en sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un libro blanco que los califica para un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento al que pertenece el cliente potencial al destino [!DNL Azure Event Hubs], recibiría este evento en [!DNL Azure Event Hubs]. En este caso, puede utilizar un enfoque propio y describir la lógica empresarial además del evento, ya que considera que funcionará mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

Consulte [Flujo de trabajo de destinos de almacenamiento en la nube ](./workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento en la nube, incluido [!DNL Azure Event Hubs].

Para destinos [!DNL Azure Event Hubs] , introduzca la siguiente información en el flujo de trabajo de creación de destino:

## Paso de autenticación {#authentication-step}

* **[!UICONTROL SAS Key Name]** y  **[!UICONTROL SAS Key]**: Rellene el nombre y la clave de la clave SAS. Obtenga información sobre cómo autenticarse en [!DNL Azure Event Hubs] con claves SAS en la [documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Rellene el  [!DNL Azure Event Hubs] espacio de nombres. Obtenga información sobre los espacios de nombres [!DNL Azure Event Hubs] en la [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Entrada necesaria en el paso de autenticación](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

## Paso de configuración {#setup-step}

* **[!UICONTROL Name]**: Rellene un nombre para la conexión a  [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes de nivel Premium&quot;, &quot;Hombres interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Proporcione un nombre para la emisión a su  [!DNL Azure Event Hubs] destino.
* **[!UICONTROL Marketing actions]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![Datos necesarios en el paso de configuración](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Datos exportados {#exported-data}

Los datos [!DNL Experience Platform] exportados llegan a [!DNL Azure Event Hubs] en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este cliente potencial son ECID y correo electrónico.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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