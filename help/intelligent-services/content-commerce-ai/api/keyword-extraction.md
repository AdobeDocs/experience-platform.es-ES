---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Extracción de color
topic: Developer guide
description: El servicio de extracción de palabras clave, cuando se le proporciona un documento de texto, extrae automáticamente palabras clave o frases clave que describan mejor el tema del documento. Para extraer palabras clave, se utiliza una combinación de algoritmos de extracción de palabras clave con nombre (NER) y sin supervisión.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---


# Extracción de palabras clave

>[!NOTE]
>
>[!DNL Content and Commerce AI] está en versión beta. La documentación está sujeta a cambios.

El servicio de extracción de palabras clave, cuando se le proporciona un documento de texto, extrae automáticamente palabras clave o frases clave que describan mejor el tema del documento. Para extraer palabras clave, se utiliza una combinación de algoritmos de extracción de palabras clave con nombre (NER) y sin supervisión.

**Extracción de palabras clave sin supervisión**

Para la extracción de palabras clave sin supervisión, se utiliza [[!DNL YAKE]](http://yake.inesctec.pt/) . [!DNL YAKE] es un método de extracción de palabras clave rápido y preciso, sin supervisión, que se utiliza para seleccionar las palabras clave más importantes de un documento. Las palabras clave [!DNL YAKE] extraídas se filtran para seleccionar solamente frases nuevas.

**Reconocimiento de entidad con nombre**

Para el reconocimiento de entidades con nombre, se utiliza el modelo OntoNotes de [[!DNL spaCy]](https://spacy.io/). Este modelo asigna vectores de token específicos de contexto, etiquetas de parte de voz (POS), análisis de dependencia y entidades con nombre. El modelo OntoNotes es uno de los [!DNL spaCy] modelos principales. Puede encontrar más información sobre el modelo OntoNotes [aquí](https://spacy.io/models/en).

Las entidades con nombre reconocidas por [!DNL Content and Commerce AI] se enumeran en la siguiente tabla:

| Nombre de entidad | Descripción |
| --- | --- |
| PERSONA | Personas, incluyendo ficción. |
| NORP | Nacionalidades o grupos religiosos o políticos. |
| GPE | Países, ciudades y estados. |
| LOC | Lugares sin GPE, cordilleras, masas de agua. |
| FAC | Edificios, aeropuertos, autopistas, puentes, etc. |
| ORG | Compañías, agencias, instituciones, etc. |
| PRODUCTO | Objetos, vehículos, alimentos, etc. (No servicios). |
| EVENTO | Huracanes, batallas, guerras, eventos deportivos, etc. con nombre. |
| WORK_OF_ART | Títulos de libros, canciones, etc. |
| LEY | Los documentos designados se convierten en leyes. |
| IDIOMA | Cualquier idioma con nombre. |

Los resultados de [!DNL OntoNotes] se combinan con las palabras clave de [!DNL YAKE], y luego se devuelven en orden de clasificación según su importancia.

**Formato API**

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

Consulte la tabla debajo de la carga útil de ejemplo para obtener más información sobre los parámetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qué [!DNL Sensei Content Framework] se utiliza. Verifique que dispone de la información adecuada `analyzer_id` antes de realizar su solicitud. Para el servicio de extracción de palabras clave, el `analyzer_id` ID es:
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
| `analyzer_id` | ID del [!DNL Sensei] servicio en el que se implementa la solicitud. Este ID determina cuál de los [!DNL Sensei Content Frameworks] se utiliza. Para obtener servicios personalizados, póngase en contacto con el equipo de Content and Commerce AI para configurar un ID personalizado. | Sí |
| `application-id` | ID de la aplicación creada. | Sí |
| `data` | Matriz que contiene un objeto JSON con cada objeto de la matriz que representa un documento. Cualquier parámetro pasado como parte de esta matriz anula los parámetros globales especificados fuera de la `data` matriz. Cualquiera de las propiedades restantes que se describen a continuación en esta tabla se puede sobrescribir desde dentro `data`. | Sí |
| `language` | Idioma del texto de entrada. El valor predeterminado es `en`. | No |
| `content-type` | Se utiliza para indicar si la entrada es parte del cuerpo de la solicitud o una dirección URL firmada para un bucket S3. El valor predeterminado de esta propiedad es `inline`. | Sí |
| `encoding` | Formato de codificación del texto de entrada. Esto puede ser `utf-8` o `utf-16`. El valor predeterminado de esta propiedad es `utf-8`. | No |
| `threshold` | El umbral de puntuación (0 a 1) por encima del cual deben devolverse los resultados. Utilice el valor `0` para devolver todos los resultados. El valor predeterminado de esta propiedad es `0`. | No |
| `top-N` | Número de resultados que se van a devolver (no puede ser un entero negativo). Utilice el valor `0` para devolver todos los resultados. Cuando se utiliza junto con `threshold`, el número de resultados devueltos es el menor de cualquiera de los límites establecidos. El valor predeterminado de esta propiedad es `0`. | No |
| `custom` | Parámetros personalizados que se van a pasar. Esta propiedad requiere un objeto JSON válido para funcionar. Consulte el [apéndice](#appendix) para obtener más información sobre los parámetros personalizados. | No |
| `content-id` | ID única para el elemento de datos que se devuelve en la respuesta. Si no se pasa, se asigna un ID generado automáticamente. | No |
| `content` | Contenido utilizado por el servicio de extracción de palabras clave. El contenido puede ser texto sin procesar (tipo de contenido &quot;en línea&quot;). <br> Si el contenido es un archivo en S3 (tipo de contenido &#39;s3-bucket&#39;), pase la dirección URL firmada. Cuando el contenido es parte de request-body, la lista de los elementos de datos debe tener un solo objeto. Si se pasa más de un objeto, solo se procesa el primer objeto. | Sí |

**Respuesta**

Una respuesta correcta devuelve un objeto JSON que contiene palabras clave extraídas en la `response` matriz.

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

## Apéndice {#appendix}

La siguiente tabla contiene los parámetros disponibles que se pueden utilizar desde dentro `custom`.

| Nombre | Descripción | Obligatorio |
| --- | --- | --- |
| `min-n` | El número mínimo de palabras requeridas en las palabras clave. | No |
| `entity-types` | Tipos de entidades a devolver. Consulte la tabla de reconocimiento de entidad con nombre al principio de este documento. | No |