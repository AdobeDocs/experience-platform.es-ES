---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de destinos de marketing por correo electrónico
topic: tutorial
translation-type: tm+mt
source-git-commit: f31b03f027d8b44f761917f4edf19a0b5eedd76c
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 1%

---


# Crear destinos de marketing por correo electrónico y activar datos mediante llamadas de API en Adobe [!DNL Real-time Customer Data Platform]

Este tutorial muestra cómo utilizar las llamadas de API para conectarse a sus datos de Adobe Experience Platform, crear un destino [de marketing de](../../rtcdp/destinations/email-marketing-destinations.md)correo electrónico, crear un flujo de datos para el nuevo destino creado y activar los datos en el nuevo destino creado.

Este tutorial utiliza el destino de Adobe Campaign en todos los ejemplos, pero los pasos son idénticos para todos los destinos de marketing por correo electrónico.

![Información general: los pasos para crear un destino y activar segmentos](/help/rtcdp/destinations/assets/flow-api-destinations-steps-overview.png)

Si prefiere utilizar la interfaz de usuario en el CDP en tiempo real de Adobe para conectar un destino y activar datos, consulte [Conectar un destino](../../rtcdp/destinations/connect-destination.md) y [Activar perfiles y segmentos en los tutoriales de destino](../../rtcdp/destinations/activate-destinations.md) .

