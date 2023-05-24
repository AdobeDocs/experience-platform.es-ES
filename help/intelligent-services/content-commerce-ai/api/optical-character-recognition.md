---
keywords: OCR;presencia de texto;reconocimiento óptico de caracteres
solution: Experience Platform
title: Presencia de texto y reconocimiento óptico de caracteres
description: En la API de etiquetado de contenido, el servicio Presencia de texto/Reconocimiento óptico de caracteres (OCR) puede indicar si hay texto en una imagen determinada. Si el texto está presente, OCR puede devolver el texto.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 4%

---

# Presencia de texto y reconocimiento óptico de caracteres

El servicio Presencia de texto/Reconocimiento óptico de caracteres (OCR), cuando se proporciona una imagen, puede indicar si hay texto en la imagen. Si el texto está presente, OCR puede devolver el texto.

La siguiente imagen se utilizó en la solicitud de ejemplo que se muestra en este documento:

![Imagen de muestra](../images/sample_image.png)

**Formato de API**

```http
POST /services/v2/predict
```

**Solicitud**

La siguiente solicitud comprueba si hay texto en función de la imagen de entrada proporcionada en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

Ejecución con imagen en línea:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Respuesta**

Una respuesta correcta devuelve el texto detectado en la variable `tags` para cada imagen que se pasó en la solicitud. Si no hay texto en una imagen determinada, `is_text_present` es 0 y `tags` es una lista vacía.

[result0, result1, ...]: lista de respuestas para cada documento de entrada. Cada resultado es un diccionario con claves:

1. request_element_id: índice correspondiente al archivo de entrada para esta respuesta, 0 para la primera imagen de la lista de documentos de la solicitud, 1 para la siguiente, etc.
2. etiquetas: lista de diccionarios, cada diccionario tiene dos claves: texto, que es una palabra reconocida de la imagen, y relevancia, que se calcula como la fracción del área del cuadro delimitador del texto extraído en comparación con la imagen completa. 0,01 se traduciría en un texto que ocupe al menos el 1 % de la imagen.
3. is_text_present: 0 o 1 según si el texto está presente en la imagen. Si las etiquetas son 0, la lista está vacía.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Solicitud**

La siguiente solicitud comprueba si hay texto en función de la imagen de entrada proporcionada en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

Ejecución con URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `documents` | Lista de elementos JSON con cada elemento en la lista que representa una imagen. Los parámetros que se pasan como parte de esta lista anulan el parámetro global especificado fuera de la lista para el elemento de lista correspondiente. | Sí |
| `sensei:multipart_field_name` | field_name para leer la ruta del archivo de entrada. | Sí |
| `repo:path` | URL asignada al recurso de imagen. | Sí |
| `sensei:repoType` | &quot;HTTP&quot; (para presigned-url). | No |
| `dc:format` | Formato codificado de la imagen de entrada. Solo se permiten formatos de imagen como jpeg, jpg, png y tiff para la codificación de imágenes. Dc:format se compara con los formatos permitidos. | No |
| `correct_with_dictionary` | ¿Si corregir las palabras con un diccionario de inglés? Si no está activada, podría reconocer palabras que no estén en inglés. El valor predeterminado es True: activado.) Tenga en cuenta que cuando el diccionario está activado, no es necesario que siempre obtenga una palabra en inglés. Intentamos corregirlo, pero si no es posible dentro de una cierta distancia de edición, devolvemos la palabra original. | No |
| `filter_with_dictionary` | ¿Si se filtran las palabras para que contengan solo las del diccionario inglés? Si se activa, las palabras devueltas siempre pertenecerán al gran inglés , que comprende 470.000 palabras. | No |
| `min_probability` | ¿Cuál es la probabilidad mínima de las palabras reconocidas? El servicio solo devuelve las palabras que se extraen de la imagen y que tienen una buena probabilidad que min_probability. El valor predeterminado es 0,2. | No |
| `min_relevance` | ¿Cuál es la relevancia mínima de las palabras reconocidas? El servicio solo devuelve las palabras que se extraen de la imagen y que tienen una relevancia buena a min_relevancia. El valor predeterminado es 0,01. La relevancia se calcula como la fracción del área del cuadro delimitador del texto extraído en comparación con la imagen completa. 0,01 se traduciría en un texto que ocupe al menos el 1 % de la imagen. | No |

| Nombre | Tipo de datos | Requerido | Predeterminado | Valores | Descripción |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL con prefijo de la imagen de la que se debe extraer el texto. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de repositorio donde se almacena la imagen. |
| `sensei:multipart_field_name` | string | - | - | - | Utilícelo al pasar la imagen como un argumento de varias partes en lugar de usar direcciones URL prefirmadas. |
| `dc:format` | string | Sí | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | La codificación de imagen se comprueba con los tipos de codificación de entrada permitidos antes de procesarse. |