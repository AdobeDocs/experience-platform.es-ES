---
keywords: Experience Platform;inicio;temas populares; tutoriales de API; API de destinos de flujo continuo; Plataforma
solution: Experience Platform
title: Conéctese a destinos de flujo continuo y active los datos mediante la API de servicio de flujo en Adobe Experience Platform
description: Este documento cubre la creación de destinos de flujo continuo mediante la API de Adobe Experience Platform
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 2%

---

# Conectarse a destinos de flujo continuo y activar datos mediante la API de servicio de flujo

>[!IMPORTANT]
> 
>Para conectarse a un destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions).
>
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
>
>Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

En este tutorial se explica cómo utilizar las llamadas de API para conectarse a los datos de Adobe Experience Platform y crear una conexión con un destino de almacenamiento en la nube de flujo continuo ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) o [Centros de eventos de Azure](../catalog/cloud-storage/azure-event-hubs.md)), cree un flujo de datos para el nuevo destino creado y active los datos para el nuevo destino creado.

Este tutorial utiliza la variable [!DNL Amazon Kinesis] destino en todos los ejemplos, pero los pasos son idénticos para [!DNL Azure Event Hubs].

![Información general: los pasos para crear un destino de flujo continuo y activar segmentos](../assets/api/streaming-destination/overview.png)

Si prefiere usar la interfaz de usuario en Platform para conectarse a un destino y activar datos, consulte la [Conectar un destino](../ui/connect-destination.md) y [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../ui/activate-segment-streaming-destinations.md) tutoriales.

