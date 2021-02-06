---
keywords: Experience Platform;inicio;temas populares;segmento;Segmento;crear segmento;segmentación;crear un segmento;Servicio de segmentación;
solution: Experience Platform
title: Crear un segmento con la API de servicio de segmentación
topic: tutorial
type: Tutorial
description: Siga este tutorial para aprender a desarrollar, probar, previsualización y guardar una definición de segmento mediante la API de servicio de segmentación de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Creación de un segmento mediante la API de servicio de segmentación

Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento mediante [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obtener información sobre cómo generar segmentos mediante la interfaz de usuario, consulte la [guía del Generador de segmentos](../ui/overview.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos [!DNL Adobe Experience Platform] servicios que intervienen en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md):: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API [!DNL Platform].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Desarrollar una definición de segmento

El primer paso en la segmentación es definir un segmento, representado en una construcción denominada definición de segmento. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado PQL. Los predicados PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione a [!DNL Real-time Customer Profile]. Consulte la [guía de PQL](../pql/overview.md) para obtener más información sobre cómo escribir consultas de PQL.

Puede crear una nueva definición de segmento haciendo una solicitud de POST al extremo `/segment/definitions` en la API [!DNL Segmentation]. El siguiente ejemplo describe cómo dar formato a una solicitud de definición, incluida la información necesaria para que un segmento se defina correctamente.

Para obtener una explicación detallada sobre cómo definir un segmento, lea la guía para desarrolladores de [definición de segmento](../api/segment-definitions.md#create).

## Calcular y previsualización de una audiencia {#estimate-and-preview-an-audience}

A medida que desarrolla la definición del segmento, puede utilizar las herramientas de estimación y previsualización dentro de [!DNL Real-time Customer Profile] para obtener información de nivel de resumen de vista que le ayudará a aislar la audiencia esperada. Las estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado y el intervalo de confianza. Las previsualizaciones proporcionan listas paginadas de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

Al estimar y previsualizar su audiencia, puede probar y optimizar sus predicados PQL hasta que produzcan un resultado deseado, donde se pueden utilizar en una definición de segmento actualizada.

Existen dos pasos necesarios para realizar una previsualización o una estimación del segmento:

1. [Crear un trabajo de previsualización](#create-a-preview-job)
2. [Vista estimada o ](#view-an-estimate-or-preview) vista previa con el ID del trabajo de previsualización

### Cómo se generan las estimaciones

Las muestras de datos se utilizan para evaluar segmentos y estimar el número de perfiles aptos. Los nuevos datos se cargan en la memoria cada mañana (entre las 12:00 y las 2:00 PT, que es entre las 7:00 y las 9:00 UTC), y todas las consultas de segmentación se calculan utilizando los datos de muestra de ese día. En consecuencia, cualquier campo nuevo agregado o datos adicionales recopilados se reflejarán en las estimaciones al día siguiente.

El tamaño de la muestra depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades de la tienda de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Las estimaciones suelen durar entre 10 y 15 segundos, comenzando con una estimación aproximada y refinándose a medida que se leen más registros.

### Crear un trabajo de previsualización

Puede crear un nuevo trabajo de previsualización haciendo una solicitud de POST al extremo `/preview`.

Encontrará instrucciones detalladas sobre cómo crear un trabajo de previsualización en la [guía de extremos de previsualizaciones y estimaciones](../api/previews-and-estimates.md#create-preview).

### Vista de una estimación o previsualización

Los procesos de estimación y previsualización se ejecutan de forma asíncrona, ya que diferentes consultas pueden tardar varios períodos en completarse. Una vez iniciada la consulta, puede utilizar las llamadas de API para recuperar (GET) el estado actual de la estimación o previsualización a medida que avanza.

Mediante la API [!DNL Segmentation Service], puede buscar el estado actual de un trabajo de previsualización mediante su ID. Si el estado es &quot;RESULT_READY&quot;, puede realizar la vista de los resultados. Para buscar el estado actual de un trabajo de previsualización, lea la sección sobre [recuperación de una sección de trabajo de previsualización](../api/previews-and-estimates.md#get-preview) en la guía de extremos de previsualizaciones y estimaciones. Para buscar el estado actual de un trabajo de estimación, lea la sección sobre [recuperación de un trabajo de estimación](../api/previews-and-estimates.md#get-estimate) en la guía de extremos de previsualizaciones y estimaciones.


## Pasos siguientes

Una vez desarrollada, probada y guardada la definición del segmento, puede crear un trabajo de segmento para crear una audiencia mediante la API [!DNL Segmentation Service]. Consulte el tutorial sobre [evaluación y acceso a los resultados del segmento](./evaluate-a-segment.md) para ver los pasos detallados sobre cómo hacerlo.