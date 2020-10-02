---
keywords: Azure event hub destination;azure event hub;azure eventhub
title: (Beta) Destino de los centros de Evento de Azure
seo-title: (Beta) Destino de los centros de Evento de Azure
description: Cree una conexión saliente en tiempo real con el almacenamiento de los centros de Evento de Azure para transmitir datos desde el Experience Platform.
seo-description: Cree una conexión saliente en tiempo real con el almacenamiento de los centros de Evento de Azure para transmitir datos desde el Experience Platform.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] destino

>[!IMPORTANT]
>
>El [!DNL Azure Event Hubs] destino en Adobe Real-time CDP está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

[!DNL Azure Event Hubs] es una plataforma de transmisión de datos importantes y un servicio de ingestión de evento. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un concentrador de evento se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento o lotes.

Puede crear una conexión saliente en tiempo real con el [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Azure Event Hubs], consulte la documentación de [Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] través de llamadas de API, consulte el tutorial [de API de destinos de](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)flujo continuo.
* Para conectarse a [!DNL Azure Event Hubs] mediante la interfaz de usuario CDP en tiempo real de Adobe, consulte las secciones a continuación.

![AWS Kinesis en la interfaz de usuario](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Casos de uso {#use-cases}

Al utilizar los destinos de flujo continuo, como [!DNL Azure Event Hubs]el, puede transmitir fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a los sistemas que elija.

Por ejemplo, un cliente potencial descargó un documento técnico que los califica en un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento en el que se encuentra el cliente potencial al [!DNL Azure Event Hubs] destino, recibirá este evento en [!DNL Azure Event Hubs]. Allí puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial sobre el evento, como piensa que funcionaría mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Exportación** de perfil: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [de activación de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destino.\

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos [!DNL Azure Event Hubs].

Para [!DNL Azure Event Hubs] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

### En el paso Autenticación {#authentication-step}

* **[!UICONTROL Nombre]** de clave SAS y clave **** SAS: Rellene el nombre y la clave de la clave SAS. Obtenga información sobre la autenticación con [!DNL Azure Event Hubs] claves SAS en la documentación [de](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Área de nombres]**: Rellene su [!DNL Azure Event Hubs] Área de nombres. Obtenga información sobre [!DNL Azure Event Hubs] Áreas de nombres en la documentación [de](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrada requerida en el paso de autenticación](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### En el paso Configuración {#setup-step}

* **[!UICONTROL Nombre]**: Rellene un nombre para la conexión a [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: Proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes Premium&quot;, &quot;Hombres interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Proporcione un nombre para el flujo al [!DNL Azure Event Hubs] destino.

![Datos requeridos en el paso de configuración](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.


## Datos exportados {#exported-data}

Los datos exportados [!DNL Experience Platform] llegan al formato [!DNL Azure Event Hubs] JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha cualificado para un segmento determinado y ha salido de otro. Las identidades de este cliente potencial son ECID y correo electrónico.

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
>* [Conectar con los centros de Evento de Azure y activar datos mediante llamadas de API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destino de Kinesis de AWS](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md)