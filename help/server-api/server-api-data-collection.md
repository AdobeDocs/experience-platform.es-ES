---
title: Recopilación de datos
description: Descubra cómo la API de Adobe Experience Platform Edge Network Server estructura los datos recopilados.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---


# Recopilación de datos

[!DNL Server API] ofrece dos tipos de extremos de recopilación de datos:

* [Extremos de recopilación de datos interactivos](interactive-data-collection.md), utilizados cuando el cliente espera que el servidor devuelva una respuesta. Estos extremos también pueden devolver contenido de otros servicios de Edge Network, mientras realizan la recopilación de datos.
* [Recopilación de datos de evento no interactiva](non-interactive-data-collection.md), utilizada cuando no se espera ninguna respuesta del servidor. Estos extremos solo se utilizan para la recopilación de datos.

## `Event` objeto {#event-object}

Los datos recopilados por [!DNL Server API] están estructurados en el objeto `Event`. A continuación se describe la estructura de este objeto.

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `xdm` | Objeto | *Requerido*. Objeto JSON que contiene datos en formato XDM, correspondiente al esquema del conjunto de datos. |
| `data` | Objeto | *Opcional*. Objeto JSON que contiene datos de forma libre que el Edge Network puede asignar a XDM. |

