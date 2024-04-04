---
solution: Experience Platform
title: Creación de una definición de segmento mediante la API del servicio de segmentación
type: Tutorial
description: Siga este tutorial para aprender a desarrollar, probar, previsualizar y guardar una definición de segmento mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 9966385968540701f66acbb70c0810906650b7e1
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 6%

---

# Creación de una definición de segmento mediante la API del servicio de segmentación

Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento mediante [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obtener información sobre cómo generar definiciones de segmentos mediante la interfaz de usuario, consulte la [Guía del Generador de segmentos](../ui/overview.md).

## Introducción

Este tutorial requiere una comprensión práctica de los distintos [!DNL Adobe Experience Platform] servicios implicados en la creación de definiciones de segmentos. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite crear audiencias utilizando definiciones de segmentos u otras fuentes externas a partir de datos del perfil del cliente en tiempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).

Las secciones siguientes proporcionan información adicional que deberá conocer para poder realizar llamadas correctamente a [!DNL Platform] API.

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Desarrollar una definición de segmento

El primer paso de la segmentación es definir una definición de segmento. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado PQL. Los predicados PQL definen las reglas para la definición del segmento en función de las condiciones relacionadas con cualquier registro o datos de series temporales que proporcione a [!DNL Real-Time Customer Profile]. Consulte la [Guía de PQL](../pql/overview.md) para obtener más información sobre cómo escribir consultas PQL.

Puede crear una nueva definición de segmento realizando una solicitud de POST a `/segment/definitions` punto final en la [!DNL Segmentation] API. En el siguiente ejemplo se describe cómo dar formato a una solicitud de definición, incluida la información necesaria para que una definición de segmento se defina correctamente.

Para obtener una explicación detallada sobre cómo definir una definición de segmento, lea la [guía para desarrolladores de definición de segmentos](../api/segment-definitions.md#create).

## Calcular y previsualizar una audiencia {#estimate-and-preview-an-audience}

A medida que desarrolle su definición de segmento, puede utilizar las herramientas de estimación y vista previa dentro de [!DNL Real-Time Customer Profile] para ver información de resumen que le ayude a aislar la audiencia esperada. Las estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado y el intervalo de confianza. Las vistas previas proporcionan listas paginadas de perfiles aptos para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

Al estimar y previsualizar la audiencia, puede probar y optimizar los predicados PQL hasta que produzcan un resultado deseado, donde luego se pueden utilizar en una definición de segmento actualizada.

Existen dos pasos necesarios para obtener una vista previa o una estimación de la definición de su segmento:

1. [Creación de un trabajo de vista previa](#create-a-preview-job)
2. [Ver estimación o previsualización](#view-an-estimate-or-preview) uso del ID del trabajo de vista previa

### Cómo se generan las estimaciones

A medida que los datos habilitados para Perfil del cliente en tiempo real se incorporan a Platform, se almacenan en el almacén de datos de perfil. Cuando la ingesta de registros en el almacén de perfiles aumenta o disminuye el recuento total de perfiles en más del 5 %, se activa un trabajo de muestreo para actualizar el recuento. Si el recuento de perfiles no cambia en más del 5 %, el trabajo de muestreo se ejecutará automáticamente semanalmente.

La forma en que se activa la muestra depende del tipo de ingesta que se utilice:

- Para los flujos de trabajo de datos de flujo continuo, se realiza una comprobación cada hora para determinar si se ha alcanzado el umbral de aumento o disminución del 5 %. Si se ha alcanzado este umbral, se activa automáticamente un trabajo de muestra para actualizar el recuento.
- Para la ingesta por lotes, en los 15 minutos siguientes a la ingesta correcta de un lote en el almacén de perfiles, si se alcanza el umbral de aumento o disminución del 5 %, se ejecuta un trabajo para actualizar el recuento. Con la API de perfil puede obtener una vista previa del último trabajo de ejemplo correcto, así como una distribución de perfiles de lista por conjunto de datos y por área de nombres de identidad.

El tamaño de la muestra depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades en el almacén de perfiles | Tamaño de muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Las estimaciones suelen durar entre 10 y 15 segundos, comenzando con una estimación aproximada y perfeccionando a medida que se leen más registros.

### Creación de un trabajo de vista previa

Puede crear un nuevo trabajo de vista previa realizando una solicitud de POST al `/preview` punto final.

Puede encontrar instrucciones detalladas sobre la creación de un trabajo de vista previa en la [guía de extremos de previsualizaciones y estimaciones](../api/previews-and-estimates.md#create-preview).

### Ver una estimación o previsualización

Los procesos de estimación y vista previa se ejecutan de forma asíncrona, ya que las distintas consultas pueden tardar distintos periodos en completarse. Una vez iniciada una consulta, puede utilizar llamadas a la API para recuperar (GET) el estado actual de la estimación o previsualización a medida que progresa.

Uso del [!DNL Segmentation Service] API, puede buscar el estado actual de un trabajo de vista previa por su ID. Si el estado es &quot;RESULT_READY&quot;, puede ver los resultados. Para consultar el estado actual de un trabajo de vista previa, lea la sección sobre [sección recuperación de un trabajo de vista previa](../api/previews-and-estimates.md#get-preview) en la guía de previsualizaciones y estimaciones de extremos. Para consultar el estado actual de un trabajo de estimación, lea la sección sobre [recuperación de un trabajo de estimación](../api/previews-and-estimates.md#get-estimate) en la guía de previsualizaciones y estimaciones de extremos.


## Pasos siguientes

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede crear un trabajo de segmento para crear una audiencia utilizando [!DNL Segmentation Service] API. Consulte el tutorial sobre [evaluación y acceso a los resultados de los segmentos](./evaluate-a-segment.md) para ver los pasos detallados sobre cómo hacerlo.
