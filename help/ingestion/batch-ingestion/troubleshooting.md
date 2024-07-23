---
keywords: Experience Platform;inicio;temas populares;datos ingeridos;solución de problemas;faq;Ingesta;Ingesta por lotes;ingesta por lotes;
solution: Experience Platform
title: Guía de resolución de problemas de ingesta por lotes
description: Esta documentación le ayudará a responder a las preguntas más frecuentes sobre las API de ingesta de datos por lotes de Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 37b241f15f297263cc7aa20f382c115a2d131c7e
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# Guía de solución de problemas de ingesta por lotes

Esta documentación le ayudará a responder a las preguntas más frecuentes acerca de las API de Adobe Experience Platform [!DNL Batch Data Ingestion].

## Llamadas API por lotes

### ¿Los lotes se activan inmediatamente después de recibir HTTP 200 OK del API CompleteBatch?

La respuesta `200 OK` de la API significa que el lote se ha aceptado para el procesamiento; no estará activo hasta que pase a su estado final, como Activo o Error.

### ¿Es seguro reintentar la llamada a la API CompleteBatch después de un error?

Sí, es seguro volver a intentar la llamada de API. A pesar del error, es posible que la operación se haya realizado correctamente y que el lote se haya aceptado correctamente. Sin embargo, se espera que los clientes tengan mecanismos de reintento en caso de que falle la API y, de hecho, se les anima a volver a intentarlo. Si la operación se realiza correctamente, la API devolverá el resultado correcto, incluso después de volver a intentarlo.

### ¿Cuándo se debe utilizar la API de carga de archivos grandes?

