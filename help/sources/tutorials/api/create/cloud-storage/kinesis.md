---
keywords: Experience Platform;home;popular topics;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creación de un conector Kinesis de Amazon mediante la API de servicio de flujo
topic: overview
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar a un Experience Platform a una cuenta de Amazon Kinesis.
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 2%

---


# Creación de un [!DNL Amazon Kinesis] conector mediante la API de servicio de flujo

>[!NOTE]
>
>El [!DNL Amazon Kineses] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la [!DNL Flow Service] API para guiarle por los pasos para conectarse [!DNL Experience Platform] a una [!DNL Amazon Kinesis] cuenta.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a una [!DNL Amazon Kinesis] cuenta mediante la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse con su [!DNL Amazon Kinesis] cuenta, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | ID de la clave de acceso de su [!DNL Kinesis] cuenta. |
| `secretKey` | Clave de acceso secreta de su [!DNL Kinesis] cuenta. |
| `region` |  | Región de su [!DNL Kinesis] cuenta. |
| `connectionSpec.id` | ID de especificación de [!DNL Kinesis] conexión: `86043421-563b-46ec-8e6c-e23184711bf6` |

Para obtener más información sobre estos valores, consulte [este documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)de Kinesis.

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

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por [!DNL Amazon Kinesis] cuenta, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "auth": {
            "specName": "Basic Authentication for Kinesis",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretKey": "secretKey"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.accessKeyId` | ID de la clave de acceso de su [!DNL Kinesis] cuenta. |
| `auth.params.secretKey` | Clave de acceso secreta de su [!DNL Kinesis] cuenta. |
| `auth.params.region` | Región de su [!DNL Kinesis] cuenta. |
| `connectionSpec.id` | ID de especificación de [!DNL Kinesis] conexión: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos del almacenamiento de nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una [!DNL Amazon Kinesis] conexión mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API](../../explore/cloud-storage.md)de servicio de flujo.