---
keywords: OCR;presencia de texto;reconocimiento óptico de caracteres
solution: Experience Platform
title: Presencia de texto y reconocimiento óptico de caracteres
description: En la API de AI de contenido y comercio, el servicio de presencia de texto / reconocimiento óptico de caracteres (OCR) puede indicar si hay texto en una imagen determinada. Si hay texto, OCR puede devolver el texto.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Presencia de texto y reconocimiento óptico de caracteres

>[!NOTE]
>
>La API de contenido y comercio está en fase beta. La documentación está sujeta a cambios.

El servicio Presencia de texto / Reconocimiento óptico de caracteres (OCR), cuando se le da una imagen, puede indicar si el texto está presente en la imagen. Si hay texto, OCR puede devolver el texto.

La siguiente imagen se utilizó en la solicitud de ejemplo mostrada en este documento:

![imagen de prueba](../images/shef.jpeg)

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud comprueba si hay texto presente en función de la imagen de entrada proporcionada en la carga útil. Consulte la tabla siguiente a la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone del `analyzer_id` antes de realizar la solicitud. Póngase en contacto con el equipo beta de Content and Commerce AI para recibir su `analyzer_id` para este servicio.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
    }]
  }'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `analyzer_id` | La variable [!DNL Sensei] ID de servicio en el que se implementa su solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de AI de contenido y comercio para configurar un ID personalizado. | Sí |
| `application-id` | ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON con cada objeto en la matriz que representa una imagen pasada. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data` matriz. Las propiedades restantes que se describen a continuación en esta tabla se pueden sobrescribir desde `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada forma parte del cuerpo de la solicitud o si es una url firmada para un compartimento S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | El formato de archivo de la imagen de entrada. Actualmente solo se pueden procesar imágenes de JPEG y PNG. El valor predeterminado de esta propiedad es `jpeg`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilizar el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un número entero negativo). Utilizar el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devueltos es el menor de ambos conjuntos de límites. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Cualquier parámetro personalizado que se vaya a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. | No |
| `content-id` | ID exclusivo del elemento de datos que se devuelve en la respuesta. Si no se pasa esto, se asigna un ID generado automáticamente. | No |
| `content` | El contenido puede ser una imagen sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (tipo de contenido s3-bucket), pase la dirección URL firmada. | Sí |

**Respuesta**

Una respuesta correcta devuelve el texto detectado en la variable `feature_value` matriz. El texto se lee y se devuelve de arriba a abajo de izquierda a derecha. Esto significa que si se detectó &quot;Me encanta el Adobe&quot;, su carga útil devuelve &quot;I&quot;, &quot;Me encanta&quot; y &quot;Adobe&quot; en objetos separados. En el objeto al que se le asigna una `feature_name` que contiene la palabra y un `feature_value` que contiene una métrica de confianza para ese texto.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
