---
keywords: clasificación de texto;Clasificación de texto
solution: Experience Platform
title: Clasificación de texto en la API de IA de contenido y comercio
description: El servicio de clasificación de texto, cuando recibe un fragmento de texto, puede clasificarlo en una o más etiquetas. La clasificación puede ser de una sola etiqueta, de varias etiquetas o jerárquica.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: 081e31727b4e78126e60896b3b850c5589526152
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# Clasificación de texto

>[!NOTE]
>
>Content and Commerce AI está en versión beta. La documentación está sujeta a cambios.

El servicio de clasificación de texto, cuando recibe un fragmento de texto, puede clasificarlo en una o más etiquetas. La clasificación puede ser de una sola etiqueta, de varias etiquetas o jerárquica.

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud clasifica el texto de un fragmento según los parámetros de entrada proporcionados en la carga útil. Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina cuál [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone de los `analyzer_id` antes de realizar la solicitud. Póngase en contacto con el equipo beta de Content and Commerce AI para recibir su `analyzer_id` para este servicio.

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
| `analyzer_id` | El [!DNL Sensei] ID de servicio en el que se implementa la solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de inteligencia artificial aplicada al contenido y al comercio para configurar un ID personalizado. | Sí |
| `application-id` | El ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON y cada objeto de la matriz que representa un documento. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de `data` matriz. Cualquiera de las propiedades restantes descritas a continuación en esta tabla se puede anular desde `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada es parte del cuerpo de la solicitud o una URL firmada para un bloque de S3. El valor predeterminado de esta propiedad es `inline`. | No |
| `encoding` | Formato de codificación del texto de entrada. Esto puede ser `utf-8` o `utf-16`. El valor predeterminado de esta propiedad es `utf-8`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual se deben devolver los resultados. Utilice el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | El número de resultados que se van a devolver (no puede ser un entero negativo). Utilice el valor `0` para devolver todos los resultados. Cuando se usa en conjunto con `threshold`, el número de resultados devueltos es el menor de los establecidos. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Parámetros personalizados que se van a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. | No |
| `content-id` | ID único del elemento de datos que se devuelve en la respuesta. Si no se pasa, se asigna un ID generado automáticamente. | No |
| `content` | El contenido utilizado por el servicio de clasificación de texto. El contenido puede ser texto sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (tipo de contenido &quot;s3-bucket&quot;), pase la URL firmada. | Sí |

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
