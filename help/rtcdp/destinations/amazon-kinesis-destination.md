---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Destino de Amazon Kinesis
seo-title: Destino de Amazon Kinesis
description: Cree una conexión saliente en tiempo real con el almacenamiento Kinesis de Amazon para transmitir datos desde Adobe Experience Platform.
seo-description: Cree una conexión saliente en tiempo real con el almacenamiento Kinesis de Amazon para transmitir datos desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---


# (Beta) [!DNL Amazon Kinesis] destino


>[!IMPORTANT]
>
>El [!DNL Amazon Kinesis] destino en Adobe Real-time CDP está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

El [!DNL Kinesis Data Streams] servicio le permite [!DNL Amazon Web Services] recopilar y procesar grandes flujos de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con el [!DNL Amazon Kinesis] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Amazon Kinesis], consulte la documentación [de](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Para conectarse a [!DNL Amazon Kinesis] través de llamadas de API, consulte el tutorial [de API de destinos de](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)flujo continuo.
* Para conectarse a [!DNL Amazon Kinesis] mediante la interfaz de usuario CDP en tiempo real de Adobe, consulte las secciones a continuación.

![Amazon Kinesis en la interfaz de usuario](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Casos de uso {#use-cases}

Al utilizar los destinos de flujo continuo, como [!DNL Amazon Kinesis]el, puede transmitir fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a los sistemas que elija.

Por ejemplo, un cliente potencial descargó un documento técnico que los califica en un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento en el que se encuentra el cliente potencial al [!DNL Amazon Kinesis] destino, recibirá este evento en [!DNL Amazon Kinesis]. Allí puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial sobre el evento, como piensa que funcionaría mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Exportación** de perfil: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [de activación de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destino.

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento de [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos los admitidos por [!DNL Amazon].

Para [!DNL Amazon Kinesis] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

### En el paso Autenticación {#authentication-step}

* **[!DNL Amazon Web Services]clave de acceso y clave** secreta: En [!DNL Amazon Web Services], genere un `access key - secret access key` par para otorgar acceso CDP en tiempo real de Adobe a su [!DNL Amazon Kinesis] cuenta. Obtenga más información en la documentación [de los servicios Web de](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.
* **región**: Indicar a qué [!DNL Amazon Web Services] región se transmitirán los datos.

![Campos de entrada en el paso de cuenta](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### En el paso Configuración {#setup-step}

* **Nombre**: Proporcione un nombre para la conexión a [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción de la conexión a [!DNL Amazon Kinesis].
* **stream**: Proporcione el nombre de un flujo de datos existente en su [!DNL Amazon Kinesis] cuenta. CDP en tiempo real de Adobe exportará datos a este flujo.

![Campos de entrada en el paso de autenticación](/help/rtcdp/destinations/assets/aws-kinesis-setup-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Datos exportados {#exported-data}

Los datos exportados [!DNL Experience Platform] llegan al formato [!DNL Amazon Kinesis] JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha cualificado para un segmento determinado y ha salido de otro. Las identidades de este cliente potencial son ECID y correo electrónico.

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
>* [Conéctese a Amazon Kinesis y active los datos mediante llamadas de API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destino de los centros de Evento de Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md)

