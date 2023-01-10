---
keywords: Experience Platform;inicio;temas populares;segmento;segmento;crear segmento;segmentación;crear segmento;servicio de segmentación;
solution: Experience Platform
title: Creación de un segmento mediante la API del servicio de segmentación
type: Tutorial
description: Siga este tutorial para aprender a desarrollar, probar, previsualizar y guardar una definición de segmento mediante la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Creación de un segmento mediante la API del servicio de segmentación

Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento utilizando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obtener información sobre cómo crear segmentos mediante la interfaz de usuario, consulte la [Guía del Generador de segmentos](../ui/overview.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de las distintas [!DNL Adobe Experience Platform] servicios relacionados con la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite generar segmentos de audiencia a partir de datos del perfil del cliente en tiempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas correctamente al [!DNL Platform] API.

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Desarrollo de una definición de segmento

El primer paso en la segmentación es definir un segmento, representado en una construcción denominada definición de segmento. Una definición de segmento es un objeto que encapsula una consulta escrita en [!DNL Profile Query Language] (PQL). Este objeto también se denomina predicado PQL. Los predicados de PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione a [!DNL Real-Time Customer Profile]. Consulte la [Guía de PQL](../pql/overview.md) para obtener más información sobre cómo escribir consultas PQL.

Puede crear una nueva definición de segmento realizando una solicitud de POST al `/segment/definitions` en la variable [!DNL Segmentation] API. El siguiente ejemplo describe cómo dar formato a una solicitud de definición, incluida la información necesaria para que un segmento se defina correctamente.

Para obtener una explicación detallada sobre cómo definir un segmento, lea la [guía para desarrolladores de definiciones de segmentos](../api/segment-definitions.md#create).

## Calcular y previsualizar una audiencia {#estimate-and-preview-an-audience}

A medida que desarrolle su definición de segmento, puede utilizar las herramientas de estimación y vista previa dentro de [!DNL Real-Time Customer Profile] para ver información de resumen que le ayude a aislar la audiencia esperada. Las estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia y el intervalo de confianza previstos. Las vistas previas proporcionan listas paginadas de perfiles aptos para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

Al estimar y previsualizar la audiencia, puede probar y optimizar sus predicados PQL hasta que produzcan un resultado deseado, donde luego se puedan utilizar en una definición de segmento actualizada.

Se requieren dos pasos para obtener una vista previa o una estimación del segmento:

1. [Crear un trabajo de vista previa](#create-a-preview-job)
2. [Ver estimación o vista previa](#view-an-estimate-or-preview) uso del ID del trabajo de vista previa

### Cómo se generan las estimaciones

Las muestras de datos se utilizan para evaluar segmentos y estimar el número de perfiles aptos. Los nuevos datos se cargan en la memoria cada mañana (entre las 12:00 y las 2:00 de la mañana, hora del Pacífico, que es entre las 7 y las 9:00 horas, hora universal) y todas las consultas de segmentación se calculan utilizando los datos de muestra de ese día. Por consiguiente, cualquier campo nuevo añadido o dato adicional recopilado se reflejará en las estimaciones al día siguiente.

El tamaño de la muestra depende del número total de entidades en el almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades en el almacén de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| de 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Las estimaciones suelen durar entre 10 y 15 segundos, empezando por una estimación aproximada y refinándose a medida que se leen más registros.

### Crear un trabajo de vista previa

Puede crear un nuevo trabajo de vista previa realizando una solicitud de POST al `/preview` punto final.

Puede encontrar instrucciones detalladas sobre la creación de un trabajo de vista previa en la [guía de extremos de vista previa y estimación](../api/previews-and-estimates.md#create-preview).

### Ver una estimación o vista previa

Los procesos de estimación y vista previa se ejecutan asincrónicamente, ya que las distintas consultas pueden tardar distintos períodos en completarse. Una vez iniciada una consulta, puede utilizar las llamadas a la API para recuperar (GET) el estado actual de la estimación o vista previa a medida que avanza.

Al usar la variable [!DNL Segmentation Service] API, puede buscar el estado actual de un trabajo de vista previa por su ID. Si el estado es &quot;RESULT_READY&quot;, puede ver los resultados. Para buscar el estado actual de un trabajo de vista previa, lea la sección en [recuperación de una sección de trabajo de vista previa](../api/previews-and-estimates.md#get-preview) en la guía de extremos de vista previa y estimación. Para consultar el estado actual de un trabajo de estimación, lea la sección de [recuperación de un trabajo de estimación](../api/previews-and-estimates.md#get-estimate) en la guía de extremos de vista previa y estimación.


## Pasos siguientes

Una vez que haya desarrollado, probado y guardado su definición de segmento, puede crear un trabajo de segmento para crear una audiencia usando el [!DNL Segmentation Service] API. Consulte el tutorial en [evaluación y acceso a resultados de segmentos](./evaluate-a-segment.md) para ver los pasos detallados sobre cómo hacerlo.
