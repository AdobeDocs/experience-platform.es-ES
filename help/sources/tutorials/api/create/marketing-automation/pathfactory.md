---
title: Creación de una conexión base de PathFactory mediante la API de Flow Service
description: Obtenga información sobre cómo autenticar su cuenta de PathFactory con un Experience Platform mediante la API de Flow Service.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Crear una conexión base [!DNL PathFactory] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Lea este documento para aprender a crear una conexión base para [!DNL PathFactory] mediante la [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL PathFactory] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias {#gather-credentials}

Para acceder a su cuenta de PathFactory en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Nombre de usuario | Su nombre de usuario de la cuenta [!DNL PathFactory]. Esto es esencial para identificar su cuenta en el sistema. |
| Contraseña | La contraseña asociada a su cuenta de [!DNL PathFactory]. Asegúrese de que se mantenga seguro para evitar el acceso no autorizado. |
| Dominio | El dominio asociado con su cuenta de [!DNL PathFactory]. Esto generalmente hace referencia al identificador único dentro de la dirección URL [!DNL PathFactory]. |
| Token de acceso | Un token único usado para la autenticación de API a fin de asegurar la comunicación segura entre sus sistemas y [!DNL PathFactory]. |
| Extremos de API | Puntos finales específicos de API para acceder a los datos: visitantes, sesiones y vistas de páginas. Cada extremo corresponde a diferentes conjuntos de datos que puede recuperar. **Nota:** Están predefinidos por [!DNL PathFactory] y son específicos de los datos a los que desea tener acceso: <ul><li>**Extremo de visitantes**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Punto final de sesiones**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Extremo de vistas de página**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Para obtener más información sobre cómo proteger y usar sus credenciales, y cómo obtener y actualizar su token de acceso, visite el [[!DNL PathFactory] Centro de soporte técnico](https://support.pathfactory.com/categories/adobe/). Este recurso ofrece guías completas sobre la administración de las credenciales y la garantía de una integración de API eficaz y segura.

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL PathFactory] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientId` | Identificador de cliente asociado con la aplicación [!DNL PathFactory]. |
| `auth.params.clientSecret` | Secreto de cliente asociado a la aplicación [!DNL PathFactory]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL PathFactory]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL PathFactory] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Platform mediante la API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
