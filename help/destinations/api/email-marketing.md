---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Conectarse a destinos de marketing por correo electrónico y activar datos mediante la API de servicio de flujo
description: Este documento cubre la creación de destinos de marketing por correo electrónico mediante la API de Adobe Experience Platform
topic-legacy: tutorial
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 1%

---

# Conectarse a destinos de marketing por correo electrónico y activar datos mediante la API de servicio de flujo

Este tutorial muestra cómo utilizar las llamadas de API para conectarse a los datos de Adobe Experience Platform, crear un [destino de marketing por correo electrónico](../catalog/email-marketing/overview.md), crear un flujo de datos para el nuevo destino creado y activar los datos en el nuevo destino creado.

Este tutorial utiliza el destino de Adobe Campaign en todos los ejemplos, pero los pasos son idénticos para todos los destinos de marketing por correo electrónico.

![Información general: los pasos para crear un destino y activar segmentos](../assets/api/email-marketing/overview.png)

Si prefiere utilizar la interfaz de usuario en Platform para conectar un destino y activar datos, consulte los tutoriales [Connect a destination](../ui/connect-destination.md) y [Activate profiles and segments to a destination](../ui/activate-destinations.md) .

## Introducción

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
* [[!DNL Catalog Service]](../../catalog/home.md):  [!DNL Catalog] es el sistema de registro para la ubicación y el linaje de datos dentro de  [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para activar los datos en destinos de marketing por correo electrónico en Platform.

### Recopilar las credenciales necesarias

Para completar los pasos de este tutorial, debe tener preparadas las siguientes credenciales, según el tipo de destinos a los que esté conectando y activando segmentos.

* Para conexiones [!DNL Amazon] S3 a plataformas de marketing por correo electrónico: `accessId`, `secretKey`
* Para conexiones SFTP a plataformas de marketing por correo electrónico: `domain`, `port`, `username`, `password` o `ssh key` (según el método de conexión a la ubicación FTP)

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados opcionales y requeridos

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Los recursos de [!DNL Experience Platform] se pueden aislar en entornos limitados virtuales específicos. En las solicitudes a las API [!DNL Platform] , puede especificar el nombre y el ID del simulador de pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Experience Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

### Documentación de Swagger

Puede encontrar la documentación de referencia adjunta para todas las llamadas a la API en este tutorial en Swagger. Consulte la [documentación de la API del servicio de flujo en Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Le recomendamos que utilice este tutorial y la página de documentación de Swagger en paralelo.

## Obtener la lista de destinos disponibles {#get-the-list-of-available-destinations}

![Pasos de destino paso 1](../assets/api/email-marketing/step1.png)

Como primer paso, debe decidir a qué destino de marketing por correo electrónico desea activar los datos. Para empezar, realice una llamada para solicitar una lista de destinos disponibles a los que puede conectarse y activar segmentos. Realice la siguiente solicitud de GET al extremo `connectionSpecs` para devolver una lista de destinos disponibles:

**Formato de API**

```http
GET /connectionSpecs
```

**Solicitud**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Respuesta**

Una respuesta correcta contiene una lista de destinos disponibles y sus identificadores únicos (`id`). Almacene el valor del destino que planea utilizar, tal como se requerirá en pasos adicionales. Por ejemplo, si desea conectar y enviar segmentos a Adobe Campaign, busque el siguiente fragmento en la respuesta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Conéctese a sus [!DNL Experience Platform] datos {#connect-to-your-experience-platform-data}

![Información general sobre los pasos de destino paso 2](../assets/api/email-marketing/step2.png)

A continuación, debe conectarse a los datos [!DNL Experience Platform] para poder exportar los datos de perfil y activarlos en el destino preferido. Esto consta de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso a los datos en [!DNL Experience Platform], configurando una conexión base.
2. A continuación, con el ID de conexión base, realizará otra llamada en la que creará una conexión de origen, que establece la conexión con los datos [!DNL Experience Platform].


### Autorizar el acceso a los datos en [!DNL Experience Platform]

**Formato de API**

```http
POST /connections
```

**Solicitud**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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


* `{CONNECTION_SPEC_ID}`: Utilice el ID de especificación de conexión para el servicio de perfil unificado:  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta contiene el identificador único de la conexión base (`id`). Almacene este valor como sea necesario en el siguiente paso para crear la conexión de origen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Conéctese a sus [!DNL Experience Platform] datos {#connect-to-platform-data}

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilice el ID que ha obtenido en el paso anterior.
* `{CONNECTION_SPEC_ID}`: Utilice el ID de especificación de conexión para  [!DNL Unified Profile Service] -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada a [!DNL Unified Profile Service]. Esto confirma que se ha conectado correctamente a los datos [!DNL Experience Platform]. Almacene este valor tal como es necesario en un paso posterior.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Conectarse al destino de marketing por correo electrónico {#connect-to-email-marketing-destination}

![Pasos de destino paso 3](../assets/api/email-marketing/step3.png)

En este paso, está configurando una conexión con el destino de marketing por correo electrónico que desee. Esto consta de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso al proveedor de servicios de correo electrónico, configurando una conexión base.
2. A continuación, con el ID de conexión base, realizará otra llamada en la que creará una conexión de destino, que especifica la ubicación en la cuenta de almacenamiento en la que se entregarán los datos exportados, así como el formato de los datos que se exportarán.

### Autorizar el acceso al destino de marketing por correo electrónico

**Formato de API**

```http
POST /connections
```

**Solicitud**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Utilice el ID de especificación de conexión que obtuvo en el paso  [Obtener la lista de destinos](#get-the-list-of-available-destinations) disponibles.
* `{S3 or SFTP}`: rellene el tipo de conexión deseado para este destino. En el [catálogo de destino](../catalog/overview.md), desplácese hasta el destino que prefiera para ver si se admiten los tipos de conexión S3 o SFTP.
* `{ACCESS_ID}`: Su ID de acceso para su ubicación de almacenamiento  [!DNL Amazon] S3.
* `{SECRET_KEY}`: La clave secreta para la ubicación de almacenamiento de  [!DNL Amazon] S3.

**Respuesta**

Una respuesta correcta contiene el identificador único de la conexión base (`id`). Almacene este valor como sea necesario en el siguiente paso para crear una conexión de destino.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Especificar la ubicación de almacenamiento y el formato de los datos

[!DNL Adobe Experience Platform] exporta datos para destinos de marketing por correo electrónico y almacenamiento en la nube en forma de  [!DNL CSV] archivos.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automáticamente los archivos de exportación en 5 millones de registros (filas) por archivo. Cada fila representa un perfil.
>
>Los nombres de archivos divididos se añaden con un número que indica que el archivo forma parte de una exportación más grande, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Utilice el ID de conexión base que obtuvo en el paso anterior.
* `{CONNECTION_SPEC_ID}`: Utilice la especificación de conexión que obtuvo en el paso  [Obtener la lista de destinos](#get-the-list-of-available-destinations) disponibles.
* `{BUCKETNAME}`: Su compartimento  [!DNL Amazon] S3, donde Platform depositará la exportación de datos.
* `{FILEPATH}`: La ruta en el directorio de compartimentos de  [!DNL Amazon] S3 donde Platform depositará la exportación de datos.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de destino recién creada al destino de marketing de correo electrónico. Almacene este valor tal como es necesario en pasos posteriores.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Crear un flujo de datos

![Pasos de destino paso 4](../assets/api/email-marketing/step4.png)

Con los ID obtenidos en los pasos anteriores, ahora puede crear un flujo de datos entre los datos [!DNL Experience Platform] y el destino en el que desea activar los datos. Considere este paso como la construcción de la canalización, a través de la cual fluirán los datos más adelante, entre [!DNL Experience Platform] y el destino deseado.

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
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`: Utilice el flujo para el destino de marketing por correo electrónico al que desee conectarse. Para obtener la especificación de flujo, realice una operación de GET en el extremo `flowspecs` . Consulte la documentación de Swagger aquí: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. En la respuesta, busque `upsTo` y copie el ID correspondiente del destino de marketing de correo electrónico al que desea conectarse. Por ejemplo, para Adobe Campaign, busque `upsToCampaign` y copie el parámetro `id`.
* `{SOURCE_CONNECTION_ID}`: Utilice el ID de conexión de origen que obtuvo en el paso  [Conectar con su Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilice el ID de conexión de destino que obtuvo en el paso  [Conectar con destino](#connect-to-email-marketing-destination) de marketing por correo electrónico.

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado y un `etag`. Tenga en cuenta ambos valores. como lo hará en el siguiente paso, para activar segmentos.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activar datos en el nuevo destino

![Pasos de destino paso 5](../assets/api/email-marketing/step5.png)

Después de crear todas las conexiones y el flujo de datos, ahora puede activar los datos de perfil en la plataforma de marketing por correo electrónico. En este paso, se selecciona qué segmentos y qué atributos de perfil se envían al destino y se pueden programar y enviar datos al destino.

Para activar segmentos en el nuevo destino, debe realizar una operación de PATCH JSON similar al ejemplo siguiente. Puede activar varios segmentos y atributos de perfil en una llamada. Para obtener más información sobre el PATCH JSON, consulte la [especificación RFC](https://tools.ietf.org/html/rfc6902).

**Formato de API**

```http
PATCH /flows
```

**Solicitud**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{DATAFLOW_ID}`: Utilice el flujo de datos obtenido en el paso anterior.
* `{ETAG}`: Utilice la etiqueta que obtuvo en el paso anterior.
* `{SEGMENT_ID}`: Proporcione el ID de segmento que desea exportar a este destino. Para recuperar los ID de segmento de los segmentos que desea activar, vaya a **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, seleccione **[!UICONTROL Segmentation Service API]** en el menú de navegación de la izquierda y busque la operación `GET /segment/definitions` en **[!UICONTROL Segment Definitions]**.
* `{PROFILE_ATTRIBUTE}`: Por ejemplo, `"person.lastName"`

**Respuesta**

Busque una respuesta 202 OK. No se devuelve ningún cuerpo de respuesta. Para validar que la solicitud era correcta, consulte el paso siguiente, Validar el flujo de datos.

## Validación del flujo de datos

![Pasos de destino paso 6](../assets/api/email-marketing/step6.png)

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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilice el flujo de datos del paso anterior.
* `{ETAG}`: Utilice la etiqueta del paso anterior.

**Respuesta**

La respuesta devuelta debe incluir en el parámetro `transformations` los segmentos y atributos de perfil que envió en el paso anterior. Un parámetro `transformations` de muestra en la respuesta podría tener el siguiente aspecto:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
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

## Pasos siguientes

Siguiendo este tutorial, ha conectado correctamente Platform a uno de los destinos de marketing por correo electrónico preferidos y ha configurado un flujo de datos en el destino correspondiente. Los datos salientes ahora se pueden utilizar en el destino para campañas de correo electrónico, publicidad segmentada y muchos otros casos de uso. Consulte las páginas siguientes para obtener más información:

* [Información general sobre los destinos](../home.md)
* [Descripción general del catálogo de destinos](../catalog/overview.md)
