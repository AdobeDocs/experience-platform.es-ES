---
keywords: Experience Platform;home;popular topics;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Creación de un conector Amazon Redshift mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar Experience Platform a Amazon Redshift (en adelante, "Redshift").
translation-type: tm+mt
source-git-commit: 36620a229fc8e6e3fa4545bfc775a49bc89935bb
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---


# Cree un conector [!DNL Amazon Redshift] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Amazon Redshift] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a [!DNL Amazon Redshift] (en adelante denominada &quot;[!DNL Redshift]&quot;).

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse con éxito a [!DNL Redshift] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Redshift], debe proporcionar las siguientes propiedades de conexión:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `server` | El servidor asociado a su cuenta [!DNL Redshift]. |
| `username` | El nombre de usuario asociado a su cuenta [!DNL Redshift]. |
| `password` | La contraseña asociada a su cuenta [!DNL Redshift]. |
| `database` | La base de datos [!DNL Redshift] a la que está accediendo. |

Para obtener más información sobre cómo empezar, consulte [este documento Redshift](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](../../../../../tutorials/authentication.md). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL Redshift], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

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
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `auth.params.server` | Su servidor [!DNL Redshift]. |
| `auth.params.database` | Base de datos asociada a su cuenta [!DNL Redshift]. |
| `auth.params.password` | La contraseña asociada a su cuenta [!DNL Redshift]. |
| `auth.params.username` | El nombre de usuario asociado a su cuenta [!DNL Redshift]. |
| `connectionSpec.id` | La especificación de conexión `id` de su cuenta [!DNL Redshift] recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Redshift] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este identificador de conexión en el siguiente tutorial cuando aprenda a [explorar bases de datos o sistemas NoSQL mediante la API de servicio de flujo](../../explore/database-nosql.md).