El tamaño de archivo recomendado para utilizar la API de carga de archivos grandes es de 256 MB o más. Encontrará más información sobre cómo usar la API de carga de archivos grandes [aquí](./api-overview.md#ingest-large-parquet-files).

### ¿Por qué falla la llamada API de finalización de archivo grande?

Si se encuentran fragmentos de un archivo grande superpuestos o no se encuentran, el servidor responde con una petición HTTP 400 incorrecta. Esto puede ocurrir porque es posible cargar fragmentos superpuestos, ya que las validaciones de rango se realizan en el momento de finalizar el archivo, cuando los fragmentos del archivo se vinculan entre sí.

## Compatibilidad con ingesta

### ¿Cuáles son los formatos de ingesta admitidos?

Actualmente, se admiten tanto Parquet como JSON. El CSV se admite en versiones anteriores: aunque los datos se promocionarán a formato principal y se realizarán comprobaciones preliminares, no se admitirán funciones modernas, como conversión, partición o validación de filas.

### ¿Dónde se debe especificar el formato de entrada por lotes?

El formato de entrada debe especificarse en el momento de la creación del lote dentro de la carga útil. A continuación se muestra un ejemplo de cómo especificar el formato de entrada por lotes:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### ¿Por qué los datos cargados no aparecen en el conjunto de datos?

Para que los datos aparezcan en el conjunto de datos, el lote debe marcarse como completado. Todos los archivos que desee introducir deben cargarse antes de marcar el lote como completado. A continuación puede ver un ejemplo de cómo marcar un lote como completado:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### ¿Cómo se ingiere JSON multilínea?

Para ingerir JSON multilínea, el indicador `isMultiLineJson` debe establecerse en el momento de la creación del lote. A continuación puede ver un ejemplo de esto:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### ¿Cuál es la diferencia entre las líneas JSON (JSON de una sola línea) y JSON de varias líneas?

Para las líneas JSON, hay un objeto JSON por línea. Por ejemplo:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Para JSON de varias líneas, un objeto puede ocupar varias líneas, mientras que todos los objetos se agrupan en una matriz JSON. Por ejemplo:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

De manera predeterminada, [!DNL Batch Data Ingestion] utiliza JSON de una sola línea.

### ¿Se admite la ingesta de CSV?

La ingesta de CSV solo se admite para esquemas planos. Actualmente no se admite la ingesta de datos jerárquicos en CSV.

Para obtener todas las funciones de ingesta de datos, es necesario utilizar los formatos JSON o Parquet.

### ¿Qué tipos de validación se realizan en los datos?

Se realizan tres niveles de validación en los datos:

- Esquema: la ingesta por lotes garantiza que el esquema del de los datos introducidos coincida con el esquema del conjunto de datos.
- Tipo de datos: la ingesta por lotes garantiza que el tipo de cada campo ingerido coincida con el tipo definido en el esquema del conjunto de datos.
- Restricciones: la ingesta por lotes garantiza que las restricciones, como &quot;Obligatorio&quot;, &quot;enumeración&quot; y &quot;formato&quot;, se definan correctamente en la definición del esquema.

### ¿Cómo se puede reemplazar un lote ya ingerido?

Un lote ya introducido se puede reemplazar mediante la función Reproducción por lotes. Encontrará más información sobre la reproducción por lotes [aquí](./api-overview.md#replay-a-batch).

### ¿Cómo se monitoriza la ingesta por lotes?

Una vez que se ha indicado un lote para la promoción por lotes, el progreso de la ingesta por lotes se puede monitorizar con la siguiente solicitud:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Con esta solicitud, obtendrá una respuesta similar a la siguiente:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Estados de lotes

### ¿Cuáles son los estados de lote posibles?

Un lote puede, en su ciclo de vida, pasar por los siguientes estados:

| Estado | Datos escritos en Principal | Descripción |
| ------ | ---------------------- | ----------- |
| Abandonado | | El cliente no ha podido completar el lote en el periodo de tiempo esperado. |
| Anulado | | El cliente ha llamado explícitamente, a través de las API [!DNL Batch Data Ingestion], a una operación de anulación para el lote especificado. Una vez que un lote se encuentra en el estado Cargado, el lote no se puede cancelar. |
| Activo/Con éxito | x | El lote se ha promocionado correctamente de fase a maestro y ahora está disponible para el consumo descendente. **Nota:** Activo y de Éxito se usan indistintamente. |
| Archivado | | El lote se ha archivado en almacenamiento en frío. |
| Fallido/Fallo | | Un estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Se registra un error procesable, junto con el lote, para permitir a los clientes corregir y volver a enviar los datos. **Nota:** se ha producido un error y los errores se utilizan indistintamente. |
| Inactivo | x | El lote se ha promocionado correctamente, pero se ha revertido o ha caducado. El lote ya no estará disponible para el consumo descendente, pero los datos subyacentes permanecerán en Principal hasta que se hayan retenido, archivado o eliminado de otra forma. |
| Cargando | | El cliente está escribiendo datos para el lote. El lote está **no** listo para la promoción, en este momento. |
| Cargado | | El cliente ha completado la escritura de datos para el lote. El lote está listo para la promoción. |
| Retenido | | Los datos se han sacado de Principal y en un archivo designado en el lago de datos de Adobe. |
| Ensayo | | El cliente ha indicado correctamente el lote para la promoción y los datos se están almacenando en zona intermedia para su consumo descendente. |
| Intentando de nuevo | | El cliente ha indicado el lote para su promoción, pero debido a un error, un servicio de monitorización de lotes está reintentando el lote. Este estado se puede utilizar para indicar a los clientes que puede haber un retraso en la ingesta de los datos. |
| Parado | | El cliente ha indicado el lote para la promoción, pero después de `n` reintentos de un servicio de supervisión de lotes, la promoción de lotes se ha detenido. |

### ¿Qué significa &quot;Ensayo&quot; para los lotes?

Cuando un lote está en &quot;Ensayo&quot;, significa que el lote se marcó correctamente para su promoción y que los datos se están almacenando en zona intermedia para su consumo descendente.

### ¿Qué significa cuando un lote se está &quot;reintentando&quot;?

Cuando un lote está en &quot;Reintentando&quot;, significa que la ingesta de datos del lote se ha detenido temporalmente debido a problemas intermitentes. Cuando esto sucede, no requiere la intervención del cliente.

### ¿Qué significa cuando un lote está &quot;bloqueado&quot;?

Cuando un lote está &quot;estancado&quot;, significa que [!DNL Data Ingestion Services] está experimentando dificultades al ingerir el lote y que se han agotado todos los reintentos.

### ¿Qué significa si un lote sigue &quot;Cargando&quot;?

Cuando un lote está en &quot;Cargando&quot;, significa que no se ha llamado al API CompleteBatch para promocionar el lote.

### ¿Existe alguna manera de saber si un lote se ha ingerido correctamente?

Sí, una vez que el estado del lote es &quot;Activo&quot;, el lote se ha introducido correctamente. Para averiguar el estado del lote, siga los pasos detallados [anteriormente](#how-is-batch-ingestion-monitored).

### ¿Qué sucede después de que falla un lote? {#what-if-a-batch-fails}

Cuando un lote falla, el proceso se detiene y devuelve un estado `Failure`. El motivo del error se puede identificar en la sección `errors` de la carga útil. A continuación se muestran ejemplos de errores:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Una vez corregidos los errores, se puede volver a cargar el lote.

## Compatibilidad con lotes

### ¿Cómo se deben eliminar los lotes?

En lugar de eliminar directamente de [!DNL Catalog], los lotes deben eliminarse mediante cualquiera de los métodos siguientes:

1. Si el lote está en curso, se debe cancelar.
2. Si el lote se domina correctamente, el lote debe revertirse.

### ¿Qué métricas de nivel de lote están disponibles?

Las siguientes métricas de nivel de lote están disponibles para lotes en el estado Activo/Correcto:

| Métrica | Descripción |
| ------ | ----------- |
| inputByteSize | Número total de bytes clasificados para que [!DNL Data Ingestion Services] se procese. |
| inputRecordSize | Número total de filas almacenadas en zona intermedia para que [!DNL Data Ingestion Services] se procese. |
| outputByteSize | Número total de bytes generados por [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | Número total de filas que [!DNL Data Ingestion Services] ha agregado a [!DNL Data Lake]. |
| partitionCount | Número total de particiones escritas en [!DNL Data Lake]. |

### ¿Por qué las métricas no están disponibles en algunos lotes?

Existen dos razones por las que las métricas pueden no estar disponibles en el lote:

1. El lote nunca llegó correctamente al estado Activo/Correcto.
2. El lote se promocionó mediante una ruta de promoción heredada, como la ingesta de CSV.

### ¿Qué significan los distintos códigos de estado?

| Código de estado | Descripción |
| ----------- | ----------- |
| 106 | El archivo del conjunto de datos está vacío. |
| 118 | El archivo CSV contiene una fila de encabezado vacía. |
| 200 | El lote se ha aceptado para su procesamiento y pasará a un estado final, como Activo o Error. Una vez enviado, el lote se puede supervisar mediante el extremo `GetBatch`. |
| 400 | Solicitud incorrecta. Se devuelve si faltan fragmentos o si hay trozos superpuestos en un lote. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
