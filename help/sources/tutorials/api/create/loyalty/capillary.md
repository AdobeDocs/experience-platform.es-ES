---
title: Conexión de Capillary a Experience Platform mediante la API de Flow Service
description: Aprenda a conectar Capillary a Experience Platform mediante API.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: b3b1542f7e297f4ca872a155ac3801266bc1e6a6
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# Conectar [!DNL Capillary Streaming Events] a Experience Platform mediante la API [!DNL Flow Service]

>[!AVAILABILITY]
>
>El origen [!DNL Capillary Streaming Events] está en la versión beta. Lea los [términos y condiciones](../../../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea esta guía para aprender a usar [!DNL Capillary Streaming Events] y la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) para transmitir datos de su cuenta de [!DNL Capillary] a Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Lea la [[!DNL Capillary Streaming Events] descripción general](../../../../connectors/loyalty/capillary.md) para obtener información sobre la autenticación.

### Uso de API de Experience Platform

Lea la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas a las API de Experience Platform correctamente.

>[!BEGINSHADEBOX]

## Lista de comprobación de procesos de desarrollador

1. Cree o elija su **esquema de modelo de datos de experiencia (XDM)** de destino mediante el Registro de esquemas. Use este esquema XDM para **crear un conjunto de datos** en el servicio de catálogo.
2. Cree una **conexión base** para almacenar sus credenciales de [!DNL Capillary].
3. Cree una **conexión de origen** para enlazarla a su `baseConnectionId`.
4. Cree una **conexión de destino** para asegurarse de que sus datos aterrizan en el lago de datos.
5. Use la preparación de datos para crear asignaciones que asignen los campos de origen de [!DNL Capillary] a los campos XDM correctos.
6. Crear un flujo de datos con `sourceConnectionId`, `targetConnectionId` y `mappingID`
7. Pruebe con eventos de transacción/perfil de muestra únicos para verificar el flujo de datos.

>[!ENDSHADEBOX]

## Crear una conexión base {#base-connection}

Una conexión base conserva las credenciales y los detalles de conexión. Para crear una conexión base para [!DNL Capillary], realice una petición POST al extremo `/connections` de la API [!DNL Flow Service] y proporcione sus credenciales [!DNL Capillary] en el cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Capillary]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Respuesta**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Crear una conexión de origen

Para crear una conexión de origen, realice una petición POST al extremo `/sourceConnections` y proporcione el identificador de conexión base.

**Formato de API**

