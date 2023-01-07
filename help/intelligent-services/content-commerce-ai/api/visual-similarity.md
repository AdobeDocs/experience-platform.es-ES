---
keywords: Similitud visual;similitud visual;api de ccai
solution: Experience Platform
title: Similitud visual en la API de AI de contenido y comercio
description: El servicio de similitud visual, cuando se le da una imagen, encuentra automáticamente imágenes visualmente similares de un catálogo.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Similitud visual

>[!NOTE]
>
>[!DNL Content and Commerce AI] está en versión beta. La documentación está sujeta a cambios.

El servicio de similitud visual, cuando se le da una imagen, encuentra automáticamente imágenes visualmente similares de un catálogo.

La siguiente imagen se utilizó en la solicitud de ejemplo mostrada en este documento:

![imagen de prueba](../images/Query_Image.jpeg)

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud recupera imágenes visualmente similares de un catálogo, en función de los parámetros de entrada proporcionados en la carga útil. Consulte la tabla siguiente a la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone del `analyzer_id` antes de realizar la solicitud. Póngase en contacto con el equipo beta de Content and Commerce AI para recibir su `analyzer_id` para este servicio.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {}
            }]
          }
      }
    ]
}'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `analyzer_id` | La variable [!DNL Sensei] ID de servicio en el que se implementa su solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de AI de contenido y comercio para configurar un ID personalizado. | Sí |
| `application-id` | El ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON y cada objeto de la matriz representa una imagen. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data` matriz. Las propiedades restantes que se describen a continuación en esta tabla se pueden sobrescribir desde `data`. | Sí |
| `content-id` | ID exclusivo del elemento de datos que se devuelve en la respuesta. Si no se pasa esto, se asigna un ID generado automáticamente. | No |
| `content` | El contenido que analiza el servicio de similitud visual. En caso de que la imagen forme parte del cuerpo de la solicitud, utilice `-F file=@<filename>` en el comando curl para pasar la imagen, dejando este parámetro como una cadena vacía. <br> Si la imagen es un archivo en S3, pase la url firmada. Cuando el contenido forma parte del cuerpo de la solicitud, la lista de elementos de datos solo debe tener un objeto. Si se pasa más de un objeto, solo se procesa el primer objeto. | Sí |
| `content-type` | Se utiliza para indicar si la entrada forma parte del cuerpo de la solicitud o si es una url firmada para un compartimento S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | El formato de archivo de la imagen de entrada. Actualmente solo se pueden procesar imágenes de JPEG y PNG. El valor predeterminado de esta propiedad es `jpeg`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilizar el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un número entero negativo). Utilizar el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devueltos es el menor de ambos conjuntos de límites. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Cualquier parámetro personalizado que se vaya a pasar. | No |
| `historic-metadata` | Matriz que puede pasarse metadatos. | No |

**Respuesta**

Una respuesta correcta devuelve un valor `response` matriz que contiene una `feature_value` y `feature_name` para cada una de las imágenes visualmente similares que se encuentran en el catálogo.

Se devolvieron las siguientes imágenes visualmente similares en la respuesta de ejemplo que se muestra a continuación:

![imágenes similares](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
