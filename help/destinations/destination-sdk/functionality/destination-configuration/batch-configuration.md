---
description: Obtenga información sobre cómo configurar los ajustes de exportación de archivos para los destinos creados con Destination SDK.
title: Configuración por lotes
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 5%

---


# Configuración por lotes {#batch-configuration}

Utilice las opciones de configuración por lotes en el Destination SDK para permitir a los usuarios personalizar los nombres de los archivos exportados y configurar la programación de exportación según sus preferencias.

Cuando crea destinos basados en archivos mediante Destination SDK, puede configurar los programas predeterminados de nomenclatura y exportación de archivos, o puede dar a los usuarios la opción de configurar estos ajustes desde la interfaz de usuario de Platform. Por ejemplo, puede configurar comportamientos como:

* Incluir información específica en el nombre del archivo, como ID de segmento, ID de destino o información personalizada.
* Permite a los usuarios personalizar el nombre de los archivos desde la interfaz de usuario de Platform.
* Configure las exportaciones de archivos para que se produzcan en intervalos de tiempo establecidos.
* Defina qué opciones de asignación de nombres de archivos y de personalización de programaciones de exportación pueden ver los usuarios en la interfaz de usuario de Platform.

Los ajustes de configuración de lotes forman parte de la configuración de destino para destinos basados en archivos.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) o consulte la guía sobre cómo [usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puede configurar la asignación de nombres a los archivos y exportar la configuración de programación mediante el `/authoring/destinations` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Actualizar una configuración de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artículo describe todas las opciones de configuración por lotes compatibles que puede utilizar para el destino y muestra lo que verán los clientes en la interfaz de usuario de Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | No |
| Integraciones basadas en archivos (por lotes) | Sí |

## Parámetros admitidos {#supported-parameters}

Los valores que configure aquí aparecen en la [Programar exportación de segmentos](../../../ui/activate-batch-profile-destinations.md#scheduling) paso del flujo de trabajo de activación de destinos basados en archivos.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Establecer como `true` para permitir a los clientes especificar qué atributos de perfil son obligatorios. El valor predeterminado es `false`. Consulte [Atributos obligatorios](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obtener más información. |
| `allowDedupeKeyFieldSelection` | Booleano | Establecer como `true` para permitir a los clientes especificar claves de deduplicación. El valor predeterminado es `false`.  Consulte [Claves de deduplicación](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) para obtener más información. |
| `defaultExportMode` | Enum | Define el modo predeterminado de exportación de archivos. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> El valor predeterminado es `DAILY_FULL_EXPORT`. Consulte la [documentación de activación por lotes](../../../ui/activate-batch-profile-destinations.md#scheduling) para obtener más información sobre la programación de exportaciones de archivos. |
| `allowedExportModes` | Lista | Define los modos de exportación de archivos disponibles para los clientes. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define la frecuencia de exportación de archivos disponible para los clientes. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Define la frecuencia de exportación de archivos predeterminada. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> El valor predeterminado es `DAILY`. |
| `defaultStartTime` | Cadena | Define la hora de inicio predeterminada para la exportación de archivos. Utiliza el formato de archivo de 24 horas. El valor predeterminado es &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Cadena | *Requerido*. Lista de macros de nombres de archivo disponibles para que los usuarios puedan elegir. Esto determina qué elementos se adjuntan a los nombres de archivo exportados (ID de segmento, nombre de organización, fecha y hora de exportación, etc.). Al configurar `defaultFilename`, asegúrese de evitar la duplicación de macros. <br><br>Valores compatibles: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independientemente del orden en que defina las macros, la interfaz de usuario del Experience Platform siempre las mostrará en el orden presentado aquí. <br><br> If `defaultFilename` está vacío, la variable `allowedFilenameAppendOptions` La lista debe contener al menos una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Cadena | *Requerido*. Macros de nombres de archivo predeterminados preseleccionados que los usuarios pueden desmarcar.<br><br> Las macros de esta lista son un subconjunto de las definidas en `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Cadena | *Opcional*. Define las macros de nombre de archivo predeterminadas para los archivos exportados. Los usuarios no pueden sobrescribirlos. <br><br>Cualquier macro definida por `allowedFilenameAppendOptions` se añadirá después de `defaultFilename` macros. <br><br>If `defaultFilename` está vacío, debe definir al menos una macro en `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## Configuración de nombre de archivo {#file-name-configuration}

Utilice las macros de configuración de nombre de archivo para definir qué deben incluir los nombres de archivo exportados. Las macros de la tabla siguiente describen los elementos que se encuentran en la interfaz de usuario de [configuración de nombre de archivo](../../../ui/activate-batch-profile-destinations.md#file-names) en el Navegador.

>[!TIP]
> 
>Como práctica recomendada, debe incluir siempre la variable `SEGMENT_ID` en los nombres de archivo exportados. Los ID de segmento son únicos, por lo que incluirlos en el nombre de archivo es la mejor manera de garantizar que los nombres de archivo también sean únicos.

| Macro | Etiqueta de la interfaz de usuario | Descripción | Ejemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nombre de destino en la interfaz de usuario. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID de segmento] | ID de segmento único generado por la plataforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nombre del segmento] | Nombre de segmento definido por el usuario | VIP suscriptor |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID único, generado por la plataforma de la instancia de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nombre de destino] | Nombre definido por el usuario de la instancia de destino. | Mi destino publicitario de 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nombre de la organización] | Nombre de la organización de clientes en Adobe Experience Platform. | Mi nombre de organización |
| `SANDBOX_NAME` | [!UICONTROL Nombre de la zona protegida] | Nombre del simulador de pruebas utilizado por el cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Fecha y hora] | `DATETIME` y `TIMESTAMP` ambos definen cuándo se generó el archivo, pero en diferentes formatos. <br><br><ul><li>`DATETIME` utiliza el siguiente formato: AAAAMMDD_HHMMSS.</li><li>`TIMESTAMP` utiliza el formato Unix de 10 dígitos. </li></ul> `DATETIME` y `TIMESTAMP` son mutuamente excluyentes y no se pueden usar simultáneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido por el usuario que se incluirá en el nombre del archivo. No se puede usar en `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Fecha y hora] | Marca de fecha y hora de 10 dígitos del momento en que se generó el archivo, en formato Unix. | 1652131584 |

{style="table-layout:auto"}

### Ejemplo de configuración de nombre de archivo

El ejemplo de configuración siguiente muestra la correspondencia entre la configuración utilizada en la llamada de API y las opciones mostradas en la interfaz de usuario.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![Imagen de interfaz de usuario que muestra la pantalla de configuración del nombre de archivo con macros preseleccionadas](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo puede configurar la asignación de nombres a archivos y las programaciones de exportación para los destinos basados en archivos.

Para obtener más información sobre los otros componentes de destino, consulte los siguientes artículos:

* [Configuración de autenticación de cliente](customer-authentication.md)
* [Autenticación OAuth2](oauth2-authentication.md)
* [Campos de datos del cliente](customer-data-fields.md)
* [Atributos de interfaz de usuario](ui-attributes.md)
* [Configuración del esquema](schema-configuration.md)
* [Configuración del área de nombres de identidad](identity-namespace-configuration.md)
* [Configuraciones de asignación admitidas](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuración de metadatos de audiencia](audience-metadata-configuration.md)
* [Política de agregación](aggregation-policy.md)
* [Calificaciones históricas de perfil](historical-profile-qualifications.md)