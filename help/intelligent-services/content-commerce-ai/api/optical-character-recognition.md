---
keywords: text classification;Text classification
solution: Experience Platform
title: Extremo de la API de clasificación de texto
topic: Developer guide
description: El servicio de clasificación de texto, cuando se le asigna un fragmento de texto, puede clasificarlo en una o varias etiquetas. La clasificación puede ser de una sola etiqueta, de varias etiquetas o jerárquica.
translation-type: tm+mt
source-git-commit: d57d4412ffd8beccc529681db559007a14ff8120
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---


# Presencia de texto y reconocimiento óptico de caracteres

>[!NOTE]
>
>Content and Commerce AI está en versión beta. La documentación está sujeta a cambios.

El servicio Presencia de texto / Reconocimiento óptico de caracteres (OCR), cuando se le proporciona una imagen, puede indicar si hay texto en la imagen. Si hay texto, OCR puede devolver el texto.

En la solicitud de ejemplo mostrada en este documento se utilizó la siguiente imagen:

![probar imagen](../images/shef.jpeg)

**Formato API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud comprueba si hay texto en función de la imagen de entrada proporcionada en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Verifique que dispone de la información adecuada `analyzer_id` antes de realizar su solicitud. Póngase en contacto con el equipo beta de Content and Commerce AI para recibir su `analyzer_id` solicitud de este servicio.

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
| `analyzer_id` | ID del [!DNL Sensei] servicio en el que se implementa la solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utiliza. Para obtener servicios personalizados, póngase en contacto con el equipo de Content and Commerce AI para configurar un ID personalizado. | Sí |
| `application-id` | ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON con cada objeto de la matriz que representa una imagen pasada. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la `data` matriz. Cualquiera de las propiedades restantes que se describen a continuación en esta tabla se puede sobrescribir desde dentro `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada es parte del cuerpo de la solicitud o una dirección URL firmada para un bucket S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | Formato de archivo de la imagen de entrada. Actualmente solo se pueden procesar imágenes JPEG y PNG. El valor predeterminado de esta propiedad es `jpeg`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilice el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un entero negativo). Utilice el valor `0` para devolver todos los resultados. Cuando se utiliza junto con `threshold`, el número de resultados devueltos es el menor de cualquiera de los límites establecidos. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Parámetros personalizados que se van a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. | No |
| `content-id` | ID única para el elemento de datos que se devuelve en la respuesta. Si no se pasa, se asigna un ID generado automáticamente. | No |
| `content` | El contenido puede ser una imagen sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (tipo de contenido &#39;s3-bucket&#39;), pase la dirección URL firmada. | Sí |

**Respuesta**

Una respuesta correcta devuelve el texto detectado en la `feature_value` matriz. El texto se lee y se devuelve de arriba abajo de izquierda a derecha. Esto significa que si se detectó &quot;Me encanta el Adobe&quot;, su carga útil devuelve &quot;I&quot;, &quot;Me encanta&quot; y &quot;Adobe&quot; en objetos separados. En el objeto se le asigna un `feature_name` contenido que contiene la palabra y un `feature_value` que contiene una métrica de confianza para ese texto.

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
