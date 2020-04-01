---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de una conexión de flujo mediante la API
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182

---


# Creación de una conexión de flujo mediante la API

Este tutorial le ayudará a empezar a utilizar las API de inserción de flujo continuo, que forman parte de las API de servicio de inserción de datos de Adobe Experience Platform.

## Primeros pasos

Se requiere el registro de la conexión de flujo continuo para el inicio de datos de flujo continuo a Adobe Experience Platform. Al registrar una conexión de flujo continuo, debe proporcionar algunos detalles clave, como la fuente de datos de flujo.

Después de registrar una conexión de flujo continuo, usted, como productor de datos, tendrá una dirección URL única que puede utilizarse para transmitir datos a Platform.

Este tutorial también requiere un conocimiento práctico de varios servicios de Adobe Experience Platform. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): Marco normalizado mediante el cual la Plataforma organiza los datos de experiencia.
- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.

Las siguientes secciones proporcionan información adicional que debe conocer para realizar llamadas a las API de inserción de flujo continuo.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Crear una conexión

Una conexión especifica el origen y contiene la información necesaria para que el flujo sea compatible con las API de inserción de flujo continuo.

**Formato API**

```http
POST /flowservice/connections
```

**Solicitud**

>[!NOTE] Los valores de la lista `providerId` y de la lista `connectionSpec` deben **** utilizarse como se muestra en el ejemplo, ya que son lo que especifica a la API que está creando una conexión de flujo para la transmisión de flujo continuo de ingesta.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El `id` de la conexión recién creada. Esto se denominará `{CONNECTION_ID}`. |
| `etag` | Identificador asignado a la conexión, que especifica la revisión de la conexión. |

## Obtener URL de recopilación de datos

Con la conexión creada, ahora puede recuperar la dirección URL de recopilación de datos.

**Formato API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El `id` valor de la conexión que creó anteriormente. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la conexión solicitada. La dirección URL de recopilación de datos se crea automáticamente con la conexión y se puede recuperar con el `inletUrl` valor.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Pasos siguientes

Ahora que ha creado una conexión de flujo continuo, puede transmitir series temporales o datos de registro, lo que le permite ingestar datos dentro de la plataforma. Para aprender a transmitir datos de series temporales a Platform, vaya al tutorial [de datos de series temporales de](./streaming-time-series-data.md)flujo continuo. Para obtener información sobre cómo transmitir datos de registros a Platform, vaya al tutorial [de datos de registros de](./streaming-record-data.md)flujo continuo.

## Apéndice

Esta sección proporciona información adicional sobre la creación de conexiones de flujo mediante la API.

### Conexiones de flujo autenticadas

La recopilación de datos autenticada permite a los servicios de Adobe Experience Platform, como Perfil e identidad del cliente en tiempo real, diferenciar entre registros procedentes de fuentes de confianza y fuentes que no son de confianza. Los clientes que deseen enviar información de identificación personal (PII) pueden hacerlo enviando Tokenes de acceso IMS como parte de la solicitud POST; si el testigo IMS es válido, los registros se marcan como recopilados a partir de fuentes válidas.

Encontrará más información sobre la creación de una conexión de flujo autenticada en el tutorial [](create-authenticated-streaming-connection.md)de creación de una conexión de flujo autenticada.