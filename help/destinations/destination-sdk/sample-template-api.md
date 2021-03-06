---
description: En esta página se enumeran y describen todas las operaciones de API que puede realizar con el extremo API `/authoring/testing/template/sample` para obtener una plantilla de transformación de mensaje de prueba para su destino.
title: Obtener operaciones de API de plantilla de ejemplo
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Obtener operaciones de API de plantilla de ejemplo {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**Punto de conexión de API**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

En esta página se enumeran y describen todas las operaciones de API que puede realizar mediante la `/authoring/testing/template/sample` extremo de API, para generar un [plantilla de transformación de mensaje](./message-format.md#using-templating) para su destino. Para obtener una descripción de la funcionalidad admitida por este extremo, lea [crear plantilla](./create-template.md).

## Introducción a las operaciones de API de plantillas de ejemplo {#get-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Obtener plantilla de ejemplo {#generate-sample-template}

Puede obtener una plantilla de ejemplo realizando una solicitud de GET al `authoring/testing/template/sample/` y proporcionando el ID de destino de la configuración de destino en función de la cual esté creando la plantilla.

>[!TIP]
>
>* El ID de destino que debe usar aquí es el `instanceId` que corresponde a una configuración de destino, creada con el `/destinations` punto final. Consulte la [referencia de la API de configuración de destino](./destination-configuration-api.md#retrieve-list).


**Formato de API**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID de la configuración de destino para la que se está generando una plantilla de transformación de mensaje. |

**Solicitud**

La siguiente solicitud genera una nueva plantilla de ejemplo, configurada mediante los parámetros proporcionados en la carga útil.

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

Si el ID de destino que proporciona corresponde a una configuración de destino con [agregación del mejor esfuerzo](./destination-configuration.md#best-effort-aggregation) y `maxUsersPerRequest=1` en la política de agregación, la solicitud devuelve una plantilla de ejemplo similar a esta:

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

Si el ID de destino que proporciona corresponde a una plantilla de servidor de destino con [agregación configurable](./destination-configuration.md#configurable-aggregation) o [agregación del mejor esfuerzo](./destination-configuration.md#best-effort-aggregation) con `maxUsersPerRequest` bueno que uno, la solicitud devuelve una plantilla de ejemplo similar a esta:

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

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo generar una plantilla de transformación de mensaje usando la variable `/authoring/testing/template/sample` extremo de API. A continuación, puede usar la variable [Punto final de API de plantilla de renderización](./render-template-api.md) para generar perfiles exportados basados en la plantilla y compararlos con el formato de datos esperado del destino.
