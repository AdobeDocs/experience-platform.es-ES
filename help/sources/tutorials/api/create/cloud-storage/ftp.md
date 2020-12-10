---
keywords: Experience Platform;home;popular topics; File Transfer Protocol; file transfer protocol
solution: Experience Platform
title: Creación de un conector FTP mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar al Experience Platform a un servidor FTP (Protocolo de transferencia de archivos).
translation-type: tm+mt
source-git-commit: 807b3110606daa6b8d42d2f9048668f7c121c8f4
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---


# Creación de un conector FTP mediante la [!DNL Flow Service] API

>[!NOTE]
>
>El conector FTP está en versión beta. Las funciones y la documentación están sujetas a cambios. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Este tutorial utiliza la [!DNL Flow Service] API para guiarle por los pasos para conectarse [!DNL Experience Platform] a un servidor FTP (Protocolo de transferencia de archivos).

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un servidor FTP mediante la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse a FTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con el servidor FTP. |
| `username` | El nombre de usuario con acceso al servidor FTP. |
| `password` | La contraseña del servidor FTP. |

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de FTP, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

### Creación de una conexión FTP mediante autenticación básica

Para crear una conexión FTP mediante autenticación básica, realice una solicitud de POST a la [!DNL Flow Service] API y proporcione los valores de la conexión `host`, `userName`y `password`.

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
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.host` | El nombre de host del servidor FTP. |
| `auth.params.username` | El nombre de usuario asociado al servidor FTP. |
| `auth.params.password` | La contraseña asociada al servidor FTP. |
| `connectionSpec.id` | ID de especificación de conexión del servidor FTP: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor FTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión FTP con la [!DNL Flow Service] API y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API](../../explore/cloud-storage.md) de servicio de flujo o [ingesta de datos de parqué mediante la API](../../cloud-storage-parquet.md)de servicio de flujo.
