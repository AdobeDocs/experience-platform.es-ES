---
title: Ampliar las programaciones de exportación de conjuntos de datos para flujos de datos creados antes de noviembre de 2024
description: Obtenga información sobre cómo ampliar la programación de exportación para los flujos de datos de exportación de conjuntos de datos creados antes de noviembre de 2024 que dejarán de funcionar el 1 de septiembre de 2025.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 6f8b906729ec31cc0c4847ccd0ae0f89f63a1627
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Ampliar las programaciones de exportación de conjuntos de datos para flujos de datos creados antes de noviembre de 2024

>[!IMPORTANT]
>
>**Acción necesaria**: Si su organización tiene [flujos de datos de exportación de conjuntos de datos](export-datasets.md) creados antes de noviembre de 2024, estos flujos de datos dejarán de funcionar el 1 de septiembre de 2025. En esta guía se explica cómo ampliar la programación de exportación más allá de esta fecha para los flujos de datos que desea mantener.

## Información general {#overview}

En la versión de [septiembre de 2024 de Experience Platform](/help/release-notes/2024/september-2024.md#destinations), Adobe introdujo una fecha de finalización predeterminada del **1 de mayo de 2025** para todos los flujos de datos de exportación de conjuntos de datos creados antes de la versión de septiembre de 2024.

**Esta fecha se ha actualizado desde el 1 de septiembre de 2025** para todos los flujos de datos de exportación de conjuntos de datos creados **antes de noviembre de 2024**.

Los flujos de datos de exportación de conjuntos de datos creados antes de noviembre de 2024 dejarán de exportar datos el **1 de septiembre de 2025** a menos que amplíe manualmente su fecha de caducidad.

Si necesita que los flujos de datos sigan exportando datos después del **1 de septiembre de 2025**, debe ampliar sus programaciones para cada destino al que esté exportando conjuntos de datos, siguiendo los pasos de esta guía.

## Destinos afectados {#affected-destinations}

Su organización puede tener flujos de datos de exportación de conjuntos de datos activos que envíen datos a los destinos enumerados a continuación. Siga los pasos de las secciones siguientes y vea el vídeo del tutorial para aprender a identificar qué conjuntos de datos están configurados para que caduquen.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Tutorial de vídeo {#video}

Vea el siguiente vídeo para obtener una demostración paso a paso de cómo identificar las exportaciones de conjuntos de datos con próximas fechas de finalización y ampliar la programación de exportación para los flujos de datos que desea mantener.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Paso 1: Identificar los flujos de datos afectados {#identify-dataflows}

Antes de ampliar la programación de exportación para los flujos de datos de exportación del conjunto de datos, primero debe identificar qué flujos de datos se ven afectados por la próxima fecha de caducidad. Siga los pasos a continuación para localizar los flujos de datos que requieren alguna acción.

1. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** en la interfaz de usuario de Experience Platform.
2. Seleccione **[!UICONTROL Activar]** en un destino que tenga flujos de datos de exportación de conjuntos de datos activos.

   >[!TIP]
   >
   >Utilice el filtro **[!UICONTROL Tipos de datos]** de la parte izquierda del catálogo para filtrar los destinos disponibles por **[!UICONTROL Conjuntos de datos]**.

3. Seleccione el tipo de datos **[!UICONTROL Datasets]** para mostrar solo los flujos de datos con exportaciones de conjuntos de datos.
   ![Captura de pantalla que muestra cómo filtrar flujos de datos por tipo de datos.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Seleccione el encabezado de columna **[!UICONTROL Created]** y elija **[!UICONTROL Orden ascendente]** para ver los flujos de datos más antiguos.
   ![Captura de pantalla que muestra cómo ordenar flujos de datos en orden ascendente.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identifique cuál de los flujos de datos creados antes de noviembre de 2024 desea mantener.

## Paso 2: Acceso al flujo de trabajo de exportación de conjuntos de datos {#access-workflow}

Para cada flujo de datos que desee conservar, debe acceder al flujo de trabajo de exportación de conjuntos de datos para modificar la programación.

1. Seleccione el nombre del flujo de datos en la columna **[!UICONTROL Nombre]**. Esto lo lleva a la página **[!UICONTROL Flujo de datos se ejecuta]**.
2. En esta página, seleccione la opción **[!UICONTROL Exportar conjuntos de datos]**.
   ![Captura de pantalla que muestra la opción exportar conjuntos de datos en la página de ejecuciones de flujo de datos.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. En la página **[!UICONTROL Seleccionar conjuntos de datos]**, seleccione **[!UICONTROL Siguiente]**. No es necesario agregar ningún conjunto de datos nuevo al flujo de datos.
4. Esto lo lleva a la página **[!UICONTROL Programación]**, donde también puede ver una notificación que le informa de la fecha de caducidad de la exportación del conjunto de datos.
   ![Flujos de datos de exportación de conjuntos de datos con notificación de caducidad](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Paso 3: Ampliación de la programación de exportación {#extend-export-schedule}

Ahora puede modificar la programación de exportación para que se extienda más allá del 1 de septiembre de 2025.

1. Seleccione **[!UICONTROL Editar programación]**.
   ![Captura de pantalla del paso Programación que muestra el botón Editar programación.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Seleccione una nueva programación de exportación y luego seleccione **[!UICONTROL Guardar]**.
   ![Captura de pantalla del paso Programación que muestra las opciones de programación.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Consulte la [documentación de exportación del conjunto de datos](export-datasets.md#scheduling) para obtener instrucciones detalladas sobre cómo configurar las programaciones de exportación del conjunto de datos.

## ¿Qué sucede si me pierdo la fecha límite del 1 de septiembre de 2025? {#missed-deadline}

Si los flujos de datos de exportación del conjunto de datos caducan el 1 de septiembre de 2025 y no ha ampliado sus programaciones, existe un período de gracia de **30 días** en el que puede ponerse en contacto con Adobe para volver a habilitar los flujos de datos sin perder datos. Esto incluye datos que no se exportaron entre el 1 de septiembre y la fecha en que se puso en contacto con Adobe.

>[!IMPORTANT]
>
>Aunque Adobe proporciona este período de gracia, recomendamos encarecidamente ampliar sus programaciones antes de la fecha límite del 1 de septiembre de 2025 para garantizar exportaciones de datos ininterrumpidas y evitar cualquier posible interrupción del servicio.
