---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Punto final de API de trabajos de privacidad
description: Obtenga información sobre cómo administrar los trabajos de privacidad para aplicaciones de Experience Cloud mediante la API de Privacy Service.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 2%

---

# Extremo de trabajos de privacidad

Este documento explica cómo trabajar con trabajos de privacidad mediante llamadas a la API. Concretamente, abarca el uso de la `/job` punto final en la [!DNL Privacy Service] API. Antes de leer esta guía, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API de, incluidos los encabezados obligatorios y cómo leer llamadas de API de ejemplo.

>[!NOTE]
>
>Si intenta administrar las solicitudes de consentimiento u exclusión de clientes, consulte la [guía de extremo de consentimiento](./consent.md).

## Enumerar todos los trabajos {#list}

Puede ver una lista de todos los trabajos de privacidad disponibles en su organización realizando una solicitud de GET a `/jobs` punto final.

**Formato de API**

Este formato de solicitud utiliza un `regulation` parámetro de consulta en `/jobs` punto final; por lo tanto, comienza con un signo de interrogación (`?`) como se muestra a continuación. La respuesta se pagina, lo que permite utilizar otros parámetros de consulta (`page` y `size`) para filtrar la respuesta. Puede separar varios parámetros mediante el símbolo et (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parámetro | Descripción |
| --- | --- |
| `{REGULATION}` | Tipo de regulación que se va a consultar. Los valores aceptados incluyen: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li><li>`cpa`</li><li>`ctdpa`</li></ul><br>Consulte la información general sobre [regulaciones compatibles](../regulations/overview.md) para obtener más información sobre las normas de privacidad que representan los valores anteriores. |
| `{PAGE}` | Página de datos que se va a mostrar, con numeración basada en 0. El valor predeterminado es `0`. |
| `{SIZE}` | El número de resultados que se mostrarán en cada página. El valor predeterminado es `1` y el máximo es `100`. Si se supera el máximo, la API devolverá un error de 400 códigos. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera una lista paginada de todos los trabajos de una organización, a partir de la tercera página con un tamaño de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de trabajos, cada uno de los cuales contiene detalles como `jobId`. En este ejemplo, la respuesta contendría una lista de 50 trabajos, a partir de la tercera página de resultados.

### Acceso a páginas subsiguientes

Para recuperar el siguiente conjunto de resultados en una respuesta paginada, debe realizar otra llamada de API al mismo extremo mientras aumenta el `page` parámetro de consulta por 1.

## Creación de un trabajo de privacidad {#create-job}

>[!IMPORTANT]
>
>El Privacy Service solo está diseñado para solicitudes de derechos de los interesados y consumidores. No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos. El Adobe tiene la obligación legal de cumplirlos en el momento oportuno. Como tal, no se permiten las pruebas de carga en el Privacy Service, ya que es un entorno de solo producción y crea un registro de solicitudes de privacidad válidas innecesarias.
>
>Ahora se establece un límite diario de carga estricto para ayudar a evitar el abuso del servicio. Si se detecta que algún usuario abusa del sistema, se deshabilitará el acceso al servicio. Luego se celebrará una reunión posterior con ellos para abordar sus acciones y discutir el uso aceptable de Privacy Service.

Antes de crear una nueva solicitud de trabajo, primero debe recopilar información de identificación de los interesados a cuyos datos desea acceder, eliminar o excluir de la venta. Una vez que tenga los datos necesarios, deben proporcionarse en la carga útil de una solicitud del POST a `/jobs` punto final.

>[!NOTE]
>
>Las aplicaciones compatibles de Adobe Experience Cloud utilizan valores diferentes para identificar a los interesados. Consulte la guía de [Aplicaciones de Privacy Service y Experience Cloud](../experience-cloud-apps.md) para obtener más información sobre los identificadores necesarios para sus aplicaciones. Para obtener instrucciones más generales sobre cómo determinar qué ID enviar a [!DNL Privacy Service], consulte el documento sobre [datos de identidad en solicitudes de privacidad](../identity-data.md).

El [!DNL Privacy Service] La API admite dos tipos de solicitudes de trabajo para datos personales:

* [Acceso o eliminación](#access-delete): Acceda (lea) o elimine datos personales.
* [Exclusión de la venta](#opt-out): Marque los datos personales como no aptos para la venta.

>[!IMPORTANT]
>
>Aunque las solicitudes de acceso y eliminación se pueden combinar como una sola llamada de API, las solicitudes de exclusión deben realizarse por separado.

### Creación de un trabajo de acceso o eliminación {#access-delete}

Esta sección muestra cómo realizar una solicitud de trabajo de acceso o eliminación mediante la API.

**Formato de API**

```http
POST /jobs
```

**Solicitud**

La siguiente solicitud crea una nueva solicitud de trabajo, configurada por los atributos proporcionados en la carga útil como se describe a continuación.

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
| `companyContexts` **(Obligatorio)** | Matriz que contiene información de autenticación de su organización. Cada identificador enumerado incluye los siguientes atributos: <ul><li>`namespace`: el área de nombres de un identificador.</li><li>`value`: El valor del identificador.</li></ul>Lo es **obligatorio** que utiliza uno de los identificadores `imsOrgId` como su `namespace`, con su `value` que contiene el ID único de su organización. <br/><br/>Los identificadores adicionales pueden ser calificadores de compañía específicos de productos (por ejemplo, `Campaign`), que identifican una integración con una aplicación de Adobe perteneciente a su organización. Los valores potenciales incluyen nombres de cuenta, códigos de cliente, ID de inquilino u otros identificadores de aplicación. |
| `users` **(Obligatorio)** | Matriz que contiene una colección de al menos un usuario cuya información desea eliminar o a la que desea acceder. Se puede proporcionar un máximo de 1000 ID de usuario en una sola solicitud. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`: Identificador de un usuario que se utiliza para clasificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella o buscarla más tarde.</li><li>`action`: una matriz que enumera las acciones deseadas que se deben realizar en los datos del usuario. Según las acciones que desee realizar, esta matriz debe incluir `access`, `delete`, o ambas.</li><li>`userIDs`: una colección de identidades del usuario. El número de identidades que un solo usuario puede tener está limitado a nueve. Cada identidad consta de un `namespace`, a `value`y un calificador de área de nombres (`type`). Consulte la [apéndice](appendix.md) para obtener más información sobre estas propiedades requeridas.</li></ul> Para obtener una explicación más detallada de `users` y `userIDs`, consulte la [guía de solución de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Obligatorio)** | Una matriz de productos de Adobe para incluir en el procesamiento. Si falta este valor o está vacío, la solicitud es rechazada. Incluya solo productos con los que su organización tenga una integración. Consulte la sección sobre [valores de producto aceptados](appendix.md) en el apéndice para obtener más información. |
| `expandIDs` | Una propiedad opcional que, cuando se establece en `true`, representa una optimización para procesar los ID en las aplicaciones (actualmente solo compatible con [!DNL Analytics]). Si se omite, el valor predeterminado es `false`. |
| `priority` | Propiedad opcional utilizada por Adobe Analytics que establece la prioridad para procesar solicitudes. Los valores aceptados son `normal` y `low`. If `priority` se omite, el comportamiento predeterminado es `normal`. |
| `analyticsDeleteMethod` | Una propiedad opcional que especifica cómo debe gestionar Adobe Analytics los datos personales. Se aceptan dos valores posibles para este atributo: <ul><li>`anonymize`: todos los datos a los que hace referencia la colección de ID de usuario dada se hacen anónimos. If `analyticsDeleteMethod` se omite, este es el comportamiento predeterminado.</li><li>`purge`: todos los datos se eliminan por completo.</li></ul> |
| `mergePolicyId` | Al realizar solicitudes de privacidad para el Perfil del cliente en tiempo real (`profileService`), si lo desea, puede proporcionar el ID del específico [política de combinación](../../profile/merge-policies/overview.md) que desee utilizar para la vinculación de ID. Al especificar una política de combinación, las solicitudes de privacidad pueden incluir información de la audiencia al devolver datos de un cliente. Solo se puede especificar una política de combinación por solicitud. Si no se proporciona ninguna política de combinación, la información de segmentación no se incluye en la respuesta. |
| `regulation` **(Obligatorio)** | La regulación del trabajo de privacidad. Se aceptan los siguientes valores: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte la información general sobre [regulaciones compatibles](../regulations/overview.md) para obtener más información sobre las normas de privacidad que representan los valores anteriores. |

{style="table-layout:auto"}

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
| `jobId` | Un ID único de solo lectura generado por el sistema para un trabajo. Este valor se utiliza en el siguiente paso para buscar un trabajo específico. |

{style="table-layout:auto"}

Una vez enviada correctamente la solicitud de trabajo, puede continuar con el siguiente paso de [comprobación del estado del trabajo](#check-status).

## Comprobar el estado de un trabajo {#check-status}

Puede recuperar información sobre un trabajo específico, como su estado de procesamiento actual, incluyendo el de ese trabajo `jobId` en la ruta de una petición de GET a `/jobs` punto final.

>[!IMPORTANT]
>
>Los datos de los trabajos creados anteriormente solo están disponibles para su recuperación en los 30 días posteriores a la fecha de finalización del trabajo.

**Formato de API**

```http
GET /jobs/{JOB_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{JOB_ID}` | El ID del trabajo que desea buscar. Este ID se devuelve en `jobId` en respuestas de API correctas para [creación de un trabajo](#create-job) y [enumerar todos los trabajos](#list). |

{style="table-layout:auto"}

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
| `productStatusResponse` | Cada objeto dentro de `productResponses` contiene información sobre el estado actual del trabajo con respecto a un [!DNL Experience Cloud] aplicación. |
| `productStatusResponse.status` | La categoría de estado actual del trabajo. Consulte la tabla siguiente para obtener una lista de [categorías de estado disponibles](#status-categories) y sus significados correspondientes. |
| `productStatusResponse.message` | El estado específico del trabajo, correspondiente a la categoría de estado. |
| `productStatusResponse.responseMsgCode` | Un código estándar para los mensajes de respuesta de producto recibidos por [!DNL Privacy Service]. Los detalles del mensaje se proporcionan en `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Una explicación más detallada del estado del trabajo. Los mensajes para estados similares pueden variar entre productos. |
| `productStatusResponse.results` | Para determinados estados, algunos productos pueden devolver un `results` que proporciona información adicional no cubierta por `responseMsgDetail`. |
| `downloadURL` | Si el estado del trabajo es `complete`, este atributo proporciona una URL para descargar los resultados del trabajo como archivo ZIP. Este archivo está disponible para descargar durante 60 días después de completarse el trabajo. |

{style="table-layout:auto"}

### Categorías de estado del trabajo {#status-categories}

En la tabla siguiente se enumeran las diferentes categorías de estado de trabajo posibles y su significado correspondiente:

| Categoría de estado | Significado |
| -------------- | -------- |
| `complete` | El trabajo se ha completado y (si es necesario) los archivos se cargan desde cada aplicación. |
| `processing` | Las aplicaciones han reconocido el trabajo y se están procesando en este momento. |
| `submitted` | El trabajo se envía a todas las solicitudes aplicables. |
| `error` | Se ha producido un error en el procesamiento del trabajo. Se puede obtener información más específica recuperando los detalles individuales del trabajo. |

{style="table-layout:auto"}

>[!NOTE]
>
>Un trabajo enviado podría permanecer en un `processing` estado si tiene un trabajo secundario dependiente que aún se está procesando.

## Pasos siguientes

Ahora sabe cómo crear y supervisar trabajos de privacidad mediante [!DNL Privacy Service] API. Para obtener información sobre cómo realizar las mismas tareas utilizando la interfaz de usuario, consulte la [Información general de IU de Privacy Service](../ui/overview.md).
