---
keywords: Experience Platform;inicio;temas populares; Protocolo de transferencia de archivos; protocolo de transferencia de archivos
solution: Experience Platform
title: Creación de una conexión base FTP mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor FTP (Protocolo de transferencia de archivos) mediante la API de servicio de flujo.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Creación de una conexión base FTP mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector FTP está en versión beta. Las funciones y la documentación están sujetas a cambios. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL FTP] (Protocolo de transferencia de archivos) mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a un servidor [!DNL FTP] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL FTP], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su servidor [!DNL FTP]. |
| `username` | El nombre de usuario con acceso a su servidor [!DNL FTP]. |
| `password` | La contraseña de su servidor [!DNL FTP]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL FTP] es: `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL FTP] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL FTP]:

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
| `connectionSpec.id` | El ID de especificación de conexión del servidor FTP: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor FTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión FTP utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID de conexión para [explorar las tiendas en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md) o [incorporar datos de parqué mediante la API de servicio de flujo](../../cloud-storage-parquet.md).