```http
POST /flowservice/sourceConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con información detallada de la conexión de origen recién creada, incluido su identificador único (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Configuraciones de esquema

>[!BEGINTABS]

>[!TAB Ingesta de perfil]

Los perfiles contienen atributos de identidad y lealtad. Vea la siguiente carga útil para ver un ejemplo basado en el esquema de perfil [!DNL Capillary]. Puede configurar y asignar este esquema a un perfil individual de XDM.

**Solicitud**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Respuesta**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Ingesta de transacciones]

Las transacciones capturan actividades comerciales. Vea la siguiente carga útil para ver un ejemplo en función del esquema de eventos [!DNL Capillary]. Puede configurar y asignar este esquema a un evento de experiencia XDM.

**Solicitud**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Respuesta**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### Migración de datos históricos

Puede introducir sus datos históricos de lealtad y transacciones en Experience Platform. Simplemente exporte sus datos como archivos CSV estructurados de [!DNL Capillary], transfiéralos de forma segura mediante [!DNL SFTP] e ingréselos en sus conjuntos de datos de Experience Platform. Después de la migración inicial, los datos se mantendrán actualizados en tiempo real a través del conector impulsado por evento.

### Creación de un esquema XDM de destino {#target-schema}

Un esquema del Modelo de datos de experiencia (XDM) proporciona una forma estandarizada de organizar y describir los datos de experiencia del cliente dentro de Experience Platform. Para introducir los datos de origen en Experience Platform, primero debe crear un esquema XDM de destino que defina la estructura y los tipos de datos que desea introducir. Este esquema sirve como modelo para el conjunto de datos de Experience Platform donde residirán los datos ingeridos.

Se puede crear un esquema XDM de destino realizando una petición POST a la [API del Registro de esquemas](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, lea las siguientes guías:

* [Cree un esquema con la API](../../../../../xdm/api/schemas.md).
* [Crear un esquema con la interfaz de usuario](../../../../../xdm/tutorials/create-schema-ui.md).

Una vez creado, el esquema XDM de destino `$id` se requerirá más adelante para el conjunto de datos de destino y la asignación.

## Crear un conjunto de datos de destinatario {#target-dataset}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente estructurada como una tabla con columnas (esquema) y filas (campos). Los datos que se incorporan correctamente a Experience Platform se almacenan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

Puede crear un conjunto de datos de destino realizando una petición POST a la [API del servicio de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), al mismo tiempo que proporciona el ID del esquema de destino en la carga útil. Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, lea la guía sobre [crear un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).


## Creación de una conexión de destino {#target}

Una conexión de destino representa la conexión con el destino donde aterrizan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este id. de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Creación de una asignación {#mapping}

A continuación, asigne los datos de origen al esquema de destino al que se adhiere el conjunto de datos de destino. Para crear una asignación, realice una petición POST al extremo `mappingSets` de la [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Incluya el ID del esquema XDM de destino y los detalles de los conjuntos de asignaciones que desee crear.

Asigne los campos capilares a los campos de esquema XDM correspondientes de la siguiente manera:

| Esquema de origen | Esquema de público destinatario |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>Puede descargar los [eventos y asignaciones de perfiles](../../../../images/tutorials/create/capillary/mappings.zip) para [!DNL Capillary] e [importar los archivos a la preparación de datos](../../../../../data-prep/ui/mapping.md#import-mapping) cuando esté listo para asignar los datos.

### Creación de un flujo de datos {#flow}

Después de crear la conexión de origen, la asignación y la conexión de destino, puede configurar un flujo de datos para mover datos de [!DNL Capillary] a Experience Platform.

Los flujos de datos habituales incluyen:

* **Flujo de datos de perfil**: Ingesta [!DNL Capillary] datos de perfil en un conjunto de datos de perfil individual XDM.
* **Flujo de datos de transacción**: Ingesta [!DNL Capillary] datos de transacción en un conjunto de datos XDM ExperienceEvent.

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` se encuentra en segundos UNIX epoch.

**Respuesta**

Una respuesta correcta devuelve el flujo de datos con su ID de flujo de datos correspondiente.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Control de errores

El conector incluye un control de errores sólido para los siguientes casos:

* **Errores de autenticación**: actualiza automáticamente las credenciales de Adobe cuando falla la autenticación.
* **Errores de límite de velocidad**: Implementa reintentos con retroceso exponencial cuando se alcanzan los límites de velocidad de API.
* **Errores de red**: Registra y reintenta las solicitudes de red con errores.
* **Errores de validación de datos**: Registra cargas no válidas para su revisión y resolución manuales.

Todos los errores se registran con detalles como el tipo de error, la marca de tiempo, la carga útil de solicitud y la respuesta de la API de Adobe para facilitar la resolución de problemas y la depuración.

## Prueba de la conexión

Siga los pasos a continuación para conocer los pasos que puede seguir para probar la conexión:

* Realice una petición GET a `/connections/{BASE_CONNECTION_ID}` y proporcione el identificador de la conexión base para comprobar que existe dicha conexión. Durante este paso, también puede comprobar que el estado de la conexión base está establecido en `active`.
* Realice una petición GET a `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` y proporcione el identificador de la conexión de origen para comprobar la conexión de origen.
* Utilice su URL de extremo de flujo continuo para enviar una carga útil de perfil de muestra (utilice el JSON de ingesta de perfil).
* Vaya al conjunto de datos en la interfaz de usuario de Experience Platform y ejecute una consulta en el conjunto de datos para confirmar los registros.
* Utilice los registros de preparación de datos para buscar errores.
* Si debe abrir un ticket de asistencia, asegúrese de que dispone de lo siguiente:
   * Solicitar carga útil
   * Cuerpo de respuesta
   * Request-id
   * timestamp
   * ID de recursos.

## Apéndice

Visite la siguiente documentación para obtener guías sobre operaciones adicionales

* [Supervisar flujos de datos](../../../../../dataflows/ui/monitor-sources.md)
* [Actualizar flujos de datos](../../../ui/update-dataflows.md)
* [Eliminar flujos de datos](../../../ui/delete.md)
* [Actualizar cuenta de origen](../../../ui/update.md)
