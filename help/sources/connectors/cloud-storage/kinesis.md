---
keywords: Experience Platform;inicio;temas populares;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Información general sobre el conector de origen de Amazon Kinesis
topic-legacy: overview
description: Obtenga información sobre cómo conectar Amazon Kinesis a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos desde  [!DNL Amazon Kinesis] en tiempo real.

## Requisitos previos

La siguiente sección proporciona más información sobre la configuración previa necesaria para poder crear una conexión de origen [!DNL Kinesis].

### Configuración de la directiva de acceso

Un flujo [!DNL Kinesis] requiere los siguientes permisos para crear una conexión de origen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Estos permisos se organizan a través de la consola [!DNL Kinesis] y Platform los comprueba una vez que introduce las credenciales y selecciona el flujo de datos.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para crear una conexión de origen [!DNL Kinesis].

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

Para obtener más información sobre el control del acceso para [!DNL Kinesis] flujos de datos, consulte el siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configurar el tipo de iterador

[!DNL Kinesis] admite los siguientes tipos de iteradores para permitirle especificar el orden en que se leen los datos:

| Tipo de iterador | Descripción |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Los datos se leen empezando por una posición identificada por un número de secuencia específico. |
| `AFTER_SEQUENCE_NUMBER` | Los datos se leen comenzando después de la posición identificada con un número de secuencia específico. |
| `AT_TIMESTAMP` | Los datos se leen a partir de una posición identificada por una marca de tiempo específica. |
| `TRIM_HORIZON` | Los datos se leen a partir del registro de datos más antiguo. |
| `LATEST` | Los datos se leen a partir del registro de datos más reciente. |

Actualmente, una fuente de interfaz de usuario [!DNL Kinesis] solo admite `TRIM_HORIZON`, mientras que la API admite `TRIM_HORIZON` y `LATEST` como modos de obtener datos. El valor predeterminado del iterador que utiliza Platform para el origen [!DNL Kinesis] es `TRIM_HORIZON`.

Para obtener más información sobre los tipos de iterador, consulte el siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Conectar [!DNL Amazon Kinesis] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Amazon Kinesis] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Recopilación de datos de flujo continuo mediante la API del servicio de flujo](../../tutorials/api/collect/streaming.md)

### Uso de la interfaz de usuario

- [Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
