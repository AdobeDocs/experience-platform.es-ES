---
keywords: Experience Platform;inicio;temas populares;Nube de servicios de Oracle;Nube de servicios de oracle
title: Creación de una conexión de Oracle Service Cloud Source mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a la nube de servicios de Oracle mediante la API de Flow Service.
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---

# Crear una conexión de origen de nube de Oracle Service mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Oracle Service Cloud] quedará obsoleto a finales de mayo de 2025. Como alternativa, puede utilizar el origen [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para Oracle Service Cloud mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a Oracle Service Cloud mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con la nube de Oracle Service, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La URL de host de la instancia de Oracle Service Cloud. |
| `username` | El nombre de usuario de su cuenta de usuario de Oracle Service Cloud. |
| `password` | La contraseña de su cuenta de Oracle Service Cloud. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El identificador de especificación de conexión para la nube de Oracle Service es: `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

Para obtener más información sobre cómo autenticar su cuenta de Oracle Service Cloud, consulte la [[!DNL Oracle] guía de autenticación](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione al mismo tiempo las credenciales de autenticación de Oracle Service Cloud como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para Oracle Service Cloud:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.host` | La URL de host de la instancia de Oracle Service Cloud. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de Oracle Service Cloud. |
| `auth.params.password` | La contraseña asociada a su cuenta de Oracle Service Cloud. |
| `connectionSpec.id` | Id. de especificación de conexión de nube de servicio de Oracle: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión base de Oracle Service Cloud mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de éxito de los clientes a Platform mediante la API  [!DNL Flow Service] ](../../collect/customer-success.md)
