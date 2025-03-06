---
title: Conecte AWS Redshift A Experience Platform Mediante La API De Flow Service
description: Aprenda a conectar Adobe Experience Platform a AWS Redshift mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---

# Conectar [!DNL AWS Redshift] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL AWS Redshift] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea esta guía para saber cómo conectar su cuenta de origen de [!DNL AWS Redshift] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL AWS Redshift] a Experience Platform en Azure {#azure}

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL AWS Redshift] a Experience Platform en Azure.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL AWS Redshift], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| `server` | El nombre del servidor de su instancia [!DNL AWS Redshift]. |
| `port` | El puerto TCP que usa un servidor [!DNL AWS Redshift] para detectar conexiones de cliente. |
| `username` | El nombre de usuario asociado con su cuenta de [!DNL AWS Redshift]. |
| `password` | La contraseña que corresponde a la cuenta de usuario. |
| `database` | Base de datos [!DNL AWS Redshift] de la que se van a obtener datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL AWS Redshift] es `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL AWS Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Crear una conexión base para [!DNL AWS Redshift] en Experience Platform en Azure [#azure-base]

>[!NOTE]
>
>El estándar de codificación predeterminado para [!DNL Redshift] es Unicode. Esto no se puede cambiar.

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL AWS Redshift] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

+++Seleccione para ver el ejemplo

La siguiente solicitud crea una conexión base para [!DNL AWS Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre del servidor de su instancia [!DNL AWS Redshift]. |
| `auth.params.port` | El puerto TCP que usa un servidor [!DNL AWS Redshift] para detectar conexiones de cliente. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL AWS Redshift]. |
| `auth.params.password` | La contraseña que corresponde a la cuenta de usuario. |
| `auth.params.database` | Base de datos [!DNL AWS Redshift] de la que se van a obtener datos. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Respuesta**

+++Seleccione para ver el ejemplo

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Conectar [!DNL AWS Redshift] a Experience Platform en AWS Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en AWS Web Services (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL AWS Redshift] a Experience Platform en AWS.

### Crear una conexión base para [!DNL AWS Redshift] en Experience Platform en AWS {#aws-base}

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL AWS Redshift]:

+++Seleccione para ver el ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | El nombre del servidor de su instancia [!DNL AWS Redshift]. |
| `auth.params.port` | El puerto TCP que usa un servidor [!DNL AWS Redshift] para detectar conexiones de cliente. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL AWS Redshift]. |
| `auth.params.password` | La contraseña que corresponde a la cuenta de usuario. |
| `auth.params.database` | Base de datos [!DNL AWS Redshift] de la que se van a obtener datos. |
| `auth.params.schema` | Nombre del esquema asociado con la base de datos [!DNL AWS Redshift]. Debe asegurarse de que el usuario al que desea otorgar acceso a la base de datos también tenga acceso a este esquema. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el almacenamiento en el siguiente tutorial.

+++Seleccione para ver el ejemplo

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL AWS Redshift] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
