---
title: Creación de una conexión base de Microsoft Dynamics mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Platform a una cuenta de Microsoft Dynamics mediante la API de Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: bda26fa4ecf4f54cb36ffbedf6a9aa13faf7a09d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 5%

---

# Conectar [!DNL Microsoft Dynamics] a Experience Platform mediante la API [!DNL Flow Service]

Lea esta guía para saber cómo conectar su origen de [!DNL Microsoft Dynamics] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectar correctamente Platform a una cuenta de Dynamics mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación básica]

| Credencial | Descripción |
| --- | --- |
| `serviceUri` | La URL de servicio de su instancia [!DNL Dynamics]. |
| `username` | El nombre de usuario de su cuenta de usuario [!DNL Dynamics]. |
| `password` | Contraseña de su cuenta de [!DNL Dynamics]. |

>[!TAB Autenticación de clave y principal de servicio]

| Credencial | Descripción |
| --- | --- |
| `servicePrincipalId` | Identificador de cliente de su cuenta de [!DNL Dynamics]. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |

>[!ENDTABS]

Para obtener más información sobre cómo empezar, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Crear una conexión base

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Dynamics]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Dynamics] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para crear una conexión base de [!DNL Dynamics] con autenticación básica, realice una petición POST a la API [!DNL Flow Service] y proporcione los valores de `serviceUri`, `username` y `password` de la conexión.

**Solicitud**

La siguiente solicitud crea una conexión base para un origen de [!DNL Dynamics] mediante autenticación básica.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de servicio asociado con la instancia [!DNL Dynamics]. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Dynamics]. |
| `auth.params.password` | La contraseña asociada a su cuenta de [!DNL Dynamics]. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador único (`id`).

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Autenticación basada en clave principal de servicio]

Para crear una conexión base [!DNL Dynamics] mediante la autenticación basada en claves principales de servicio, realice una petición POST a la API [!DNL Flow Service] y proporcione los valores de `serviceUri`, `servicePrincipalId` y `servicePrincipalKey` de la conexión.

**Solicitud**

La siguiente solicitud crea una conexión base para un origen de [!DNL Dynamics] mediante la autenticación básica basada en clave principal de servicio.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de servicio asociado con la instancia [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | Identificador de cliente de su cuenta de [!DNL Dynamics]. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `auth.params.servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`).

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Exploración de las tablas de datos

Para explorar las tablas de datos de [!DNL Dynamics], realice una petición GET al extremo `/connections/{BASE_CONNECTION_ID}/explore` y proporcione el identificador de conexión base como parte de los parámetros de la consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base. Utilice este ID para explorar el contenido y la estructura de su origen. |

**Solicitud**

La siguiente solicitud recupera la lista de tablas y vistas disponibles para un origen de [!DNL Dynamics] con el identificador de conexión base: `dd668808-25da-493f-8782-f3433b976d1e`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el directorio de tablas y vistas [!DNL Dynamics] en el nivel raíz.

+++Seleccione para ver el ejemplo de respuesta

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++


## Inspeccionar la estructura de una tabla

Para inspeccionar la estructura de una tabla específica, realice una petición GET a `/connections/{BASE_CONNECTION_ID}/explore` y proporcione la ruta de acceso a la tabla específica como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Parámetro de consulta | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base. Utilice este ID para explorar el contenido y la estructura de su origen. |
| `{TABLE_PATH}` | La ruta a la tabla concreta que desea explorar. |

**Solicitud**

La siguiente solicitud recupera la estructura y el contenido de una tabla [!DNL Dynamics] con la ruta de acceso `workflowdependency`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el contenido de la ruta `workflowdependency`.

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Inspeccionar la estructura de una vista

En [!DNL Dynamics], una vista hace referencia a las columnas que se van a mostrar, al ancho de cada columna, al sistema predeterminado en el que se ordena una lista de registros y a los filtros predeterminados aplicados para restringir qué registros aparecerán en la lista.

Para inspeccionar la estructura de una vista, realice una petición GET a `/connections/{BASE_CONNECTION_ID}/explore` y especifique la ruta de la vista en los parámetros de la consulta. Además, debe especificar `objectType` como `view`.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Parámetro de consulta | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base. Utilice este ID para explorar el contenido y la estructura de su origen. |
| `{VIEW_PATH}` | La ruta a la vista que desea inspeccionar. |

**Solicitud**

La siguiente solicitud recupera `accountView1`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve la estructura de `accountView1`.

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Vista previa del tipo de entidad

Para obtener una vista previa del contenido de una vista, realice una petición GET a `/connections/{BASE_CONNECTION_ID}/explore` e incluya la ruta de acceso de la vista y `preview=true` en los parámetros de la consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Parámetro de consulta | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base. Utilice este ID para explorar el contenido y la estructura de su origen. |
| `{VIEW_PATH}` | La ruta a la vista que desea inspeccionar. |


**Solicitud**

La siguiente solicitud obtiene una vista previa del contenido de `accountView1`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el contenido de `accountView1`.

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Crear una conexión de origen para la vista de ingesta

Para crear una conexión de origen e introducir una vista, realice una petición POST al extremo `/sourceConnections`, proporcione el nombre de la tabla y especifique `entityType` como `view` en el cuerpo de la solicitud.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen [!DNL Dynamics] e introduce vistas.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Respuesta**

Una respuesta correcta devuelve el ID de la conexión de origen recién generado y su etiqueta correspondiente.

+++Seleccione para ver el ejemplo de respuesta

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Microsoft Dynamics] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos de CRM a Platform mediante la API  [!DNL Flow Service] ](../../collect/crm.md)
