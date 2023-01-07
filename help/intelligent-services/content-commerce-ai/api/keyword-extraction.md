---
keywords: Experience Platform;introducción;ai de contenido;ai de comercio;ai de contenido y comercio;extracción de palabras clave;extracción de palabras clave
solution: Experience Platform
title: Extracción de palabras clave en la API de AI de contenido y comercio
description: El servicio de extracción de palabras clave, cuando se le da un documento de texto, extrae automáticamente palabras clave o jerarquías que describan mejor el asunto del documento. Para extraer palabras clave, se utiliza una combinación de algoritmos de extracción de palabras clave sin supervisión y reconocimiento de entidad con nombre (NER).
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# Extracción de palabras clave

>[!NOTE]
>
>[!DNL Content and Commerce AI] está en versión beta. La documentación está sujeta a cambios.

El servicio de extracción de palabras clave, cuando se le da un documento de texto, extrae automáticamente palabras clave o jerarquías que describan mejor el asunto del documento. Para extraer palabras clave, se utiliza una combinación de algoritmos de extracción de palabras clave sin supervisión y reconocimiento de entidad con nombre (NER).

Las entidades con nombre reconocidas por [!DNL Content and Commerce AI] se enumeran en la siguiente tabla:

| Nombre de la entidad | Descripción |
| --- | --- |
| PERSONA | Personas, incluyendo ficción. |
| NORP | Nacionalidades o grupos religiosos o políticos. |
| GPE | Países, ciudades y estados. |
| LOC | Lugares no GPE, cordilleras, masas de agua. |
| FAC | Edificios, aeropuertos, autopistas, puentes, etc. |
| ORG | Empresas, agencias, instituciones, etc. |
| PRODUCTO | Objetos, vehículos, alimentos, etc. (No servicios). |
| EVENT | Nombrados huracanes, batallas, guerras, eventos deportivos, etc. |
| WORK_OF_ART | Títulos de libros, canciones, etc. |
| LEY | Documentos con nombre convertidos en leyes. |
| IDIOMA | Cualquier idioma con nombre. |

>[!NOTE]
>
>Si planea procesar PDF, vaya a las instrucciones para [Extracción de palabras clave del PDF](#pdf-extraction) dentro de este documento. Además, la compatibilidad con tipos de archivo adicionales como docx, ppt, amd xml se configuran para su lanzamiento en una fecha posterior.

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud extrae palabras clave de un documento en función de los parámetros de entrada proporcionados en la carga útil.

JSON simplificado del archivo de entrada:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Consulte la tabla siguiente a la carga útil de ejemplo para obtener más información sobre los parámetros de entrada que se muestran.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone del `analyzer_id` antes de realizar la solicitud. Para el servicio de extracción de palabras clave, la variable `analyzer_id` El ID es:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

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
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `analyzer_id` | La variable [!DNL Sensei] ID de servicio en el que se implementa su solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de AI de contenido y comercio para configurar un ID personalizado. | Sí |
| `application-id` | El ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON y cada objeto de la matriz representa un documento. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data` matriz. Las propiedades restantes que se describen a continuación en esta tabla se pueden sobrescribir desde `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada forma parte del cuerpo de la solicitud o si es una url firmada para un compartimento S3. El valor predeterminado de esta propiedad es `inline`. | Sí |
| `encoding` | El formato de codificación del texto de entrada. Esto puede ser `utf-8` o `utf-16`. El valor predeterminado de esta propiedad es `utf-8`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilizar el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un número entero negativo). Utilizar el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devueltos es el menor de ambos conjuntos de límites. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Cualquier parámetro personalizado que se vaya a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. Consulte la [apéndice](#appendix) para obtener más información sobre los parámetros personalizados. | No |
| `content-id` | ID exclusivo del elemento de datos que se devuelve en la respuesta. Si no se pasa esto, se asigna un ID generado automáticamente. | No |
| `content` | Contenido utilizado por el servicio de extracción de palabras clave. El contenido puede ser texto sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (tipo de contenido s3-bucket), pase la dirección url firmada. Cuando el contenido forma parte del cuerpo de la solicitud, la lista de elementos de datos solo debe tener un objeto. Si se pasa más de un objeto, solo se procesa el primer objeto. | Sí |

**Respuesta**

Una respuesta correcta devuelve un objeto JSON que contiene palabras clave extraídas en la variable `response` matriz.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## Extracción de palabras clave del PDF {#pdf-extraction}

El servicio de extracción de palabras clave admite PDF; sin embargo, es necesario utilizar un nuevo AnalyzerID para archivos de PDF y cambiar el tipo de documento a PDF. Consulte el ejemplo siguiente para obtener más información.

**Formato de API**

```http
POST /services/v1/predict
```

**Solicitud**

La siguiente solicitud extrae palabras clave de un documento de PDF en función de los parámetros de entrada proporcionados en la carga útil.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Compruebe que dispone del `analyzer_id` antes de realizar la solicitud. Para la extracción de palabras clave del PDF, la variable `analyzer_id` El ID es:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| `analyzer_id` | La variable [!DNL Sensei] ID de servicio en el que se implementa su solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utilizan. Para obtener servicios personalizados, póngase en contacto con el equipo de AI de contenido y comercio para configurar un ID personalizado. | Sí |
| `application-id` | El ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON y cada objeto de la matriz representa un documento. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la matriz `data` matriz. Las propiedades restantes que se describen a continuación en esta tabla se pueden sobrescribir desde `data`. | Sí |
| `language` | Idioma de entrada. El valor predeterminado es `en` (inglés). | No |
| `content-type` | Se utiliza para indicar el tipo de contenido de las entradas. Esto debe configurarse como `file`. | Sí |
| `encoding` | El formato de codificación de la entrada. Esto debe configurarse como `pdf`. Más tipos de codificación se configuran para que se admitan en una fecha posterior. | Sí |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilizar el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un número entero negativo). Utilizar el valor `0` para devolver todos los resultados. Cuando se usa junto con `threshold`, el número de resultados devueltos es el menor de ambos conjuntos de límites. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Cualquier parámetro personalizado que se vaya a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. Consulte la [apéndice](#appendix) para obtener más información sobre los parámetros personalizados. | No |
| `content-id` | ID exclusivo del elemento de datos que se devuelve en la respuesta. Si no se pasa esto, se asigna un ID generado automáticamente. | No |
| `content` | Esto debe configurarse como `file`. | Sí |

**Respuesta**

Una respuesta correcta devuelve un objeto JSON que contiene palabras clave extraídas en la variable `response` matriz.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Para obtener más información y un ejemplo sobre el uso de la extracción de PDF que contenga instrucciones sobre cómo configurar, implementar e integrar con el servicio de nube de AEM. Visite la [Repositorio de github de extracción de PDF CCAI](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Apéndice {#appendix}

La siguiente tabla contiene los parámetros disponibles que se pueden utilizar desde `custom`.

| Nombre | Descripción | Obligatorio |
| --- | --- | --- |
| `min-n` | El número mínimo de palabras necesarias en las palabras clave. | No |
| `entity-types` | Tipos de entidades a devolver. Consulte la tabla de reconocimiento de entidades con nombre al principio de este documento. | No |
