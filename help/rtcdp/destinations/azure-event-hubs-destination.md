---
title: Destino de los centros de Evento de Azure
seo-title: Destino de los centros de Evento de Azure
description: Cree una conexión saliente en tiempo real con el almacenamiento de los centros de Evento de Azure para transmitir datos desde la plataforma de experiencia.
seo-description: Cree una conexión saliente en tiempo real con el almacenamiento de los centros de Evento de Azure para transmitir datos desde la plataforma de experiencia.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Destino de los centros de Evento de Azure

## Información general {#overview}

[!DNL Azure Event Hubs] es una plataforma de transmisión de datos importantes y un servicio de ingestión de evento. Puede recibir y procesar millones de eventos por segundo. Los datos enviados a un concentrador de evento se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento o lotes.

Puede crear una conexión saliente en tiempo real con su [!DNL Azure Event Hubs] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Azure Event Hubs], consulte la documentación de [Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Para conectarse a [!DNL Azure Event Hubs] través de llamadas de API, consulte el tutorial [de API de destinos de]flujo continuo.
* Para conectarse a [!DNL Azure Event Hubs] mediante la interfaz de usuario de CDP en tiempo real de Adobe, consulte las secciones siguientes.

![AWS Kinesis en la interfaz de usuario](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Casos de uso {#use-cases}

Al utilizar los destinos de flujo continuo, como los centros de Evento de Azure, puede suministrar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a los sistemas que elija.

Por ejemplo, un cliente potencial descargó un documento técnico que los califica en un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento en el que el cliente potencial se encuentra en el destino de los centros de Evento de Azure, recibirá este evento en los centros de Evento de Azure. Allí puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial sobre el evento, como piensa que funcionaría mejor con sus sistemas de TI empresariales.

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos [!DNL Azure Event Hubs].

Para [!DNL Azure Event Hubs] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

### En el paso Cuenta {#account-step}

* **[!UICONTROL Nombre]** de clave SAS y clave **** SAS: Rellene el nombre y la clave de la clave SAS. Obtenga información sobre la autenticación con [!DNL Azure Event Hubs] claves SAS en la documentación [de](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Área de nombres]**: Rellene su [!DNL Azure Event Hubs] Área de nombres. Obtenga información sobre [!DNL Azure Event Hubs] Áreas de nombres en la documentación [de](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrada requerida en el paso de autenticación](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### En el paso Autenticación {#authentication-step}

* **[!UICONTROL Nombre]**: Rellene un nombre para la conexión a [!DNL Azure Event Hubs].
* **[!UICONTROL Descripción]**: Proporcione una descripción de la conexión.  Ejemplos: &quot;Clientes Premium&quot;, &quot;Hombres interesados en el kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Proporcione un nombre para el flujo al [!DNL Azure Event Hubs] destino.

![Datos requeridos en el paso de configuración](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.


## Datos exportados {#exported-data}

Los datos exportados de la plataforma de experiencias llegan [!DNL Azure Event Hubs] en formato JSON. Por ejemplo, un flujo de evento que contenga la identidad de correo electrónico con hash de una audiencia que haya salido de un determinado segmento podría tener el siguiente aspecto:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* Vínculo al tutorial de la API de Azure Evento Hubs
>* [Destino de AWS Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md)