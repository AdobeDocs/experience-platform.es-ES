---
keywords: Amazon Kinesis;destino de kinesis;kinesis
title: Conexión de Amazon Kinesis
description: Cree una conexión saliente en tiempo real al almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# (Beta) Conexión [!DNL Amazon Kinesis]

## Información general {#overview}

>[!IMPORTANT]
>
>El destino [!DNL Amazon Kinesis] en Platform está actualmente en versión beta. La documentación y las funciones están sujetas a cambios.

El servicio [!DNL Kinesis Data Streams] de [!DNL Amazon Web Services] le permite recopilar y procesar grandes flujos de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con su almacenamiento [!DNL Amazon Kinesis] para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Amazon Kinesis], consulte la [documentación de Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectarse a [!DNL Amazon Kinesis] mediante programación, consulte el [tutorial de API de destinos de transmisión](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Amazon Kinesis] mediante la interfaz de usuario de Platform, consulte las secciones a continuación.

![Amazon Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Al utilizar destinos de flujo continuo como [!DNL Amazon Kinesis], puede alimentar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados en sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un libro blanco que los califica para un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento al que pertenece el cliente potencial al destino [!DNL Amazon Kinesis], recibiría este evento en [!DNL Amazon Kinesis]. En este caso, puede utilizar un enfoque propio y describir la lógica empresarial además del evento, ya que considera que funcionará mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [audiencias](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Permisos [!DNL Amazon Kinesis] requeridos {#required-kinesis-permission}

Para conectar y exportar datos correctamente a sus flujos [!DNL Amazon Kinesis], el Experience Platform necesita permisos para las siguientes acciones:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Estos permisos se organizan a través de la consola [!DNL Kinesis] y Platform los comprueba una vez que configura el destino de Kinesis en la interfaz de usuario de Platform.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para exportar correctamente los datos a un destino [!DNL Kinesis].

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `kinesis:ListStreams` | Acción que enumera las secuencias de datos de Amazon Kinesis. |
| `kinesis:PutRecord` | Acción que escribe un registro de datos único en un flujo de datos de Kinesis. |
| `kinesis:PutRecords` | Acción que escribe varios registros de datos en un flujo de datos de Kinesis en una sola llamada. |

Para obtener más información sobre el control del acceso para [!DNL Kinesis] flujos de datos, lea el siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!DNL Amazon Web Services]clave de acceso y clave** secreta: En  [!DNL Amazon Web Services], genere un  `access key - secret access key` par para conceder a Platform acceso a su  [!DNL Amazon Kinesis] cuenta. Obtenga más información en la [documentación de los servicios web de Amazon](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **región**: Indique a qué  [!DNL Amazon Web Services] región se retransmitirán los datos.
* **Nombre**: Proporcione un nombre a la conexión para  [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción para la conexión a  [!DNL Amazon Kinesis].
* **flujo**: Proporcione el nombre de un flujo de datos existente en su  [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Los datos [!DNL Experience Platform] exportados llegan a [!DNL Amazon Kinesis] en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este cliente potencial son ECID y correo electrónico.

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
>* [Conectarse a Amazon Kinesis y activar datos mediante la API de servicio de flujo](../../api/streaming-destinations.md)
* [Destino de los centros de eventos de Azure](./azure-event-hubs.md)
* [Tipos y categorías de destino](../../destination-types.md)

