---
keywords: Experience Platform;inicio;temas populares;datos ingestados;solución de problemas;preguntas frecuentes;ingesta por lotes;ingesta por lotes;
solution: Experience Platform
title: Guía de solución de problemas de ingesta de lotes
description: Esta documentación ayudará a responder a las preguntas más frecuentes sobre las API de ingesta de datos por lotes de Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# Guía de solución de problemas de ingesta por lotes

Esta documentación ayudará a responder a las preguntas más frecuentes sobre Adobe Experience Platform [!DNL Batch Data Ingestion] API.

## Llamadas de API por lotes

### ¿Los lotes están activos inmediatamente después de recibir HTTP 200 OK de la API CompleteBatch?

La variable `200 OK` La respuesta de la API significa que el lote se ha aceptado para su procesamiento; no está activo hasta que pasa a su estado final, como Activo o Fallo.

### ¿Es seguro volver a intentar la llamada de API CompleteBatch después de que falle?

Sí: es seguro volver a intentar la llamada de API. A pesar del fallo, es posible que la operación haya tenido éxito y que el lote haya sido aceptado con éxito. Sin embargo, se espera que los clientes tengan mecanismos de reintento en caso de que falle la API y, de hecho, se les recomienda que lo vuelvan a intentar. Si la operación se realiza correctamente, la API devolverá un error, incluso después de volver a intentarlo.

### ¿Cuándo se debe utilizar la API de carga de archivos grandes?

