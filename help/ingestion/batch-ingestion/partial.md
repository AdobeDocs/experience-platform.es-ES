---
keywords: Experience Platform;inicio;temas populares;ingesta por lotes;ingesta por lotes;ingesta parcial;ingesta parcial;Recuperar error;recuperar error;ingesta parcial por lotes;ingesta parcial;ingesta parcial;ingesta parcial;
solution: Experience Platform
title: Resumen de ingesta parcial por lotes
description: Este documento proporciona un tutorial para administrar la ingesta parcial por lotes.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

---

# Ingesta parcial por lotes

La ingesta parcial por lotes es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral. Con esta capacidad, los usuarios pueden introducir correctamente todos sus datos correctos en Adobe Experience Platform, mientras que todos sus datos incorrectos se agrupan por separado, junto con los detalles de por qué no es válido.

Este documento proporciona un tutorial para administrar la ingesta parcial por lotes.

## Introducción

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform implicados en la ingesta parcial por lotes. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [Ingesta por lotes](./overview.md): Método que [!DNL Experience Platform] ingiere y almacena datos de archivos de datos, como CSV y Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que necesitará saber para poder realizar llamadas exitosas a [!DNL Experience Platform] API.

### Lectura de llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas de API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Experience Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

## Habilite un lote para la ingesta parcial por lotes en la API {#enable-api}

