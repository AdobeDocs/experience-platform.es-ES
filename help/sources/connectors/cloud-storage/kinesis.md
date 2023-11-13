---
title: Información general sobre el conector de origen de Amazon Kinesis
description: Obtenga información sobre cómo conectar Amazon Kinesis a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] origen

>[!IMPORTANT]
>
>El [!DNL Amazon Kinesis] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform], y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Las fuentes de almacenamiento en la nube pueden incorporar sus propios datos en [!DNL Platform] sin necesidad de descargar, formatear ni cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes. [!DNL Platform] le permite introducir datos de [!DNL Amazon Kinesis] en tiempo real.

>[!NOTE]
>
>El factor de escala para [!DNL Kinesis] debe aumentarse si necesita introducir datos de gran volumen. En este momento, el volumen máximo de datos que puede traer de su [!DNL Kinesis] cuenta a Platform es de 4000 registros por segundo. Para ampliar e ingerir datos de mayor volumen, póngase en contacto con su representante de Adobe.

## Requisitos previos

En la siguiente sección se proporciona más información sobre la configuración de requisitos previos necesaria para crear un [!DNL Kinesis] conexión de origen.

### Configurar la directiva de acceso

A [!DNL Kinesis] La secuencia requiere los siguientes permisos para crear una conexión de origen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Estos permisos se organizan a través de la variable [!DNL Kinesis] y son comprobados por Platform una vez que introduce sus credenciales y selecciona el flujo de datos.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para crear una [!DNL Kinesis] conexión de origen.

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
| `kinesis:GetShardIterator` | Una acción necesaria para atravesar registros. |
| `kinesis:GetRecords` | Una acción necesaria para obtener registros de un ID de desplazamiento o compartido específico. |
| `kinesis:DescribeStream` | Una acción que devuelve información con respecto al flujo, incluido el mapa compartido, que es necesario para generar un ID compartido. |
| `kinesis:ListStreams` | Una acción necesaria para enumerar los flujos disponibles que puede seleccionar en la interfaz de usuario. |

Para obtener más información sobre el control de acceso de [!DNL Kinesis] secuencias de datos, consulte lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configuración del tipo de iterador

[!DNL Kinesis] admite los siguientes tipos de iterador para permitirle especificar el orden en que se leen los datos:

| Tipo de iterador | Descripción |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Los datos se leen a partir de una posición identificada por un número de secuencia específico. |
| `AFTER_SEQUENCE_NUMBER` | Los datos se leen comenzando después de la posición identificada por un número de secuencia específico. |
| `AT_TIMESTAMP` | Los datos se leen a partir de una posición identificada por una marca de tiempo específica. |
| `TRIM_HORIZON` | Los datos se leen a partir del registro de datos más antiguo. |
| `LATEST` | Los datos se leen a partir del registro de datos más reciente. |

A [!DNL Kinesis] Actualmente, la fuente de IU solo admite `TRIM_HORIZON`, mientras que la API admite ambas `TRIM_HORIZON` y `LATEST` como modos para obtener datos. El valor del iterador predeterminado que Platform utiliza para [!DNL Kinesis] el origen es `TRIM_HORIZON`.

Para obtener más información sobre los tipos de iteradores, consulte lo siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connect [!DNL Amazon Kinesis] hasta [!DNL Platform]

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Amazon Kinesis] hasta [!DNL Platform] mediante las API de o la interfaz de usuario de:

### Uso de API

- [Crear una conexión de origen de Amazon Kinesis mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Recopilación de datos de flujo continuo mediante la API de Flow Service](../../tutorials/api/collect/streaming.md)

### Uso de la IU

- [Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configure un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
