---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Trabajos
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 2%

---


# Trabajos de privacidad

Las siguientes secciones explican las llamadas que puede realizar mediante el `/jobs` punto final de la API de Privacy Service. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

## Crear un trabajo de privacidad {#create-job}

Antes de crear una nueva solicitud de trabajo, primero debe recopilar información de identificación acerca de los sujetos de datos cuyos datos desea acceder, eliminar o exclusión de venta. Una vez que tenga los datos requeridos, deben proporcionarse en la carga útil de una solicitud POST al extremo raíz.

>[!NOTE] Las aplicaciones compatibles de Adobe Experience Cloud utilizan valores diferentes para identificar los sujetos de datos. Consulte la guía sobre [Privacy Service y las aplicaciones](../experience-cloud-apps.md) de Experience Cloud para obtener más información sobre los identificadores necesarios para sus aplicaciones.

La API de Privacy Service admite dos tipos de solicitudes de trabajo para datos personales:

* [Acceso y/o eliminación](#access-delete): Acceder (leer) o eliminar datos personales.
* [Exclusión la venta](#opt-out): Marque los datos personales como no vendidos.

>[!IMPORTANT] Aunque las solicitudes de acceso y eliminación se pueden combinar como una sola llamada de API, las solicitudes de exclusión se deben realizar por separado.

### Crear un trabajo de acceso o eliminación {#access-delete}

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
| `companyContexts` **(Requerido)** | Matriz que contiene información de autenticación para su organización. Cada identificador de la lista incluye los atributos siguientes: <ul><li>`namespace`:: Área de nombres de un identificador.</li><li>`value`:: El valor del identificador.</li></ul>Es **necesario** que uno de los identificadores utilice `imsOrgId` como su `namespace`, con `value` el identificador único de su organización de IMS. <br/><br/>Los identificadores adicionales pueden ser calificadores de compañía específicos del producto (por ejemplo, `Campaign`), que identifican una integración con una aplicación de Adobe que pertenece a su organización. Los valores potenciales incluyen nombres de cuenta, códigos de cliente, ID de inquilino u otros identificadores de aplicación. |
| `users` **(Requerido)** | Matriz que contiene una colección de por lo menos un usuario cuya información desea obtener o eliminar. Se puede proporcionar un máximo de 1000 ID de usuario en una sola solicitud. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`:: Identificador de un usuario que se utiliza para calificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella fácilmente o buscarla más adelante.</li><li>`action`:: Matriz que lista las acciones que se deben realizar en los datos del usuario. Según las acciones que desee realizar, esta matriz debe incluir `access`, `delete`o ambas.</li><li>`userIDs`:: Colección de identidades para el usuario. El número de identidades que un usuario puede tener está limitado a nueve. Cada identidad consta de un calificador `namespace`, un `value`y una Área de nombres (`type`). Consulte el [apéndice](appendix.md) para obtener más información sobre estas propiedades requeridas.</li></ul> Para obtener una explicación más detallada de `users` y `userIDs`, consulte la guía de [solución de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Requerido)** | Una matriz de productos de Adobe que se incluirán en el procesamiento. Si falta este valor o si está vacío, se rechazará la solicitud. Incluya únicamente productos con los que su organización tenga una integración. Consulte la sección sobre los valores [del producto](appendix.md) aceptados en el apéndice para obtener más información. |
| `expandIDs` | Una propiedad opcional que, cuando se establece en `true`, representa una optimización para procesar los ID en las aplicaciones (actualmente solo admitida por Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propiedad opcional utilizada por Adobe Analytics que establece la prioridad para procesar solicitudes. Los valores aceptados son `normal` y `low`. Si `priority` se omite, el comportamiento predeterminado es `normal`. |
| `analyticsDeleteMethod` | Una propiedad opcional que especifica cómo Adobe Analytics debe gestionar los datos personales. Se aceptan dos valores posibles para este atributo: <ul><li>`anonymize`:: Todos los datos a los que hace referencia la colección dada de ID de usuario se vuelven anónimos. Si `analyticsDeleteMethod` se omite, este es el comportamiento predeterminado.</li><li>`purge`:: Todos los datos se eliminan por completo.</li></ul> |
| `regulation` **(Requerido)** | Reglamento de la solicitud. Debe ser uno de los tres valores siguientes: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

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

Una vez que haya enviado correctamente la solicitud de trabajo, puede pasar al siguiente paso de [comprobar el estado](#check-status)del trabajo.

### Creación de un trabajo de exclusión {#opt-out}

En esta sección se muestra cómo realizar una solicitud de trabajo de exclusión mediante la API.

**Formato API**

```http
POST /jobs
```

**Solicitud**

La siguiente solicitud crea una nueva solicitud de trabajo, configurada por los atributos suministrados en la carga útil como se describe a continuación.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
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
        "action": ["opt-out-of-sale"],
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
        "action": ["opt-out-of-sale"],
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
| `companyContexts` **(Requerido)** | Matriz que contiene información de autenticación para su organización. Cada identificador de la lista incluye los atributos siguientes: <ul><li>`namespace`:: Área de nombres de un identificador.</li><li>`value`:: El valor del identificador.</li></ul>Es **necesario** que uno de los identificadores utilice `imsOrgId` como su `namespace`, con `value` el identificador único de su organización de IMS. <br/><br/>Los identificadores adicionales pueden ser calificadores de compañía específicos del producto (por ejemplo, `Campaign`), que identifican una integración con una aplicación de Adobe que pertenece a su organización. Los valores potenciales incluyen nombres de cuenta, códigos de cliente, ID de inquilino u otros identificadores de aplicación. |
| `users` **(Requerido)** | Matriz que contiene una colección de por lo menos un usuario cuya información desea obtener o eliminar. Se puede proporcionar un máximo de 1000 ID de usuario en una sola solicitud. Cada objeto de usuario contiene la siguiente información: <ul><li>`key`:: Identificador de un usuario que se utiliza para calificar los ID de trabajo independientes en los datos de respuesta. Se recomienda elegir una cadena única y fácilmente identificable para este valor, de modo que se pueda hacer referencia a ella fácilmente o buscarla más adelante.</li><li>`action`:: Una matriz que lista las acciones que se desean realizar en los datos. Para las solicitudes de exclusión de venta, la matriz solo debe contener el valor `opt-out-of-sale`.</li><li>`userIDs`:: Colección de identidades para el usuario. El número de identidades que un usuario puede tener está limitado a nueve. Cada identidad consta de un calificador `namespace`, un `value`y una Área de nombres (`type`). Consulte el [apéndice](appendix.md) para obtener más información sobre estas propiedades requeridas.</li></ul> Para obtener una explicación más detallada de `users` y `userIDs`, consulte la guía de [solución de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Requerido)** | Una matriz de productos de Adobe que se incluirán en el procesamiento. Si falta este valor o si está vacío, se rechazará la solicitud. Incluya únicamente productos con los que su organización tenga una integración. Consulte la sección sobre los valores [del producto](appendix.md) aceptados en el apéndice para obtener más información. |
| `expandIDs` | Una propiedad opcional que, cuando se establece en `true`, representa una optimización para procesar los ID en las aplicaciones (actualmente solo admitida por Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propiedad opcional utilizada por Adobe Analytics que establece la prioridad para procesar solicitudes. Los valores aceptados son `normal` y `low`. Si `priority` se omite, el comportamiento predeterminado es `normal`. |
| `analyticsDeleteMethod` | Una propiedad opcional que especifica cómo Adobe Analytics debe gestionar los datos personales. Se aceptan dos valores posibles para este atributo: <ul><li>`anonymize`:: Todos los datos a los que hace referencia la colección dada de ID de usuario se vuelven anónimos. Si `analyticsDeleteMethod` se omite, este es el comportamiento predeterminado.</li><li>`purge`:: Todos los datos se eliminan por completo.</li></ul> |
| `regulation` **(Requerido)** | Reglamento de la solicitud. Debe ser uno de los tres valores siguientes: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Respuesta**

Una respuesta correcta devuelve los detalles de los trabajos recién creados.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Propiedad | Descripción |
| --- | --- |
| `jobId` | Un ID exclusivo y de solo lectura generado por el sistema para un trabajo. Este valor se utiliza para buscar un trabajo específico en el paso siguiente. |

Una vez que haya enviado correctamente la solicitud de trabajo, puede continuar con el siguiente paso para comprobar el estado del trabajo.

## Comprobar el estado de un trabajo {#check-status}

Mediante uno de los `jobId` valores devueltos en el paso anterior, puede recuperar información sobre ese trabajo, como su estado de procesamiento actual.

>[!IMPORTANT] Los datos de los trabajos creados anteriormente solo están disponibles para su recuperación en los 30 días posteriores a la fecha de finalización del trabajo.

**Formato API**

```http
GET /jobs/{JOB_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{JOB_ID}` | ID del trabajo que desea buscar, devuelto en `jobId` la respuesta del paso [](#create-job)anterior. |

**Solicitud**

La siguiente solicitud recupera los detalles del trabajo que `jobId` se proporciona en la ruta de solicitud.

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
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
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
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propiedad | Descripción |
| --- | --- |
| `productStatusResponse` | Estado actual del trabajo. En la tabla siguiente se proporcionan detalles sobre cada posible estado. |
| `downloadURL` | Si el estado del trabajo es `complete`, este atributo proporciona una URL para descargar los resultados del trabajo como archivo ZIP. Este archivo está disponible para su descarga durante 60 días tras finalizar el trabajo. |

### Respuestas al estado del trabajo

La siguiente tabla lista los distintos estados de trabajo posibles y su significado correspondiente:

| Código de estado | Mensaje de estado | Significado |
| ----------- | -------------- | -------- |
| 1 | Completar | El trabajo se ha completado y (si es necesario) los archivos se cargan desde cada aplicación. |
| 2 | Procesamiento | Las aplicaciones han reconocido el trabajo y se están procesando. |
| 3 | Submitted | El trabajo se envía a todas las solicitudes correspondientes. |
| 4 | Error | Error en el procesamiento del trabajo: se puede obtener información más específica recuperando los detalles del trabajo individual. |

>[!NOTE] Un trabajo enviado puede permanecer en estado de procesamiento si tiene un trabajo secundario dependiente que aún se está procesando.

## Lista de todos los trabajos

Puede realizar una vista de una lista de todas las solicitudes de trabajo disponibles dentro de su organización mediante una solicitud GET al extremo raíz (`/`).

**Formato API**

Este formato de solicitud utiliza un parámetro de `regulation` consulta en el extremo raíz (`/`), por lo tanto comienza con un signo de interrogación (`?`) como se muestra a continuación. La respuesta está paginada, lo que le permite utilizar otros parámetros de consulta (`page` y `size`) para filtrar la respuesta. Puede separar varios parámetros mediante ampersands (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parámetro | Descripción |
| --- | --- |
| `{REGULATION}` | El tipo de regulación para el que se debe realizar la consulta. Los valores aceptados son `gdpr`, `ccpa`y `pdpa_tha`. |
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

Una respuesta correcta devuelve una lista de trabajos, y cada trabajo contiene detalles como el `jobId`. En este ejemplo, la respuesta contendría una lista de 50 trabajos, comenzando en la tercera página de resultados.

### Acceso a páginas subsiguientes

Para obtener el siguiente conjunto de resultados en una respuesta paginada, debe realizar otra llamada de API al mismo extremo mientras aumenta el parámetro de `page` consulta en 1.

## Pasos siguientes

Ahora sabe cómo crear y supervisar trabajos de privacidad mediante la API de Privacy Service. Para obtener información sobre cómo realizar las mismas tareas mediante la interfaz de usuario, consulte la descripción general [de la interfaz de usuario de](../ui/overview.md)Privacy Service.
