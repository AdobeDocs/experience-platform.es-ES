---
keywords: Amazon Kinesis;destino de kinesis;kinesis
title: Conexión de Amazon Kinesis
description: Cree una conexión saliente en tiempo real al almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---


# (Beta) Conexión [!DNL Amazon Kinesis]

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

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

## Conectar destino {#connect-destination}

Consulte [Flujo de trabajo de destinos de almacenamiento en la nube ](./workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento en la nube, incluidos los admitidos por [!DNL Amazon].

Para destinos [!DNL Amazon Kinesis] , introduzca la siguiente información en el flujo de trabajo de creación de destino:

## Paso de autenticación {#authentication-step}

* **[!DNL Amazon Web Services]clave de acceso y clave** secreta: En  [!DNL Amazon Web Services], genere un  `access key - secret access key` par para conceder a Platform acceso a su  [!DNL Amazon Kinesis] cuenta. Obtenga más información en la [documentación de los servicios web de Amazon](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **región**: Indique a qué  [!DNL Amazon Web Services] región se retransmitirán los datos.

![Campos de entrada en el paso de cuenta](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

## Paso de configuración {#setup-step}

* **Nombre**: Proporcione un nombre a la conexión para  [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción para la conexión a  [!DNL Amazon Kinesis].
* **flujo**: Proporcione el nombre de un flujo de datos existente en su  [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.
* **[!UICONTROL Marketing actions]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![Campos de entrada en el paso de autenticación](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

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
>* [Destino de los centros de eventos de Azure](./azure-event-hubs.md)
>* [Tipos y categorías de destino](../../destination-types.md)

