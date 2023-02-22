---
title: Incorporación de datos cifrados
description: Adobe Experience Platform permite la ingesta de archivos cifrados a través de fuentes por lotes de almacenamiento en la nube.
hide: true
hidefromtoc: true
source-git-commit: 526c9665843efaeb0e98423dc424a4193434f583
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# Ingesta de datos cifrada

Adobe Experience Platform permite la ingesta de archivos cifrados a través de fuentes por lotes de almacenamiento en la nube. Con la incorporación de datos cifrados, puede aprovechar los mecanismos de cifrado asimétricos para transferir de forma segura datos por lotes al Experience Platform. Actualmente, los mecanismos de cifrado asimétrico admitidos son PGP y GPG.

El proceso de incorporación de datos cifrados es el siguiente:

1. [Creación de un par de claves de cifrado mediante API de Experience Platform](#create-encryption-key-pair). El par de claves de cifrado consta de una clave privada y una clave pública. Una vez creada, puede copiar o descargar la clave pública, junto con su ID de clave pública y el tiempo de caducidad correspondientes. Durante este proceso, el Experience Platform almacenará la clave privada en un almacén seguro.
2. Utilice la clave pública para cifrar el archivo de datos que desea introducir.
3. Coloque el archivo cifrado en el almacenamiento en la nube.
4. Una vez que el archivo cifrado esté listo, [crear una conexión de origen y un flujo de datos para el origen de almacenamiento en la nube](#create-a-dataflow-for-encrypted-data). Durante el paso de creación del flujo, debe proporcionar una `encryption` e incluya su ID de clave pública.
5. El Experience Platform recupera la clave privada del almacén seguro para descifrar los datos en el momento de la ingesta.

Este documento proporciona pasos sobre cómo generar un par de claves de cifrado para cifrar los datos e ingerirlos al Experience Platform mediante fuentes de almacenamiento en la nube.

## Primeros pasos

Este tutorial requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
   * [Fuentes de almacenamiento en la nube](../api/collect/cloud-storage.md): Cree un flujo de datos para llevar los datos por lotes del origen de almacenamiento en la nube al Experience Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Crear par de claves de cifrado {#create-encryption-key-pair}

El primer paso para introducir datos cifrados en el Experience Platform es crear el par de claves de cifrado realizando una solicitud del POST al `/encryption/keys` punto final del [!DNL Connectors] API.

**Formato de API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Solicitud**

La siguiente solicitud genera un par de claves de cifrado utilizando el algoritmo de cifrado PGP.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `encryptionAlgorithm` | El tipo de algoritmo de codificación que utiliza. Los tipos de codificación admitidos son `PGP` y `GPG`. |
| `params.passPhrase` | La frase de contraseña proporciona una capa adicional de protección para las claves de cifrado. Tras la creación, el Experience Platform almacena la frase de contraseña en una bóveda segura diferente de la clave pública. Debe proporcionar una cadena que no esté vacía como frase de contraseña. |

**Respuesta**

Una respuesta correcta devuelve la clave pública, el ID de clave pública y la hora de caducidad de las claves. La hora de caducidad se establece automáticamente en 180 días después de la fecha de generación de la clave. Actualmente, el tiempo de caducidad no se puede configurar.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Conecte el origen de almacenamiento en la nube al Experience Platform mediante la función [!DNL Flow Service] API

Una vez que haya recuperado el par de claves de cifrado, puede continuar y crear una conexión de origen para el origen de almacenamiento en la nube y llevar los datos cifrados a Platform.

En primer lugar, debe crear una conexión base para autenticar el origen con Platform. Para crear una conexión base y autenticar el origen, seleccione el origen que desee utilizar en la lista siguiente:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Almacenamiento de Azure Data Lake Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Almacenamiento de archivos de Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Zona de aterrizaje de datos](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Almacenamiento en la nube de Google](../api/create/cloud-storage/google.md)
* [Almacenamiento de objetos de oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Después de crear una conexión base, debe seguir los pasos descritos en el tutorial para [creación de una conexión de origen para un origen de almacenamiento en la nube](../api/collect/cloud-storage.md) para crear una conexión de origen, una conexión de destino y una asignación.

## Crear un flujo de datos para datos cifrados {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Debe tener lo siguiente para crear un flujo de datos para la incorporación de datos cifrados:
>* [ID de clave pública](#create-encryption-key-pair)
>* [ID de conexión de origen](../api/collect/cloud-storage.md#source)
>* [ID de conexión de Target](../api/collect/cloud-storage.md#target)
>* [ID de asignación](../api/collect/cloud-storage.md#mapping)


Para crear un flujo de datos, realice una solicitud de POST al `/flows` punto final del [!DNL Flow Service] API. Para ingerir datos cifrados, debe agregar una `encryption` para `transformations` e incluya la propiedad `publicKeyId` que se creó en un paso anterior.

**Formato de API**

```http
POST /flows
```

**Solicitud**

La siguiente solicitud crea un flujo de datos para ingerir datos cifrados para un origen de almacenamiento en la nube.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
          "frequency": "once"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | El ID de especificación de flujo que corresponde a los orígenes de almacenamiento en la nube. |
| `sourceConnectionIds` | El ID de conexión de origen. Este ID representa la transferencia de datos de la fuente a Platform. |
| `targetConnectionIds` | El ID de conexión de destino. Este ID representa el lugar donde llegan los datos una vez que se transfieren a Platform. |
| `transformations[x].params.mappingId` | El ID de asignación. |
| `transformations.name` | Al ingerir archivos cifrados, debe proporcionar `Encryption` como parámetro de transformaciones adicionales para su flujo de datos. |
| `transformations[x].params.publicKeyId` | El ID de clave pública que ha creado. Este ID es la mitad del par de claves de cifrado que se utiliza para cifrar los datos del almacenamiento en la nube. |
| `scheduleParams.startTime` | Hora de inicio del flujo de datos en tiempo de época. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day`o `week`. |
| `scheduleParams.interval` | El intervalo designa el periodo entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un número entero distinto de cero. El intervalo no es necesario cuando la frecuencia está establecida como `once` y debe ser bueno o igual que `15` para otros valores de frecuencia. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado para sus datos cifrados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado un par de claves de cifrado para sus datos de almacenamiento en la nube y un flujo de datos para ingerir los datos cifrados mediante la variable [!DNL Flow Service API]. Para obtener actualizaciones de estado sobre la integridad, errores y métricas del flujo de datos, lea la guía de [monitorización del flujo de datos mediante [!DNL Flow Service] API](./monitor.md).