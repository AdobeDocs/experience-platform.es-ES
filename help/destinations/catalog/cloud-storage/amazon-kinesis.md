---
keywords: Amazon Kinesis;destino de kinesis;kinesis
title: Conexión de Amazon Kinesis
description: Cree una conexión saliente en tiempo real al almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# (Beta) [!DNL Amazon Kinesis] connection

## Información general {#overview}

>[!IMPORTANT]
>
>La variable [!DNL Amazon Kinesis] el destino en Platform está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

La variable [!DNL Kinesis Data Streams] servicio por [!DNL Amazon Web Services] permite recopilar y procesar flujos grandes de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con su [!DNL Amazon Kinesis] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información, consulte [!DNL Amazon Kinesis], consulte la [Documentación de Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectarse a [!DNL Amazon Kinesis] mediante programación, consulte la [Tutorial de la API de destinos de flujo continuo](../../api/streaming-destinations.md).
* Para conectarse a [!DNL Amazon Kinesis] con la interfaz de usuario de Platform, consulte las secciones siguientes.

![Amazon Kinesis en la interfaz de usuario](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Mediante destinos de flujo continuo como [!DNL Amazon Kinesis], puede incorporar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un libro blanco que los califica para un segmento de &quot;alta propensión a convertir&quot;. Asignando el segmento en el que se encuentra el cliente potencial a [!DNL Amazon Kinesis] destino, recibiría este evento en [!DNL Amazon Kinesis]. En este caso, puede utilizar un enfoque propio y describir la lógica empresarial además del evento, ya que considera que funcionará mejor con sus sistemas de TI empresariales.

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de audiencia](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Requerido [!DNL Amazon Kinesis] permissions {#required-kinesis-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon Kinesis] flujos, el Experience Platform necesita permisos para las siguientes acciones:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Estos permisos se organizan mediante la variable [!DNL Kinesis] y Platform los comprobará una vez que haya configurado el destino de Kinesis en la interfaz de usuario de Platform.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para exportar correctamente los datos a un [!DNL Kinesis] destino.

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

Para obtener más información sobre cómo controlar el acceso a [!DNL Kinesis] flujos de datos, lea lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!DNL Amazon Web Services]clave de acceso y clave secreta**: En [!DNL Amazon Web Services], genere un `access key - secret access key` par para conceder acceso a Platform a su [!DNL Amazon Kinesis] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Indicar qué [!DNL Amazon Web Services] región a la que transmitir los datos.
* **Nombre**: Proporcione un nombre a la conexión para [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción para la conexión a [!DNL Amazon Kinesis].
* **flujo**: Proporcione el nombre de un flujo de datos existente en su [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](../../ui/activate-streaming-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Su exportación [!DNL Experience Platform] los datos llegan a [!DNL Amazon Kinesis] en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este cliente potencial son ECID y correo electrónico.

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
>* [Conectarse a Amazon Kinesis y activar datos mediante la API de servicio de flujo](../../api/streaming-destinations.md)
>* [Destino de los centros de eventos de Azure](./azure-event-hubs.md)
>* [Tipos y categorías de destino](../../destination-types.md)

