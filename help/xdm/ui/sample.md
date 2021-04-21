---
solution: Experience Platform
title: Generar datos de ejemplo para un esquema XDM en la interfaz de usuario
description: Obtenga información sobre cómo generar datos JSON de muestra basados en un esquema existente en la interfaz de usuario de Adobe Experience Platform.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Generar datos de ejemplo para un esquema XDM en la interfaz de usuario

Para poder introducir datos en Adobe Experience Platform, el formato y la estructura de los datos deben cumplir con un esquema del Modelo de datos de experiencia (XDM) existente. Dependiendo de la complejidad del esquema para un conjunto de datos en particular, puede ser difícil determinar la forma exacta de los datos que el conjunto de datos espera al ingerirlos.

Para cualquier esquema que defina en la interfaz de usuario del Experience Platform, puede generar un objeto JSON de muestra que se ajuste a la estructura del esquema. Este objeto puede servir de plantilla para cualquier dato que se incorpore en conjuntos de datos que empleen el esquema en cuestión.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo. En la pestaña **[!UICONTROL Browse]**, busque el esquema para el que desea generar datos de ejemplo. Selecciónela en la lista y el carril derecho se actualiza para mostrar detalles sobre el esquema. Desde aquí, seleccione **[!UICONTROL Download sample file]**.

![](../images/ui/sample/sample-data.png)

El explorador descarga un archivo JSON de muestra. Ahora puede utilizar este archivo como referencia para estructurar los datos al ingerirlos en conjuntos de datos que empleen este esquema.

## Pasos siguientes

Esta guía explica cómo generar un archivo JSON de muestra a partir de un esquema XDM en la interfaz de usuario de Platform. Para obtener información sobre cómo generar datos de ejemplo mediante la API del Registro de esquemas, consulte la [guía de extremo de datos de ejemplo](../api/sample-data.md).

Una vez que esté listo para empezar a introducir datos, consulte el tutorial sobre [asignación de un archivo CSV a XDM](../../ingestion/tutorials/map-a-csv-file.md) para aprender a asignar un archivo de datos plano (como un CSV) a un esquema XDM e ingerirlo en Platform. Como alternativa, puede establecer una [conexión de origen](../../sources/home.md) para incorporar los datos de un origen externo y asignarlos a XDM.

Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Schemas] en la interfaz de usuario, consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](./overview.md).
