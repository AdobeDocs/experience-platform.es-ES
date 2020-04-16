---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector SFTP mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: a038abcdc411b638f41b94dea0140518c12f5600

---


# Creación de un conector SFTP mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la plataforma de experiencia a un servidor SFTP (Protocolo seguro de transferencia de archivos).

Si prefiere utilizar la interfaz de usuario en la plataforma de experiencia, el tutorial [de la](../../../ui/create/cloud-storage/ftp-sftp.md) interfaz de usuario proporciona instrucciones paso a paso para realizar acciones similares.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a un servidor SFTP mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte a SFTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con el servidor SFTP. |
| `username` | El nombre de usuario con acceso al servidor SFTP. |
| `password` | La contraseña del servidor SFTP. |

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

Para crear una conexión SFTP, debe existir un conjunto de especificaciones de conexión SFTP en el servicio de flujo. El primer paso para conectar Plataforma a SFTP es recuperar estas especificaciones.

**Formato API**

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión para SFTP realizando una solicitud GET y utilizando parámetros de consulta.

El envío de una solicitud GET sin parámetros de consulta devolverá especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=name=="sftp"` para obtener información específica para SFTP.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sftp"
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión de un servidor SFTP.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sftp"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la especificación de conexión del servidor SFTP, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión base.

```json
{
    "items": [
        {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "name": "sftp",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for sftp",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to sftp",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specify the name or IP address of the SFTP server."
                            },
                            "userName": {
                                "type": "string",
                                "description": "Specify the user who has access to the SFTP server."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the password for the user (userName).",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userName",
                            "password"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creación de una conexión base

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión de base por cuenta SFTP, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

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
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.host` | El nombre de host del servidor SFTP. |
| `auth.params.username` | El nombre de usuario asociado al servidor SFTP. |
| `auth.params.password` | La contraseña asociada al servidor SFTP. |
| `connectionSpec.id` | Especificación `id` de conexión del servidor SFTP recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión SFTP mediante la API de servicio de flujo y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API](../../explore/cloud-storage.md) de servicio de flujo o [ingesta de datos de parqué mediante la API](../../cloud-storage-parquet.md)de servicio de flujo.
