---
title: Información general sobre el conector Source Kinesis de Amazon
description: Aprenda a conectar Amazon Kinesis a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Fuente de [!DNL Amazon Kinesis] 

>[!IMPORTANT]
>
>- El origen [!DNL Amazon Kinesis] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.
>
>- Ahora puede usar el origen [!DNL Amazon Kinesis] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform proporciona conectividad nativa para proveedores de la nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure]. Puede llevar los datos de estos sistemas a [!DNL Experience Platform].

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a [!DNL Experience Platform] sin necesidad de descargarlos, formatearlos o cargarlos. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o estar delimitados. Cada paso del proceso se integra en el flujo de trabajo de orígenes. [!DNL Experience Platform] le permite traer datos de [!DNL Amazon Kinesis] en tiempo real.

>[!NOTE]
>
>El factor de escala de [!DNL Kinesis] debe aumentarse si necesita ingerir datos de gran volumen. En la actualidad, el volumen máximo de datos que puede traer de su cuenta de [!DNL Kinesis] a Experience Platform es de 4000 registros por segundo. Para ampliar e introducir datos de mayor volumen, póngase en contacto con su representante de Adobe.

## Requisitos previos

La siguiente sección proporciona más información sobre la configuración de requisitos previos necesaria para poder crear una conexión de origen de [!DNL Kinesis].

### Configurar la directiva de acceso

Una secuencia [!DNL Kinesis] requiere los siguientes permisos para crear una conexión de origen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Estos permisos se organizan a través de la consola [!DNL Kinesis] y Experience Platform los comprueba cuando escribe sus credenciales y selecciona el flujo de datos.

El ejemplo siguiente muestra los derechos de acceso mínimos necesarios para crear una conexión de origen de [!DNL Kinesis].

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

Para obtener más información sobre el control del acceso a las secuencias de datos de [!DNL Kinesis], consulte el siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configuración del tipo de iterador

[!DNL Kinesis] admite los siguientes tipos de iterador para permitirle especificar el orden en que se leen los datos:

| Tipo de iterador | Descripción |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Los datos se leen a partir de una posición identificada por un número de secuencia específico. |
| `AFTER_SEQUENCE_NUMBER` | Los datos se leen comenzando después de la posición identificada por un número de secuencia específico. |
| `AT_TIMESTAMP` | Los datos se leen a partir de una posición identificada por una marca de tiempo específica. |
| `TRIM_HORIZON` | Los datos se leen a partir del registro de datos más antiguo. |
| `LATEST` | Los datos se leen a partir del registro de datos más reciente. |

Actualmente, un origen de interfaz de usuario [!DNL Kinesis] solo admite `TRIM_HORIZON`, mientras que la API admite `TRIM_HORIZON` y `LATEST` como modos para obtener datos. El valor de iterador predeterminado que utiliza Experience Platform para el origen [!DNL Kinesis] es `TRIM_HORIZON`.

Para obtener más información sobre los tipos de iterador, consulte el siguiente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Conectar [!DNL Amazon Kinesis] a [!DNL Experience Platform]

>[!NOTE]
>
>Después de crear o actualizar un flujo de datos de flujo continuo, se requiere una breve pausa de 5 minutos en la ingesta de datos para evitar cualquier posible instancia de pérdida o caída de datos.

La siguiente documentación proporciona información sobre cómo conectar [!DNL Amazon Kinesis] a [!DNL Experience Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Crear una conexión de origen de Amazon Kinesis mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Recopilación de datos de flujo continuo mediante la API de Flow Service](../../tutorials/api/collect/streaming.md)

### Uso de la IU

- [Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configure un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
