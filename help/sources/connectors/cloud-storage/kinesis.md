---
keywords: Experience Platform;inicio;temas populares;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Información general sobre el conector de origen de Amazon Kinesis
description: Obtenga información sobre cómo conectar Amazon Kinesis a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform]y [!DNL Azure]. Puede incorporar los datos de estos sistemas a [!DNL Platform].

Las fuentes de almacenamiento en la nube pueden incorporar sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos de [!DNL Amazon Kinesis] en tiempo real.

>[!NOTE]
>
>El factor de escala para [!DNL Kinesis] debe aumentarse si necesita ingerir datos de gran volumen. Actualmente, el volumen máximo de datos que puede obtener de su [!DNL Kinesis] La cuenta a Platform es de 4000 registros por segundo. Para ampliar e incorporar datos de mayor volumen, póngase en contacto con su representante de Adobe.

## Requisitos previos

En la siguiente sección se proporciona más información sobre la configuración de requisitos previos necesaria para poder crear una [!DNL Kinesis] conexión de origen.

### Configuración de la directiva de acceso

A [!DNL Kinesis] La secuencia requiere los siguientes permisos para crear una conexión de origen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Estos permisos se organizan mediante la variable [!DNL Kinesis] y son verificados por Platform una vez que haya introducido sus credenciales y seleccionado el flujo de datos.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para crear un [!DNL Kinesis] conexión de origen.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
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
| `kinesis:GetShardIterator` | Acción necesaria para recorrer los registros. |
| `kinesis:GetRecords` | Acción necesaria para obtener registros de un desplazamiento o ID compartido específico. |
| `kinesis:DescribeStream` | Acción que devuelve información sobre el flujo, incluido el mapa compartido, que es necesario para generar un ID compartido. |
| `kinesis:ListStreams` | Acción necesaria para enumerar los flujos disponibles que puede seleccionar en la interfaz de usuario. |

Para obtener más información sobre cómo controlar el acceso a [!DNL Kinesis] flujos de datos, consulte lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configurar el tipo de iterador

[!DNL Kinesis] admite los siguientes tipos de iteradores para permitirle especificar el orden en que se leen los datos:

| Tipo de iterador | Descripción |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Los datos se leen empezando por una posición identificada por un número de secuencia específico. |
| `AFTER_SEQUENCE_NUMBER` | Los datos se leen comenzando después de la posición identificada con un número de secuencia específico. |
| `AT_TIMESTAMP` | Los datos se leen a partir de una posición identificada por una marca de tiempo específica. |
| `TRIM_HORIZON` | Los datos se leen a partir del registro de datos más antiguo. |
| `LATEST` | Los datos se leen a partir del registro de datos más reciente. |

A [!DNL Kinesis] El origen de la interfaz de usuario solo es compatible actualmente `TRIM_HORIZON`, mientras que la API admite ambas `TRIM_HORIZON` y `LATEST` como modos para obtener datos. El valor de iterador predeterminado que utiliza Platform para la variable [!DNL Kinesis] el origen es `TRIM_HORIZON`.

Para obtener más información sobre los tipos de iteradores, consulte lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connect [!DNL Amazon Kinesis] a [!DNL Platform]

La siguiente documentación proporciona información sobre cómo conectar [!DNL Amazon Kinesis] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Recopilación de datos de flujo continuo mediante la API del servicio de flujo](../../tutorials/api/collect/streaming.md)

### Uso de la interfaz de usuario

- [Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
