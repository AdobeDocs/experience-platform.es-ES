---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Storage Gen2;almacenamiento azure data lake;Azure
solution: Experience Platform
title: Crear una conexión de origen de Azure Data Lake Storage Gen2 mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Azure Data Lake Storage Gen2 mediante la API de servicio de flujo.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure] Data Lake Storage Gen2 mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a [!DNL Azure] Data Lake Storage Gen2 (en adelante, &quot;ADLS Gen2&quot;).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente una conexión de origen ADLS Gen2 mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a ADLS Gen2, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La dirección URL. |
| `servicePrincipalId` | El ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene su aplicación. |

Para obtener más información sobre estos valores, consulte [este documento de ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de ADLS Gen2, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión ADLS-Gen2, su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para ADLS-Gen2 es `0ed90a81-07f4-4586-8190-b40eccef1c5a`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
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
| `auth.params.url` | El extremo URL de su cuenta de ADLS Gen2. |
| `auth.params.servicePrincipalId` | El ID de principal de servicio de su cuenta de ADLS Gen2. |
| `auth.params.servicePrincipalKey` | La clave principal de servicio de su cuenta ADLS Gen2. |
| `auth.params.tenant` | La información del inquilino de su cuenta de ADLS Gen2. |
| `connectionSpec.id` | El ID de especificación de conexión ADLS Gen2: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el almacenamiento en la nube en el siguiente paso.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión ADLS Gen2 mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar las tiendas en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md) o [incorporar datos de parqué mediante la API de servicio de flujo](../../cloud-storage-parquet.md).
