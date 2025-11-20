---
solution: Experience Platform
title: Generate Sample Data for an XDM Schema in the UI
description: Learn how to generate sample JSON data based on an existing schema in the Adobe Experience Platform user interface.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 14%

---

# Generar datos de muestra para un esquema XDM en la interfaz de usuario {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Descargar archivo de muestra"
>abstract="Genere un objeto JSON de muestra que se ajuste a la estructura del esquema elegido. Este objeto puede servir como plantilla para garantizar que los datos tengan el formato correcto para su ingesta a conjuntos de datos que emplean ese esquema. El explorador descargará el archivo JSON de muestra."

In order to ingest data into Adobe Experience Platform, the format and structure of the data must comply with an existing Experience Data Model (XDM) schema. Depending on the complexity of the schema for a particular dataset, it can be difficult to determine the exact shape of the data that the dataset expects upon ingestion.

For any schema that you define in the Experience Platform UI, you can generate a sample JSON object that conforms to the schema&#39;s structure. This object can serve as a template for any data that is ingested into datasets that employ the schema in question.

In the Experience Platform UI, select **[!UICONTROL Schemas]** in the left navigation. Under the **[!UICONTROL Browse]** tab, locate the schema that you want to generate sample data for. Select it from the list, and the right rail updates to show details about the schema. From here, select **[!UICONTROL Download sample file]**.

![The Browse tab of the Schemas workspace with a schema selected and download sample file highlighted.](../images/ui/sample/sample-data.png)

A sample JSON file is downloaded by the browser. You can now use this file as a reference for how to structure your data when ingesting into datasets that employ this schema.

## Próximos pasos

This guide covered how to generate a sample JSON file from an XDM schema in the Experience Platform UI. To learn how to generate sample data using the Schema Registry API, see the [sample data endpoint guide](../api/sample-data.md).

Once you are ready to start ingesting data, see the tutorial on [mapping a CSV file to XDM](../../ingestion/tutorials/map-csv/overview.md) to learn how to map a flat data file (such as a CSV) to an XDM schema and ingest it into Experience Platform. Alternatively, you can establish a [source connection](../../sources/home.md) to bring in your data from an external source and map it to XDM.

For more information on the capabilities of the [!UICONTROL Schemas] workspace in the UI, refer to the [[!UICONTROL Schemas] workspace overview](./overview.md).
