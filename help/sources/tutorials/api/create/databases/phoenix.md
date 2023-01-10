---
keywords: Experience Platform;inicio;temas populares;Phoenix;phoenix
solution: Experience Platform
title: Creación de una conexión base de Phoenix mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo conectar una base de datos de Phoenix a Adobe Experience Platform mediante la API de servicio de flujo.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Cree un [!DNL Phoenix] conexión base utilizando [!DNL Flow Service] API

>[!NOTE]
>
>La variable [!DNL Phoenix] El conector está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la variable [!DNL Flow Service] API para guiarle por los pasos para conectar un [!DNL Phoenix] a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Phoenix] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Phoenix], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host de la variable [!DNL Phoenix] servidor. |
| `username` | El nombre de usuario que utiliza para acceder a [!DNL Phoenix] Servidor. |
| `password` | La contraseña correspondiente al usuario. |
| `port` | El puerto TCP en el que [!DNL Phoenix] server utiliza para detectar conexiones de cliente. Si se conecta a [!DNL Azure] HDInsights, especifique el puerto como 443. |
| `httpPath` | La URL parcial correspondiente a la variable [!DNL Phoenix] servidor. Especifique /basephoenix0 si usa [!DNL Azure] Clúster de HDInsights. |
| `enableSsl` | Un valor booleano. Especifica si las conexiones al servidor se cifran mediante SSL. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Phoenix] es: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obtener más información sobre cómo empezar, consulte [este documento de Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Phoenix] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Phoenix]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | El host de la variable [!DNL Phoenix] servidor. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Phoenix] conexión. |
| `auth.params.password` | La contraseña asociada a su [!DNL Phoenix] conexión. |
| `auth.params.port` | El puerto TCP para su [!DNL Phoenix] conexión. |
| `auth.params.httpPath` | La ruta http parcial para su [!DNL Phoenix] conexión. |
| `auth.params.enableSsl` | El valor booleano que especifica si las conexiones al servidor se cifran con SSL. |
| `connectionSpec.id` | La variable [!DNL Phoenix] id. de especificación de conexión: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Phoenix] conexión base utilizando [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante el [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante el [!DNL Flow Service] API](../../collect/database-nosql.md)
