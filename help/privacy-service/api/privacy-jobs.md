---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Extremo de trabajos de privacidad
topic: developer guide
description: Obtenga información sobre cómo administrar trabajos de privacidad para aplicaciones Experience Cloud mediante la API de Privacy Service.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---


# Extremo de trabajos de privacidad

Este documento explica cómo trabajar con trabajos de privacidad mediante llamadas de API. Específicamente, abarca el uso del extremo `/job` en la API [!DNL Privacy Service]. Antes de leer esta guía, consulte la [sección de introducción](./getting-started.md#getting-started) para obtener información importante que debe conocer a fin de realizar llamadas exitosas a la API, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

>[!NOTE]
>
>Si intenta administrar las solicitudes de consentimiento o de exclusión de los clientes, consulte la [guía de extremo de consentimiento](./consent.md).

## Lista de todos los trabajos {#list}

Puede realizar una vista de una lista de todos los trabajos de privacidad disponibles en su organización mediante una solicitud de GET al extremo `/jobs`.

**Formato API**

Este formato de solicitud utiliza un parámetro de consulta `regulation` en el extremo `/jobs`, por lo tanto comienza con un signo de interrogación (`?`) como se muestra a continuación. La respuesta está paginada, lo que le permite usar otros parámetros de consulta (`page` y `size`) para filtrar la respuesta. Puede separar varios parámetros mediante ampersands (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parámetro | Descripción |
| --- | --- |
| `{REGULATION}` | El tipo de regulación para el que se debe realizar la consulta. Los valores aceptados incluyen: <ul><li>`gdpr` (Unión Europea)</li><li>`ccpa` (California)</li><li>`lgpd_bra` (Brasil)</li><li>`nzpa_nzl` (Nueva Zelanda)</li><li>`pdpa_tha` (Tailandia)</li></ul> |
| `{PAGE}` | La página de datos que se va a mostrar, mediante la numeración basada en 0. El valor predeterminado es `0`. |
| `{SIZE}` | Número de resultados que se mostrarán en cada página. El valor predeterminado es `1` y el máximo es `100`. Si se supera el máximo, la API devuelve un error de 400 códigos. |

**Solicitud**

La siguiente solicitud recupera una lista paginada de todos los trabajos dentro de una organización de IMS, comenzando desde la tercera página con un tamaño de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de trabajos, y cada trabajo contiene detalles como su `jobId`. En este ejemplo, la respuesta contendría una lista de 50 trabajos, comenzando en la tercera página de resultados.

### Acceso a páginas subsiguientes

Para obtener el siguiente conjunto de resultados en una respuesta paginada, debe realizar otra llamada de API al mismo extremo mientras aumenta el parámetro de consulta `page` en 1.

## Crear un trabajo de privacidad {#create-job}

Antes de crear una nueva solicitud de trabajo, primero debe recopilar información de identificación acerca de los sujetos de datos cuyos datos desea acceder, eliminar o exclusión de venta. Una vez que tenga los datos requeridos, deben proporcionarse en la carga útil de una solicitud de POST al extremo `/jobs`.

>[!NOTE]
>
>Las aplicaciones compatibles de Adobe Experience Cloud utilizan diferentes valores para identificar los sujetos de datos. Consulte la guía sobre [aplicaciones de Privacy Service y Experience Cloud](../experience-cloud-apps.md) para obtener más información sobre los identificadores requeridos para sus aplicaciones. Para obtener instrucciones más generales sobre cómo determinar a qué ID se enviarán [!DNL Privacy Service], consulte el documento sobre [datos de identidad en solicitudes de privacidad](../identity-data.md).

La API [!DNL Privacy Service] admite dos tipos de solicitudes de trabajo para datos personales:

* [Acceso y/o eliminación](#access-delete): Acceder (leer) o eliminar datos personales.
* [Exclusión la venta](#opt-out): Marque los datos personales como no vendidos.

>[!IMPORTANT]
>
>Aunque las solicitudes de acceso y eliminación se pueden combinar como una sola llamada de API, las solicitudes de exclusión se deben realizar por separado.

### Crear un trabajo de acceso/eliminación {#access-delete}

Esta sección muestra cómo realizar una solicitud de trabajo de acceso o eliminación mediante la API.

**Formato API**

```http
POST /jobs
```

**Solicitud**

La siguiente solicitud crea una nueva solicitud de trabajo, configurada por los atributos suministrados en la carga útil como se describe a continuación.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propiedad | Descripción |
| --- | --- |
| `companyContexts` **(Requerido)** | Matriz que contiene información de autenticación para su organización. Cada identificador de la lista incluye los atributos siguientes: <ul><li>`namespace`:: Área de nombres de un identificador.</li><li>`value`:: El valor del identificador.</li></ul>Es **necesario** que uno de los identificadores utilice `imsOrgId` como `namespace`, con su `value` que contenga el identificador único de su organización de IMS. <br/><br/>Los identificadores adicionales pueden ser calificadores de compañía específicos del producto (por ejemplo,  `Campaign`), que identifican una integración con una aplicación de Adobe que pertenece a su organización. Los valores potenciales incluyen nombres de cuenta, códigos de cliente, ID de inquilino u otros identificadores de aplicación. |
| `users` **(Requerido)** | Matriz que contiene una colección de por lo menos un usuario cuya información desea obtener o eliminar. Se puede proporcionar un máximo de 1000 ID de usuario en una sola solicitud. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`:: Identificador de un usuario que se utiliza para calificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella fácilmente o buscarla más adelante.</li><li>`action`:: Matriz que lista las acciones que se deben realizar en los datos del usuario. Según las acciones que desee realizar, esta matriz debe incluir `access`, `delete` o ambas.</li><li>`userIDs`:: Colección de identidades para el usuario. El número de identidades que un usuario puede tener está limitado a nueve. Cada identidad consta de un `namespace`, un `value` y un calificador de Área de nombres (`type`). Consulte el [apéndice](appendix.md) para obtener más información sobre estas propiedades requeridas.</li></ul> Para obtener una explicación más detallada de `users` y `userIDs`, consulte la [guía de solución de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Requerido)** | Una matriz de productos de Adobe que se incluirán en el procesamiento. Si falta este valor o si está vacío, se rechazará la solicitud. Incluya únicamente productos con los que su organización tenga una integración. Consulte la sección sobre [valores del producto aceptados](appendix.md) en el apéndice para obtener más información. |
| `expandIDs` | Una propiedad opcional que, cuando se establece en `true`, representa una optimización para procesar los ID en las aplicaciones (actualmente solo admitida por [!DNL Analytics]). Si se omite, este valor predeterminado es `false`. |
| `priority` | Propiedad opcional utilizada por Adobe Analytics que establece la prioridad para procesar solicitudes. Los valores aceptados son `normal` y `low`. Si se omite `priority`, el comportamiento predeterminado es `normal`. |
| `analyticsDeleteMethod` | Una propiedad opcional que especifica cómo Adobe Analytics debe gestionar los datos personales. Se aceptan dos valores posibles para este atributo: <ul><li>`anonymize`:: Todos los datos a los que hace referencia la colección dada de ID de usuario se vuelven anónimos. Si se omite `analyticsDeleteMethod`, este es el comportamiento predeterminado.</li><li>`purge`:: Todos los datos se eliminan por completo.</li></ul> |
| `regulation` **(Requerido)** | La regulación del trabajo de privacidad. Se aceptan los siguientes valores: <ul><li>`gdpr` (Unión Europea)</li><li>`ccpa` (California)</li><li>`lgpd_bra` (Brasil)</li><li>`nzpa_nzl` (Nueva Zelanda)</li><li>`pdpa_tha` (Tailandia)</li></ul> |

**Respuesta**

Una respuesta correcta devuelve los detalles de los trabajos recién creados.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Propiedad | Descripción |
| --- | --- |
| `jobId` | Un ID exclusivo y de solo lectura generado por el sistema para un trabajo. Este valor se utiliza en el siguiente paso de buscar un trabajo específico. |

Una vez que haya enviado correctamente la solicitud de trabajo, puede pasar al siguiente paso de [comprobación del estado del trabajo](#check-status).

## Comprobar el estado de un trabajo {#check-status}

Puede recuperar información sobre un trabajo específico, como su estado de procesamiento actual, incluyendo el `jobId` de ese trabajo en la ruta de una solicitud de GET al extremo `/jobs`.

>[!IMPORTANT]
>
>Los datos de los trabajos creados anteriormente solo están disponibles para su recuperación en los 30 días posteriores a la fecha de finalización del trabajo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{JOB_ID}` | ID del trabajo que desea buscar. Este ID se devuelve en `jobId` en respuestas de API correctas para [crear un trabajo](#create-job) y [enumerar todos los trabajos](#list). |

**Solicitud**

La siguiente solicitud recupera los detalles del trabajo cuyo `jobId` se proporciona en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo especificado.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propiedad | Descripción |
| --- | --- |
| `productStatusResponse` | Cada objeto dentro de la matriz `productResponses` contiene información sobre el estado actual del trabajo con respecto a una aplicación [!DNL Experience Cloud] específica. |
| `productStatusResponse.status` | La categoría de estado actual del trabajo. Consulte la tabla siguiente para obtener una lista de [categorías de estado disponibles](#status-categories) y sus significados correspondientes. |
| `productStatusResponse.message` | Estado específico del trabajo, correspondiente a la categoría de estado. |
| `productStatusResponse.responseMsgCode` | Código estándar para los mensajes de respuesta del producto recibidos por [!DNL Privacy Service]. Los detalles del mensaje se proporcionan en `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una explicación más detallada del estado del trabajo. Los mensajes para estados similares pueden variar entre productos. |
| `productStatusResponse.results` | Para ciertos estados, algunos productos pueden devolver un objeto `results` que proporciona información adicional que no está cubierta por `responseMsgDetail`. |
| `downloadURL` | Si el estado del trabajo es `complete`, este atributo proporciona una dirección URL para descargar los resultados del trabajo como archivo ZIP. Este archivo está disponible para su descarga durante 60 días tras finalizar el trabajo. |

### Categorías de estado del trabajo {#status-categories}

La siguiente tabla lista las diferentes categorías posibles de estado del trabajo y su significado correspondiente:

| Categoría de estado | Significado |
| -------------- | -------- |
| `complete` | El trabajo se ha completado y (si es necesario) los archivos se cargan desde cada aplicación. |
| `processing` | Las aplicaciones han reconocido el trabajo y se están procesando. |
| `submitted` | El trabajo se envía a todas las solicitudes correspondientes. |
| `error` | Error en el procesamiento del trabajo: se puede obtener información más específica recuperando los detalles del trabajo individual. |

>[!NOTE]
>
>Un trabajo enviado puede permanecer en un estado `processing` si tiene un trabajo secundario dependiente que aún se está procesando.

## Pasos siguientes

Ahora sabe cómo crear y supervisar trabajos de privacidad mediante la API [!DNL Privacy Service]. Para obtener información sobre cómo realizar las mismas tareas mediante la interfaz de usuario, consulte la [información general de la interfaz de usuario del Privacy Service](../ui/overview.md).