El tamaño de archivo recomendado para usar la API de carga de archivos grandes es de 256 MB o más. Encontrará más información sobre cómo utilizar la API de carga de archivos grande [here](./api-overview.md#ingest-large-parquet-files).

### ¿Por qué falla la llamada a la API Large File Complete?

Si se encuentran fragmentos de un archivo grande superpuestos o que faltan, el servidor responde con una solicitud incorrecta HTTP 400. Esto puede ocurrir porque es posible cargar fragmentos superpuestos, ya que las validaciones de rango se realizan en el momento de la finalización del archivo, cuando los fragmentos del archivo se unen.

## Compatibilidad con Ingesta

### ¿Cuáles son los formatos de ingesta compatibles?

Actualmente, tanto Parquet como JSON son compatibles. El CSV se admite en base a elementos heredados. Aunque los datos se promocionarán para realizar comprobaciones maestras y preliminares, no se admitirán funciones modernas, como conversión, partición o validación de filas.

### ¿Dónde se debe especificar el formato de entrada por lotes?

El formato de entrada debe especificarse en el momento de creación del lote dentro de la carga útil. A continuación se muestra un ejemplo de cómo especificar el formato de entrada por lotes:

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

Para que los datos aparezcan en el conjunto de datos, el lote debe marcarse como completado. Todos los archivos que desee introducir deben cargarse antes de marcar el lote como completo. A continuación se muestra un ejemplo de marca de un lote como completo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### ¿Cómo se incorpora JSON multilínea?

Para ingerir JSON multilínea, la variable `isMultiLineJson` el indicador debe establecerse en el momento de la creación del lote. A continuación se puede ver un ejemplo de esto:

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

Para el JSON multilínea, un objeto puede ocupar varias líneas, mientras que todos los objetos están ajustados en una matriz JSON. Por ejemplo:

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

### ¿Se admite la ingesta de CSV?

La ingesta de CSV solo es compatible con esquemas planos. Actualmente, no se admite la ingesta de datos jerárquicos en CSV.

Para obtener todas las funciones de ingesta de datos, es necesario utilizar los formatos JSON o Parquet.

### ¿Qué tipos de validación se realizan en los datos?

Existen tres niveles de validación realizados en los datos:

- Schema - Batch Ingestion garantiza que el esquema del de los datos introducidos coincida con el esquema del conjunto de datos.
- Tipo de datos: la ingesta por lotes garantiza que el tipo de cada campo ingerido coincida con el tipo definido en el esquema del conjunto de datos.
- Restricciones - La Ingesta de lotes garantiza que las restricciones, como &quot;Requerido&quot;, &quot;enumeración&quot; y &quot;formato&quot;, se definan correctamente en la definición del esquema.

### ¿Cómo se puede reemplazar un lote ingerido?

Un lote ya ingerido se puede reemplazar mediante la función Reproducción por lotes. Encontrará más información sobre la reproducción por lotes [here](./api-overview.md#replay-a-batch).

### ¿Cómo se controla la ingestión por lotes?

Una vez que se ha señalado un lote para la promoción por lotes, el progreso de la ingesta por lotes puede monitorizarse con la siguiente solicitud:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Con esta solicitud, obtendrá una respuesta similar a esta:

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

### ¿Cuáles son los posibles estados de lote?

Un lote puede, en su ciclo vital, pasar por los siguientes estados:

| Estado | Datos escritos en Master | Descripción |
| ------ | ---------------------- | ----------- |
| Abandonado |  | El cliente no pudo completar el lote en el intervalo de tiempo esperado. |
| Anulado |  | El cliente ha invocado explícitamente, a través de la variable [!DNL Batch Data Ingestion] API, una operación de anulación para el lote especificado. Una vez que un lote está en el estado Loaded, el lote no se puede anular. |
| Activo/Correcto | x | El lote se ha promocionado correctamente de escenario a maestro y ahora está disponible para el consumo descendente. **Nota:** Active y Success se utilizan de forma intercambiable. |
| Archivado |  | El lote se ha archivado en almacenamiento en frío. |
| Error/error |  | Estado de terminal que resulta de una configuración incorrecta o de datos incorrectos. Se registra un error procesable, junto con el lote, que permite a los clientes corregir y volver a enviar los datos. **Nota:** Los errores y los errores se utilizan de forma intercambiable. |
| Inactivo | x | El lote se promocionó correctamente, pero se ha revertido o ha caducado. El lote ya no estará disponible para el consumo descendente, pero los datos subyacentes permanecerán en Master hasta que se hayan retenido, archivado o eliminado de otro modo. |
| Carga |  | El cliente está escribiendo datos para el lote. El lote es **not** listo para la promoción, en este momento. |
| Cargado |  | El cliente ha completado la escritura de datos para el lote. El lote está listo para la promoción. |
| Conservado |  | Los datos se han extraído de Master y de un archivo designado en Adobe Data Lake. |
| Ensayo |  | El cliente ha señalado correctamente el lote para su promoción y los datos se están montando para su consumo descendente. |
| Reintentando |  | El cliente ha señalado el lote para su promoción, pero debido a un error, el servicio de supervisión de lotes está reintentando el lote. Este estado se puede utilizar para informar a los clientes de que puede haber un retraso en la ingesta de los datos. |
| Estancado |  | El cliente ha señalado el lote para su promoción, pero después de `n` reintentos por parte de un servicio de supervisión por lotes, la promoción por lotes se ha estancado. |

### ¿Qué significa &quot;Ensayo&quot; para los lotes?

Cuando un lote se encuentra en &quot;Ensayo&quot;, significa que el lote se ha señalado correctamente para su promoción y que los datos se están montando para su consumo descendente.

### ¿Qué significa cuando un lote está &quot;reintentando&quot;?

Cuando un lote se está &quot;reintentando&quot;, significa que la ingesta de datos del lote se ha detenido temporalmente debido a problemas intermitentes. Cuando esto sucede, no requiere la intervención del cliente.

### ¿Qué significa cuando un lote está &quot;Paralizado&quot;?

Cuando un lote está en &quot;Estancado&quot;, significa que [!DNL Data Ingestion Services] está experimentando dificultades para ingerir el lote y todos los reintentos se han agotado.

### ¿Qué significa si un lote sigue siendo &quot;Cargando&quot;?

Cuando un lote se encuentra en &quot;Carga&quot;, significa que no se ha llamado a la API CompleteBatch para promocionar el lote.

### ¿Existe alguna forma de saber si un lote se ha introducido correctamente?

Una vez que el estado del lote es &quot;Activo&quot;, el lote se ha introducido correctamente. Para averiguar el estado del lote, siga los pasos detallados [previous](#how-is-batch-ingestion-monitored).

### ¿Qué sucede después de que falla un lote?

Cuando falla un lote, el motivo del error se puede identificar en la variable `errors` de la carga útil. A continuación se pueden ver ejemplos de errores:

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

En lugar de eliminar directamente de [!DNL Catalog], los lotes deben eliminarse utilizando cualquiera de los métodos que se indican a continuación:

1. Si el lote está en curso, se debe anular el lote.
2. Si el lote se administra correctamente, el lote debe revertirse.

### ¿Qué métricas a nivel de lote están disponibles?

Las siguientes métricas a nivel de lote están disponibles para lotes en el estado Activo/Correcto:

| Métrica | Descripción |
| ------ | ----------- |
| inputByteSize | El número total de bytes configurados para [!DNL Data Ingestion Services] para procesar. |
| inputRecordSize | El número total de filas organizadas para [!DNL Data Ingestion Services] para procesar. |
| outputByteSize | El número total de bytes exportados por [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| outputRecordSize | El número total de filas resultante de [!DNL Data Ingestion Services] a [!DNL Data Lake]. |
| particiónCount | El número total de particiones escritas en [!DNL Data Lake]. |

### ¿Por qué las métricas no están disponibles en algunos lotes?

Existen dos razones por las que las métricas pueden no estar disponibles en el lote:

1. El lote nunca llegó correctamente al estado Activo/Correcto.
2. El lote se promocionó mediante una ruta de promoción heredada, como la ingesta de CSV.

### ¿Qué significan los diferentes códigos de estado?

| Código de estado | Descripción |
| ----------- | ----------- |
| 106 | El archivo del conjunto de datos está vacío. |
| 118 | El archivo CSV contiene una fila de encabezado vacía. |
| 200 | El lote se ha aceptado para su procesamiento y pasará a un estado final, como Activo o Fallo. Una vez enviado, el lote puede monitorizarse utilizando la variable `GetBatch` punto final. |
| 400 | Solicitud incorrecta. Se devuelve si faltan fragmentos o si se superponen en un lote. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
