---
keywords: Experience Platform;introducción;contenido;etiquetado de contenido;etiquetado de color;extracción de color;
solution: Experience Platform
title: Etiquetado de colores en la API de etiquetado de contenido
description: Cuando se proporciona una imagen, el servicio de etiquetado de color puede calcular el histograma de colores de píxeles y ordenarlos por colores dominantes en bloques.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 5%

---

# Etiquetado de color

El servicio de etiquetado de colores, cuando se proporciona una imagen, puede calcular un histograma de colores de píxeles y ordenarlos por colores dominantes en bloques. Los colores de los píxeles de la imagen se agrupan en 40 colores predominantes que son representativos del espectro de colores. A continuación, se calcula un histograma de los valores de color entre esos 40 colores. El servicio tiene dos variantes:

**Etiquetado de colores (imagen completa)**

Este método extrae un histograma de colores en toda la imagen.

**Etiquetado de colores (con máscara)**

Este método utiliza un extractor de primer plano basado en aprendizaje profundo para identificar objetos en primer plano. El modelo está formado sobre un catálogo de imágenes de comercio electrónico. Una vez extraído el objeto en primer plano, se calcula un histograma sobre los colores dominantes como se describió anteriormente.

La siguiente imagen se utilizó en el ejemplo mostrado en este documento:

![imagen de prueba](../images/QQAsset1.jpg)

**Formato de API**

```http
POST /services/v2/predict
```

**Solicitud**

La siguiente solicitud de ejemplo utiliza el método de imagen completa para el etiquetado de colores.

La siguiente solicitud extrae colores de una imagen en función de los parámetros de entrada proporcionados en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `application-id` | El ID de la aplicación creada. | Sí |
| `documents` | Una lista de elementos JSON con cada elemento en la lista que representa un documento. | Sí |
| `top_n` | El número de resultados que se van a devolver (no puede ser un entero negativo). Utilice el valor `0` para devolver todos los resultados. Cuando se usa en conjunto con `threshold`, el número de resultados devueltos es el menor de los establecidos. El valor predeterminado de esta propiedad es `0`. | No |
| `min_coverage` | Umbral de cobertura por encima del cual se deben devolver los resultados. Excluya el parámetro para devolver todos los resultados. | No |
| `resize_image` | Indica si se va a cambiar el tamaño de la imagen de entrada. De forma predeterminada, se cambia el tamaño de las imágenes a 320*320 píxeles antes de realizar el etiquetado de colores. Para fines de depuración, también podemos permitir que el código se ejecute en imagen completa, estableciendo este valor en False. | No |
| `enable_mask` | Activa/Desactiva el etiquetado de color en la máscara. | No |

| Nombre | Tipo de datos | Requerido | Predeterminado | Valores | Descripción |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | Dirección URL del documento del que se extraerán las frases clave. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de repositorio donde se almacena la imagen. |
| `sensei:multipart_field_name` | string | - | - | - | Utilícelo al pasar un archivo de imagen como argumento de varias partes en lugar de utilizar direcciones URL prefirmadas. |
| `dc:format` | string | Sí | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | La codificación de imagen se comprueba con los tipos de codificación de entrada permitidos antes de procesarse. |

**Respuesta**

Una respuesta correcta devuelve los detalles de los colores extraídos. Cada color se representa mediante una `feature_value` , que contiene la siguiente información:

- Un nombre de color
- El porcentaje en que aparece este color en relación con la imagen
- El valor RGB del color

En el primer objeto de ejemplo siguiente, la variable `feature_value` de `Mud_Green,0.069,102,72,95` significa que el color encontrado es verde barro, el verde barro se encuentra en el 6,9% de la imagen y tiene un valor RGB de 102,72,95.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
