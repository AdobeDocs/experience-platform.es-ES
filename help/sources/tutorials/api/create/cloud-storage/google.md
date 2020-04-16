---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de Almacenamiento de Google Cloud mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 96be7084d5d2efb86b7bba27f1a92bd9c0055fba

---


# Creación de un conector de Almacenamiento de Google Cloud mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la plataforma de experiencia a una cuenta de Almacenamiento de Google Cloud.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a una cuenta de Almacenamiento de Google Cloud mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con su cuenta de Almacenamiento de Google Cloud, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de la clave de acceso de su cuenta de Almacenamiento de Google Cloud. |
| `secretAccessKey` | La clave de acceso secreto de su cuenta de Almacenamiento de Google Cloud. |

Para obtener información sobre cómo empezar, visite [este documento](https://cloud.google.com/docs/authentication)de Google Cloud.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Buscar especificaciones de conexión

Antes de conectar Platform a un Almacenamiento de Google Cloud, debe comprobar que existen especificaciones de conexión para el Almacenamiento de Google Cloud. Si no existen especificaciones de conexión, no se puede establecer una conexión.

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión para el Almacenamiento de Google Cloud realizando una solicitud GET y utilizando parámetros de consulta.

**Formato API**

El envío de una solicitud GET sin parámetros de consulta devolverá especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=name=="google-cloud"` para obtener información específica sobre Google Cloud Almacenamiento.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name==google-cloud
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión de Google Cloud Almacenamiento.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-cloud"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las especificaciones de conexión para el Almacenamiento de Google Cloud, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión base.

```json
{
    "items": [
        {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "name": "google-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-cloud",
                    "type": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to google-cloud storage connector.",
                        "properties": {
                            "accessKeyId": {
                                "type": "string",
                                "description": "Access Key Id for the user account"
                            },
                            "secretAccessKey": {
                                "type": "string",
                                "description": "Secret Access Key for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creación de una conexión base

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión de base por cuenta de Almacenamiento de Google Cloud, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage base connection",
        "description": "Base connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.accessKeyId` | ID de clave de acceso asociado a su cuenta de Almacenamiento de Google Cloud. |
| `auth.params.secretAccessKey` | La clave de acceso secreto asociada a su cuenta de Almacenamiento de Google Cloud. |
| `connectionSpec.id` | Especificación de conexión `id` de la cuenta de Almacenamiento de Google Cloud recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos del almacenamiento de nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de Almacenamiento de Google Cloud mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API](../../explore/cloud-storage.md) de servicio de flujo o [ingesta de datos de parqué mediante la API](../../cloud-storage-parquet.md)de servicio de flujo.