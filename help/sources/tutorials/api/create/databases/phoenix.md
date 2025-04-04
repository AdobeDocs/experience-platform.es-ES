---
title: Creación de una conexión base de Phoenix mediante la API de Flow Service
description: Aprenda a conectar una base de datos de Phoenix a Adobe Experience Platform mediante la API de Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Crear una conexión base [!DNL Phoenix] mediante la API [!DNL Flow Service]

>[!WARNING]
>
>El origen [!DNL Phoenix] quedará obsoleto a finales de junio de 2025.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial proporciona pasos sobre cómo crear una conexión base y conectar su cuenta de [!DNL Phoenix] a Adobe Experience Platform mediante la API [!DNL Flow Service].

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Phoenix] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Debe proporcionar las siguientes credenciales de autenticación para conectar su cuenta de [!DNL Phoenix] a Experience Platform.

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Dirección IP o nombre de host del servidor [!DNL Phoenix]. |
| `username` | El nombre de usuario que utiliza para obtener acceso al servidor [!DNL Phoenix]. |
| `password` | La contraseña correspondiente al usuario. |
| `port` | El puerto TCP que utiliza el servidor [!DNL Phoenix] para detectar conexiones de cliente. Si se está conectando a [!DNL Azure HDInsights], especifique el puerto como 443. Si no se proporciona este parámetro, el valor predeterminado es 8765. |
| `httpPath` | La dirección URL parcial correspondiente al servidor [!DNL Phoenix]. Especifique /hbasephoenix0 si utiliza [!DNL Azure] clúster de HDInsights. |
| `enableSsl` | Un valor booleano. Especifica si las conexiones al servidor se cifran con SSL. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Phoenix] es: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obtener más información sobre cómo empezar, consulte [este documento de Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear una conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Phoenix] en el cuerpo de la solicitud.

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
| `auth.params.host` | Host del servidor [!DNL Phoenix]. |
| `auth.params.username` | El nombre de usuario asociado con su conexión [!DNL Phoenix]. |
| `auth.params.password` | La contraseña asociada con su conexión [!DNL Phoenix]. |
| `auth.params.port` | El puerto TCP para su conexión [!DNL Phoenix]. |
| `auth.params.httpPath` | Ruta http parcial para su conexión [!DNL Phoenix]. |
| `auth.params.enableSsl` | Valor booleano que especifica si las conexiones con el servidor se cifran mediante SSL. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Phoenix]: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Phoenix] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
