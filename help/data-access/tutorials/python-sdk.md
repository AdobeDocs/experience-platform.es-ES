---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api
solution: Experience Platform
title: SDK de acceso a datos de Python seguro
topic: tutorial
type: Tutorial
description: El SDK de acceso a datos Secure Python es un kit de desarrollo de software que permite leer y escribir conjuntos de datos desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---


# SDK seguro [!DNL Python] [!DNL Data Access]

El SDK seguro [!DNL Python] [!DNL Data Access] es un kit de desarrollo de software que permite leer y escribir conjuntos de datos desde Adobe Experience Platform.

## Primeros pasos

Debe haber completado el tutorial de [autenticación](../../tutorials/authentication.md) para tener acceso a los valores y realizar llamadas al SDK seguro [!DNL Python] [!DNL Data Access] :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. El uso del [!DNL Python] SDK requiere el nombre y el ID del simulador para pruebas en el que se realizará la operación:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

## Configuración de entorno

De forma predeterminada, los extremos de servicio se establecen en puntos finales de entorno de integración. Como resultado, para señalar a producción, establezca las siguientes variables de entorno en los siguientes valores:

| Variable | Extremo |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

Además, las credenciales se pueden agregar como variables de entorno.

| Variable | Valor |
| -------- | ----- |
| `ORG_ID` | Su `{IMS_ORG}` ID. |
| `SERVICE_API_KEY` | Su `{API_KEY}` valor. |
| `USER_TOKEN` | Su `{ACCESS_TOKEN}` valor. |
| `SERVICE_TOKEN` | Su `{SERVICE_TOKEN}`, que puede necesitar para autorizar solicitudes de canal de retorno entre servicios. |
| `SANDBOX_ID` | El `{SANDBOX_ID}` valor del simulador para pruebas. |
| `SANDBOX_NAME` | El `{SANDBOX_NAME}` valor del simulador para pruebas. |

## Instalación

Todos los paquetes se envían a `./dist` después de la compilación.

### Rueda

```python
python3 setup.py bdist_wheel --universal
```

Desde el directorio del proyecto, cargue la rueda en el entorno [!DNL Python] 3.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Archivo de huevo

```python
python3 setup.py bdist_egg
```

## Lectura de un conjunto de datos

Después de configurar las variables de entorno y completar la instalación, el conjunto de datos ahora se puede leer en el dataframe de pandas.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### SELECCIONAR columnas del conjunto de datos

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtener información de partición:

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Cláusula DISTINCT

La cláusula DISTINCT permite recuperar todos los valores distintos en un nivel de fila/columna, eliminando todos los valores de duplicado de la respuesta.

A continuación se muestra un ejemplo del uso de la `distinct()` función:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### cláusula WHERE

El [!DNL Python] SDK admite determinados operadores para ayudar a filtrar el conjunto de datos.

>[!NOTE]
>
>Las funciones utilizadas para filtrar distinguen entre mayúsculas y minúsculas.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

A continuación se muestra un ejemplo del uso de estas funciones de filtrado:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Cláusula ORDER BY

La cláusula ORDER BY permite ordenar los resultados recibidos por una columna específica en un orden específico (ascendente o descendente). En el [!DNL Python] SDK, esto se realiza mediante la `sort()` función .

A continuación se muestra un ejemplo del uso de la `sort()` función:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Cláusula LIMIT

La cláusula LIMIT permite a los usuarios limitar el número de registros recibidos del conjunto de datos.

A continuación se muestra un ejemplo del uso de la `limit()` función:

```python
df = dataset_reader.limit(100).read()
```

### Cláusula OFFSET

La cláusula OFFSET permite a los usuarios omitir filas, desde el principio, hasta el inicio de devolver filas desde un punto posterior. En combinación con LIMIT, se puede utilizar para iterar filas en bloques.

A continuación se muestra un ejemplo del uso de la `offset()` función:

```python
df = dataset_reader.offset(100).read()
```

## Escritura de un conjunto de datos

El [!DNL Python] SDK admite la escritura de conjuntos de datos. Los usuarios deberán proporcionar el dataframe pandas que se debe escribir en el conjunto de datos.

### Escribiendo el juego de datos de pandas

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Directorio de Userspace (Verificación)

Para trabajos de ejecución más prolongada, es posible que los usuarios necesiten almacenar pasos intermedios. En casos como este, el [!DNL Python] SDK permite al usuario leer y escribir en un espacio de usuario.

>[!NOTE]
>
>El SDK **no almacena las rutas a los datos** . Los usuarios deberán almacenar la ruta correspondiente a sus datos respectivos.

### Escribir en espacio de usuario

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Leer desde el espacio de usuario

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
