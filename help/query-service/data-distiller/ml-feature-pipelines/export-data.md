---
title: Exportar datos a entornos XML externos
description: Aprenda a compartir un conjunto de datos de formación preparado, creado con Data Distiller, en una ubicación de almacenamiento en la nube que su entorno de ML pueda leer para entrenar y puntuar su modelo.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 3%

---

# Exportación de datos a entornos XML externos

Este documento muestra cómo compartir un conjunto de datos de formación preparado creado con Data Distiller en una ubicación de almacenamiento en la nube que su entorno de ML puede leer para entrenar y puntuar el modelo. El ejemplo aquí exporta el conjunto de datos de formación a [Zona de aterrizaje de datos (DLZ)](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html). Puede cambiar el destino de almacenamiento según sea necesario para trabajar con su entorno de aprendizaje automático.

El [Servicio de flujo para destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) se utiliza para completar la canalización de funciones aterrizando un conjunto de datos de funciones calculadas en una ubicación de almacenamiento en la nube adecuada.

## Crear la conexión de origen {#create-source-connection}

La conexión de origen es responsable de configurar la conexión con el conjunto de datos de Adobe Experience Platform para que el flujo resultante sepa exactamente dónde buscar los datos y en qué formato.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Creación de la conexión de destino {#create-target-connection}

La conexión de destino es responsable de conectarse al sistema de archivos de destino. Esto requiere primero crear una conexión base a la cuenta de almacenamiento en la nube (la zona de aterrizaje de datos en este ejemplo) y luego una conexión de destino a una ruta de archivo específica con opciones de compresión y formato especificadas.

Cada uno de los destinos de almacenamiento en la nube disponibles se identifica mediante un ID de especificación de conexión:

| Tipo de almacenamiento en nube | ID de especificación de conexión |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Almacenamiento de Azure Blob | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Zona de aterrizaje de datos | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Almacenamiento de Google Cloud | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## Creación del flujo de datos {#create-data-flow}

El paso final es crear un flujo de datos entre el conjunto de datos especificado en la conexión de origen y la ruta de acceso del archivo de destino especificada en la conexión de destino.

Cada tipo de almacenamiento en la nube disponible se identifica con un ID de especificación de flujo:

| Tipo de almacenamiento en nube | ID de especificación de flujo |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Almacenamiento de Azure Blob | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Zona de aterrizaje de datos | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Almacenamiento de Google Cloud | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

El siguiente código crea un flujo de datos con una programación configurada para iniciarse en un futuro lejano. Esto le permite almacenar en déclencheur flujos ad hoc durante el desarrollo del modelo. Una vez que tenga un modelo entrenado, puede actualizar la programación del flujo de datos para compartir el conjunto de datos de funciones en la programación deseada.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Con el flujo de datos creado, ahora puede almacenar en déclencheur una ejecución de flujo ad hoc para compartir el conjunto de datos de funciones bajo demanda:

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Uso compartido optimizado en la zona de aterrizaje de datos

Para compartir un conjunto de datos en la zona de aterrizaje de datos más fácilmente, la variable `aepp` La biblioteca proporciona un `exportDatasetToDataLandingZone` que ejecuta los pasos anteriores en una sola llamada a la función:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Este código crea la conexión de origen, la conexión de destino y el flujo de datos en función de los parámetros proporcionados, y ejecuta una ejecución ad hoc del flujo de datos en un solo paso.
