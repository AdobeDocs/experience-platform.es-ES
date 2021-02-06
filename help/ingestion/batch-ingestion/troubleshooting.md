---
keywords: Experience Platform;inicio;temas populares;datos ingestados;solución de problemas;faq;ingestión;ingestión por lotes;ingestión por lotes;
solution: Experience Platform
title: Guía de resolución de problemas de inserción de lotes
topic: troubleshooting
description: 'Esta documentación ayudará a responder preguntas frecuentes sobre las API de inserción de datos por lotes de Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---


# Guía de resolución de problemas de ingestión por lotes

Esta documentación ayudará a responder preguntas frecuentes sobre las API [!DNL Batch Data Ingestion] de Adobe Experience Platform.

## Llamadas a la API por lotes

### ¿Los lotes se activan inmediatamente después de recibir un HTTP 200 OK de la API CompleteBatch?

La respuesta `200 OK` de la API significa que el lote ha sido aceptado para su procesamiento; no está activo hasta que transición a su estado final, como Activo o Fallo.

### ¿Es seguro volver a intentar la llamada de API CompleteBatch después de que se produzca un error?

Sí: es seguro volver a intentar la llamada de API. A pesar del fracaso, es posible que la operación se haya realizado correctamente y que el lote se haya aceptado correctamente. Sin embargo, se espera que los clientes tengan mecanismos de reintento en caso de error de API y, de hecho, se les recomienda que lo intenten. Si la operación se ha realizado correctamente, la API devolverá el resultado satisfactorio, incluso después de volver a intentarlo.

### ¿Cuándo se debe utilizar la API de carga de archivos grandes?

