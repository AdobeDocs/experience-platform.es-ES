---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta parcial;ingesta parcial;Recuperar error;recuperar error;ingesta parcial por lotes;ingesta parcial;ingesta parcial;ingesta parcial;
solution: Experience Platform
title: Resumen de ingesta parcial por lotes
description: Este documento proporciona un tutorial para administrar la ingesta parcial por lotes.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Ingesta parcial por lotes

La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral. Con esta capacidad, los usuarios pueden introducir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se agrupan por separado, junto con los detalles de por qué no es válido.

Este documento proporciona un tutorial para administrar la ingesta parcial por lotes.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform implicados en la ingesta parcial por lotes. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [Ingesta por lotes](./overview.md): el método que [!DNL Platform] incorpora y almacena datos de archivos de datos, como CSV y Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que deberá conocer para poder realizar llamadas correctamente a [!DNL Platform] API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../../sandboxes/home.md).

## Habilite un lote para la ingesta parcial por lotes en la API {#enable-api}

>[!NOTE]
>
>En esta sección se describe la activación de un lote para la ingesta parcial por lotes mediante la API. Para obtener instrucciones sobre el uso de la interfaz de usuario, lea la [habilitar un lote para la ingesta parcial por lotes en la IU](#enable-ui) paso.

Puede crear un nuevo lote con la ingesta parcial habilitada.

Para crear un nuevo lote, siga los pasos de la [guía para desarrolladores de ingesta por lotes](./api-overview.md). Una vez que llegue al **[!UICONTROL Crear lote]** paso, agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un indicador que permite [!DNL Platform] para generar mensajes de error detallados sobre el lote. |
| `partialIngestionPercent` | Porcentaje de errores aceptables antes de que falle todo el lote. Por lo tanto, en este ejemplo, un máximo del 5 % del lote puede ser errores antes de que falle. |


## Habilitar un lote para la ingesta parcial por lotes en la IU {#enable-ui}

>[!NOTE]
>
>En esta sección se describe la activación de un lote para la ingesta parcial por lotes mediante la interfaz de usuario. Si ya ha habilitado un lote para la ingesta parcial por lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un lote para la ingesta parcial mediante [!DNL Platform] IU, puede crear un nuevo lote a través de conexiones de origen, crear un nuevo lote en un conjunto de datos existente o crear un nuevo lote a través de la &quot;[!UICONTROL Asignar CSV a flujo XDM]&quot;.

### Crear una nueva conexión de origen {#new-source}

Para crear una nueva conexión de origen, siga los pasos indicados en la sección [Resumen de orígenes](../../sources/home.md). Una vez que llegue al **[!UICONTROL Detalles del flujo de datos]** paso, tome nota de la **[!UICONTROL Ingesta parcial]** y **[!UICONTROL Diagnósticos de error]** campos.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

El **[!UICONTROL Ingesta parcial]** permite activar o desactivar el uso de la ingesta parcial por lotes.

El **[!UICONTROL Diagnósticos de error]** La opción solo aparece cuando la variable **[!UICONTROL Ingesta parcial]** la opción está desactivada. Esta función permite [!DNL Platform] para generar mensajes de error detallados sobre los lotes ingeridos. Si la variable **[!UICONTROL Ingesta parcial]** se activa, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

El **[!UICONTROL Umbral de error]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

### Usar un conjunto de datos existente {#existing-dataset}

Para utilizar un conjunto de datos existente, comience seleccionando un conjunto de datos. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

El **[!UICONTROL Ingesta parcial]** permite activar o desactivar el uso de la ingesta parcial por lotes.

El **[!UICONTROL Diagnósticos de error]** La opción solo aparece cuando la variable **[!UICONTROL Ingesta parcial]** la opción está desactivada. Esta función permite [!DNL Platform] para generar mensajes de error detallados sobre los lotes ingeridos. Si la variable **[!UICONTROL Ingesta parcial]** se activa, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

El **[!UICONTROL Umbral de error]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

Ahora, puede cargar datos mediante el **Añadir datos** y se incorporará mediante la ingesta parcial.

### Utilice el &quot;[!UICONTROL Asignar CSV a esquema XDM]&quot; flujo {#map-flow}

Para usar el complemento &quot;[!UICONTROL Asignar CSV a esquema XDM]&quot;, siga los pasos que se indican en la [Tutorial sobre asignación de un archivo CSV](../tutorials/map-csv/overview.md). Una vez que llegue al **[!UICONTROL Añadir datos]** paso, tome nota de la **[!UICONTROL Ingesta parcial]** y **[!UICONTROL Diagnósticos de error]** campos.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

El **[!UICONTROL Ingesta parcial]** permite activar o desactivar el uso de la ingesta parcial por lotes.

El **[!UICONTROL Diagnósticos de error]** La opción solo aparece cuando la variable **[!UICONTROL Ingesta parcial]** la opción está desactivada. Esta función permite [!DNL Platform] para generar mensajes de error detallados sobre los lotes ingeridos. Si la variable **[!UICONTROL Ingesta parcial]** se activa, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Umbral de error]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

## Pasos siguientes {#next-steps}

En este tutorial se explica cómo crear o modificar un conjunto de datos para habilitar la ingesta parcial por lotes. Para obtener más información sobre la ingesta por lotes, lea la [guía para desarrolladores de ingesta por lotes](./api-overview.md).

Para obtener información sobre la monitorización de los errores de ingesta parcial, lea la [guía de diagnósticos de error de ingesta por lotes](../quality/error-diagnostics.md).
