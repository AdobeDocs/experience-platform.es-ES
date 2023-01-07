---
keywords: Experience Platform;introducción;ai de contenido;ai de comercio;ai de contenido y comercio;extracción de color;extracción de color
solution: Experience Platform
title: Extracción de color en la API de IA de contenido y comercio
description: El servicio de extracción de color, cuando se proporciona una imagen, puede calcular el histograma de colores de píxeles y ordenarlos mediante colores dominantes en bloques.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Extracción de color

>[!NOTE]
>
>[!DNL Content and Commerce AI] está en versión beta. La documentación está sujeta a cambios.

El servicio de extracción de color, cuando se proporciona una imagen, puede calcular un histograma de colores de píxeles y ordenarlos mediante colores dominantes en bloques. Los colores de los píxeles de la imagen se agrupan en 40 colores predominantes que son representativos del espectro de colores. A continuación, se calcula un histograma de valores de color entre esos 40 colores. El servicio tiene dos variantes:

**Extracción de color (imagen completa)**

Este método extrae un histograma de color en toda la imagen.

**Extracción de color (con máscara)**

Este método utiliza un extractor en primer plano basado en el aprendizaje profundo para identificar los objetos en primer plano. El modelo está formado en un catálogo de imágenes de comercio electrónico. Una vez extraído el objeto frontal, un histograma se calcula sobre los colores dominantes como se describió anteriormente.

Se ha utilizado la siguiente imagen en el ejemplo mostrado en este documento:

![imagen de prueba](../images/QQAsset1.jpg)

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud de ejemplo utiliza el método de imagen completa para la extracción de color.

La siguiente solicitud extrae colores de una imagen en función de los parámetros de entrada proporcionados en la carga útil. Consulte la tabla siguiente a la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone del `analyzer_id` antes de realizar la solicitud. Para el servicio de extracción de color, la variable `analyzer_id` El ID es:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
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
| `data` | Matriz que contiene objetos JSON. Cada objeto de la matriz representa una imagen. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data` matriz. Las propiedades restantes que se describen a continuación en esta tabla se pueden sobrescribir desde `data`. | Sí |
| `content-id` | ID exclusivo del elemento de datos que se devuelve en la respuesta. Si no se pasa esto, se asigna un ID generado automáticamente. | No |
| `content` | El contenido que debe analizar el servicio de extracción de color. En caso de que la imagen forme parte del cuerpo de la solicitud, utilice `-F file=@<filename>` en el comando curl para pasar la imagen, dejando este parámetro como una cadena vacía. <br> Si la imagen es un archivo en S3, pase la url firmada. Cuando el contenido forma parte del cuerpo de la solicitud, la lista de elementos de datos solo debe tener un objeto. Si se pasa más de un objeto, solo se procesa el primer objeto. | Sí |
| `content-type` | Se utiliza para indicar si la entrada forma parte del cuerpo de la solicitud o si es una url firmada para un compartimento S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | El formato de archivo de la imagen de entrada. Actualmente solo se pueden procesar imágenes de JPEG y PNG. El valor predeterminado de esta propiedad es `jpeg`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilizar el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un número entero negativo). Utilizar el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devueltos es el menor de ambos conjuntos de límites. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Cualquier parámetro personalizado que se vaya a pasar. | No |
| `historic-metadata` | Matriz que puede pasarse metadatos. | No |

**Respuesta**

Una respuesta correcta devuelve los detalles de los colores extraídos. Cada color se representa mediante un `feature_value` , que contiene la siguiente información:

- Un nombre de color
- Porcentaje que aparece este color en relación con la imagen
- El valor de RGB del color

En el primer objeto de ejemplo siguiente, la variable `feature_value` de `White,0.59,251,251,243` significa que el color encontrado es blanco, el blanco se encuentra en el 59% de la imagen, y tiene un valor RGB de 251,251,243.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Propiedad | Descripción |
| --- | --- |
| `content_id` | El nombre de la imagen que se cargó en la solicitud del POST. |
| `feature_value` | Matriz cuyos objetos contienen claves con el mismo nombre de propiedad. Estas claves contienen una cadena que representa el nombre del color, un porcentaje en el que aparece este color en relación con la imagen enviada en la variable `content_id`y el valor RGB del color. |
