---
keywords: Experience Platform;inicio;temas populares;ingestión por lotes;ingestión por lotes;ingestión parcial;Ingesta parcial;Error de recuperación;error de recuperación;Ingesta parcial por lotes;ingestión parcial por lotes;parcial;ingestión;ingestión;ingestión;
solution: Experience Platform
title: Información general sobre la ingestión parcial por lotes
topic: overview
description: Este documento proporciona un tutorial para administrar la ingestión parcial por lotes.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---


# Ingestión parcial por lotes

La ingestión parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un cierto umbral. Con esta capacidad, los usuarios pueden transferir correctamente todos los datos correctos a Adobe Experience Platform mientras que todos los datos incorrectos se agrupan por lotes por separado, junto con los detalles de por qué no son válidos.

Este documento proporciona un tutorial para administrar la ingestión parcial por lotes.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los diversos servicios de Adobe Experience Platform que intervienen en la ingestión parcial de lotes. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Ingesta](./overview.md) por lotes: Método que  [!DNL Platform] ingiere y almacena datos de archivos de datos, como CSV y Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a las [!DNL Platform] API de forma satisfactoria.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

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

## Habilitar un lote para la ingestión parcial por lotes en la API {#enable-api}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingestión parcial por lotes mediante la API. Para obtener instrucciones sobre cómo usar la interfaz de usuario, lea [habilitar un lote para la ingestión parcial por lotes en el paso de la interfaz de usuario](#enable-ui).

Puede crear un nuevo lote con la ingestión parcial activada.

Para crear un nuevo lote, siga los pasos de la [guía para desarrolladores de ingestión por lotes](./api-overview.md). Una vez que llegue al paso **[!UICONTROL Crear lote]**, agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un indicador que permite que [!DNL Platform] genere mensajes de error detallados sobre el lote. |
| `partialIngestionPercentage` | El porcentaje de errores aceptables antes de que se produzca un error en todo el lote. Así que, en este ejemplo, un máximo del 5% del lote puede ser error, antes de que falle. |


## Habilitar un lote para la ingestión parcial por lotes en la interfaz de usuario {#enable-ui}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingestión parcial por lotes mediante la interfaz de usuario. Si ya ha habilitado un lote para la ingestión parcial por lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un lote para la ingestión parcial a través de la interfaz de usuario [!DNL Platform], puede crear un nuevo lote a través de conexiones de origen, crear un nuevo lote en un conjunto de datos existente o crear un nuevo lote a través de &quot;[!UICONTROL Asignar CSV al flujo XDM]&quot;.

### Crear una nueva conexión de origen {#new-source}

Para crear una nueva conexión de origen, siga los pasos enumerados en la [información general de fuentes](../../sources/home.md). Una vez que llegue al paso **[!UICONTROL Detalle de flujo de datos]**, tome nota de los campos **[!UICONTROL Ingestión parcial]** y **[!UICONTROL Diagnósticos de error]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La opción **[!UICONTROL de ingestión parcial]** le permite habilitar o deshabilitar el uso de ingestión parcial por lotes.

La opción **[!UICONTROL Diagnósticos de error]** sólo aparece cuando la opción **[!UICONTROL de ingestión parcial]** está desactivada. Esta función permite que [!DNL Platform] genere mensajes de error detallados sobre los lotes ingestados. Si se activa la opción **[!UICONTROL de inserción parcial]**, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

El **[!UICONTROL umbral de error]** permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

### Usar un conjunto de datos existente {#existing-dataset}

Para utilizar un conjunto de datos existente, seleccione un conjunto de datos para el inicio. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La opción **[!UICONTROL de ingestión parcial]** le permite habilitar o deshabilitar el uso de ingestión parcial por lotes.

La opción **[!UICONTROL Diagnósticos de error]** sólo aparece cuando la opción **[!UICONTROL de ingestión parcial]** está desactivada. Esta función permite que [!DNL Platform] genere mensajes de error detallados sobre los lotes ingestados. Si se activa la opción **[!UICONTROL de inserción parcial]**, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

El **[!UICONTROL umbral de error]** permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

Ahora, puede cargar datos con el botón **Añadir datos** y se ingesta usando ingestión parcial.

### Utilice el flujo &quot;[!UICONTROL Asignar CSV al esquema XDM]&quot; {#map-flow}

Para utilizar el flujo &quot;[!UICONTROL Asignar CSV al esquema XDM]&quot;, siga los pasos enumerados en el [Tutorial de archivo CSV](../tutorials/map-a-csv-file.md). Una vez que llegue al paso **[!UICONTROL Añadir datos]**, tome nota de los campos **[!UICONTROL Ingestión parcial]** y **[!UICONTROL Diagnósticos de error]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La opción **[!UICONTROL de ingestión parcial]** le permite habilitar o deshabilitar el uso de ingestión parcial por lotes.

La opción **[!UICONTROL Diagnósticos de error]** sólo aparece cuando la opción **[!UICONTROL de ingestión parcial]** está desactivada. Esta función permite que [!DNL Platform] genere mensajes de error detallados sobre los lotes ingestados. Si se activa la opción **[!UICONTROL de inserción parcial]**, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL El]** umbral de error permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5 %.

## Pasos siguientes {#next-steps}

Este tutorial trata sobre cómo crear o modificar un conjunto de datos para habilitar la ingestión parcial por lotes. Para obtener más información sobre la ingestión por lotes, lea la [guía para desarrolladores de ingestión por lotes](./api-overview.md).

Para obtener información sobre la supervisión de los errores de ingestión parcial, lea la [guía de diagnóstico de errores de ingestión por lotes](../quality/error-diagnostics.md).
