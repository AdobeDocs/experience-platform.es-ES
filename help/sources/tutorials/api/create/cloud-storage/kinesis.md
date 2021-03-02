---
keywords: Experience Platform;inicio;temas populares;Kinesis;kinesis;Amazon Kinesis;amazonía cinesis
solution: Experience Platform
title: Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Amazon Kinesis mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: ed14fe464a4dc82f54902c8dc92fe00bc2a5381e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 2%

---


# Creación de una conexión de origen [!DNL Amazon Kinesis] mediante la API de servicio de flujo

>[!NOTE]
>
>El conector [!DNL Amazon Kineses] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a una cuenta [!DNL Amazon Kinesis].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a una cuenta [!DNL Amazon Kinesis] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta [!DNL Amazon Kinesis], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de clave de acceso para su cuenta [!DNL Kinesis]. |
| `secretKey` | La clave de acceso secreta para su cuenta [!DNL Kinesis]. |
| `region` | Región de la cuenta [!DNL Kinesis]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

Para obtener más información sobre estos valores, consulte [este documento de Kinesis](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cada cuenta [!DNL Amazon Kinesis], ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

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
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region: "{REGION}
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
| `auth.params.accessKeyId` | El ID de clave de acceso para su cuenta [!DNL Kinesis]. |
| `auth.params.secretKey` | La clave de acceso secreta para su cuenta [!DNL Kinesis]. |
| `auth.params.region` | Región de la cuenta [!DNL Kinesis]. Para obtener más información sobre las regiones, consulte el documento [IP address allow list](../../../../ip-address-allow-list.md) |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos del almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión [!DNL Amazon Kinesis] mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [recopilar datos de flujo continuo mediante la API de servicio de flujo](../../collect/streaming.md).