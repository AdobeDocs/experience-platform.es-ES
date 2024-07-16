---
keywords: clasificación de texto;Clasificación de texto
solution: Experience Platform
title: Clasificación de texto en el contenido y la API de Commerce AI
description: El servicio de clasificación de texto, cuando recibe un fragmento de texto, puede clasificarlo en una o más etiquetas. La clasificación puede ser de una sola etiqueta, de varias etiquetas o jerárquica.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# Clasificación de texto

>[!NOTE]
>
>La IA de Content and Commerce está en versión beta. La documentación está sujeta a cambios.

El servicio de clasificación de texto, cuando recibe un fragmento de texto, puede clasificarlo en una o más etiquetas. La clasificación puede ser de una sola etiqueta, de varias etiquetas o jerárquica.

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud clasifica el texto de un fragmento según los parámetros de entrada proporcionados en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se usa. Verifique que cuenta con el `analyzer_id` apropiado antes de realizar su solicitud. Póngase en contacto con el equipo beta de Content y Commerce AI para recibir su `analyzer_id` para este servicio.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `analyzer_id` | El ID de servicio [!DNL Sensei] en el que se implementó su solicitud. Este identificador determina cuáles de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de Contenido y Commerce AI para configurar un ID personalizado. | Sí |
| `application-id` | El ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON y cada objeto de la matriz que representa un documento. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data`. Cualquiera de las propiedades restantes descritas a continuación en esta tabla se puede anular desde dentro de `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada es parte del cuerpo de la solicitud o una URL firmada para un bloque de S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | Formato de codificación del texto de entrada. Puede ser `utf-8` o `utf-16`. El valor predeterminado de esta propiedad es `utf-8`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual se deben devolver los resultados. Utilice el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | El número de resultados que se van a devolver (no puede ser un entero negativo). Utilice el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devuelto es el menor de los establecidos. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Parámetros personalizados que se van a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. | No |
| `content-id` | ID único del elemento de datos que se devuelve en la respuesta. Si no se pasa, se asigna un ID generado automáticamente. | No |
| `content` | El contenido utilizado por el servicio de clasificación de texto. El contenido puede ser texto sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (&#39;s3-bucket&#39; content-type), pase la dirección URL firmada. | Sí |

**Respuesta**

Una respuesta correcta devuelve el texto clasificado en una matriz de respuestas.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
