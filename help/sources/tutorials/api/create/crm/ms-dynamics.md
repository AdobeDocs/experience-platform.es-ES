---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Creación de un conector de Microsoft Dynamics mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: En este tutorial se utiliza la API de servicio de flujo para ayudarle a seguir los pasos necesarios para conectar la plataforma a una cuenta de Microsoft Dynamics (en adelante denominada "Dynamics") para recopilar datos de CRM.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# Creación de un [!DNL Microsoft Dynamics] conector mediante la [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la [!DNL Flow Service] API para guiarle por los pasos necesarios para conectarse [!DNL Platform] a una cuenta [!DNL Microsoft Dynamics] (en adelante denominada &quot;Dynamics&quot;) para recopilar datos de CRM.

Si prefiere utilizar la interfaz de usuario en [!DNL Experience Platform], el tutorial [de interfaz de usuario del conector de origen de](../../../ui/create/crm/dynamics.md) Dynamics proporciona instrucciones paso a paso para realizar acciones similares.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): E[!DNL xperience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Platform] a una cuenta de Dynamics mediante la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse a [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La dirección URL del servicio de su [!DNL Dynamics] instancia. |
| `username` | El nombre de usuario de su cuenta [!DNL Dynamics] de usuario. |
| `password` | La contraseña de su [!DNL Dynamics] cuenta. |

Para obtener más información sobre cómo empezar, visite [este documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)de Dynamics.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Buscar especificaciones de conexión

Antes de conectarse [!DNL Platform] a una [!DNL Dynamics] cuenta, debe comprobar que existen especificaciones de conexión para [!DNL Dynamics]. Si no existen especificaciones de conexión, no se puede establecer una conexión.

Cada fuente disponible tiene su propio conjunto exclusivo de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión [!DNL Dynamics] mediante una solicitud de GET y parámetros de consulta.

**Formato API**

El envío de una solicitud de GET sin parámetros de consulta devolverá las especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=name=="dynamics-online"` para obtener información específica para [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión para [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las especificaciones de conexión para [!DNL Dynamics], incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión base.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creación de una conexión base

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión base por [!DNL Dynamics] cuenta, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

Realice la siguiente solicitud de POST para crear una conexión base.

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
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
| `auth.params.serviceUri` | El URI de servicio asociado a su [!DNL Dynamics] instancia. |
| `auth.params.username` | El nombre de usuario asociado a su [!DNL Dynamics] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Dynamics] cuenta. |
| `connectionSpec.id` | La especificación `id` de conexión de su [!DNL Dynamics] cuenta recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta contiene el identificador único (`id`) de la conexión base. Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base para su [!DNL Dynamics] cuenta mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión base en el siguiente tutorial a medida que aprenda a [explorar sistemas CRM mediante la API](../../explore/crm.md)de servicio de flujo.