El tamaño de archivo recomendado para utilizar la API de carga de archivos grandes es de 256 MB o más. Encontrará más información sobre cómo utilizar la API de carga de archivos grandes [aquí](./api-overview.md#ingest-large-parquet-files).

### ¿Por qué falla la llamada a la API Large File Complete?

Si se encuentran fragmentos de un archivo grande superpuestos o que faltan, el servidor responde con una solicitud incorrecta HTTP 400. Esto puede ocurrir porque es posible cargar fragmentos superpuestos, ya que las validaciones de rango se realizan en el momento de la finalización del archivo, cuando los fragmentos de archivo se unen.

## Compatibilidad de inserción

### ¿Cuáles son los formatos de ingesta admitidos?

Actualmente, tanto Parquet como JSON son compatibles. El CSV se admite en base a elementos heredados; mientras que los datos se promocionarán como maestros y se realizarán comprobaciones preliminares, no se admitirán funciones modernas, como conversión, partición o validación de filas.

### ¿Dónde se debe especificar el formato de entrada por lotes?

El formato de entrada debe especificarse en el momento de la creación del lote dentro de la carga útil. A continuación se muestra un ejemplo de cómo especificar el formato de entrada por lotes:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### ¿Por qué no aparecen los datos cargados en el conjunto de datos?

Para que los datos aparezcan en el conjunto de datos, el lote debe marcarse como completado. Todos los archivos que desee ingerir deben cargarse antes de marcar el lote como completado. A continuación se muestra un ejemplo de cómo marcar un lote como completo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### ¿Cómo se ingiere JSON multilínea?

Para ingestar JSON multilínea, el indicador `isMultiLineJson` debe establecerse en el momento de la creación del lote. A continuación se muestra un ejemplo de esto:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### ¿Cuál es la diferencia entre las líneas JSON (JSON de una sola línea) y JSON de varias líneas?

Para líneas JSON, hay un objeto JSON por línea. Por ejemplo:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Para JSON multilínea, un objeto puede ocupar varias líneas, mientras que todos los objetos se envuelven en una matriz JSON. Por ejemplo:

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

De forma predeterminada, [!DNL Batch Data Ingestion] utiliza JSON de una sola línea.

### ¿Se admite la ingestión de CSV?

La ingestión de CSV solo se admite para esquemas planos. Actualmente, no se admite la ingesta de datos jerárquicos en CSV.

Para obtener todas las funciones de inserción de datos, es necesario utilizar los formatos JSON o Parquet.

### ¿Qué tipos de validación se realizan en los datos?

Se realizan tres niveles de validación en los datos:

- Esquema: la ingestión por lotes garantiza que el esquema de la cantidad de datos ingestados coincida con el esquema del conjunto de datos.
- Tipo de datos: la ingestión por lotes garantiza que el tipo de cada campo ingestado coincida con el tipo definido en el esquema del conjunto de datos.
- Restricciones: la ingestión de lotes garantiza que las restricciones, como &quot;Requerido&quot;, &quot;enumeración&quot; y &quot;formato&quot;, se definan correctamente en la definición de esquema.

### ¿Cómo se puede reemplazar un lote ingerido?

Un lote ya ingerido se puede reemplazar mediante la función Reproducción por lotes. Encontrará más información sobre la reproducción por lotes [aquí](./api-overview.md#replay-a-batch).

### ¿Cómo se monitoriza la ingestión por lotes?

Una vez que se ha indicado un lote para la promoción por lotes, el progreso de la ingestión por lotes puede controlarse con la siguiente solicitud:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Con esta solicitud, obtendrá una respuesta similar a esta:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

## Estados de lote

### ¿Cuáles son los posibles estados de lote?

Un lote puede, en su ciclo vital, pasar por los siguientes estados:

| Estado | Datos escritos en el maestro | Descripción |
| ------ | ---------------------- | ----------- |
| Abandonado |  | El cliente no pudo completar el lote en el intervalo de tiempo esperado. |
| Anulado |  | El cliente ha llamado explícitamente, a través de las API [!DNL Batch Data Ingestion], una operación de anulación para el lote especificado. Una vez que un lote está en estado Cargado, no se puede anular el lote. |
| Activo/Correcto | x | El lote se ha promocionado correctamente de escenario a maestro y ahora está disponible para el consumo de flujo descendente. **Nota:** Activo y Éxito se utilizan indistintamente. |
| Archivado |  | El lote ha sido archivado en almacenamiento frío. |
| Fallado/Error |  | Estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Se registra un error procesable, junto con el lote, para permitir a los clientes corregir y volver a enviar los datos. **Nota:** Fallo y Error se utilizan indistintamente. |
| Inactivo | x | El lote se promocionó correctamente, pero se ha revertido o ha caducado. El lote ya no estará disponible para el consumo de flujo descendente, pero los datos subyacentes permanecerán en Master hasta que se hayan retenido, archivado o eliminado de otro modo. |
| Cargando |  | El cliente está escribiendo datos para el lote. El lote está **no** listo para la promoción, en este momento. |
| Cargado |  | El cliente ha terminado de escribir los datos del lote. El lote está listo para la promoción. |
| Conservado |  | Los datos han sido extraídos de Master y de un archivo designado en Adobe Data Lake. |
| Ensayo |  | El cliente ha indicado correctamente el lote para la promoción y los datos se están escalonando para su consumo en el flujo descendente. |
| Reintentar |  | El cliente ha indicado el lote para la promoción, pero debido a un error, un servicio de supervisión de lotes lo está reintentando. Este estado se puede utilizar para indicar a los clientes que puede haber un retraso en la ingesta de datos. |
| Detenido |  | El cliente ha indicado el lote para la promoción, pero después de `n` reintentos por parte de un servicio de monitoreo de lotes, la promoción de lotes se ha estancado. |

### ¿Qué significa &quot;Ensayo&quot; para los lotes?

Cuando un lote se encuentra en &quot;Ensayo&quot;, significa que el lote se marcó correctamente para la promoción y que los datos se están escalonando para el consumo en sentido descendente.

### ¿Qué significa cuando un lote está &quot;reintentando&quot;?

Cuando un lote se está &quot;reintentando&quot;, significa que la ingestión de datos del lote se ha detenido temporalmente debido a problemas intermitentes. Cuando esto sucede, no requiere la intervención del cliente.

### ¿Qué significa cuando un lote está &quot;Detenido&quot;?

Cuando un lote se encuentra en &quot;Parado&quot;, significa que [!DNL Data Ingestion Services] está experimentando dificultades para ingerir el lote y todos los reintentos se han agotado.

### ¿Qué significa si un lote sigue siendo &quot;Cargando&quot;?

Cuando un lote está en &quot;Cargando&quot;, significa que no se ha llamado a la API CompleteBatch para promocionar el lote.

### ¿Existe alguna forma de saber si un lote se ha ingerido correctamente?

Una vez que el estado del lote es &quot;Activo&quot;, el lote se ha ingestado correctamente. Para averiguar el estado del lote, siga los pasos detallados [previous](#how-is-batch-ingestion-monitored).

### ¿Qué sucede después de que falla un lote?

Cuando un lote falla, el motivo por el que falla se puede identificar en la sección `errors` de la carga útil. A continuación se pueden ver ejemplos de errores:

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

En lugar de eliminar directamente de [!DNL Catalog], los lotes deben eliminarse con cualquiera de los métodos que se indican a continuación:

1. Si el lote está en curso, se debe cancelar el lote.
2. Si el lote se masteriza correctamente, se debe revertir el lote.

### ¿Qué métricas de nivel de lote están disponibles?

Las siguientes métricas a nivel de lote están disponibles para lotes en el estado Activo/Éxito:

| Métrica | Descripción |
| ------ | ----------- |
| inputByteSize | El número total de bytes que [!DNL Data Ingestion Services] se va a procesar. |
| inputRecordSize | El número total de filas que se han montado para [!DNL Data Ingestion Services] procesarse. |
| outputByteSize | Número total de bytes exportados por [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | El número total de filas que [!DNL Data Ingestion Services] genera en [!DNL Data Lake]. |
| partitionCount | Número total de particiones escritas en [!DNL Data Lake]. |

### ¿Por qué las métricas no están disponibles en algunos lotes?

Existen dos razones por las que las métricas pueden no estar disponibles en el lote:

1. El lote nunca llegó correctamente al estado Activo/Correcto.
2. El lote se promocionó mediante una ruta de promoción heredada, como la ingestión de CSV.

### ¿Qué significan los diferentes códigos de estado?

| Código de estado | Descripción |
| ----------- | ----------- |
| 106 | El archivo de conjunto de datos está vacío. |
| 118 | El archivo CSV contiene una fila de encabezado vacía. |
| 200 | Se ha aceptado el lote para su procesamiento y se realizará la transición a un estado final, como Activo o Fallo. Una vez enviado, el lote puede monitorizarse utilizando el punto final `GetBatch`. |
| 400 | Solicitud incorrecta. Se devuelve si faltan fragmentos o si se superponen en un lote. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
