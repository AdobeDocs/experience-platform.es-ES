---
keywords: Experience Platform;home;popular topics;segment;Segment;create segment;segmentation;create a segment;Segmentation Service;
solution: Experience Platform
title: Crear un segmento
topic: tutorial
type: Tutorial
description: Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento mediante la API de servicio de segmentación de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Crear un segmento

Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento mediante la [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obtener información sobre cómo generar segmentos mediante la interfaz de usuario, consulte la guía [Generador de segmentos](../ui/overview.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos [!DNL Adobe Experience Platform] servicios que intervienen en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!Servicio de segmentación de Adobe Experience Platform DNL]](../home.md): Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [[!Modelo de datos de experiencia DNL (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a las [!DNL Platform] API de forma satisfactoria.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Desarrollar una definición de segmento

El primer paso en la segmentación es definir un segmento, representado en una construcción denominada definición **de** segmento. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado **PQL**. Los predicados PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione a [!DNL Real-time Customer Profile]. Consulte la guía [](../pql/overview.md) PQL para obtener más información sobre cómo escribir consultas PQL.

Puede crear una nueva definición de segmento haciendo una solicitud de POST al `/segment/definitions` extremo en la [!DNL Segmentation] API. El siguiente ejemplo describe cómo dar formato a una solicitud de definición, incluida la información necesaria para que un segmento se defina correctamente.

Para obtener una explicación detallada sobre cómo definir un segmento, lea la guía para desarrolladores de definiciones de [segmentos](../api/segment-definitions.md#create).

## Calcular y previsualización de una audiencia {#estimate-and-preview-an-audience}

A medida que desarrolla la definición del segmento, puede utilizar las herramientas de previsualización y estimación dentro de [!DNL Real-time Customer Profile] la información de nivel de resumen de vista para asegurarse de aislar la audiencia esperada. Las estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado y el intervalo de confianza. Las previsualizaciones proporcionan listas paginadas de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

Al estimar y previsualizar su audiencia, puede probar y optimizar sus predicados PQL hasta que produzcan un resultado deseado, donde se pueden utilizar en una definición de segmento actualizada.

Existen dos pasos necesarios para realizar una previsualización o una estimación del segmento:

1. [Crear un trabajo de previsualización](#create-a-preview-job)
2. [Previsualización](#view-an-estimate-or-preview) o estimación de vista con el ID del trabajo de previsualización

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

Puede crear un nuevo trabajo de previsualización realizando una solicitud de POST al `/preview` extremo.

Encontrará instrucciones detalladas sobre la creación de un trabajo de previsualización en la guía de [previsualizaciones y estimaciones](../api/previews-and-estimates.md#create-preview).

### Vista de una estimación o previsualización

Los procesos de estimación y previsualización se ejecutan de forma asíncrona, ya que diferentes consultas pueden tardar varios períodos en completarse. Una vez iniciada la consulta, puede utilizar las llamadas de API para recuperar (GET) el estado actual de la estimación o previsualización a medida que avanza.

Con la API, puede buscar el estado actual de un trabajo de previsualización por su ID. [!DNL Segmentation Service] Si el estado es &quot;RESULT_READY&quot;, puede realizar la vista de los resultados. Para buscar el estado actual de un trabajo de previsualización, lea la sección sobre [recuperación de un trabajo de previsualización](../api/previews-and-estimates.md#get-preview) en la guía de extremos de previsualizaciones y estimaciones. Para buscar el estado actual de un trabajo de estimación, lea la sección sobre [recuperar un trabajo](../api/previews-and-estimates.md#get-estimate) de estimación en la guía de extremos de previsualizaciones y estimaciones.


## Pasos siguientes

Una vez desarrollada, probada y guardada la definición del segmento, puede crear un trabajo de segmento para crear una audiencia mediante la [!DNL Segmentation Service] API. Consulte el tutorial sobre la [evaluación y el acceso a los resultados](./evaluate-a-segment.md) de los segmentos para ver los pasos detallados sobre cómo hacerlo.