---
description: Esta página enumera y describe todas las operaciones de API que puede realizar mediante el punto final de la API "/authoring/testing/template/sample" para obtener una plantilla de transformación de mensaje de prueba para su destino.
title: Obtener operaciones de API de plantilla de muestra
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Obtener operaciones de API de plantilla de muestra {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Extremo de API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Esta página enumera y describe todas las operaciones de API que puede realizar con la variable `/authoring/testing/template/sample` Extremo de API, para generar un [plantilla de transformación de mensaje](./message-format.md#using-templating) para su destino. Para obtener una descripción de la funcionalidad admitida por este extremo, lea [crear plantilla](./create-template.md).

## Introducción a las operaciones de API de plantilla de muestra {#get-started}

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Obtener plantilla de muestra {#generate-sample-template}

Puede obtener una plantilla de ejemplo realizando una solicitud de GET a la variable `authoring/testing/template/sample/` y proporcionar el ID de destino de la configuración de destino en función de la que esté creando la plantilla.

>[!TIP]
>
>* El ID de destino que debe utilizar aquí es el `instanceId` que corresponde a una configuración de destino, creada con la variable `/destinations` punto final. Consulte la [referencia de API de configuración de destino](./destination-configuration-api.md#retrieve-list).


**Formato de API**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID de la configuración de destino para la que está generando una plantilla de transformación de mensajes. |

**Solicitud**

La siguiente solicitud genera una nueva plantilla de ejemplo, configurada por los parámetros proporcionados en la carga útil.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una plantilla de ejemplo que puede editar para que coincida con el formato de datos esperado.

Si el ID de destino proporcionado corresponde a una configuración de destino con [agregación de mejor esfuerzo](./destination-configuration.md#best-effort-aggregation) y `maxUsersPerRequest=1` en la directiva de agregación, la solicitud devuelve una plantilla de ejemplo similar a esta:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Si el ID de destino proporcionado corresponde a una plantilla de servidor de destino con [agregación configurable](./destination-configuration.md#configurable-aggregation) o [agregación de mejor esfuerzo](./destination-configuration.md#best-effort-aggregation) con `maxUsersPerRequest` bueno que uno, la solicitud devuelve una plantilla de ejemplo similar a esta:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo generar una plantilla de transformación de mensajes utilizando `/authoring/testing/template/sample` Extremo de API. A continuación, puede utilizar la variable [Extremo de API de plantilla de procesamiento](./render-template-api.md) para generar perfiles exportados basados en la plantilla y compararlos con el formato de datos esperado del destino.