## Introducción

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM) [!DNL]](../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [[!Servicio de catálogo DNL]](../../catalog/home.md): [!DNL Catalog] es el sistema de registro para la ubicación y linaje de datos dentro de [!DNL Experience Platform].
* [[!Sandboxes DNL]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que debe conocer para activar datos en destinos de marketing por correo electrónico en CDP en tiempo real de Adobe.

### Recopilar las credenciales necesarias

Para completar los pasos de este tutorial, debe tener listas las siguientes credenciales, según el tipo de destinos a los que esté conectando y activando segmentos.

* Para conexiones [!DNL Amazon] S3 a plataformas de marketing por correo electrónico: `accessId`, `secretKey`
* Para conexiones SFTP a plataformas de marketing por correo electrónico: `domain`, `port`, `username`, `password` o `ssh key` (según el método de conexión a la ubicación FTP)

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados opcionales y requeridos

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Los recursos de [!DNL Experience Platform] pueden aislarse en entornos limitados virtuales específicos. En las solicitudes a [!DNL Platform] las API, puede especificar el nombre y la ID del simulador para pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Experience Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

<!--

### Definitions

Before starting this tutorial, familiarize yourself with the following terms which we'll use throughout the tutorial:

**Flow**: 

**Base Connection**: 

**Target Connection**: 

**Source Connection**: 

-->

### Documentación de Swagger

Puede encontrar la documentación de referencia adjunta para todas las llamadas de API en este tutorial en Swagger. Consulte la documentación de la API de servicio de [flujo en Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Le recomendamos que utilice este tutorial y la página de documentación de Swagger en paralelo.

## Obtener la lista de los destinos disponibles {#get-the-list-of-available-destinations}

![Pasos de destino paso 1](/help/rtcdp/destinations/assets/flow-api-destinations-step1.png)

Como primer paso, debe decidir a qué destino de mercadotecnia de correo electrónico desea activar los datos. Para empezar, realice una llamada para solicitar una lista de los destinos disponibles a los que puede conectar y activar segmentos. Realice la siguiente solicitud de GET al punto final para devolver una lista de los destinos disponibles: `connectionSpecs`

**Formato API**

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

Una respuesta correcta contiene una lista de los destinos disponibles y sus identificadores únicos (`id`). Almacene el valor del destino que va a usar, como será necesario en otros pasos. Por ejemplo, si desea conectar y enviar segmentos a Adobe Campaign, busque el siguiente fragmento en la respuesta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Conectar a sus [!DNL Experience Platform] datos {#connect-to-your-experience-platform-data}

![Pasos de destino, paso 2](/help/rtcdp/destinations/assets/flow-api-destinations-step2.png)

A continuación, debe conectarse a sus [!DNL Experience Platform] datos para poder exportar los datos de perfil y activarlos en el destino que prefiera. Se trata de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso a sus datos en [!DNL Experience Platform], configurando una conexión base.
2. A continuación, utilizando el ID de conexión base, realizará otra llamada en la que creará una conexión de origen, que establecerá la conexión con los [!DNL Experience Platform] datos.


### Autorice el acceso a sus datos en [!DNL Experience Platform]

**Formato API**

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
--header 'x-sandbox-name: {SANDBOX_NAME} \
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


* `{CONNECTION_SPEC_ID}`:: Utilice el ID de especificación de conexión para el servicio de Perfil unificado - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta contiene el identificador único (`id`) de la conexión base. Almacene este valor como sea necesario en el paso siguiente para crear la conexión de origen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Conectar a sus [!DNL Experience Platform] datos

**Formato API**

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

* `{BASE_CONNECTION_ID}`:: Utilice el Id obtenido en el paso anterior.
* `{CONNECTION_SPEC_ID}`:: Utilice el ID de especificación de conexión para [!DNL Unified Profile Service] - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada a [!DNL Unified Profile Service]. Esto confirma que se ha conectado correctamente a los [!DNL Experience Platform] datos. Almacene este valor tal como se requiere en un paso posterior.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Conectar con el destino de marketing por correo electrónico {#connect-to-email-marketing-destination}

![Pasos de destino, paso 3](/help/rtcdp/destinations/assets/flow-api-destinations-step3.png)

En este paso, está configurando una conexión con el destino de mercadotecnia de correo electrónico deseado. Se trata de dos subpasos que se describen a continuación.

1. En primer lugar, debe realizar una llamada para autorizar el acceso al proveedor de servicio de correo electrónico, configurando una conexión base.
2. A continuación, utilizando el ID de conexión base, realizará otra llamada en la que creará una conexión de destinatario, que especifica la ubicación en la cuenta de almacenamiento donde se entregarán los datos exportados, así como el formato de los datos que se exportarán.

### Autorizar el acceso al destino de mercadotecnia por correo electrónico

**Formato API**

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
    "description": "your company's holiday campaign",
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

* `{CONNECTION_SPEC_ID}`:: Utilice el ID de especificación de conexión que obtuvo en el paso [Obtener la lista de los destinos](#get-the-list-of-available-destinations)disponibles.
* `{S3 or SFTP}`:: rellene el tipo de conexión deseado para este destino. En el catálogo [de](../../rtcdp/destinations/destinations-catalog.md)destino, desplácese hasta el destino que prefiera para ver si se admiten los tipos de conexión S3 o SFTP.
* `{ACCESS_ID}`:: Su ID de acceso para la ubicación del almacenamiento [!DNL Amazon] S3.
* `{SECRET_KEY}`:: La clave secreta para la ubicación del almacenamiento [!DNL Amazon] S3.

**Respuesta**

Una respuesta correcta contiene el identificador único (`id`) de la conexión base. Almacene este valor como sea necesario en el paso siguiente para crear una conexión de destinatario.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Especificar la ubicación del almacenamiento y el formato de los datos

**Formato API**

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
    "baseConnection": "{BASE_CONNECTION_ID}",
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

* `{BASE_CONNECTION_ID}`:: Utilice el ID de conexión base que obtuvo en el paso anterior.
* `{CONNECTION_SPEC_ID}`:: Utilice la especificación de conexión que obtuvo en el paso [Obtener la lista de los destinos](#get-the-list-of-available-destinations)disponibles.
* `{BUCKETNAME}`:: Su bucket [!DNL Amazon] S3, donde CDP en tiempo real depositará la exportación de datos.
* `{FILEPATH}`:: La ruta en el directorio de bucket de [!DNL Amazon] S3 donde CDP en tiempo real depositará la exportación de datos.

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de destinatario recién creada al destino de marketing por correo electrónico. Almacene este valor tal como se requiere en pasos posteriores.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Crear un flujo de datos

![Pasos de destino, paso 4](/help/rtcdp/destinations/assets/flow-api-destinations-step4.png)

Con los ID obtenidos en los pasos anteriores, ahora puede crear un flujo de datos entre los datos [!DNL Experience Platform] y el destino en el que activará los datos. Considere este paso como la construcción de la canalización, a través de la cual los datos fluirán más adelante, entre [!DNL Experience Platform] y el destino deseado.

Para crear un flujo de datos, realice una solicitud de POST, como se muestra a continuación, mientras proporciona los valores que se mencionan a continuación dentro de la carga útil.

Realice la siguiente solicitud de POST para crear un flujo de datos.

**Formato API**

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

* `{FLOW_SPEC_ID}`:: Utilice el flujo para el destino de marketing por correo electrónico al que desea conectarse. Para obtener la especificación de flujo, realice una operación de GET en el `flowspecs` extremo. Consulte la documentación de Swagger aquí: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. En la respuesta, busque `upsTo` y copie el ID correspondiente del destino de marketing por correo electrónico al que desea conectarse. Por ejemplo, para Adobe Campaign, busque `upsToCampaign` y copie el `id` parámetro.
* `{SOURCE_CONNECTION_ID}`:: Utilice el ID de conexión de origen obtenido en el paso [Conectar con su Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`:: Utilice el ID de conexión de destinatario obtenido en el paso [Conectar con destino](#connect-to-email-marketing-destination)de marketing por correo electrónico.

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado y un `etag`. Anote ambos valores. como lo hará en el paso siguiente, para activar segmentos.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activar datos en el nuevo destino

![Pasos de destino, paso 5](/help/rtcdp/destinations/assets/flow-api-destinations-step5.png)

Después de crear todas las conexiones y el flujo de datos, ahora puede activar los datos de perfil en la plataforma de marketing por correo electrónico. En este paso, se selecciona qué segmentos y qué atributos de perfil se envían al destino y se pueden programar y enviar datos al destino.

Para activar segmentos en el nuevo destino, debe realizar una operación de PATCH JSON, similar a la que se muestra a continuación. Puede activar varios segmentos y atributos de perfil en una sola llamada. Para obtener más información sobre el PATCH JSON, consulte la especificación [](https://tools.ietf.org/html/rfc6902)RFC.

**Formato API**

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

* `{DATAFLOW_ID}`:: Utilice el flujo de datos obtenido en el paso anterior.
* `{ETAG}`:: Utilice la etiqueta que obtuvo en el paso anterior.
* `{SEGMENT_ID}`:: Proporcione el ID de segmento que desea exportar a este destino. Para recuperar los ID de segmento de los segmentos que desea activar, vaya a **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, seleccione la API **[!UICONTROL de servicio]** de segmentación en el menú de navegación de la izquierda y busque la `GET /segment/definitions` operación en Definiciones **[!UICONTROL de segmentos]**.
* `{PROFILE_ATTRIBUTE}`: Por ejemplo, `"person.lastName"`

**Respuesta**

Busque una respuesta 202 OK. No se devuelve ningún cuerpo de respuesta. Para validar que la solicitud era correcta, consulte el paso siguiente, Validar el flujo de datos.

## Validar el flujo de datos

![Pasos de destino, paso 6](/help/rtcdp/destinations/assets/flow-api-destinations-step6.png)

Como último paso del tutorial, debe validar que los segmentos y atributos de perfil se hayan asignado correctamente al flujo de datos.

Para validar esto, realice la siguiente solicitud de GET:

**Formato API**

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

* `{DATAFLOW_ID}`:: Utilice el flujo de datos del paso anterior.
* `{ETAG}`:: Utilice la etiqueta del paso anterior.

**Respuesta**

La respuesta devuelta debe incluir en el `transformations` parámetro los segmentos y los atributos de perfil que ha enviado en el paso anterior. A continuación se muestra un parámetro `transformations` de muestra en la respuesta:

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

Siguiendo este tutorial, ha conectado con éxito CDP en tiempo real a uno de los destinos de mercadotecnia de correo electrónico preferidos y ha configurado un flujo de datos para el destino correspondiente. Los datos salientes ahora se pueden utilizar en el destino para campañas por correo electrónico, publicidad de destino y muchos otros casos de uso. Consulte las páginas siguientes para obtener más información:

* [Información general sobre los destinos](../../rtcdp/destinations/destinations-overview.md)
* [Descripción general del catálogo de destinos](../../rtcdp/destinations/destinations-catalog.md)