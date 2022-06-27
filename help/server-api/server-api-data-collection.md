---
title: Recopilación de datos
description: Descubra cómo la API de Adobe Experience Platform Edge Network Server estructura los datos recopilados.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 3%

---


# Recopilación de datos

La variable [!DNL Server API] ofrece dos tipos de extremos de recopilación de datos:

* [Puntos finales de recopilación de datos interactivos](interactive-data-collection.md), se utiliza cuando el cliente espera que el servidor devuelva una respuesta. Estos extremos también pueden devolver contenido de otros servicios de red perimetral al realizar la recopilación de datos.
* [Recopilación de datos de eventos no interactivos](non-interactive-data-collection.md), se utiliza cuando no se espera ninguna respuesta del servidor. Estos extremos solo se utilizan para la recopilación de datos.

## `Event` object {#event-object}

Los datos que recopila el [!DNL Server API] está estructurado en la variable `Event` objeto. A continuación se describe la estructura de este objeto.

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
| `xdm` | Objeto | *Requerido*. El objeto JSON que contiene datos en formato XDM, correspondiente al esquema del conjunto de datos. |
| `data` | Objeto | *Opcional*. El objeto JSON que contiene datos de forma libre, que la red perimetral puede asignar a XDM. |

