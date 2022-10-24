---
title: Personalización a través de Adobe Target
description: Aprenda a utilizar la API del servidor para ofrecer y procesar experiencias personalizadas creadas en Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: d6573f8f4d779fb7ed11b44561a0ad9667748b27
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 3%

---

# Personalización a través de Adobe Target

## Información general {#overview}

La API de servidor de red perimetral puede ofrecer y procesar experiencias personalizadas creadas en Adobe Target, con la ayuda del [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>Experiencias de personalización creadas a través de la variable [Compositor de experiencias visuales (VEC) de Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) no son totalmente compatibles con la API del servidor. La API del servidor puede **retrieve** actividades creadas por VEC, pero la API del servidor no puede **render** actividades creadas por VEC. Si desea procesar las actividades creadas por VEC, utilice la variable [SDK web](../edge/home.md).

## Configurar el conjunto de datos {#configure-your-datastream}

Antes de poder usar la API de servidor junto con Adobe Target, debe activar la personalización de Adobe Target en la configuración del conjunto de datos.

Consulte la [guía sobre la adición de servicios a un conjunto de datos](../edge/datastreams/overview.md#adobe-target-settings), para obtener información detallada sobre cómo habilitar Adobe Target.

Al configurar el conjunto de datos, puede (opcionalmente) proporcionar valores para [!DNL Property Token], [!DNL Target Environment ID]y [!DNL Target Third Party ID Namespace].

![La imagen de la interfaz de usuario muestra la pantalla de configuración del servicio datastream, con Adobe Target seleccionado](assets/target-datastream.png)

Puede elegir entre lo siguiente [!DNL Analytics Logging] opciones:

* **[!DNL Server Side]**: Esta es la opción predeterminada para [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es). Cuando se selecciona esta opción, cada vez que Target devuelve el contenido personalizado, se muestra la variable [!DNL A4T] los datos se envían automáticamente a Analytics en función de la respuesta del motor de personalización de Target.
* **[!DNL Client Side]**: Cuando se selecciona esta opción, cada vez que Target devuelve el contenido personalizado, se muestra la variable [!DNL A4T] se devuelven datos a la aplicación que realiza la llamada. Si tiene intención de registrar estos datos en Analytics, debe asegurarse de que se incluyen en los informes en una llamada posterior a [!DNL Analytics].

   >[!IMPORTANT]
   >
   >Además de seleccionar **[!UICONTROL Lado del cliente]** en la configuración de Target, también debe deshabilitar Analytics para que la red perimetral devuelva la variable [!DNL A4T] volver a la respuesta.


## Parámetros personalizados {#custom-parameters}

La mayoría de los campos de la [!DNL XDM] parte de cada solicitud se serializa en notación de puntos y luego se envía a Target como personalizado o [!DNL mbox] parámetros.


### Ejemplo {#custom-parameters-example}

Dadas las siguientes muestras XDM:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Al crear audiencias en Target, los siguientes valores estarán disponibles como parámetros personalizados:

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Actualizaciones de perfil de Target {#profile-update}

La variable [!DNL Server API] permite actualizar el perfil de Target. Para actualizar un perfil de Target, asegúrese de que los datos de perfil se pasen en la variable `data` de la solicitud con el siguiente formato:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Consulta de actividades de Target {#querying-target-activities}

### Esquemas {#schemas}

La parte de consulta de la solicitud determina qué contenido devuelve Target. En el `personalization` objeto, `schemas` determina el tipo de contenido que Target devolverá.

En situaciones en las que no esté seguro de qué tipo de ofertas va a recuperar, debe incluir los cuatro esquemas en la consulta de personalización a la red perimetral:

* **Ofertas basadas en HTML:**
https://ns.adobe.com/personalization/html-content-item
* **Ofertas basadas en JSON:**
https://ns.adobe.com/personalization/json-content-item
* **Ofertas de redireccionamiento de Target**
https://ns.adobe.com/personalization/redirect-item
* **Ofertas de manipulación DOM de Target**
https://ns.adobe.com/personalization/dom-action

### Ámbitos de decisión {#decision-scopes}

Adobe Target [!DNL mbox] los nombres deben incluirse en la variable `decisionScopes` para devolver el contenido adecuado.

#### Ejemplo {#decision-scopes-example}

En el ejemplo siguiente, se solicitan los cuatro tipos de oferta junto con una actividad de Target llamada `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
      ]
   }
}
```

## Ejemplo de llamada a la API {#api-example}

**Formato de API**

```http
POST /ee/v2/interact
```

### Solicitud {#request}

A continuación se describe una solicitud completa que incluye un objeto XDM completo, parámetros de perfil y la consulta de Target apropiada.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Respuesta {#response}

La red perimetral devolverá una respuesta similar a la que se muestra a continuación.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Si el visitante cumple los requisitos para una actividad de personalización basada en los datos enviados a Adobe Target, el contenido de la actividad relevante se encuentra en la sección `handle` objeto, donde el tipo es `personalization:decisions`.

En ocasiones, se devuelve otro contenido en `handle` también. Otros tipos de contenido no son relevantes para la personalización de Target. Si el visitante cumple los requisitos para varias actividades, cada actividad será independiente `personalization` en la matriz.

En la tabla siguiente se explican los elementos clave de esa parte de la respuesta.

| Propiedad | Descripción | Ejemplo |
|---|---|---|
| `scope` | El nombre de mbox de Target que generó las ofertas propuestas. | `"scope": "serverapimbox"` |
| `items[].schema` | Esquema del contenido asociado con la oferta propuesta. Esto está relacionado con el tipo de actividad que seleccionó al crear la actividad de personalización. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | ID exclusivo de la actividad de oferta. Normalmente es un número de 6 dígitos. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Nombre de la actividad de oferta especificada por el usuario. Esto se proporciona durante el paso de creación de la actividad. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | ID exclusivo de la experiencia de personalización. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Nombre exclusivo de la experiencia de personalización. | `"experience.name": "Experience A"` |
| `items[].data.id` | El ID de la oferta propuesta. | `"id": "282484"` |
| `items[].data.format` | El formato del contenido asociado con la oferta propuesta. | `"format: "application/json` |
| `items[].data.content` | Contenido asociado con la oferta propuesta. Se utilizará para la personalización del contenido de la aplicación que realiza la llamada. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
