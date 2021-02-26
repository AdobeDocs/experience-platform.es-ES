---
keywords: Experience Platform;inicio;temas populares;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creación de una conexión Amazon Kinesis Source mediante la API de servicio de flujo
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta Kinesis de Amazon mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: 4f3d88e1241fd19dc9963f34dd60086ae2135557
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL Amazon Kinesis] mediante la API de servicio de flujo

>[!NOTE]
>
>El conector [!DNL Amazon Kineses] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a una cuenta [!DNL Amazon Kinesis].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a una cuenta [!DNL Amazon Kinesis] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta [!DNL Amazon Kinesis], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de la clave de acceso de su cuenta [!DNL Kinesis]. |
| `secretKey` | La clave de acceso secreto de su cuenta [!DNL Kinesis]. |
| `region` | Región de su cuenta [!DNL Kinesis]. |
| `connectionSpec.id` | El identificador de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

Para obtener más información sobre estos valores, consulte [este documento de Kinesis](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL Amazon Kinesis], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

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
            "specName": "Aws Kinesis authentication credentials",
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
| `auth.params.accessKeyId` | El ID de la clave de acceso de su cuenta [!DNL Kinesis]. |
| `auth.params.secretKey` | La clave de acceso secreto de su cuenta [!DNL Kinesis]. |
| `auth.params.region` | Región de su cuenta [!DNL Kinesis]. |
| `connectionSpec.id` | El identificador de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos del almacenamiento de nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Amazon Kinesis] mediante API y se obtuvo un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [recopilar datos de flujo mediante la API de servicio de flujo](../../collect/streaming.md).