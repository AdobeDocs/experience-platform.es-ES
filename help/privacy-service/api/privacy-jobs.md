---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de la API de trabajos de privacidad
topic-legacy: developer guide
description: Obtenga información sobre cómo administrar los trabajos de privacidad para aplicaciones de Experience Cloud mediante la API de Privacy Service.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 3%

---

# Punto final de trabajos de privacidad

Este documento explica cómo trabajar con trabajos de privacidad mediante llamadas API. En concreto, abarca el uso de la variable `/job` en la variable [!DNL Privacy Service] API. Antes de leer esta guía, consulte [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

>[!NOTE]
>
>Si está intentando administrar las solicitudes de consentimiento o exclusión de los clientes, consulte la [guía de extremo de consentimiento](./consent.md).

## Enumerar todos los trabajos {#list}

Puede ver una lista de todos los trabajos de privacidad disponibles en su organización realizando una solicitud de GET a la `/jobs` punto final.

**Formato de API**

Este formato de solicitud utiliza un `regulation` parámetro de consulta en la variable `/jobs` , por lo tanto comienza con un signo de interrogación (`?`) como se muestra a continuación. La respuesta está paginada, lo que le permite utilizar otros parámetros de consulta (`page` y `size`) para filtrar la respuesta. Puede separar varios parámetros usando el símbolo &amp; (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parámetro | Descripción |
| --- | --- |
| `{REGULATION}` | El tipo de regulación que se va a consultar. Los valores aceptados incluyen: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte la descripción general sobre [regulaciones compatibles](../regulations/overview.md) para obtener más información sobre las normas de privacidad que representan los valores anteriores. |
| `{PAGE}` | La página de datos que se va a mostrar, utilizando una numeración basada en 0. El valor predeterminado es `0`. |
| `{SIZE}` | Número de resultados que se mostrarán en cada página. El valor predeterminado es `1` y el máximo es `100`. Si se supera el máximo, la API devuelve un error de código 400. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud recupera una lista paginada de todos los trabajos dentro de una organización de IMS, empezando desde la tercera página con un tamaño de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de trabajos, cada uno de los cuales contiene detalles como su `jobId`. En este ejemplo, la respuesta contendría una lista de 50 trabajos, empezando en la tercera página de resultados.

### Acceso a páginas posteriores

Para obtener el siguiente conjunto de resultados en una respuesta paginada, debe realizar otra llamada de API al mismo extremo mientras aumenta la variable `page` parámetro de consulta por 1.

## Crear un trabajo de privacidad {#create-job}

Antes de crear una nueva solicitud de trabajo, primero debe recopilar información de identificación sobre los interesados cuyos datos desee acceder, eliminar o excluir de la venta. Una vez que tenga los datos requeridos, estos deben proporcionarse en la carga útil de una solicitud del POST al `/jobs` punto final.

>[!NOTE]
>
>Las aplicaciones compatibles con Adobe Experience Cloud utilizan valores diferentes para identificar interesados. Consulte la guía de [aplicaciones de Privacy Service y Experience Cloud](../experience-cloud-apps.md) para obtener más información sobre los identificadores necesarios para sus aplicaciones. Para obtener instrucciones más generales sobre cómo determinar a qué ID enviar a [!DNL Privacy Service], consulte el documento en [datos de identidad en solicitudes de privacidad](../identity-data.md).

La variable [!DNL Privacy Service] La API admite dos tipos de solicitudes de trabajo para datos personales:

* [Acceso o eliminación](#access-delete): Acceder (leer) o eliminar datos personales.
* [Exclusión de la venta](#opt-out): Marque los datos personales como no vendidos.

>[!IMPORTANT]
>
>Aunque las solicitudes de acceso y eliminación se pueden combinar como una sola llamada de API, las solicitudes de exclusión se deben realizar por separado.

### Crear un trabajo de acceso/eliminación {#access-delete}

En esta sección se explica cómo realizar una solicitud de trabajo de acceso o eliminación mediante la API.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Propiedad | Descripción |
| --- | --- |
| `companyContexts` **(Obligatorio)** | Matriz que contiene información de autenticación para su organización. Cada identificador enumerado incluye los siguientes atributos: <ul><li>`namespace`: El espacio de nombres de un identificador.</li><li>`value`: El valor del identificador.</li></ul>Es **obligatorio** que uno de los identificadores utiliza `imsOrgId` como su `namespace`, con su `value` que contiene el ID exclusivo de su organización de IMS. <br/><br/>Los identificadores adicionales pueden ser calificadores de empresa específicos del producto (por ejemplo, `Campaign`), que identifican una integración con una aplicación de Adobe que pertenece a su organización. Los posibles valores incluyen nombres de cuenta, códigos de cliente, ID de inquilino u otros identificadores de aplicación. |
| `users` **(Obligatorio)** | Matriz que contiene una colección de al menos un usuario cuya información desea acceder o eliminar. Se puede proporcionar un máximo de 1000 ID de usuario en una única solicitud. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`: Identificador de un usuario que se utiliza para clasificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella o buscarla más adelante.</li><li>`action`: Matriz que enumera las acciones deseadas que deben realizarse en los datos del usuario. En función de las acciones que desee realizar, esta matriz debe incluir `access`, `delete`, o ambas.</li><li>`userIDs`: Una colección de identidades para el usuario. El número de identidades que un solo usuario puede tener está limitado a nueve. Cada identidad consiste en una `namespace`, `value`y un calificador de área de nombres (`type`). Consulte la [apéndice](appendix.md) para obtener más información sobre estas propiedades requeridas.</li></ul> Para obtener una explicación más detallada de `users` y `userIDs`, consulte la [guía de solución de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Obligatorio)** | Una matriz de productos de Adobe para incluir en el procesamiento. Si falta este valor o está vacío, se rechazará la solicitud. Incluya únicamente productos con los que su organización tenga una integración. Consulte la sección sobre [valores de producto aceptados](appendix.md) en el apéndice para obtener más información. |
| `expandIDs` | Una propiedad opcional que, cuando se establece en `true`, representa una optimización para el procesamiento de los ID en las aplicaciones (actualmente solo compatible con [!DNL Analytics]). Si se omite, el valor predeterminado es `false`. |
| `priority` | Una propiedad opcional utilizada por Adobe Analytics que establece la prioridad para el procesamiento de solicitudes. Los valores aceptados son `normal` y `low`. If `priority` se omite, el comportamiento predeterminado es `normal`. |
| `analyticsDeleteMethod` | Una propiedad opcional que especifica cómo debe gestionar Adobe Analytics los datos personales. Se aceptan dos valores posibles para este atributo: <ul><li>`anonymize`: Todos los datos a los que hace referencia la recopilación determinada de ID de usuario se vuelven anónimos. If `analyticsDeleteMethod` se omite, este es el comportamiento predeterminado.</li><li>`purge`: Todos los datos se eliminan por completo.</li></ul> |
| `mergePolicyId` | Al realizar solicitudes de privacidad para el Perfil del cliente en tiempo real (`profileService`), si lo desea, puede proporcionar el ID del [combinar directiva](../../profile/merge-policies/overview.md) que desea utilizar para la vinculación de ID. Al especificar una directiva de combinación, las solicitudes de privacidad pueden incluir información de segmentos al devolver datos a un cliente. Solo se puede especificar una directiva de combinación por solicitud. Si no se proporciona ninguna directiva de combinación, la información de segmentación no se incluye en la respuesta. |
| `regulation` **(Obligatorio)** | La regulación del trabajo de privacidad. Se aceptan los siguientes valores: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte la descripción general sobre [regulaciones compatibles](../regulations/overview.md) para obtener más información sobre las normas de privacidad que representan los valores anteriores. |

{style=&quot;table-layout:auto&quot;}

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
| `jobId` | Un ID único y de solo lectura generado por el sistema para un trabajo. Este valor se utiliza en el siguiente paso de la búsqueda de un trabajo específico. |

{style=&quot;table-layout:auto&quot;}

Una vez que haya enviado correctamente la solicitud de trabajo, puede continuar con el siguiente paso de [comprobación del estado del trabajo](#check-status).

## Comprobar el estado de un trabajo {#check-status}

Puede recuperar información sobre un trabajo específico, como su estado de procesamiento actual, incluyendo el de ese trabajo `jobId` en la ruta de una solicitud de GET al `/jobs` punto final.

>[!IMPORTANT]
>
>Los datos de los trabajos creados anteriormente solo están disponibles para su recuperación en un plazo de 30 días a partir de la fecha de finalización del trabajo.

**Formato de API**

```http
GET /jobs/{JOB_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{JOB_ID}` | El ID del trabajo que desea buscar. Este ID se devuelve en `jobId` en respuestas de API correctas para [creación de un trabajo](#create-job) y [listar todos los trabajos](#list). |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud recupera los detalles del trabajo cuya `jobId` se proporciona en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `productStatusResponse` | Cada objeto dentro de la variable `productResponses` matriz contiene información sobre el estado actual del trabajo con respecto a un [!DNL Experience Cloud] aplicación. |
| `productStatusResponse.status` | La categoría de estado actual del trabajo. Consulte la tabla siguiente para obtener una lista de [categorías de estado disponibles](#status-categories) y sus significados correspondientes. |
| `productStatusResponse.message` | Estado específico del trabajo, correspondiente a la categoría de estado. |
| `productStatusResponse.responseMsgCode` | Un código estándar para los mensajes de respuesta de producto recibidos por [!DNL Privacy Service]. Los detalles del mensaje se proporcionan en `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una explicación más detallada del estado del trabajo. Los mensajes para estados similares pueden variar entre productos. |
| `productStatusResponse.results` | Para ciertos estados, algunos productos pueden devolver un `results` objeto que proporciona información adicional que no abarca `responseMsgDetail`. |
| `downloadURL` | Si el estado del trabajo es `complete`, este atributo proporciona una dirección URL para descargar los resultados del trabajo como archivo ZIP. Este archivo está disponible para su descarga durante 60 días después de que finalice el trabajo. |

{style=&quot;table-layout:auto&quot;}

### Categorías de estado del trabajo {#status-categories}

La siguiente tabla enumera las diferentes categorías posibles de estado del trabajo y su significado correspondiente:

| Categoría de estado | Significado |
| -------------- | -------- |
| `complete` | El trabajo ha finalizado y, si es necesario, los archivos se cargan desde cada aplicación. |
| `processing` | Las aplicaciones han reconocido el trabajo y se están procesando actualmente. |
| `submitted` | El trabajo se envía a cada solicitud aplicable. |
| `error` | Error en el procesamiento del trabajo: se puede obtener información más específica recuperando los detalles del trabajo individual. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Un trabajo enviado puede permanecer en un `processing` si tiene un trabajo secundario dependiente que aún se está procesando.

## Pasos siguientes

Ahora sabe cómo crear y monitorizar trabajos de privacidad utilizando la variable [!DNL Privacy Service] API. Para obtener información sobre cómo realizar las mismas tareas utilizando la interfaz de usuario, consulte la [Información general sobre la IU de Privacy Service](../ui/overview.md).
