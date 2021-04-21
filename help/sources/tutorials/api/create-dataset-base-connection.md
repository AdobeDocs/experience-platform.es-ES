---
keywords: Experience Platform;inicio;temas populares;servicio de flujo de conexión de conjuntos de datos;servicio de flujo;conexión de servicio de flujo
solution: Experience Platform
title: Creación de una conexión base de conjuntos de datos de Adobe Experience Platform mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Aprenda a utilizar la API de servicio de flujo para crear una conexión de base de datos a Adobe Experience Platform.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# Crear una conexión de base de datos [!DNL Experience Platform] utilizando la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Para conectar datos de un origen de terceros a [!DNL Platform], primero debe establecerse una conexión de base de datos.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para crear una conexión de base de datos.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Guía](../../../xdm/api/getting-started.md) para desarrolladores de Schema Registry: Incluye información importante que debe conocer para realizar correctamente llamadas a la API del Registro de esquemas. Esto incluye su `{TENANT_ID}`, el concepto de &quot;contenedores&quot; y los encabezados requeridos para realizar solicitudes (con especial atención al encabezado Accept y sus posibles valores).
* [Servicio de catálogo](../../../catalog/home.md): Catálogo es el sistema de registro para la ubicación y linaje de datos dentro de  [!DNL Experience Platform].
* [Ingesta por lotes](../../../ingestion/batch-ingestion/overview.md): La API de ingesta por lotes permite introducir datos en el Experience Platform como archivos por lotes.
* [Simuladores para pruebas](../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a Data Lake mediante la API [!DNL Flow Service].

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Buscar especificaciones de conexión

El primer paso para crear una conexión de base de datos es recuperar un conjunto de especificaciones de conexión desde [!DNL Flow Service].

**Formato de API**

Cada fuente disponible tiene su propio conjunto único de especificaciones de conexión para describir propiedades del conector, como los requisitos de autenticación. Puede consultar las especificaciones de conexión para una conexión base de datos realizando una solicitud de GET y utilizando parámetros de consulta.

Al enviar una solicitud de GET sin parámetros de consulta, se devolverán especificaciones de conexión para todos los orígenes disponibles. Puede incluir la consulta `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` para obtener información para la conexión base de datos.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de conexión para una conexión base de datos.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las especificaciones de conexión y el identificador único (`id`) necesario para crear una conexión base.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Crear una conexión de base de datos

Una conexión base especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión base de conjuntos de datos, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

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
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `connectionSpec.id` | La especificación de conexión `id` recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario para crear una conexión de destino e introducir datos desde un conector de origen de terceros.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de base de datos mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar esta conexión base para crear una conexión de destino. Los siguientes tutoriales explican los pasos para crear una conexión de destino, según la categoría de conector de origen que utilice:

* [Almacenamiento en la nube](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Éxito del cliente](./collect/customer-success.md)
* [Database](./collect/database-nosql.md)
