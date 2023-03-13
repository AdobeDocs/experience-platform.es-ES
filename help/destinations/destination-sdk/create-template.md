---
description: Como parte de Destination SDK, Adobe proporciona herramientas para desarrolladores que le ayudarán a configurar y probar su destino. En esta página se describe cómo crear y probar una plantilla de transformación de mensajes.
title: Creación y prueba de una plantilla de transformación de mensajes
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Creación y prueba de una plantilla de transformación de mensajes {#create-template}

## Información general {#overview}

Como parte de Destination SDK, Adobe proporciona herramientas para desarrolladores que le ayudarán a configurar y probar su destino. En esta página se describe cómo crear y probar una plantilla de transformación de mensajes. Para obtener información sobre cómo probar el destino, lea [Pruebe la configuración de destino](./test-destination.md).

Hasta **creación y prueba de una plantilla de transformación de mensajes** entre el esquema de destino en Adobe Experience Platform y el formato de mensaje admitido por el destino, utilice el *Herramienta de creación de plantillas* se describen más adelante.  Obtenga más información sobre la transformación de datos entre el esquema de origen y el de destino en la [documento de formato de mensaje](./message-format.md#using-templating).

A continuación se ilustra cómo la creación y prueba de una plantilla de transformación de mensajes se ajusta al [flujo de trabajo de configuración de destino](./configure-destination-instructions.md) en el Destination SDK:

![Gráfico de dónde encaja el paso Crear plantilla en el flujo de trabajo de configuración de destino](./assets/create-template-step.png)

## Por qué necesita crear y probar una plantilla de transformación de mensajes {#why-create-message-transformation-template}

Uno de los primeros pasos para crear el destino en Destination SDK es pensar en cómo se transforma el formato de datos para la pertenencia a segmentos, identidades y atributos de perfil al exportarse de Adobe Experience Platform a su destino. Busque información acerca de la transformación entre el esquema XDM de Adobe y el esquema de destino en la [documento de formato de mensaje](./message-format.md#using-templating).

Para que la transformación tenga éxito, debe proporcionar una plantilla de transformación, similar a este ejemplo: [Crear una plantilla que envíe segmentos, identidades y atributos de perfil](./message-format.md#segments-identities-attributes).

Adobe proporciona una herramienta de plantilla que le permite crear y probar la plantilla de mensaje que transforma los datos del formato XDM de Adobe en el formato admitido por el destino. La herramienta tiene dos extremos de API que puede utilizar:
* Utilice el *API de plantilla de ejemplo* para obtener una plantilla de muestra.
* Utilice el *API de plantilla de procesamiento* para procesar la plantilla de muestra y poder comparar el resultado con el formato de datos esperado del destino. Después de comparar los datos exportados con el formato de datos esperado por el destino, puede editar la plantilla. De este modo, los datos exportados que genere coincidirán con el formato de datos esperado por su destino.

## Pasos que se deben seguir antes de crear la plantilla {#prerequisites}

Antes de crear la plantilla, asegúrese de completar los pasos siguientes:

1. [Crear una configuración de servidor de destino](./destination-server-api.md). La plantilla que va a generar difiere según el valor que proporcione para `maxUsersPerRequest` parámetro.
   * Uso `maxUsersPerRequest=1` si desea que una llamada de API a su destino incluya un solo perfil, junto con sus cualificaciones de segmento, identidades y atributos de perfil.
   * Uso `maxUsersPerRequest` con un valor bueno que uno si desea que una llamada de API a su destino incluya varios perfiles, junto con sus cualificaciones de segmento, identidades y atributos de perfil.
2. [Crear una configuración de destino](./destination-configuration-api.md#create) y agregue el ID de la configuración del servidor de destino en `destinationDelivery.destinationServerId`.
3. [Obtener el ID de la configuración de destino](./destination-configuration-api.md#retrieve-list) que acaba de crear, para que pueda utilizarlo en la herramienta de creación de plantillas.
4. Comprender [qué funciones y filtros puede utilizar](./supported-functions.md) en la plantilla de transformación de mensajes.

## Cómo utilizar la API de plantilla de ejemplo y la API de plantilla de procesamiento para crear una plantilla para el destino {#iterative-process}

>[!TIP]
>
>Antes de crear y editar la plantilla de transformación de mensajes, puede empezar llamando a la función [extremo de API de plantilla de procesamiento](./render-template-api.md#render-exported-data) con una plantilla sencilla que exporta los perfiles sin procesar sin aplicar ninguna transformación. La sintaxis de la plantilla simple es: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

El proceso para obtener y probar la plantilla es iterativo. Repita los pasos siguientes hasta que los perfiles exportados coincidan con el formato de datos esperado del destino.

1. Primero, [obtener una plantilla de muestra](./create-template.md#sample-template-api).
2. Utilice la plantilla de ejemplo como punto de partida para crear un borrador propio.
3. Llame a [extremo de API de plantilla de procesamiento](./create-template.md#render-template-api) con su propia plantilla. El Adobe genera perfiles de muestra basados en el esquema y devuelve el resultado de los errores encontrados.
4. Comparar los datos exportados con el formato de datos esperado por el destino. Si es necesario, edite la plantilla.
5. Repita este proceso hasta que los perfiles exportados coincidan con el formato de datos esperado del destino.

## Obtenga una plantilla de muestra mediante la API de plantilla de muestra {#sample-template-api}

>[!NOTE]
>
>Para obtener la documentación de referencia completa de la API, lea [Obtener operaciones de API de plantilla de muestra](./sample-template-api.md).

Añada un ID de destino a la llamada de, como se muestra a continuación, y la respuesta devolverá un ejemplo de plantilla correspondiente al ID de destino.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

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

## Escape de carácter en la plantilla {#character-escape-template}

Antes de utilizar la plantilla para procesar perfiles que coincidan con el formato esperado del destino, debe aplicar caracteres de escape a la plantilla, como se muestra en la grabación de pantalla a continuación.

![Vídeo que muestra cómo aplicar secuencias de escape de caracteres a una plantilla mediante una herramienta de escape de caracteres en línea](./assets/escape-characters.gif)

Puede utilizar una herramienta de escape de caracteres en línea. La demostración anterior utiliza el [Formateador de escape JSON](https://jsonformatter.org/json-escape).

## Procesar API de plantilla {#render-template-api}

Después de crear una plantilla de transformación de mensaje con el [API de plantilla de ejemplo](./create-template.md#sample-template-api), puede [procesar la plantilla](./render-template-api.md) para generar datos exportados basados en él. Esto le permite comprobar si los perfiles que Adobe Experience Platform exportaría a su destino coinciden con el formato esperado del destino.

Consulte la referencia de la API para ver ejemplos de llamadas que puede realizar:

* [Procesar una plantilla sin perfiles enviados en el cuerpo](./render-template-api.md#multiple-profiles-no-body)
* [Procesar una plantilla con perfiles enviados en el cuerpo](./render-template-api.md#multiple-profiles-with-body)

Edite la plantilla y realice llamadas al extremo de la API de la plantilla de procesamiento hasta que los perfiles exportados coincidan con el formato de datos esperado del destino.

## Añada la plantilla con caracteres de escape a la configuración del servidor de destino

Una vez que esté satisfecho con la plantilla de transformación de mensajes, agréguela a su [configuración del servidor de destino](./server-and-template-configuration.md), en `httpTemplate.requestBody.value`.
