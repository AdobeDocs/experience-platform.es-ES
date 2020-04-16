---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector Gen2 de Almacenamiento de Azure Data Lake mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 065076aee83990bcad0110f0d7704a60fac400c6

---


# Creación de un conector Gen2 de Almacenamiento de Azure Data Lake mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la plataforma de experiencia con el Almacenamiento de Azure Data Lake Gen2 (en adelante, &quot;ADLS Gen2&quot;).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente un conector de origen ADLS Gen2 mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte a ADLS Gen2, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | Dirección URL. |
| `servicePrincipalId` | El ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene la aplicación. |

Para obtener más información sobre estos valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

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

Antes de conectar Platform a ADLS Gen2, debe comprobar que existen especificaciones de conexión para ADLS Gen2. Si no existen especificaciones de conexión, no se puede establecer una conexión.

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión de ADLS Gen2 realizando una solicitud GET y utilizando parámetros de consulta.

**Formato API**

El envío de una solicitud GET sin parámetros de consulta devolverá especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=name=="adls-gen2"` para obtener información específica sobre ADLS Gen2.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="adls-gen2"
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión para ADLS Gen2.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="adls-gen2"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las especificaciones de conexión para ADLS Gen2, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión base.

```json
{
    "items": [
        {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "name": "adls-gen2",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for adls-gen2",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "properties": {
                            "url": {
                                "type": "string",
                                "description": "Endpoint for Azure Data Lake Storage Gen2."
                            },
                            "servicePrincipalId": {
                                "type": "string",
                                "description": "Service Principal Id to connect to ADLSGen2."
                            },
                            "servicePrincipalKey": {
                                "type": "string",
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "format": "password"
                            },
                            "tenant": {
                                "type": "string",
                                "description": "Tenant information(domain name or tenant ID)."
                            }
                        },
                        "required": [
                            "url",
                            "servicePrincipalId",
                            "servicePrincipalKey",
                            "tenant"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creación de una conexión base

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión de base por cuenta de ADLS Gen2, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

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
        "name": "adls-gen2",
        "description": "base connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.url` | Extremo de URL de la cuenta de ADLS Gen2. |
| `auth.params.servicePrincipalId` | ID principal de servicio de su cuenta ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Clave principal de servicio de su cuenta ADLS Gen2. |
| `auth.params.tenant` | La información del inquilino de su cuenta de ADLS Gen2. |
| `connectionSpec.id` | Especificación de conexión `id` de la cuenta de ADLS Gen2 recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el almacenamiento de nube en el próximo paso.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión ADLS Gen2 mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API](../../explore/cloud-storage.md) de servicio de flujo o [ingesta de datos de parqué mediante la API](../../cloud-storage-parquet.md)de servicio de flujo.
