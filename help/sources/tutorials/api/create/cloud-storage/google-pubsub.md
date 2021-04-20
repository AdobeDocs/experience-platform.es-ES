---
keywords: Experience Platform;inicio;temas populares;Google PubSub;google pubsub
solution: Experience Platform
title: Crear una conexión de Google PubSub Source mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Google PubSub mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL Google PubSub] mediante la API del servicio de flujo

>[!NOTE]
>
>El conector [!DNL Google PubSub] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial utiliza la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para guiarle por los pasos para conectar [!DNL Google PubSub] (en adelante denominada &quot;[!DNL PubSub]&quot;) a Adobe Experience Platform.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente una conexión de origen [!DNL PubSub] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL PubSub], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `projectId` | El ID de proyecto necesario para autenticarse [!DNL PubSub]. |
| `credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |

Para obtener más información sobre estos valores, consulte el siguiente documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication). Si utiliza la autenticación basada en cuentas de servicio, consulte la siguiente [guía de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para ver los pasos sobre cómo generar sus credenciales.

>[!TIP]
>
>Si utiliza la autenticación basada en cuentas de servicio, asegúrese de que ha concedido suficiente acceso de usuario a su cuenta de servicio y de que no hay espacios en blanco adicionales en el JSON, al copiar y pegar sus credenciales.

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cada cuenta [!DNL PubSub], ya que se puede utilizar para crear varios flujos de datos para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL PubSub], el ID del proveedor y el ID de la especificación de conexión deben proporcionarse como parte de la solicitud del POST. El ID del proveedor es `521eee4d-8cbe-4906-bb48-fb6bd4450033` y el ID de la especificación de conexión es `70116022-a743-464a-bbfe-e226a7f8210c`.

**Formato de API**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.projectId` | El ID de proyecto necesario para autenticarse [!DNL PubSub]. |
| `auth.params.credentials` | La credencial o clave necesaria para autenticarse [!DNL PubSub]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de la conexión [!DNL PubSub] recién creada. Este ID es necesario para explorar los datos del almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión [!DNL PubSub] utilizando la API [!DNL Flow Service] y ha adquirido su ID de conexión único. Puede utilizar este ID de conexión para [recopilar datos de flujo continuo mediante la API de servicio de flujo](../../collect/streaming.md).