## Introducción 

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] es el sistema de registro para la ubicación y el linaje de los datos dentro de Experience Platform.
* [Sandboxes](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para activar los datos en destinos de flujo continuo en Platform.

### Recopilar las credenciales necesarias

Para completar los pasos de este tutorial, debe tener preparadas las siguientes credenciales, según el tipo de destinos a los que esté conectando y activando segmentos.

* Para [!DNL Amazon Kinesis] conexiones: `accessKeyId`, `secretKey`, `region` o `connectionUrl`
* Para [!DNL Azure Event Hubs] conexiones: `sasKeyName`, `sasKey`, `namespace`

### Leer llamadas de API de ejemplo {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados opcionales y requeridos {#gather-values}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos del Experience Platform se pueden aislar en entornos limitados virtuales específicos. En las solicitudes a las API de plataforma, puede especificar el nombre y el ID del simulador de pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en el Experience Platform, consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

### Documentación de Swagger {#swagger-docs}

Puede encontrar la documentación de referencia adjunta para todas las llamadas a la API en este tutorial en Swagger. Consulte la [Documentación de la API del servicio de flujo en el Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Le recomendamos que utilice este tutorial y la página de documentación de Swagger en paralelo.

## Obtener la lista de destinos de flujo continuo disponibles {#get-the-list-of-available-streaming-destinations}

![Pasos de destino paso 1](../assets/api/streaming-destination/step1.png)

Como primer paso, debe decidir a qué destino de flujo se activan los datos. Para empezar, realice una llamada para solicitar una lista de destinos disponibles a los que puede conectarse y activar segmentos. Realice la siguiente solicitud de GET a la `connectionSpecs` para devolver una lista de destinos disponibles:

**Formato de API**

```http
GET /connectionSpecs
```

**Solicitud**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Respuesta**

Una respuesta correcta contiene una lista de destinos disponibles y sus identificadores únicos (`id`). Almacene el valor del destino que planea utilizar, tal como se requerirá en pasos adicionales. Por ejemplo, si desea conectarse y enviar segmentos a [!DNL Amazon Kinesis] o [!DNL Azure Event Hubs], busque el siguiente fragmento en la respuesta:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Conectarse a los datos del Experience Platform {#connect-to-your-experience-platform-data}

![Información general sobre los pasos de destino paso 2](../assets/api/streaming-destination/step2.png)

A continuación, debe conectarse a los datos del Experience Platform para poder exportar los datos de perfil y activarlos en el destino preferido. Esto consta de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso a los datos en Experience Platform, configurando una conexión base.
2. A continuación, con el ID de conexión base, realizará otra llamada en la que creará una conexión de origen, que establece la conexión con los datos del Experience Platform.


### Autorizar el acceso a los datos en el Experience Platform

**Formato de API**

```http
POST /connections
```

**Solicitud**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Usar el ID de especificación de conexión para el servicio de perfil - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta contiene el identificador único de la conexión base (`id`). Almacene este valor como sea necesario en el siguiente paso para crear la conexión de origen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Conectarse a los datos del Experience Platform {#connect-to-platform-data}

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilice el ID que ha obtenido en el paso anterior.
* `{CONNECTION_SPEC_ID}`: Usar el ID de especificación de conexión para el servicio de perfil - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) para la conexión de origen recién creada con el servicio de perfil. Esto confirma que se ha conectado correctamente a los datos del Experience Platform. Almacene este valor tal como es necesario en un paso posterior.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Conectarse al destino de flujo continuo {#connect-to-streaming-destination}

![Pasos de destino paso 3](../assets/api/streaming-destination/step3.png)

En este paso, está configurando una conexión con el destino de flujo continuo deseado. Esto consta de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso al destino de flujo continuo, configurando una conexión base.
2. A continuación, con el ID de conexión base, realizará otra llamada en la que creará una conexión de destino, que especifica la ubicación en la cuenta de almacenamiento en la que se entregarán los datos exportados, así como el formato de los datos que se exportarán.

### Autorizar el acceso al destino de flujo continuo

**Formato de API**

```http
POST /connections
```

**Solicitud**

>[!IMPORTANT]
>
>El ejemplo siguiente incluye comentarios de código con el prefijo `//`. Estos comentarios resaltan dónde deben utilizarse distintos valores para los distintos destinos de flujo continuo. Elimine los comentarios antes de utilizar el fragmento.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Utilice el ID de especificación de conexión que obtuvo en el paso [Obtener la lista de destinos disponibles](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: rellene el nombre del destino de flujo continuo: `Aws Kinesis authentication credentials` o `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *Para [!DNL Amazon Kinesis] conexiones.* Su ID de acceso para su ubicación de almacenamiento de Amazon Kinesis.
* `{SECRET_KEY}`: *Para [!DNL Amazon Kinesis] conexiones.* La clave secreta para la ubicación de almacenamiento de Amazon Kinesis.
* `{REGION}`: *Para [!DNL Amazon Kinesis] conexiones.* La región de su [!DNL Amazon Kinesis] cuenta en la que Platform transmitirá los datos.
* `{SAS_KEY_NAME}`: *Para [!DNL Azure Event Hubs] conexiones.* Rellene su nombre de clave SAS. Obtenga información sobre cómo autenticarse en [!DNL Azure Event Hubs] con claves SAS en la variable [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Para [!DNL Azure Event Hubs] conexiones.* Rellene la clave SAS. Obtenga información sobre cómo autenticarse en [!DNL Azure Event Hubs] con claves SAS en la variable [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Para [!DNL Azure Event Hubs] conexiones.* Complete la variable [!DNL Azure Event Hubs] área de nombres donde Platform transmitirá los datos. Para obtener más información, consulte [Crear un espacio de nombres de centros de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) en el [!DNL Microsoft] documentación.

**Respuesta**

Una respuesta correcta contiene el identificador único de la conexión base (`id`). Almacene este valor como sea necesario en el siguiente paso para crear una conexión de destino.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Especificar la ubicación de almacenamiento y el formato de los datos

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

>[!IMPORTANT]
>
>El ejemplo siguiente incluye comentarios de código con el prefijo `//`. Estos comentarios resaltan dónde deben utilizarse distintos valores para los distintos destinos de flujo continuo. Elimine los comentarios antes de utilizar el fragmento.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Utilice el ID de conexión base que obtuvo en el paso anterior.
* `{CONNECTION_SPEC_ID}`: Utilice la especificación de conexión obtenida en el paso [Obtener la lista de destinos disponibles](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Para [!DNL Amazon Kinesis] conexiones.* Proporcione el nombre del flujo de datos existente en su [!DNL Amazon Kinesis] cuenta. Platform exportará datos a este flujo.
* `{REGION}`: *Para [!DNL Amazon Kinesis] conexiones.* Región de la cuenta de Amazon Kinesis donde Platform transmitirá los datos.
* `{EVENT_HUB_NAME}`: *Para [!DNL Azure Event Hubs] conexiones.* Complete la variable [!DNL Azure Event Hub] nombre donde Platform transmitirá sus datos. Para obtener más información, consulte [Creación de un centro de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) en el [!DNL Microsoft] documentación.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) para la conexión de destino recién creada con el destino de flujo continuo. Almacene este valor tal como es necesario en pasos posteriores.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Creación de un flujo de datos

![Pasos de destino paso 4](../assets/api/streaming-destination/step4.png)

Con los ID obtenidos en los pasos anteriores, ahora puede crear un flujo de datos entre los datos del Experience Platform y el destino en el que desea activar los datos. Considere este paso como la construcción de la canalización, a través de la cual fluirán los datos más adelante, entre el Experience Platform y el destino deseado.

Para crear un flujo de datos, realice una solicitud de POST, como se muestra a continuación, mientras proporciona los valores mencionados a continuación dentro de la carga útil.

Realice la siguiente solicitud de POST para crear un flujo de datos.

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: El ID de especificación de flujo para destinos basados en perfiles es `71471eba-b620-49e4-90fd-23f1fa0174d8`. Utilice este valor en la llamada de .
* `{SOURCE_CONNECTION_ID}`: Utilice el ID de conexión de origen que obtuvo en el paso [Conectarse al Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilice el ID de conexión de destino que obtuvo en el paso [Conectarse al destino de flujo continuo](#connect-to-streaming-destination).

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado y un `etag`. Tenga en cuenta ambos valores. como lo hará en el siguiente paso, para activar segmentos.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activar datos en el nuevo destino {#activate-data}

![Pasos de destino paso 5](../assets/api/streaming-destination/step5.png)

Después de crear todas las conexiones y el flujo de datos, ahora puede activar los datos de perfil en la plataforma de flujo continuo. En este paso, se selecciona qué segmentos y qué atributos de perfil se envían al destino y se pueden programar y enviar datos al destino.

Para activar segmentos en el nuevo destino, debe realizar una operación de PATCH JSON similar al ejemplo siguiente. Puede activar varios segmentos y atributos de perfil en una llamada. Para obtener más información sobre el PATCH JSON, consulte la [Especificación de RFC](https://tools.ietf.org/html/rfc6902).

**Formato de API**

```http
PATCH /flows
```

**Solicitud**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

| Propiedad | Descripción |
| --------- | ----------- |
| `{DATAFLOW_ID}` | En la URL, utilice el ID del flujo de datos que creó en el paso anterior. |
| `{ETAG}` | Obtenga la variable `{ETAG}` de la respuesta del paso anterior, [Crear un flujo de datos](#create-dataflow). El formato de respuesta del paso anterior tiene comillas de escape. Debe utilizar los valores sin escape en el encabezado de la solicitud. Consulte el ejemplo siguiente: <br> <ul><li>Ejemplo de respuesta: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valor que se debe usar en la solicitud: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> El valor de etiqueta se actualiza con cada actualización correcta de un flujo de datos. |
| `{SEGMENT_ID}` | Proporcione el ID de segmento que desea exportar a este destino. Para recuperar los ID de segmento de los segmentos que desea activar, consulte [recuperar una definición de segmento](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) en la referencia de la API de Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Por ejemplo, `"person.lastName"` |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. Para agregar un segmento a un flujo de datos, utilice la variable `add` operación. |
| `path` | Define la parte del flujo que se va a actualizar. Cuando agregue un segmento a un flujo de datos, utilice la ruta especificada en el ejemplo. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |
| `id` | Especifique el ID del segmento que está agregando al flujo de datos de destino. |
| `name` | *Opcional*. Especifique el nombre del segmento que está agregando al flujo de datos de destino. Tenga en cuenta que este campo no es obligatorio y que puede agregar correctamente un segmento al flujo de datos de destino sin proporcionar su nombre. |

**Respuesta**

Busque una respuesta 202 OK. No se devuelve ningún cuerpo de respuesta. Para validar que la solicitud era correcta, consulte el paso siguiente, Validar el flujo de datos.

## Validación del flujo de datos

![Pasos de destino paso 6](../assets/api/streaming-destination/step6.png)

Como último paso del tutorial, debe validar que los segmentos y los atributos de perfil se hayan asignado correctamente al flujo de datos.

Para validar esto, realice la siguiente solicitud de GET:

**Formato de API**

```http
GET /flows
```

**Solicitud**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilice el flujo de datos del paso anterior.
* `{ETAG}`: Utilice la etiqueta del paso anterior.

**Respuesta**

La respuesta devuelta debe incluirse en la variable `transformations` parámetros de los segmentos y atributos de perfil que envió en el paso anterior. Un ejemplo `transformations` en la respuesta podría tener el siguiente aspecto:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Datos exportados**

>[!IMPORTANT]
>
> Además de los atributos de perfil y los segmentos del paso [Activar datos en el nuevo destino](#activate-data), los datos exportados en [!DNL AWS Kinesis] y [!DNL Azure Event Hubs] también incluirá información sobre el mapa de identidad. Representa las identidades de los perfiles exportados (por ejemplo [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), ID móvil, Google ID, dirección de correo electrónico, etc.). Vea el ejemplo siguiente.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Uso [!DNL Postman] colecciones para conectarse a destinos de flujo continuo  {#collections}

Para conectarse a los destinos de flujo continuo descritos en este tutorial de forma más sencilla, puede utilizar [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] es una herramienta que puede utilizar para realizar llamadas a la API y administrar bibliotecas de llamadas y entornos predefinidos.

Para este tutorial específico, haga lo siguiente [!DNL Postman] se han adjuntado colecciones:

* [!DNL AWS Kinesis] [!DNL Postman] colección
* [!DNL Azure Event Hubs] [!DNL Postman] colección

Haga clic en [here](../assets/api/streaming-destination/DestinationPostmanCollection.zip) para descargar el archivo de colecciones.

Cada colección incluye las solicitudes y variables de entorno necesarias para [!DNL AWS Kinesis]y [!DNL Azure Event Hub], respectivamente.

### Cómo usar la variable [!DNL Postman] colecciones {#how-to-use-postman-collections}

Para conectarse correctamente a los destinos utilizando el [!DNL Postman] colecciones, siga estos pasos:

* Descargar e instalar [!DNL Postman];
* [Descargar](../assets/api/streaming-destination/DestinationPostmanCollection.zip) y descomprimir las colecciones adjuntas;
* Importar las colecciones de sus carpetas correspondientes a [!DNL Postman];
* Rellene las variables de entorno según las instrucciones de este artículo;
* Ejecute el [!DNL API] solicitudes de [!DNL Postman], según las instrucciones de este artículo.

## Gestión de errores de API {#api-error-handling}

Los extremos de API de este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](/help/landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform para obtener más información sobre la interpretación de las respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha conectado correctamente Platform a uno de sus destinos de flujo continuo preferidos y ha configurado un flujo de datos en el destino correspondiente. Los datos salientes ahora se pueden utilizar en el destino para el análisis de clientes o para cualquier otra operación de datos que desee realizar. Consulte las páginas siguientes para obtener más información:

* [Información general sobre los destinos](../home.md)
* [Descripción general del catálogo de destinos](../catalog/overview.md)
