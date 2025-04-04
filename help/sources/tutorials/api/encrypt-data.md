---
title: Ingesta de datos cifrados
description: Obtenga información sobre cómo introducir archivos cifrados a través de fuentes por lotes de almacenamiento en la nube mediante la API.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 3%

---

# Ingesta de datos cifrados

Puede introducir archivos de datos cifrados en Adobe Experience Platform mediante fuentes por lotes de almacenamiento en la nube. Con la ingesta de datos cifrados, puede aprovechar los mecanismos de cifrado asimétricos para transferir datos por lotes de forma segura a Experience Platform. Actualmente, los mecanismos de cifrado asimétrico admitidos son PGP y GPG.

El proceso de ingesta de datos cifrados es el siguiente:

1. [Cree un par de claves de cifrado mediante las API de Experience Platform](#create-encryption-key-pair). El par de claves de cifrado consta de una clave privada y una clave pública. Una vez creada, puede copiar o descargar la clave pública, junto con su ID de clave pública y hora de caducidad correspondientes. Durante este proceso, Experience Platform almacenará la clave privada en un almacén seguro. **NOTA:** La clave pública de la respuesta está codificada en Base64 y debe descodificarse antes de usar.
2. Utilice la clave pública para cifrar el archivo de datos que desea introducir.
3. Coloque el archivo cifrado en el almacenamiento en la nube.
4. Una vez que el archivo cifrado esté listo, [cree una conexión de origen y un flujo de datos para el origen de almacenamiento en la nube](#create-a-dataflow-for-encrypted-data). Durante el paso de creación de flujo, debe proporcionar un parámetro `encryption` e incluir su ID de clave pública.
5. Experience Platform recupera la clave privada del almacén seguro para descifrar los datos en el momento de la ingesta.

>[!IMPORTANT]
>
>El tamaño máximo de un solo archivo cifrado es de 1 GB. Por ejemplo, puede introducir datos de 2 GB en una sola ejecución de flujo de datos, pero cualquier archivo individual de esos datos no puede superar 1 GB.

Este documento proporciona pasos sobre cómo generar un par de claves de cifrado para cifrar los datos e introducir esos datos cifrados en Experience Platform mediante fuentes de almacenamiento en la nube.

## Introducción  {#get-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
   * [Fuentes de almacenamiento en la nube](../api/collect/cloud-storage.md): Cree un flujo de datos para traer datos por lotes de su fuente de almacenamiento en la nube a Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).

### Extensiones de archivo compatibles con archivos cifrados {#supported-file-extensions-for-encrypted-files}

La lista de extensiones de archivo compatibles con los archivos cifrados es la siguiente:

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>La ingesta de archivos cifrados en fuentes de Adobe Experience Platform admite openPGP y no cualquier versión propietaria específica de PGP.

## Crear par de claves de cifrado {#create-encryption-key-pair}

>[!IMPORTANT]
>
>Las claves de cifrado son específicas de una zona protegida determinada. Por lo tanto, debe crear nuevas claves de cifrado si desea introducir datos cifrados en una zona protegida diferente, dentro de su organización.

El primer paso para la ingesta de datos cifrados en Experience Platform es crear el par de claves de cifrado realizando una petición POST al extremo `/encryption/keys` de la API [!DNL Connectors].

**Formato de API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Solicitud**

+++Ver solicitud de ejemplo

La siguiente solicitud genera un par de claves de cifrado mediante el algoritmo de cifrado PGP.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-encryption",
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | Nombre del par de claves de cifrado. |
| `encryptionAlgorithm` | El tipo de algoritmo de cifrado que está utilizando. Los tipos de cifrado admitidos son `PGP` y `GPG`. |
| `params.passPhrase` | La frase de contraseña proporciona una capa adicional de protección para las claves de cifrado. Una vez creada, Experience Platform almacena la frase de contraseña en un almacén seguro diferente de la clave pública. Debe proporcionar una cadena que no esté vacía como frase de contraseña. |

+++

**Respuesta**

+++Ver respuesta de ejemplo

Una respuesta correcta devuelve la clave pública codificada en Base64, el ID de clave pública y la hora de caducidad de las claves. La hora de caducidad se establece automáticamente en 180 días después de la fecha de generación de la clave. La hora de caducidad no se puede configurar actualmente.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Propiedad | Descripción |
| --- | --- |
| `publicKey` | La clave pública se utiliza para cifrar los datos en el almacenamiento de la nube. Esta clave corresponde a la clave privada que también se creó durante este paso. Sin embargo, la clave privada se envía inmediatamente a Experience Platform. |
| `publicKeyId` | El ID de clave pública se utiliza para crear un flujo de datos e introducir los datos cifrados del almacenamiento en la nube en Experience Platform. |
| `expiryTime` | La hora de caducidad define la fecha de caducidad del par de claves de cifrado. Esta fecha se establece automáticamente en 180 días después de la fecha de generación de claves y se muestra en formato unix timestamp. |

+++

### Recuperar claves de cifrado {#retrieve-encryption-keys}

Para recuperar todas las claves de cifrado de su organización, realice una petición GET al extremo `/encryption/keys`=nt.

**Formato de API**

```http
GET /data/foundation/connectors/encryption/keys
```

**Solicitud**

+++Ver solicitud de ejemplo

La siguiente solicitud recupera todas las claves de cifrado de la organización.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Respuesta**

+++Ver respuesta de ejemplo

Una respuesta correcta devuelve el algoritmo de cifrado, el nombre, la clave pública, el ID de clave pública, el tipo de clave y la hora de caducidad correspondiente de las claves.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Recuperar claves de cifrado por identificador {#retrieve-encryption-keys-by-id}

Para recuperar un conjunto específico de claves de cifrado, realice una petición GET al extremo `/encryption/keys` y proporcione su ID de clave pública como parámetro de encabezado.

**Formato de API**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Respuesta**

+++Ver respuesta de ejemplo

Una respuesta correcta devuelve el algoritmo de cifrado, el nombre, la clave pública, el ID de clave pública, el tipo de clave y la hora de caducidad correspondiente de las claves.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Crear par de claves administrado por el cliente {#create-customer-managed-key-pair}

Si lo desea, puede crear un par de claves de verificación de firma para firmar e introducir los datos cifrados.

Durante esta fase, debe generar su propia combinación de clave privada y clave pública y, a continuación, utilizar la clave privada para firmar los datos cifrados. A continuación, debe codificar la clave pública en Base64 y luego compartirla en Experience Platform para que Experience Platform pueda comprobar su firma.

### Compartir la clave pública en Experience Platform

Para compartir la clave pública, realice una petición POST al extremo `/customer-keys` y proporcione el algoritmo de cifrado y la clave pública codificada en Base64.

**Formato de API**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-sign-verification-keys"
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}},
      "params": {
          "passPhrase": {{PASS_PHRASE}}
      }
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `encryptionAlgorithm` | El tipo de algoritmo de cifrado que está utilizando. Los tipos de cifrado admitidos son `PGP` y `GPG`. |
| `publicKey` | La clave pública que corresponde a las claves administradas por el cliente utilizadas para firmar el cifrado. Esta clave debe tener codificación Base64. |

+++

**Respuesta**

+++Ver respuesta de ejemplo

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Propiedad | Descripción |
| --- | --- |
| `publicKeyId` | Este ID de clave pública se devuelve en respuesta al uso compartido de la clave gestionada por el cliente con Experience Platform. Puede proporcionar este ID de clave pública como ID de clave de verificación de firma al crear un flujo de datos para datos firmados y cifrados. |

+++

### Recuperar par de claves administrado por el cliente

Para recuperar las claves administradas por el cliente, realice una petición GET al extremo `/customer-keys`.

**Formato de API**

```http
GET /data/foundation/connectors/encryption/customer-keys
```

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Respuesta**

+++Ver respuesta de ejemplo

```json
[
    {
        "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
        "name": "{NAME}",
        "publicKeyId": "{PUBLIC_KEY_ID}",
        "publicKey": "{PUBLIC_KEY}",
        "keyType": "{KEY_TYPE}",
    }
]
```

+++

## Conecte su origen de almacenamiento en la nube a Experience Platform mediante la API [!DNL Flow Service]

Una vez que haya recuperado el par de claves de cifrado, ahora puede continuar y crear una conexión de origen para la fuente de almacenamiento en la nube y llevar los datos cifrados a Experience Platform.

En primer lugar, debe crear una conexión base para autenticar el origen con Experience Platform. Para crear una conexión base y autenticar el origen, seleccione el origen que desee utilizar en la lista siguiente:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure File Storage](../api/create/cloud-storage/azure-file-storage.md)
* [Zona de aterrizaje de datos](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Almacenamiento en la nube de Google](../api/create/cloud-storage/google.md)
* [Almacenamiento de objetos de Oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Después de crear una conexión base, debe seguir los pasos descritos en el tutorial para [crear una conexión de origen para un origen de almacenamiento en la nube](../api/collect/cloud-storage.md) para crear una conexión de origen, una conexión de destino y una asignación.

## Creación de un flujo de datos para datos cifrados {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Debe tener lo siguiente para crear un flujo de datos para la ingesta de datos cifrados:
>
>* [Id. de clave pública](#create-encryption-key-pair)
>* [ID. de conexión de Source](../api/collect/cloud-storage.md#source)
>* [Id. de conexión de destino](../api/collect/cloud-storage.md#target)
>* [Id. de asignación](../api/collect/cloud-storage.md#mapping)

Para crear un flujo de datos, realice una petición POST al extremo `/flows` de la API [!DNL Flow Service]. Para introducir datos cifrados, debe agregar una sección `encryption` a la propiedad `transformations` e incluir `publicKeyId` que se creó en un paso anterior.

**Formato de API**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB Crear un flujo de datos para la ingesta de datos cifrados]

**Solicitud**

+++Ver solicitud de ejemplo

La siguiente solicitud crea un flujo de datos para introducir datos cifrados para una fuente de almacenamiento en la nube.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | ID de especificación de flujo que corresponde a las fuentes de almacenamiento en la nube. |
| `sourceConnectionIds` | Identificador de conexión de origen. Este ID representa la transferencia de datos del origen a Experience Platform. |
| `targetConnectionIds` | El ID de conexión de destino. Este ID representa dónde aterrizan los datos una vez que se transfieren a Experience Platform. |
| `transformations[x].params.mappingId` | ID de asignación. |
| `transformations.name` | Al ingerir archivos cifrados, debe proporcionar `Encryption` como parámetro de transformaciones adicional para el flujo de datos. |
| `transformations[x].params.publicKeyId` | El ID de clave pública que ha creado. Este ID es la mitad del par de claves de cifrado que se usa para cifrar los datos del almacenamiento en la nube. |
| `scheduleParams.startTime` | Hora de inicio del flujo de datos en tiempo epoch. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | El intervalo designa el período entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un entero distinto de cero. El intervalo no es necesario cuando la frecuencia está establecida como `once` y debe ser mayor o igual que `15` para otros valores de frecuencia. |

+++

**Respuesta**

+++Ver respuesta de ejemplo

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado para los datos cifrados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB Cree un flujo de datos para introducir datos cifrados y firmados]

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `params.signVerificationKeyId` | El ID de la clave de verificación de firma es el mismo que el ID de la clave pública recuperado después de compartir la clave pública codificada en Base64 con Experience Platform. |

+++

**Respuesta**

+++Ver respuesta de ejemplo

Una respuesta correcta devuelve el identificador (`id`) del flujo de datos recién creado para los datos cifrados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Eliminar claves de cifrado {#delete-encryption-keys}

Para eliminar las claves de cifrado, realice una petición DELETE al extremo `/encryption/keys` y proporcione el identificador de clave pública como parámetro de encabezado.

**Formato de API**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

### Validar claves de cifrado {#validate-encryption-keys}

Para validar las claves de cifrado, realice una petición GET al extremo `/encryption/keys/validate/` y proporcione el identificador de clave pública que desea validar como parámetro de encabezado.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Solicitud**

+++Ver solicitud de ejemplo

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Respuesta**

Una respuesta correcta devuelve una confirmación de que los ID son válidos o no son válidos.

>[!BEGINTABS]

>[!TAB Válido]

Un identificador de clave pública válido devuelve el estado `Active` junto con el identificador de clave pública.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB No válido]

Un identificador de clave pública no válido devuelve el estado `Expired` junto con el identificador de clave pública.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Restricciones en la ingesta recurrente {#restrictions-on-recurring-ingestion}

La ingesta de datos cifrados no admite la ingesta de carpetas recurrentes o de varios niveles en las fuentes. Todos los archivos cifrados deben estar contenidos en una sola carpeta. Tampoco se admiten caracteres comodín con varias carpetas en una sola ruta de origen.

El siguiente es un ejemplo de una estructura de carpetas admitida, donde la ruta de origen es `/ACME-customers/*.csv.gpg`.

En esta situación, los archivos en negrita se incorporan a Experience Platform.

* clientes de ACME
   * **Archivo1.csv.gpg**
   * File2.json.gpg
   * **Archivo3.csv.gpg**
   * File4.json
   * **Archivo5.csv.gpg**

El siguiente es un ejemplo de una estructura de carpetas no compatible en la que la ruta de origen es `/ACME-customers/*`.

En este escenario, la ejecución del flujo fallará y devolverá un mensaje de error que indica que los datos no se pueden copiar desde el origen.

* clientes de ACME
   * File1.csv.gpg
   * File2.json.gpg
   * Subcarpeta1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* Lealtad a ACME
   * File6.csv.gpg


## Pasos siguientes

Siguiendo este tutorial, ha creado un par de claves de cifrado para los datos de almacenamiento en la nube y un flujo de datos para introducir los datos cifrados mediante [!DNL Flow Service API]. Para obtener actualizaciones de estado sobre la integridad, los errores y las métricas del flujo de datos, lee la guía sobre [monitorización del flujo de datos mediante la [!DNL Flow Service] API](./monitor.md).