>[!NOTE]
>
>En esta sección se describe la activación de un lote para la ingesta parcial por lotes mediante la API. Para obtener instrucciones sobre el uso de la interfaz de usuario, lea el paso [habilitar un lote para la ingesta parcial por lotes en la interfaz de usuario](#enable-ui).

Puede crear un nuevo lote con la ingesta parcial habilitada.

Para crear un nuevo lote, siga los pasos de la [guía para desarrolladores de ingesta por lotes](./api-overview.md). Una vez que llegue al paso **[!UICONTROL Create batch]**, agregue el siguiente campo dentro del cuerpo de la solicitud:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un indicador que permite que [!DNL Experience Platform] genere mensajes de error detallados sobre su lote. |
| `partialIngestionPercent` | Porcentaje de errores aceptables antes de que falle todo el lote. Por lo tanto, en este ejemplo, un máximo del 5 % del lote puede ser errores antes de que falle. |


## Habilitar un lote para la ingesta parcial por lotes en la IU {#enable-ui}

>[!NOTE]
>
>En esta sección se describe la activación de un lote para la ingesta parcial por lotes mediante la interfaz de usuario. Si ya ha habilitado un lote para la ingesta parcial por lotes mediante la API, puede pasar a la siguiente sección.

Para habilitar un lote para la ingesta parcial a través de la interfaz de usuario [!DNL Experience Platform], puede crear un nuevo lote a través de conexiones de origen, crear un nuevo lote en un conjunto de datos existente o crear un nuevo lote a través de &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Crear una nueva conexión de origen {#new-source}

Para crear una nueva conexión de origen, siga los pasos indicados en [Resumen de orígenes](../../sources/home.md). Una vez que llegue al paso **[!UICONTROL Dataflow detail]**, tome nota de los campos **[!UICONTROL Partial ingestion]** y **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial por lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta característica permite que [!DNL Experience Platform] genere mensajes de error detallados acerca de los lotes ingeridos. Si se activa la opción **[!UICONTROL Partial ingestion]**, se aplican automáticamente los diagnósticos de error mejorados.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

### Usar un conjunto de datos existente {#existing-dataset}

Para utilizar un conjunto de datos existente, comience seleccionando un conjunto de datos. La barra lateral de la derecha se rellena con información sobre el conjunto de datos.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial por lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta característica permite que [!DNL Experience Platform] genere mensajes de error detallados acerca de los lotes ingeridos. Si se activa la opción **[!UICONTROL Partial ingestion]**, se aplican automáticamente los diagnósticos de error mejorados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

Ahora puede cargar datos usando el botón **Agregar datos** y se incorporarán mediante la ingesta parcial.

### Usar el flujo &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Para usar el flujo &quot;[!UICONTROL Map CSV to XDM schema]&quot;, siga los pasos indicados en el tutorial [Asignar un archivo CSV](../tutorials/map-csv/overview.md). Una vez que llegue al paso **[!UICONTROL Add data]**, tome nota de los campos **[!UICONTROL Partial ingestion]** y **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La opción **[!UICONTROL Partial ingestion]** le permite habilitar o deshabilitar el uso de la ingesta parcial por lotes.

La opción **[!UICONTROL Error diagnostics]** solo aparece cuando la opción **[!UICONTROL Partial ingestion]** está desactivada. Esta característica permite que [!DNL Experience Platform] genere mensajes de error detallados acerca de los lotes ingeridos. Si se activa la opción **[!UICONTROL Partial ingestion]**, se aplican automáticamente los diagnósticos de error mejorados.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** le permite establecer el porcentaje de errores aceptables antes de que falle todo el lote. De forma predeterminada, este valor se establece en 5%.

## Habilitar los diagnósticos de ingesta parcial y error para un flujo de datos existente

Si se creó un flujo de datos en Experience Platform sin habilitar la ingesta parcial o los diagnósticos de error, aún se pueden habilitar estas funciones sin volver a crear el flujo. Al habilitar la ingesta parcial y los sólidos diagnósticos de error, puede mejorar en gran medida la fiabilidad y la facilidad de la resolución de problemas en los flujos de trabajo de ingesta de datos. Lea las secciones siguientes para aprender a habilitar la ingesta parcial y los diagnósticos de error para un flujo de datos existente mediante la API [!DNL Flow Service].

De forma predeterminada, es posible que los flujos de datos no tengan habilitados los diagnósticos de ingesta parcial o error. Estas funciones son útiles para identificar y aislar problemas durante la ingesta de datos. Con la API [!DNL Flow Service], puede recuperar la configuración actual del flujo de datos y aplicar los cambios necesarios mediante una petición PATCH.

Siga los pasos a continuación para habilitar la ingesta parcial y los diagnósticos de error para un flujo de datos existente.

### Recuperar detalles de flujo

Para recuperar las configuraciones del flujo de datos, realice una petición GET al extremo `/flows/{FLOW_ID}` y proporcione el ID del flujo de datos. Para obtener más información sobre cómo recuperar detalles del flujo de datos, consulte [Actualizar flujos de datos mediante la guía de  [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md).

Asegúrese de guardar el valor del campo `etag` devuelto en la respuesta. Esto es necesario para que la solicitud de actualización garantice la coherencia de la versión.

### Actualizar configuración de flujo

A continuación, realice una petición PATCH al extremo `/flows/` y proporcione el ID del flujo de datos para el que desea habilitar la ingesta parcial y los diagnósticos de error.

>[!IMPORTANT]
>
>- Incluya el valor `etag` guardado anteriormente en el encabezado de la solicitud utilizando la clave If-Match.
>- Puede modificar el valor `partialIngestionPercent` para adaptarlo a sus necesidades específicas.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**Respuesta**

Una respuesta correcta devuelve `id` del flujo de datos y un `etag` actualizado.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### Verificar la actualización

Una vez completado PATCH, realice una petición GET y recupere el flujo de datos para comprobar que los cambios se hayan completado correctamente.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud recupera información actualizada sobre el ID de flujo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del flujo de datos, confirmando que los diagnósticos de ingesta parcial y error ahora están habilitados en la sección `options`.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## Próximos pasos {#next-steps}

En este tutorial se explica cómo crear o modificar un conjunto de datos para habilitar la ingesta parcial por lotes. Para obtener más información sobre la ingesta por lotes, lea la [guía para desarrolladores de ingesta por lotes](./api-overview.md).

Para obtener información sobre la supervisión de los errores de ingesta parcial, lea la [guía de diagnóstico de errores de ingesta por lotes](../quality/error-diagnostics.md).
