---
keywords: Experience Platform;introducción;contenido;etiquetado de contenido;etiquetado de color;extracción de color;
solution: Experience Platform
title: Etiquetado de colores en la API de etiquetado de contenido
description: El servicio Etiquetado de colores, cuando se proporciona una imagen, puede calcular el histograma de colores de píxeles y ordenarlos mediante colores dominantes en bloques.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 6%

---

# Etiquetado de colores

El servicio de etiquetado de color, cuando se proporciona una imagen, puede calcular un histograma de colores de píxeles y ordenarlos mediante colores dominantes en bloques. Los colores de los píxeles de la imagen se agrupan en 40 colores predominantes que son representativos del espectro de colores. A continuación, se calcula un histograma de valores de color entre esos 40 colores. El servicio tiene dos variantes:

**Etiquetado de colores (imagen completa)**

Este método extrae un histograma de color en toda la imagen.

**Etiquetado de colores (con máscara)**

Este método utiliza un extractor en primer plano basado en el aprendizaje profundo para identificar los objetos en primer plano. Una vez extraídos los objetos en primer plano, se calcula un histograma sobre los colores dominantes tanto para las regiones en primer plano como para las de fondo, junto con toda la imagen.

**Extracción de tono**

Además de las variantes mencionadas anteriormente, puede configurar el servicio para recuperar un histograma de tonos para:

- La imagen general (cuando se utiliza la variante de imagen completa)
- La imagen general y las regiones de primer y segundo plano (al usar la variante con máscara)

Se ha utilizado la siguiente imagen en el ejemplo mostrado en este documento:

![imagen de prueba](../images/QQAsset1.jpg)

**Formato de API**

```http
POST /services/v2/predict
```

**Solicitud: variante de imagen completa**

La siguiente solicitud de ejemplo utiliza el método de imagen completa para el etiquetado de color y extrae colores de una imagen en función de los parámetros de entrada proporcionados en la carga útil. Consulte la tabla siguiente a la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Respuesta: variante de imagen completa**

Una respuesta correcta devuelve los detalles de los colores extraídos. Cada color se representa mediante un `feature_value` , que contiene la siguiente información:

- Un nombre de color
- Porcentaje que aparece este color en relación con la imagen
- El valor de RGB del color

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`significa que el color encontrado es blanco, que se encuentra en el 58,34% de la imagen, y tiene un valor de RGB promedio de 254, 254, 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Observe que el resultado aquí tiene un color extraído en la región de imagen &quot;general&quot;.

**Solicitud: variante de imagen enmascarada**

La siguiente solicitud de ejemplo utiliza el método de máscara para el etiquetado de color. Esto se habilita configurando la variable `enable_mask` parámetro a `true` en la solicitud.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>Además, la variable `retrieve_tone` parámetro también se establece en `true` en la solicitud anterior. Esto nos permite recuperar un histograma de distribución de tono sobre tonos cálidos, neutros y frescos en las regiones generales, frontales y de fondo de la imagen.

**Respuesta: variante de imagen enmascarada**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Además de los colores de la imagen general, ahora también puede ver los colores de las regiones de primer y segundo plano. Dado que la recuperación de tono está habilitada para cada una de las regiones anteriores, también puede recuperar el histograma de un tono.

**Parámetros de entrada**

| Nombre | Tipo de datos | Requerido | Predeterminado | Valores | Descripción |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Sí | - | Vea lo siguiente | Lista de elementos JSON con cada elemento en la lista que representa un documento. |
| `top_n` | number | No | 0 | Entero no negativo | Número de resultados que se van a devolver. 0, para devolver todos los resultados. Cuando se utiliza junto con el umbral, el número de resultados devueltos es menor que cualquiera de los límites. |
| `min_coverage` | number | No | 0.05 | Número real | Umbral de la cobertura por encima del cual deben devolverse los resultados. Exclude parameter para devolver todos los resultados. |
| `resize_image` | number | No | True | True/False | Indica si se debe cambiar el tamaño de la imagen de entrada o no. De forma predeterminada, el tamaño de las imágenes cambia a 320*320 píxeles antes de realizar la extracción de color. Para fines de depuración, también podemos permitir que el código se ejecute en una imagen completa, configurándolo en `False`. |
| `enable_mask` | number | No | False | True/False | Activa/desactiva la extracción de color |
| `retrieve_tone` | number | No | False | True/False | Activa/desactiva la extracción de tono |

**Objeto de documento**

| Nombre | Tipo de datos | Requerido | Predeterminado | Valores | Descripción |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL prefirmada del documento. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo de cesión temporal en la que se almacena la imagen. |
| `sensei:multipart_field_name` | string | - | - | - | Utilice esto cuando pase el archivo de imagen como un argumento de varias partes en lugar de usar direcciones URL prefirmadas. |
| `dc:format` | string | Sí | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | La codificación de imagen se comprueba para los tipos de codificación de entrada permitidos antes de procesarse. |