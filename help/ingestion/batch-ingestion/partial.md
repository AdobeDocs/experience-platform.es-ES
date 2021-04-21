---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta parcial;ingesta parcial;error de recuperación;ingesta parcial por lotes;ingesta parcial por lotes;parcial;ingesta;ingesta parcial;ingesta;ingesta
solution: Experience Platform
title: Información general sobre la ingesta parcial de lotes
topic-legacy: overview
description: Este documento proporciona un tutorial para administrar la ingesta parcial de lotes.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Ingesta parcial por lotes

La ingesta parcial de lotes es la capacidad de ingerir datos que contengan errores, hasta un umbral determinado. Con esta capacidad, los usuarios pueden ingerir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se procesan por lotes por separado, junto con los detalles de por qué no son válidos.

Este documento proporciona un tutorial para administrar la ingesta parcial de lotes.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform implicados en la ingesta parcial de lotes. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Ingesta por lotes](./overview.md): Método que  [!DNL Platform] ingesta y almacena datos de archivos de datos, como CSV y Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas a las API [!DNL Platform] correctamente.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

## Habilitar un lote para la ingesta parcial de lotes en la API {#enable-api}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingesta parcial de lotes mediante la API. Para obtener instrucciones sobre el uso de la interfaz de usuario, lea el paso [habilitar un lote para la ingesta parcial por lotes en el paso UI](#enable-ui) .

Puede crear un nuevo lote con la ingesta parcial activada.

Para crear un nuevo lote, siga los pasos de la [guía para desarrolladores de ingesta por lotes](./api-overview.md). Una vez que llegue al paso **[!UICONTROL Create batch]** , agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un indicador que permite a [!DNL Platform] generar mensajes de error detallados sobre el lote. |
| `partialIngestionPercentage` | El porcentaje de errores aceptables antes de todo el lote fallará. Por lo tanto, en este ejemplo, un máximo del 5 % del lote puede ser de errores antes de que falle. |


## Habilitar un lote para la ingesta parcial de lotes en la interfaz de usuario {#enable-ui}

>[!NOTE]
>
>En esta sección se describe cómo habilitar un lote para la ingesta parcial de lotes mediante la interfaz de usuario. Si ya ha habilitado un lote para la ingesta parcial de lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un lote para la ingesta parcial a través de la interfaz de usuario de [!DNL Platform], puede crear un nuevo lote a través de conexiones de origen, crear un nuevo lote en un conjunto de datos existente o crear un nuevo lote a través de &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Crear una nueva conexión de origen {#new-source}

Para crear una nueva conexión de origen, siga los pasos que se enumeran en la [Información general de orígenes](../../sources/home.md). Una vez que llegue al paso **[!UICONTROL Dataflow detail]**, tome nota de los campos **[!UICONTROL Partial ingestion]** y **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial de lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta función permite a [!DNL Platform] generar mensajes de error detallados sobre los lotes ingeridos. Si la opción **[!UICONTROL Partial ingestion]** está activada, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

El **[!UICONTROL Error threshold]** permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5%.

### Usar un conjunto de datos existente {#existing-dataset}

Para utilizar un conjunto de datos existente, comience seleccionando un conjunto de datos. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial de lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta función permite a [!DNL Platform] generar mensajes de error detallados sobre los lotes ingeridos. Si la opción **[!UICONTROL Partial ingestion]** está activada, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

El **[!UICONTROL Error threshold]** permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5%.

Ahora, puede cargar datos mediante el botón **Add data**, que se incorporará mediante ingesta parcial.

### Utilice el flujo [!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Para utilizar el flujo &quot;[!UICONTROL Map CSV to XDM schema]&quot;, siga los pasos que se enumeran en el tutorial [Asignar un archivo CSV](../tutorials/map-a-csv-file.md). Una vez que llegue al paso **[!UICONTROL Add data]**, tome nota de los campos **[!UICONTROL Partial ingestion]** y **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial de lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta función permite a [!DNL Platform] generar mensajes de error detallados sobre los lotes ingeridos. Si la opción **[!UICONTROL Partial ingestion]** está activada, los diagnósticos de error mejorados se aplican automáticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** permite establecer el porcentaje de errores aceptables antes de que se produzca un error en todo el lote. De forma predeterminada, este valor se establece en 5%.

## Pasos siguientes {#next-steps}

Este tutorial trata sobre cómo crear o modificar un conjunto de datos para habilitar la ingesta parcial de lotes. Para obtener más información sobre la ingesta por lotes, lea la [guía para desarrolladores sobre ingesta por lotes](./api-overview.md).

Para obtener información sobre la monitorización de los errores de ingesta parcial, lea la [guía de diagnóstico de errores de ingesta por lotes](../quality/error-diagnostics.md).
